---
title: Implementing a Technical Decision Documentation
author: Andrey Yurchenkov
datetime: 2023-10-23T00:17:19Z
slug: two-types-of-software-engineers
featured: false
draft: false
tags:
  - team
  - engineering
  - en
description:
---

Implementing a Technical Decision Documentation

In today's software development landscape, the significance of properly and timely documenting technical decisions cannot be overstated. Doing so not only helps preserve knowledge within teams but also accelerates the development process, preventing duplicated efforts and mistakes.

**Purpose of the article:** This piece aims to describe a novel system for documenting technical decisions, rooted in the GitHub platform's capabilities. We'll delve into the reasons behind this choice, the advantages of categorizing technical decisions, the primary motivations for adopting such a system, and the challenges faced during its adoption.

Choosing a Platform for Document Location: Why GitHub?

When it comes to choosing a platform to house technical documentation, there are several considerations to keep in mind. Among the myriad of options available, GitHub stands out for the following reasons:

1. **Local File Accessibility**: With GitHub, all documents are always stored locally. This means that files can be easily transferred without the hassle of navigating through cloud storage or other remote repositories.

2. **Version Control**: GitHub, being a Git-based platform, inherently offers version control. Every team member will always have the most recent version of a document, ensuring everyone is on the same page.

3. **Familiarity for Technical Teams**: Developers and other technical staff are already accustomed to GitHub. Introducing a new platform can be a challenging endeavor, so leveraging tools that the team is already familiar with can simplify the adoption process.

4. **Pull Requests for Discussion**: All discussions around the documentation can be preserved in pull requests. This feature provides an organized way to track feedback, amendments, and approvals.

5. **Highlight Specific Points**: Unlike issues, pull requests in GitHub allow for highlighting specific parts of the document. This makes the review process more streamlined and focused.

6. **Notification Configuration**: GitHub offers robust notification settings. Teams can set up alerts for new document pull requests, ensuring everyone is timely informed and can participate in discussions.

By centralizing documentation in GitHub, teams can enjoy a unified, version-controlled, and collaborative environment that enhances the overall efficiency and clarity of the technical decision-making process.

Categorizing Technical Decisions: Why Not Just RFCs?

While Request For Comments (RFCs) have been a mainstay in the OpenSource community for technical decision-making, there are distinct advantages to categorizing technical decisions for in-house teams and projects. Here's why:

1. **Predictability**: By categorizing technical decisions, team members know what to expect. They can quickly identify the type, scope, and implications of a decision based on its category.

2. **Addressing Technical Debt**: Every company accumulates technical debt over time. Many of these issues might be undocumented or not widely known. Categorizing them provides a clear structure to document, address, and track these pending tasks.

3. **A Holistic View**: While RFCs are excellent for individual proposals or changes, a categorized approach offers a broader perspective. Teams can see patterns, recurring challenges, and areas that require more attention.

4. **Learning from Past Experiences**: Consider a scenario where a team tried to address an issue in the past but didn't implement the solution. By having a categorized record, a new team can access this historical data, understand the reasons, and perhaps approach the problem with fresh insights.

5. **Evolving Nature of Tech**: Technologies, tools, and best practices are continuously evolving. What might not have been feasible a few years ago could be possible today. Categorized technical decisions can act as a timeline, showcasing the evolution of thoughts, tools, and solutions.

In essence, while RFCs are undoubtedly valuable, especially in open-source projects, the dynamic nature of in-house projects and the multifaceted challenges they present make a case for a more structured and categorized approach to technical decision-making.

Motivation Behind Adopting This System

Embracing a structured documentation system for technical decisions is not just about organizing information; it's about fostering transparency, collaboration, and informed decision-making. Here's why this system is so compelling:

1. **Transparency Across Teams**: With diverse teams working on different aspects of a project, there's a real risk of duplicated efforts or teams unknowingly tackling the same challenges. A centralized documentation system ensures that everyone is on the same page, reducing redundancy and promoting synergy.

2. **Leveraging Previous Experiences**: Teams can avoid 'reinventing the wheel' by accessing documented attempts, successes, or failures from past initiatives. This historical perspective can offer invaluable insights and accelerate problem-solving.

3. **One Source of Truth**: Consolidating all documentation in one location, like a repository, simplifies the search process. Whether it's a new team member trying to get up to speed or a seasoned developer looking for specific details, everyone knows where to find the information they need.

4. **Avoiding Fragmented Information**: Without a unified system, information tends to scatter across different platforms — from personal notes, chat threads, shared documents to internal wikis. This scattering not only complicates retrieval but also jeopardizes the completeness and accuracy of the data.

5. **Promoting a Culture of Documentation**: By standardizing the documentation process, organizations implicitly emphasize its importance. Over time, this can cultivate a culture where documentation becomes second nature to developers, improving project handovers, onboarding processes, and overall team efficiency.

In essence, the push for this documentation system goes beyond mere organization. It's about maximizing team productivity, learning from past endeavors, and ensuring that all team members, regardless of their role or tenure, have the insights they need to contribute effectively.
Challenges and Solutions in Implementation

Resistance to Change

Many developers and teams may be skeptical about introducing new processes, especially when it pertains to documentation. Unfamiliarity with this mode of operation and the lack of immediate benefits can pose barriers to active participation.

**Solution:** Gradual introduction, coupled with highlighting the long-term benefits of clear documentation. It's essential to provide training and perhaps even incentives to get everyone on board.

Over-documentation Concerns

One of the concerns that might arise is the potential for excessive documentation. Not every decision, no matter how small, requires an extensive document to justify or explain it.

**Solution:** Communication is key. Teams should be instructed to focus on documenting critical and impactful decisions. The granularity of documentation should be in line with the scale and significance of the decision.

Behavioural Challenges

Adoption is often a behavioural issue. Developers, inherently, might not be inclined towards documentation due to various reasons, including the perception of it being tedious.

**Solution:** Slow introduction, reminders, perhaps setting up a review committee to discuss open topics, and steadily cultivating a culture of documentation is the way forward.

Reinforcing the Value of Experience

Every decision in the development process involves a lot of information processing. This information, which is essentially experience, often gets lost. But it's the experience for which companies spend money and developers invest their time.

**Solution:** Emphasize the need for documentation not just as a means of record-keeping, but as a way to store collective experience. Make it clear that the goal isn't just to create documents, but to capture and share knowledge.

Conclusion

In the rapidly evolving world of technology, clear and concise documentation of technical decisions is not just beneficial—it's essential. By selecting a platform like GitHub for document localization, categorizing technical decisions, and understanding the motivations behind this systematic approach, teams can ensure that their processes are transparent and that knowledge is easily accessible.

However, the journey to successful implementation may not always be smooth. Recognizing potential challenges and preparing for them is crucial. Yet, with a steadfast commitment and a clear understanding of the advantages this system brings, organizations can foster a culture where documentation becomes an integral part of their workflow.

The ultimate goal is to cultivate an environment where teams are empowered with the knowledge of past decisions, ensuring that they are well-informed as they pave the way for future innovations.
