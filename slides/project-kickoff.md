---
layout: presentation
title: Project Kickoff
permalink: /slides/project-kickoff/
---

class: center, middle

# Project Kickoff

Setting appropriate expectations

---

# Agenda

1. [Ready, Set, Go!](#ready-set-go)
2. [Division of Labor](#division-of-labor)
3. [Discord](#discord)
4. [GitHub](#github)
5. [Product Backlog](#product-backlog)
6. [Planning Poker](#planning-poker)
7. [Sprint Backlogs](#sprint-backlogs)
8. [Task Boards](#task-boards)
9. [Git](#git)
10. [Daily Standups](#standups)
11. [Conclusions](#conclusions)

---

name: ready-set-go

# Ready, Set, Go!

--

## Kickoff

Teams are know working on their projects. Let's make sure your workflow and expectations are in order.

---

template: ready-set-go

## Sprints

Work is divided into increments:

- Sprint 0 - quick prototyping
- Sprint 1 - focus on front-end development
- Sprint 2 - adding in back-end development
- Sprint 3 - adding in database integration
- Sprint 4 - finishing what you've started

---

template: ready-set-go

## Expectations

- Teams [divide labor](#labor) fairly and wisely.
- Teams communicate primarily in-person and through [Discord](#discord).
- Teams use [GitHub](#github) as both a central code repository and a project management tool.
- The [Product Backlog](#product-backlog) represents the full list of user requirements of the project.  It gets updated regularly.
- Teams estimate work using [Planning Poker](#planning-poker) cards.
- A [Sprint Backlog](#sprint-backlogs) shows which user requirements are being worked on during the current Sprint.
- A [Task Board](#task-boards) shows the up-to-date status of all work at all times.
- Individuals use [Git](#git) systematically to isolate code and track changes.
- Teams meet primarily in person for [Daily Standups](#daily-standups).
- **At the end of each Sprint is the release of a working, but incomplete, product**.

---

name: labor

# Division of Labor

--

## Wise Use of Human Resources

- Do _not_ dedicate some humans to front-end development and others to back-end - **share all responsibilities**.
- Do _not_ let some members do all the database work - **share the responsibilities**.
- Do _teach_ each other what some of you know - **if teammates flounder, the whole team will suffer**.
- Do _not_ allow one person to dominate the role of Product Owner - **switch roles every Sprint**.
- Do _not_ allow one person to dominate the role of Scrum Master - **switch every Sprint**.
- Do _not_ assume your stakeholders (Professor, Tutor, Grader) will always tell you what to do and how to do it - **take initiative**.

---

name: discord

# Discord

--

## Channels

Each team must have two private channels set up in Discord, e.g.:

- `team_octapus` - general discussion
- `team_octapus_standups` - after each standup, document each member's answers to the three questions

Key stakeholders - professor and any course assistants, tutors, and graders - must be invited.

---

template: discord

## Organization

Each team is a member of the larger course organization.

All teams are using the same general technologies and facing the same problems.

Communicate with other teams via Discord. Help each other. Take initiative.

---

name: github

# GitHub

--

## Repository

All team members have access to their project's GitHub repository.

All repositories must include:

- **README.md** - an always up-to-date overview of the project
- **CONTRIBUTING.md** - detailed instructions that govern participation in the project
- **.gitignore** - a Git settings file that instructs git to not track certain directories and files

---

template: github

## Gitignore

Each repository must include a file named `.gitignore` in the root directory that instructs git to not track certain files and directories.

This file must instruct git to ignore (i.e. not track):

- **platform code** - e.g. React.js itself, Node.js itself, etc
- **3rd party library code** - e.g. any installed Node.js modules, python packages, etc
- **any files containing authentication credentials** - e.g. database username/password, Spotify API credentials, etc.
- **any files containing personal information** - e.g. if your app stores data about users in files or databases, don't track those

Here is an [example general-purpose `.gitignore` file](https://gist.github.com/bloombar/1bbca4aafb267920ac220864d99d6c8f).

---

name: product-backlog

# Product Backlog

--

## User Stories

Before work on a project can begin, it must have an initial *Product Backlog* - a set of user requirements for the project written in User Story form.

---

template: product-backlog

## Issues

Every GitHub repository has an `Issues` tab where User Stories in the Product Backlog should be written and stored.

- User Stories in the Product Backlog must be listed in order of importance

![GitHub user story issues](../images/github_issues_user_stories.png)

---

template: product-backlog

## Label

Create an Issue for each User Story in the Product Backlog and assign it the `user story` label to differentiate it from other types of Issues.

---

template: product-backlog
name: issue-numbers

## Issue Numbers

Once created, each Issue in GitHub is automatically assigned a unique Issue number.

You will use these numbers:

- to link up [Tasks](#tasks) to their associated User Stories.
- to link up Git [branches](#git-branches) to the issues they are meant to implement

![GitHub issue numbers](../images/github_issues_numbers.png)

---

template: product-backlog

## Issue Templates

Your use of GitHub's Issues feature must also make use of GitHub Issue Templates:

1. [Download a set of Issue Template Markdown files](https://gist.github.com/bloombar/3ba6ddd69b6364bf20a56d65ad590bd1/archive/a0aa9130ce8d86630669b67d1ec8ddae96e5f379.zip).
2. Place these example Markdown files into a directory in your repository named `.github`/`ISSUE_TEMPLATE`/.
3. Push them to the GitHub central repository.
4. Now every time you create a new User Story, Task, or Spike, GitHub will offer for you to use one these as a starter template.

---

name: planning-poker

# Planning Poker

--

## Work Estimation

At the start of each Sprint, team members discuss each User Story they are considering including in the new Sprint.

The group quickly assigns each User Story an estimated level of effort using Planning Poker or some other agreed-upon estimation scheme.

---

template: planning-poker

## Fibonacci

In planning poker, every member of the team must print a set of Fibonacci-based planning poker cards.

- Find a deck you like or design your own.
- Include a link to your deck on the CONTRIBUTING.md file.
- Bring them to Sprint Planning meetings.

![Planning poker cards](../images/agile_planning_poker.png)

---

name: sprint-backlogs

# Sprint Backlogs

--

## Selecting User Stories

Those User Stories selected for the current Sprint are added to the [Sprint Backlog](#sprint-backlogs).

In addition to the basic requirements for User Stories in the [Product Backlog](#product-backlog), User Stories in the Sprint Backlog must be assigned:

- a **GitHub Milestone** representing the current Sprint
- an **Estimate of Effort** required to complete the User Story
- a set of **Acceptance Criteria** for the User Story

![GitHub issue milestones](../images/github_issues_milestones.png)

---

template: sprint-backlogs
name: tasks

## Tasks

Each User Story selected for [the current Sprint](#sprint-backlogs) is immediately broken up into Tasks.

A `Task` is a unit of work that would ideally take one developer one day.

---

template: sprint-backlogs

## Task Requirements

- The description of each Task includes a reference to the User Story to which it belongs - writing the User Story's Issue ID number, e.g. #22, in the Task description will create a link to it.
- Each Task is assigned to a specific developer
- Each Task is saved as a GitHub Issue with the label, "task".
- Each Task is assigned the GitHub Milestone representing the current Sprint.

![GitHub issue tasks](../images/github_issues_tasks.png)

---

template: sprint-backlogs

## Spikes

Any work to be done that does not relate directly to a user requirement is documented as a Spike.

In GitHub, spikes are treated like Tasks in all respects except that they are labeled "spike", not "task".

---

template: sprint-backlogs

## Spike Requirements

- Each Spike is assigned to a specific developer
- Each Spike is saved as a GitHub Issue with the label, "spike".
- Each Spike is assigned the GitHub Milestone representing the current Sprint.

![GitHub issue spikes](../images/github_issues_spikes.png)

---

template: sprint-backlogs

## Proper Attribution

If the nature of the work requires a particular Task or Spike to be done independently by each developer, it must be split into separate Tasks or Spikes with each assigned to a single team member.

For example:

- If all team members must learn Node.js during Sprint 0, then each team member has an individual responsibility to complete this.
- There must be a distinct Spike on the Task Board for each team member indicating the current status of their personal work completing this.

---

name: task-boards

# Task Boards

--

## Concept

Each GitHub repository has a `Projects` tab, where Task Boards can be linked.

Make one Task Board for each Sprint. If your team were named `Octapus`, name your task boards:

- Team Octapus - Sprint 1
- Team Octapus - Sprint 2
- Team Octapus - Sprint 3
- Team Octapus - Sprint 4

---

template: task-boards

## Columns

Each Task Board must have the following columns:

- **Sprint Backlog (User Stories)** - the list of User Stories selected for this Sprint.
- **To Do (Tasks)** - the list of Tasks and Spikes that have not yet begun
- **In Process (Tasks)** - the list of Tasks and Spikes that are currently being worked on
- **Awaiting Review (Tasks)** - the list of Tasks and Spikes that are complete and awaiting peer review
- **Done (Tasks)** - the list of Tasks and Spikes that are complete and have passed peer review.

![GitHub task board columns](../images/github_task_board_columns.png)

---

template: task-boards

## Starting State

At the start of each Sprint, the current Task Board in GitHub must contain:

- the full list of User Stories selected for this Sprint in the "Sprint Backlog (User Stories)" column
- the full list of Tasks and Spikes in the "To Do (Tasks)" column

---

template: task-boards

## Changing State

The state of the Task Board must be kept up-to-date at all times.

- **User Stories always stay in the "Sprint Backlog" column**
- **Tasks and Spikes move around** - as developers work on their own assigned Tasks and Spikes, they are personally responsible for moving them to the appropriate columns.

---

template: task-boards

## Missing Work

Your performance evaluation/grade depends upon you accurately listing all work you are doing on the Task Board at all times.

**If you are doing work whose existence or status is not accurately reflected on the Task Board, you are not doing Agile Development and you will not receive credit for it.**

---

name: git

# Git

--

## Matching Credentials

The Git username and email you use on your development machine must match your GitHub account username and email.

```bash
git config --global user.name "Foo Barstein"
git config --global user.email fb1258@nyu.edu
```

---

template: git

## Clone

Each team member must clone their team's remote GitHub repository to their development machine.

---

template: git
name: git-branches

## Branches

Requirements:

- Make all changes to the code in isolated branches.
- Create a new branch for every Task or Spike under development.
- Never work directly in the `main` branch.
- Name branches after the User Story and Task/Spike which they are intended to implement, including:
  -- the user story issue number (if any)
  -- the task or spike issue number
  -- a shorthand name for the branch that describes what changes it includes

Examples:

- A branch intended to implement Task #9, which is part of User Story #13:

```bash
git checkout -b user-story/13/task/9/implement-user-login
```

- A branch intended to implement Spike #27:

```bash
git checkout -b spike/27/learn-react-js
```

---

template: git

## Peer Review

The developer who makes changes must never be the one to merge their own branch into the trunk.

1. The developer making changes must push their completed branch to GitHub and then issue a Pull request to the `main` branch
2. The same developer must, of course, update the position of the relevant Task that this branch implements on the Task Board.
3. A second developer must review the changes in the pull request, approve them if good, and merge them into `main`.

Both developers are responsible if poor quality code is integrated into the `main` branch.

---

name: daily-standups

# Daily Standups

--

## Concept

Every morning, the entire development team gets together. Everyone quickly and honestly answers three questions:

1. What did you do yesterday (or since last meeting)?
2. What are you doing today (or until next meeting)?
3. Do you have any problems that are blocking your progress?

---

template: daily-standups

## Documentation

The current Scrum Master must document each team member's answers to the three questions and post them to their team's Discord standups channel.

Include the Discored handle of each member and their responses and whether they were in-person or remote, e.g.

```
@foo_barstein (in-person):
- did: Completed 95% unit testing code coverage of codebase
- doing: Implementing the Observer design pattern
- blocking: Nothing
```

Include notes for all team members in a single post.

---

template: daily-standups

## Honesty

All teams must include in their Team Norms that team members agree to answer the Daily Standup three questions honestly and fully.

It is in all team members' interests to report blocking problems or underperforming team members to their "managers" immediately.

If a team member is doing the same work for several Standups in a row, yet is not reporting any blocking problems, this is a sign of a _big_ problem for the entire team.

---

name: conclusions

# Conclusions

---

# Conclusions

Thank you. Bye.
