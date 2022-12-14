---
layout: presentation
title: Requirements Engineering
permalink: /slides/requirements-engineering/
---

class: center, middle

# Requirements Engineering

A disciplined approach to figuring out what needs to be done.

---

# Agenda

1. [Overview](#overview)
1. [Motivations](#motivations)
1. [Types](#types)
1. [User Requirements](#user-requirements)
1. [Business Requirements](#business-requirements)
1. [Compliance Requirements](#compliance-requirements)
1. [Security Requirements](#security-requirements)
1. [Requirements Elicitation](#elicitation)
1. [Conclusions](#conclusions)

---

name: overview

# Overview

--

Requirements engineering is the disciplined process of defining what a project requires to be done and how it must be done.

---

name: motivations

# Motivations

--

Requirements provide several benefits to a project:

- Clearly defining the features and functionality that must be developed
- Defining the performance, security, and maintainaibility of the system
- Assisting in the cost and time estimates of the project
- Avoiding disputes by having all parties agree on what is to be done

---

name: types

# Types

--

There are two top-level categories of requirements:

- Functional
- Non-functional

---

template: types

## Functional requirements

Functional requirements describe what the system must do, in layman's terms, including:

- Services the system must provide to its users
- How the system must behave in particular situations
- What outputs the system must provide in response to particular inputs

---

template: types

## Non-functional requirements

Non-functional requirements specify constraints on either the system or the development process, including:

- Business requirements, i.e. what must the project achieve when successful in order to improve the business and when must it be done
- Compliance requirements: standards or government regulations that must be complied with
- Platform requirements: constraints on platforms or technologies that must be used
- Performance requirements: e.g. speed, size, memory, uptime, reliability, load handling, portability
- Security requirements: what security measures and practices must be integrated into the software to protect sensitive data and systems.

---

name: user-requirements

# User Requirements

--

The main variety of functional requirement, focused on the user experience.

Define what a user must be able to do with the system, written in layman's terms.

There are two popular ways of writing user requirements:

- **Use Cases**
- **User Stories**

---

template: user-requirements

## Use Cases

Describe how an _actor_ achieves their _goals_ using the system.

A list of actions and events involved in a specific user interaction.

---

template: user-requirements

## Use Cases

At a minimum contains:

- **Title** - a short phrases with an active verb describing the goal of the interaction
- **Actor** - the person or system who desires the goal
- **Scenario** - step-by-step description of how the goal is achieved by the actor

---

template: user-requirements

## Use Cases

Example:

> Title: Purchase items
>
> Actor: Customer
>
> Scenario: Customer reviews items in shopping cart. Customer provides payment and shipping information. System validates payment information and responds with a confirmation of order and provides order number that Customer can use to check on order status. System will send Customer a confirmation of order details and tracking number in an email.

---

template: user-requirements

## Use Cases

Written use cases often are accompanied by a Unified Modeling Diagram Language (UML) diagram:

![Use case diagram](https://knowledge.kitchen/mediawiki/images/f/f4/Use_case_diagram_example.png)

---

template: user-requirements

## User Stories

An alternative to Use Cases, written in user-centric language:

As a **, I want **, so I can \_\_.

- First blank is filled with the actor
- Second blank is filled with the goal
- Third blan is filled with the motivation

---

template: user-requirements

## User Stories

Each User Story also may include:

- Estimated level of effort
- Acceptance criteria

---

template: user-requirements

## User Stories

Example:

> As a customer, I want to sign up so I can start placing orders.

--

This may have the following additional notes attached:

> Estimation of effort: M
>
> Acceptance criteria:
>
> 1. Customer name is captured and saved
> 2. Customer email is captured and saved
> 3. Customer phone number is captured and saved
> 4. Customer password is captured and saved
> 5. Invalid name, email, phone, and passwords are rejected
> 6. Customer is signed in automatically after registration
> 7. An error message indicates any invalid values entered into the form

---

template: user-requirements

## Use Cases vs. User Stories

![Use cases vs. user stories](https://knowledge.kitchen/mediawiki/images/1/11/Use_cases_versus_user_stories.png)

---

name: business-requirements

# Business Requirements

--

## Overview

An organization engages in a development project for a reason.  Business requirements documents document this reason and any other business constraints.  This may include:

- project objectives 
  - i.e. how success is defined: e.g. increased income, customer base, customer satisfaction, publicity, etc.
- the scope of the project
  - what will be done
  - initial timeline
  - initial resource plan
  - time constraints
  - budget constraints
  - any other resource constraints

... and so on ...

---

name: compliance-requirements

# Compliance Requirements

--

## Overview

Software used in certain industries or certain purposes must abide by government regulation or industry standards, e.g.

Government regulations:
- [Health Insurance Portability and Accountability Act](https://en.wikipedia.org/wiki/Health_Insurance_Portability_and_Accountability_Act) (HIPPA)
- [Children's Online Privacy Protection Act](https://en.wikipedia.org/wiki/Children's_Online_Privacy_Protection_Act) (COPPA)
- [Family Educational Right to Privacy Act](https://en.wikipedia.org/wiki/Family_Educational_Rights_and_Privacy_Act) (FERPA)
- [USA Patriot Act](https://en.wikipedia.org/wiki/Patriot_Act) (includes Know Your Customer requirement for financial institutions)
- [Federal Information Security Management Act](https://en.wikipedia.org/wiki/Federal_Information_Security_Management_Act_of_2002) (FISMA)
- [Sarbanes-Oxley Act](https://en.wikipedia.org/wiki/Sarbanes%E2%80%93Oxley_Act) (SOX)
- [Gramm-Leach-Biley Act](https://en.wikipedia.org/wiki/Gramm%E2%80%93Leach%E2%80%93Bliley_Act) (GLBA)
- [New York State Information Security Breach and Notification Act](https://ag.ny.gov/new-york-state-information-security-breach-and-notification-act)
- [Federal Financial Institutions Examination Council](https://en.wikipedia.org/wiki/Federal_Financial_Institutions_Examination_Council) (FFIEC)
- [EU General Data Protection Regulation](https://en.wikipedia.org/wiki/General_Data_Protection_Regulation)

... and so on ...

---

name: security-requirements

# Security Requirements

--

## Overview

Focused on three P's: 

--

- **P**roduct:  e.g. software defects/bugs, poor data handling, faulty configuration settings, use of insecure 3rd-party platforms or tools, 

--

- **P**eople: e.g. social engineering attacks, human error

--

- **P**rocess: e.g. lack of integration of security concerns throughout process, inadequate maintenance

---

name: elicitation

# Elicitation

--

## Techniques

How do you determine the requirements of a project?

- Interviews
- Observatiion
- Intuition & brainstorming

---

template: elicitation

## Midwifery

Why do we say we "elicit" requirements?

- engage key stakeholders in an ongoing dialog
- give them the opportunity and space to formulate and evolve their thoughts
- progressively elaborate on their ideas until a clear picture of the project emerges in their minds and yours
- engage them as collaborative partners in the process

---

template: elicitation

## Interviews

It would typically be a mistake not to interview:

- Key stakeholders
- A representative sample of end-users

---

template: elicitation

## Interviews (continued)

An interview can either be conducted in an _open_ or _closed_ manner.

- **Open interviews** - are open-ended discussions where the conversation meanders.
- **Closed interviews** - follow a prepared set of questions and topics for discussion.

---

template: elicitation

## Interviews (continued again)

Start broad:
- What problem does this product solve from a business perspective?  
- What opportunity does it take advantage of?

Go deeper:
- Who the users are and what their goals and challenges might be interacting the product.
- For each type of user, what specific functionality do they need to achieve each of those goals.

Very detailed:
- establish any and all remaining thoughts of what the user needs and how the system must work technically.

---

template: elicitation

## Observation

Observing end-users achieving their goals without your system, such as with...

- an _alternative system_ or solution
- a _prototype_ of your intended system
- an _earlier version_ of your system

---


template: elicitation

## Observation (again)

Similarly to interviews, observation can either be active or passive.

- **Scripted** - observer asks the user to perform certain tasks and then records how they complete it.
- **Unscripted** - the observer silentyly watchess the user performing their everyday tasks without interruption.

---

template: elicitation

## Intuition & brainstorming

Realistically, a requirements engineer (who may also be a software engineer) already has preeconceived notions of what users might want to do with the system based on their experience.

- Running brainstorming workshops where the requirements engineer asks a group of stakeholders about certain requirements that the engineer has already intuited can help build agreement on a pre-conceived plan.

---


name: conclusions

# Conclusions

---

# Conclusions

Thank you. Bye.
