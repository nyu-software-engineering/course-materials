---
layout: presentation
title: Feature Branch Version Control Workflow
permalink: /slides/feature-branch-workflow/
---

class: center, middle

# Feature Branch Version Control Workflow

Working on code in isolation and incorporating peer review

---

# Agenda

1. [Overview](#overview)
2. [Making Changes](#making-changes)
3. [Peer Review](#peer-review)
4. [Conclusions](#conclusions)

---

name: overview

# Overview

--

## Concept

Software projects in this course will follow a "feature branch" version control workflow, where changes are made in isolated branches.

Following this workflow allows team members to work independently while minimizing code code conflicts.

---

template: overview

## Repositories

The feature branch workflow requires each developer to have access to two repositories:

1. a centralized remote repository accessible by everyone on the team, such as a GitHub repository
2. a local clone of the remote repository

---

name: making-changes

# Making Changes

--

## Pull from central repository

Before making any changes, download the latest code from the shared central repository.

With the master branch on the local machine checked out:

```bash
git pull
```

Or, if you need to be specific about where to pull from:

```bash
git pull origin master
```

---

template: making-changes

## Create a new local branch

With the latest code downloaded, create a new branch and "check it out". The name of the branch should refer to the user story, task, or spike associated with the changes that will be made.

Example for a Task with identification number 9 belonging to a User Story with identification number 13:

```bash
git checkout -b user-story/13/task/9/implement-user-login
```

Example for Spike with identification number 6:

```bash
git checkout -b spike/6/install-mongo-db-locally
```

---

template: making-changes

## Update task board

In the GitHub Task Board for this Sprint, move the card for this Task or Spike to the appropriate "In Process" column.

---

template: making-changes

## Make changes locally

Pop open your favorite code editor and go crazy.

- A feature branch addresses an individual Task or Spike and thus should not be left unmerged with the master branch for more than a day (or ~2 days for students).
- A branch that has lived longer than 3 days is likely to lead you towards "merge hell".
- A branch that has lived longer than 3 days is a problem the entire team must address.

---

template: making-changes

## Commit changes to the local branch

Add all changed files to the branch in the local repository.

```bash
git add .
git commit -m "Implementing user login task from user story #13"
```

---

template: making-changes

## Merge with latest code from central repository trunk

Download the latest code from the master branch of the shared central repository, merge it into the local feature branch, and resolve any conflicts

With the feature branch checked out:

```bash
git fetch origin
git merge origin/master
```

---

template: making-changes

## Push branch to remote repository

Once the feature branch has been merged with any recent changes to the master branch, it's time to upload the feature branch to the shared remote repository.

For example, push a feature branch for a particular Task:

```bash
git push origin user-story/13/task/9/user-login
```

---

template: making-changes

## Issue pull request

Once the feature branch has been pushed to the remote repository, the developer must issue a Pull Request to their teammates requesting that they accept the changes into the `master` branch.

This Pull Request must be made using GitHub, and assigned to the teammates. This forces teammates to perform **peer code review** on the work before it is included in the `master` branch.

---

template: making-changes

## Update task board

In the GitHub Task Board for this Sprint, move the card for this Task or Spike to the appropriate "Awaiting Review" column.

---

name: peer-review

# Peer Review

--

## Review a pull request

A second developer must review the changes in the **pull request** and either accept or reject them.

- If rejected, the approver must specify the reasons and ask the original developer to fix the problems.
- The original developer must fix all problems and notify the approver.

Download the feature branch for review

```branch
git checkout user-story/13/task/9/user-login
git pull
```

Look at the code, test it, Try it, etc.... make sure it works!

---

template: peer-review

## Merge changes locally

If approved, the reviewer and the original developer coordinate so that one of them merges the changes in the feature branch into the `master` branch.

Example of getting latest code and merging into `master`:

```bash
git checkout user-story/13/task/9/user-login
git pull
git checkout master
git pull
git merge user-story/13/task/9/user-login
```

---

template: peer-review

## Upload changes to remote repository

Once the changes have been merged into the local `master` branch, the developer who merged must upload the changes to the remote repository.

With the `master` branch checked out:

```bash
git push origin master
```

---

template: peer-review

## Update task board

Whoever merged the code must now move the corresponding Task into the "Done" column of the task board.

---

name: conclusions

# Conclusions

--

Thank you. Bye.
