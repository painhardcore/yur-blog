---
title: "HabitPulse: Making the handlers. Part 3"
author: Andrey Yurchenkov
pubDatetime: 2024-06-17T00:00:00Z
postSlug: habitpulse-part3
featured: false
draft: false
tags:
  - en
  - bot
  - golang
  - influxdb
  - telegram
  - habitpulse
  - part1
description: We need to the handlers for our bot. And now we have a working flow.
---

# HabitPulse. Making the handlers. Part 3

## Introduction

In our last article, we focused on setting up the development environment necessary for high-quality development. Now, we pivot towards defining the MVP (Minimum Viable Product) scope and constructing the main workflow for our Telegram bot.

## Defining the MVP Scope

An MVP is essential to get a functional product that can be iteratively improved. The core of our MVP for the Telegram bot will include:

- **Handlers**: The bot will have command handlers that react to user input, such as:

  - `/start`: The default handler providing information about other handlers and bot functionalities.
  - `/add`: Used to add a new activity or to append data to an existing one.
  - `/stats`: For viewing statistics related to a specific activity.
  - `/list`: To list all activities a user has, with options for each activity.

- **Interactive Buttons**: To enhance UX, the bot will feature interactive buttons for easier user interaction.

- **Data Management**: User data and activity records will be stored using InfluxDB.

- **Visualization**: Functionality to generate and share graphical statistics with users.

## Project Structure

While a single file could suffice for the MVP, we opt for a modular approach for the following reasons:

1. **Scalability**: Separate packages allow easy scaling of the bot's functionalities.
2. **Maintainability**: It simplifies maintenance and debugging.
3. **Flexibility**: This structure facilitates future improvements and additions without overhauling the codebase.

The project will be structured into packages for:

- **Bot Logic**: Handlers and command processing.
- **Database Interface**: Abstraction layer for InfluxDB operations.
- **Graph Generation**: Tooling for creating and sharing visual data representations.

## Implementation Strategy

- Handlers will be created for each command, implementing the business logic.
- A database package will handle data storage, with an interface hiding the complexities of InfluxDB.
- Graph generation will be managed by a separate package, which will provide the interface to generate and send images to users within the chat.

## Implementing handlers

So in order it to work we want to use **handlers** package which starts like that:

```go
package handlers

import (
	"fmt"
	"log"
	"strconv"
	"strings"
	"time"

	tgbotapi "github.com/go-telegram-bot-api/telegram-bot-api/v5"
	"github.com/painhardcore/habitpulse/database"
)

type BotHandlers struct {
	bot *tgbotapi.BotAPI
	db  database.DatabaseClient
	UserSession
}

type UserSession struct {
	State    string
	Activity string
}

// TODO: make it thread-safe
var userSessions = make(map[int64]*UserSession)

func NewBotHandlers(bot *tgbotapi.BotAPI, db database.DatabaseClient) *BotHandlers {
	return &BotHandlers{bot: bot, db: db}
}

func (bh *BotHandlers) StartBot() error {
	u := tgbotapi.NewUpdate(0)
	u.Timeout = 60

	updates := bh.bot.GetUpdatesChan(u)

	for update := range updates {
		if update.CallbackQuery != nil {
			bh.handleCallback(update.CallbackQuery)
		} else if update.Message != nil {
			if update.Message.IsCommand() {
				switch update.Message.Command() {
				case "start":
					bh.handleStart(update.Message)
				case "add":
					bh.handleAdd(update.Message)
				case "stats":
					bh.handleStats(update.Message)
				case "list":
					bh.handleList(update.Message)
				default:
					bh.handleUnknown(update.Message)
				}
			} else {
				bh.handleInput(update.Message)
			}
		}
	}

	return nil
}

```

Since I'm the only one use - I don't need something safe for session and I deal with it later.
Other than that - everything straightword. We bind each command with method.

Lets focus on /add method. We gonna need to add some number to activity in order to track it. And when we want to add we should list the activities with buttons

```go
func (bh *BotHandlers) getActivityButtons(useID int64) []tgbotapi.InlineKeyboardButton {
	// Display a list of activities or a button to add a new activity
	activities, err := bh.db.ListActivities(useID)
	if err != nil {
		log.Println("Error retrieving activities:", err)
		return nil
	}

	// I don't beleive there would a lot of activities, so I'm not going to paginate them
	btns := make([]tgbotapi.InlineKeyboardButton, 0, len(activities))
	for _, activity := range activities {
		button := tgbotapi.NewInlineKeyboardButtonData(activity, "select:"+activity)
		btns = append(btns, button)
	}
	return btns

}
func (bh *BotHandlers) handleAdd(message *tgbotapi.Message) {
	userID := message.From.ID
	rows := [][]tgbotapi.InlineKeyboardButton{}
	btns := bh.getActivityButtons(userID)
	if btns != nil {
		rows = append(rows, btns)
	}
	addNewButton := tgbotapi.NewInlineKeyboardButtonData("New Activity", "add_new")
	rows = append(rows, []tgbotapi.InlineKeyboardButton{addNewButton})

	keyboard := tgbotapi.NewInlineKeyboardMarkup(rows...)
	msg := tgbotapi.NewMessage(userID, "Select an activity or add a new one:")
	msg.ReplyMarkup = keyboard
	bh.bot.Send(msg)
}
```

And here we're creating the buttons with the activities and adding a separate button for a new one.

Next, when we want to work with the buttons we should handle the callbacks. It's separate function and we use Sessions, since we want to carry some context for this interaction.

```go
func (bh *BotHandlers) handleCallback(callback *tgbotapi.CallbackQuery) {
	userID := callback.From.ID
	data := strings.Split(callback.Data, ":")
	if len(data) < 1 {
		// Send error message
		return
	}

	session, exists := userSessions[userID]
	if !exists {
		session = &UserSession{}
		userSessions[userID] = session
	}

	switch data[0] {
	case "select":
		if len(data) == 2 {
			session.Activity = data[1]
			session.State = "awaiting_count"
			msg := tgbotapi.NewMessage(userID, "Enter the number for "+session.Activity+":")
			bh.bot.Send(msg)
		}
	case "add_new":
		session.State = "awaiting_activity"
		msg := tgbotapi.NewMessage(userID, "Enter the name of the new activity:")
		bh.bot.Send(msg)
	}
}
```

So after used choosed what he want - we just asking for action and now waiting to handle the input:

```go
func (bh *BotHandlers) handleInput(message *tgbotapi.Message) {
	userID := message.From.ID
	session, exists := userSessions[userID]
	if !exists {
		msg := tgbotapi.NewMessage(message.From.ID, "I don't understand you.")
		bh.bot.Send(msg)
		return
	}

	switch session.State {
	case "awaiting_activity":
		session.Activity = message.Text
		session.State = "awaiting_count"
		msg := tgbotapi.NewMessage(userID, "Enter the count for "+session.Activity+":")
		bh.bot.Send(msg)

	case "awaiting_count":
		count, err := strconv.Atoi(message.Text)
		if err != nil {
			msg := tgbotapi.NewMessage(userID, "Please enter a valid number.")
			bh.bot.Send(msg)
			return
		}

		err = bh.db.AddActivity(userID, session.Activity, count)
		if err != nil {
			log.Println("Error adding activity:", err)
			return
		}
		delete(userSessions, userID)
		dayCount, err := bh.db.GetCountForToday(userID, session.Activity)
		if err != nil {
			log.Println("Error getting days activity:", err)
		}
		stat7d := bh.getStatMessageActivity(userID, session.Activity, 7)
		msg := tgbotapi.NewMessage(userID, fmt.Sprintf("%d %s added. Today: %d.\n%s\nMore ?", count, session.Activity, dayCount, stat7d))
		btns := bh.getActivityButtons(userID)
		if btns != nil {
			msg.ReplyMarkup = tgbotapi.NewInlineKeyboardMarkup(btns)
		}
		bh.bot.Send(msg)

		session.State = ""
		session.Activity = ""
	}
}

```
