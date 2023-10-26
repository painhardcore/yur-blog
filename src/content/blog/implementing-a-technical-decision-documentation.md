---
title: Implementing a Technical Decision Documentation
author: Andrey Yurchenkov
pubDatetime: 2023-10-23T00:17:19Z
postSlug: implementing-a-technical-decision-documentation
featured: true
draft: false
tags:
  - team
  - technical documentation
  - RFC
  - engineering
  - en
description: Unlock seamless collaboration and clarity in your tech projects with our straightforward guide on effectively organizing technical documents within git repository.
---

# Implementing a Technical Decision Documentation

## Table of contents

## Introduction

Have you ever joined a new company and found yourself asking questions like, "Why do we use this database?", "Why did we choose this particular approach or technology?" How often were you met with answers like, "It's just how things evolved", or even worse, "Dave decided on it, and he's really smart!"? How many times have you noticed different teams in the company, unbeknownst to each other, working on the same issue but from different angles? Or perhaps, you once wanted to introduce something new to the workflow, but simply didn't know how and where to propose it?

If you answered "yes" to any of these questions, then this article is for you. Here, I will try to outline my perspective on how to establish an effective documentation and interaction system within an IT company, ensuring every team member feels involved, informed, and ready for collaboration.

## Motivation and Historical Context Behind Adopting This Documentation System

![Alt text](@assets/tdd/tired.png)
Joining a new team or company often brings up questions about existing systems and practices. The frequent queries of “Why is it done this way?” or “Why was this approach chosen?” usually meet the response, “That’s how it’s always been.” This prevalent scenario underscores the need for a structured documentation system for technical decisions:

- **Transparency Across Teams**: With diverse teams working on different project facets, a centralized documentation system reduces redundancy and promotes synergy by ensuring everyone's alignment.

- **Leveraging Previous Experiences**: By accessing documented past initiatives, teams can avoid 'reinventing the wheel.' This historical perspective accelerates problem-solving by offering insights from past attempts, successes, or failures.

- **One Source of Truth**: Centralizing all documentation in a single location, like a repository, ensures that everyone knows where to find required information, making the search process simpler.

- **Avoiding Fragmented Information**: A unified system prevents information scatter across different platforms, from personal notes to chat threads, shared documents, and internal wikis. Such scatter complicates retrieval and might jeopardize data completeness and accuracy.

- **Promoting a Culture of Documentation**: Standardizing the process emphasizes documentation's importance, fostering a culture where documentation becomes innate to developers, enhancing project handovers, onboarding processes, and overall team efficiency.

- **Onboarding and Historical Context**: When new members integrate into a team, they often seek to understand the system deeply. While official documentation might lag, reading historical technical decisions offers clarity. Gaining insight into the context and assumptions behind past decisions proves invaluable.

- **Evolving Systems and Assumptions**: Projects progress, and initial assumptions might become obsolete due to requirements shifts, user needs, or technology evolution. Without grasping foundational decisions, determining necessary changes becomes tough. Recognizing that an approach was based on past assumptions allows teams to pinpoint areas ripe for a fresh approach.

The push for this documentation system transcends mere organization. It aims to amplify team productivity, learn from previous endeavors, and ensure all team members have the insights needed for effective contribution. Moreover, by documenting the rationale behind technical decisions, teams preserve knowledge, creating a reference for continuous learning and iterative improvement. This ensures that systems adapt to current needs while respecting their historical context.

A common scenario encountered when joining a new company or team is the frequent questioning of existing practices and systems. Newcomers often ask, "Why is it done this way?" or "Why was this approach chosen?". The usual response is, "That's just how it's always been." This historical precedent, while at times serving as a foundation, can also be a limitation.

Understanding the 'why' behind decisions is essential, but, unfortunately, the reasoning often gets lost over time. In many instances, the choices made in the past were indeed the best for that particular moment. However, the current landscape might present new opportunities or technologies that can significantly improve upon previous decisions.

This brings us to two crucial points:

1. **Onboarding and Historical Context**: When new members join the team, they often seek a deeper understanding of the system. While official documentation or wikis might be outdated, reading about the historical technical decisions provides a clear picture. Understanding the assumptions and the context in which decisions were made can offer invaluable insights into the system's design.

2. **Evolving Systems and Assumptions**: As projects progress, initial assumptions might no longer hold. Whether it's a shift in the requirements, new user needs, or simply the evolution of technology, systems need to adapt. However, without understanding the foundational decisions, it becomes challenging to determine what should change. Recognizing that an implementation or a chosen database was rooted in past assumptions helps teams identify areas that might now benefit from a different approach.

By documenting the thought process behind technical decisions, teams not only preserve knowledge but also create a reference point. This documentation becomes a tool for continuous learning and iterative improvement, ensuring that systems evolve in alignment with present needs while respecting historical context.

## Choosing a Platform for Document Location: Why GitHub?

![Are you sure answer is here](@assets/tdd/are-y-sure-answer-here.png)
While the exact location of where all these documents are stored might not seem crucial, the choice of platform can significantly influence the efficiency of your documentation process. Here's why GitHub might be an ideal choice:``

- **Integration with Development**:

  - If your documentation relates to code, hosting it on GitHub keeps everything in one place, bridging the gap between code and documentation.

- **Local File Accessibility**:
  - With GitHub, all documents are always stored locally, allowing easy transfer without navigating through cloud storage or other remote repositories.
- **Version Control**:
  - As a Git-based platform, GitHub inherently offers version control. This ensures every team member accesses the most recent version of a document.
- **Familiarity for Technical Teams**:

  - Most developers and technical staff are already accustomed to GitHub. Leveraging familiar tools can simplify the adoption process.

- **Pull Requests for Discussion**:
  - All discussions around documentation can be tracked efficiently using pull requests, providing an organized way to track feedback, amendments, and approvals.
- **Highlight Specific Points**:
  - Unlike issues, pull requests allow highlighting specific parts of a document, streamlining the review process.
- **Notification Configuration**:
  - With robust notification settings, teams can set up alerts for new document pull requests, ensuring timely participation in discussions.
- **Searchability**:
  - GitHub's powerful search tool makes finding specific documents or sections within documents effortless.

Remember, the key is to select a platform that aligns with your team's needs and workflows. While GitHub offers numerous advantages, it's essential to evaluate if it's the right choice for your documentation requirements.

## An Overview of Essential Technical Documents

![Alt text](@assets/tdd/happy.png)
In the realm of software engineering and system design, documentation plays an invaluable role in navigating complexities and ensuring clarity for all stakeholders. This section delineates the primary types of documents and their specific purposes:

1. **RFC (Request for Comments)**:

   - **Open Discussions**: RFCs serve as a means to propose new ideas or changes, allowing all team members to discuss, contribute to, and refine the concept.
   - **Collective Decision Making**: Through RFCs, teams can collaboratively decide on the best course of action, ensuring that multiple perspectives are considered.
   - **Historical Record**: They act as a record for future reference, aiding in understanding the rationale behind certain decisions.

2. **System Design Documents**:

   - **Detailed Implementation Guide**: These documents focus on the "how" of the decision-making process. They provide a comprehensive overview of the implementation, often peppered with code examples, ensuring everyone is aligned on the specifics of the execution.
   - **Team Alignment**: System Design documents serve as detailed plans for implementing features or further development. They ensure that teammates and teams are on the same page, understanding both what will happen and how it will occur.
   - **Focus on Correctness**: The primary goal of a System Design document is to ascertain everyone's agreement on the correct approach to implementation. By detailing the design, it ensures clarity and reduces potential ambiguities.

3. **ADR (Architectural Decision Records)**:
   - **Feedback Mechanism**: ADRs provide a structured format to propose changes or introduce new solutions. They enable team members to solicit feedback, ensuring that proposed changes align with the team's vision and objectives.
   - **Retrospective Analysis**: ADRs act as a historical record of technical decisions. This retrospective perspective can be instrumental for assessing past actions and understanding the rationale behind certain choices, facilitating better decision-making in future endeavors.

> **Note**: While each document brings its unique benefits and clarity to a technical decision, it's crucial to understand that not all are mandatory for every scenario. Depending on the context, urgency, size, and other factors related to a task, some stages might be expedited. However, even the inclusion of just one type of these documents can significantly enhance the clarity and efficiency of decision-making, providing considerable positive impact.

## Organizing Documents Inside a Repository

![How everything well organized](@assets/tdd/organize.png)
If you've chosen GitHub as your platform, there's a temptation to embed this documentation directly into your current code repository. But should you?

### Why Not to Use the Same Repository for Development and Technical Documentation:

1. **Repository Focus**: A dedicated repository ensures a focus solely on technical decision documentation. Mixing it with code or other files might cause unnecessary clutter and distraction.

2. **Existing Workflows**: Your main code repository likely has various workflows set up that would be triggered with every pull request. Incorporating documentation into this could undesirably slow down the development process.

3. **Multiple Repositories**: If you don't have a monorepo but several repositories, where will you document? Doing so in all of them isn't a feasible option.

4. **Team Accessibility**: Different teams may find it inconvenient to go into someone else's repository. Having a common separate repository is more inclusive.

5. **Repository Purity**: Keeping the repository focused solely on technical decisions documentation ensures clarity and purpose, avoiding the mix of unrelated topics.

### Naming Documents:

When it comes to naming your documents, there are various approaches one can take. Personally, I found the format `year-month-day-short-description.md` most optimal. This ensures retrospective addition of any documents and provides an immediate understanding of when changes or trials were made. The format itself also allows for easy searching and filtering.

### Why Not to Use "Issues" as Technical Documentation:

1. **Review Limitations**: Issues don't allow for reviews or specific comments on particular parts of the content.
2. **Closure Ambiguity**: When an issue is closed, it's not immediately clear why. Was it accepted, rejected, or modified? Although this might be in the comments, it's not as evident.
3. **Visibility Post-Closure**: Once you close an issue, it tends to get out of sight.
4. **Lack of Structured Search**: With issues, it's hard to maintain a structured order or easily transfer, copy, or serve them elsewhere.

### Opinionated README Essentials:

1. **Clear Rules**: Clearly define all the rules, descriptions, structures, and provide examples in the README.

2. **Important Attachments**: Guidelines about adding images, naming them, where to store them in the repository, and even which services are best for creating diagrams and images.``

3. **Merging Strategy**: Adopt a merging strategy such as `squash on merge` to keep the commit history clean. However, while the document is under review, ask reviewers not to squash the commits. This allows for easy tracking of the document's evolution during the review process. Once finalized, it can be squashed for a cleaner history.

## Challenges and Solutions in Documentation Implementation

![Alt text](@assets/tdd/bund.png)

### 1. Resistance to Change

Teams may often be wary of new processes, especially those related to documentation.

**Solution:** Start by slowly introducing the system. Highlight its benefits and offer training to help with adoption.

### 2. Over-documentation Concerns

There's a risk of documenting too much, making it hard to find important decisions among minor ones.

**Solution:** Encourage teams to only document major and impactful decisions. The level of detail should match the decision's importance.

### 3. Behavioural Challenges

Some developers might avoid documentation, thinking it's boring or not useful.

**Solution:** Introduce the system step by step, send reminders, and consider having a committee to review important topics. The goal is to build a habit of documentation.

### 4. Reinforcing the Value of Experience

Decisions are based on experience and knowledge, but this can be lost over time.

**Solution:** Highlight that documentation helps save and share this valuable experience. It's not just about paperwork, but about preserving knowledge for the future.

### 5. Non-adoption of the System

People might simply not use the introduced documentation system.

**Solution:** Secure management's support. If someone is making technical decisions, encourage them to consult with the team through an RFC. After decisions are made in meetings, ensure they are recorded using an EDR. Initially, it's essential to monitor all the information emerging in the company closely — from proposals, designs, and more. Politely remind people to use the system, to create an RFC, or to document key points. With patience and consistency, piece by piece, a culture of documentation will be established.

## Conclusion

Introducing a comprehensive system for documenting technical decisions is a journey, not a sprint. Immediate results shouldn't be expected. Instead, companies and teams should recognize that this approach is a gradual integration into their culture. Initially, it might seem like an additional task with minimal immediate benefits. However, as the system grows and becomes richer with information, the advantages will become evident to all members. Over time, as everyone starts to see its utility, adoption will naturally increase.

In the early stages, leadership is crucial. Demonstrating commitment to the system, leading by example, and encouraging others to see its long-term value are essential steps. By continually emphasizing the importance of this structured documentation, and by actively using it, leaders can foster a culture where recording decisions becomes second nature.

In the end, patience and persistence will be rewarded with a robust documentation system that benefits the entire team, aiding in onboarding, decision-making, and ensuring the preservation of invaluable knowledge and experiences.
