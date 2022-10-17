---
layout: presentation
title: User Experience Design
permalink: /slides/user-experience-design/
---

class: center, middle

# User Experience Design

Ensuring software will work for the people who will use it.

---

# Agenda

1. [Overview](#overview)
2. [Discovery](#discovery)
3. [Design](#design)
4. [Reflection](#reflection)
5. [Conclusions](#conclusions)

---

name: overview

# Overview

---

template: overview

## Concept

User Experience Design (UX), sometimes called Customer Experience Design (CX) or Interaction Design (IxD), is the design of products and services in a way that achieves business goals while also meeting the needs, goals, and abilities of end-users.

---

template: overview

## Cross-Discipline

User Experience Design (UX) often requires a mixture of cross-discipline skills:

- **Technological** - e.g. comprehending what designs are technically feasible
- **Business** - e.g. internalizing the business goals at the core of all designs
- **Psychological** - e.g. predicting people's behavioral tendencies in particular contexts
- **Social** - e.g. bridging the gap between business and product development
- **Aesthetical** - e.g. abiding by conventions and norms in visual and interaction designs

---

template: overview

## Difference

User Experience Design (UX) is not a replacement for...

- **Visual Design** - e.g. the perfect static design of all interface components like images, buttons, icons and other components.
- **User Interface Design** - e.g. the perfect static design of all screens an end-user will see
- **Development** - e.g. writing code
- **Business Strategy** - e.g. identifying an organization's core business goals and how to approach them
- **Market Research** - e.g. identifying competitors in the market and the behaviors and attributes of target end-users/customers

---

template: overview

## Assumptions

We design for people with a few assumptions in mind:

--

- **People use things for a reason**: typically a desire or need that they are trying to fulfill.

--

- **Creators have motives for making things**: often profit, esteem from peers, "keeping up-with-the-Jones's", etc.

--

- **Technologies all have constraints**: every tool has its inherent limitations that restrict what can be done with it.

---

template: overview

## Everyone loves Venn diagrams...

... and User Experience Designers try to make all parties happy. This inevitably involves compromise.

![Venn diagram](../images/ux_venn_diagram.png)

---

name: discovery

# Discovery

---

template: discovery

## Concept

Similar to requirements gathering for software development as a whole, User Experience Design work often begins with the **discovery** of at least:

- organization's business goals
- end-user's needs and desires
- any technical constraints

---

template: discovery

## Method

As with **requirements gathering** more generally, User Experience Design discovery could involve:

- **Stakeholder interviews** - speak with the important people at the organization for whom the product is being designed.

--

- **Competitive analysis** - see what the competitors are doing in this same space.

--

- **User interviews and observation** - speak with potential users and observe them while they go about doing the things your tool is intended to facilitate.

--

- **Demographic research** - review market research to understand the typical desires, problems, and needs of the average person in the demographic(s) you are targeting.

--

... and anything else they can get their hands on ...

- review of an existing iteration of a given product or service
- review of any internal documenation of the product or service
- review of any analytics of the performance or success of the product or service

---

template: discovery

## Artifacts

As a result of the discovery process, the following artefacts may be produced

- **discovery document** - documents what has been discovered at a high level
- **requirements document(s)** - one or more documents outlining what must be done (e.g. business requirements, technical requirements, functional requirements, design requirements, content requirements)
- **content strategy** - how to approach the problem of developing content for the target audience
- **personas** - imaginary stereotypes of the different types of end-users of concern
- **user scenarios** - a form of requirements sometimes misleadingly called "use cases" - these describe situations in which end-userss may find themselves and how the product or service meets their needs

---

name: design

# Design

---

template: design

## Concept

Design is the implementation of the plans and blueprints of the product or service **from a user's perspective**.

It is not the implementation of the product or service itself.

---

template: design

## Method

User Experience Design process involves drafting sufficient written documents, diagrams, and sometimes prototypes to show all parties how a product or service would function over time, from a user's perspective.

---

template: design

## Artifacts

The documents drafted might include:

- flow diagrams
- ecosystem maps
- user journey maps
- content audit / gap analysis
- site map / app map
- wireframe diagrams
- prototypes

---

name: site-maps

# Site/App Maps

--

## Concept

Site/app maps are diagrams intended to show the number of categories of screens (e.g. web pages or app screens) that exist in a given web site and how many screens exist or must be built within each category.

---

template: site-maps

## Example

An example of a simple site map of a shoe shop web site.

![Site map example](../images/ux_site_map_example.png)

---

template: site-maps

## Communication goals

Site/app map diagrams are simple, fast, easy-to-draw diagrams that communicate...

--

- **the number of unique design templates** that must be created.

--

- what **categories** of screens exist in a site.

--

- the **number of levels** of screens within each category, if a user were to _drill down_ step-by-step from each category _landing screen_ to its children screens.

---

template: site-maps

## Prohibitions

Site/app maps, in order to best serve their purpose, should not...

--

- indicate more screens than you are capable of developing, filling with content, and maintaining - **make a plan that is achievable**.

--

- attempt to show every link from every screen to every other screen - **draw lines for parent-to-child relationships only**

--

- have more levels than absolutely necessary - **err on the side of fewer levels**.

--

- have more categories than necessary - **err on the side of fewer categories**.

---

name: wireframes

# Wireframe diagrams

--

## Concept

There are many types of specialized diagrams and documents produced by User Experience Designers to serve different communication needs:

--

- flow diagrams
- ecosystem maps
- user journeys
- content audits
- information taxonomies
- and more...

--

For our purposes - designing and developing screens quickly and mostly on our own - **wireframe diagrams** are the easiest to understand and produce, and provide the greatest benefit.

---

template: wireframes

## Example

An example of a perfect wireframe diagram representing a screen.

![Wireframe diagram example](../images/ux_wireframe_example.jpg)

---

template: wireframes

## Communication goals

Wireframe diagrams are simple, fast, easy-to-draw diagrams that communicate...

--

- what **type of content** will be on each screen.

--

- the approximate **position and size** of each piece of content.

--

- **notes** about any content or interactive behavior that is not obvious just looking at the diagram

---

template: wireframes

## Prohibitions

Wireframes, in order to best serve their purpose, should not include...

--

- **color** - everything should be black, white, and gray

--

- **design** - no shadows, fancy fonts, logos, icons or other graphics

--

- **real images** - use placeholder boxes instead where an image would go

--

- **real text** (also known as 'copy') - use '[lorem ipsum](https://en.wikipedia.org/wiki/Lorem_ipsum)' placeholder copy instead

---

template: wireframes

## Number

Each wireframe diagram acts as a template that is then re-used for one or more screens. Most web designers will produce distinct wireframe diagrams for at least each of the following...

--

- **home screen** - these are usually unique and follow a different template from other screens.

--

- **each level of the site/app map** - screens at the same depth level will generally follow the same, or similar, template - one for each level.

--

- **unique screens** - some screens are, by nature, somewhat unique in content and/or layout - for example "Contact Us" screens with _forms_, marketing _brochure-like_ screens intended to give a unique look-and-feel, and others...

--

- **overlays** - any content that appears superimposed over other content when something is clicked or moused over, such as a _hamburger menu_.

---

name: flow-diagrams

# Flow diagrams

--

There are many different uses for flow diagrams - they are a general diagramming style to show directionality.

--

- One useful application within User Experience Design is to show the flow of control from one screen to another in an application or web site.

--

- This can make it very clear how the screens connect to one-another as the user uses the site/app.

---

template: flow-diagrams

![Flow diagram with wireframes](../images/ux_flow_diagram_with_wireframes.png)

---

name: software

# Diagrammming Software

--

## Tools of the trade

User Experience Designers use a variety of tools to make diagrams - each organization has their own preferred toolkit. Some common options:

--

- Pencil & paper - the original classic

--

- [Draw.io](https://draw.io) - open source, always free

--

- [Figma](https://www.figma.com/) - free tier available

--

- [Sketch](https://www.sketch.com/) - free trial available

--

- [Axure RP](https://www.axure.com/) - free trial available

--

- [Omnigraffle](https://www.omnigroup.com/omnigraffle/) (Mac only) - free trial available

---

template: software

## Our choice (for beginners and for all UML diagramming)

When in doubt, use [draw.io](https://draw.io) to build your wireframes, site/app map, and any other diagrams.

- no frills
- no cost
- perfect for a small app or website

---

template: software

## Our choice (for pros and those who like good sophisticated apps)

[Figma](https://figma.com) is currently the best-in-class application for developing wireframe diagrams, prototypes, and many other sorts of diagrams and designs.

- complex functionality
- free trial
- a necessary tool for sophisticated apps or websites

---

name: prototyping

# Prototyping

--

## Concept

Once initial wireframe diagrams have been drafted, it's easy to put together a **clickable prototype** of a web site using those wireframes. Benefits of a building a prototype include...

--

- for stakeholders to all agree that this is **how the website will function**.

--

- to **count how many clicks or taps** it might take for a user to get to the content that interests them.

--

- to **show to potential end-users** to get their feedback.

--

- to **do a sanity check** before spending time and effort building the site.

---

template: prototyping

## Software tools

There are a variety of software tools for building web site prototypes.

--

- [Figma](https://www.figma.com/) - free tier available

--

- [InvisionApp](https://www.invisionapp.com/) - 1 free prototype with signup

--

- [Adobe XD](https://adobe.com/xd) - limited free version available

--

- [Axure RP](https://www.axure.com/) - free trial available

--

- [Proto.io](https://proto.io/) - free trial available

---

template: prototyping

## Our choice (when all else fails)

Use [InvisionApp](https://invision.com) to build your clickable prototypes.

- easy to use
- 1 free prototype is all we need

---

template: prototyping

## Our choice (for pros and those who like sophisticated tools)

[Figma](https://figma.com) has complex prototype functionality.

- this is overkill for most projects.
- this may scare away newbies.
- you've been warned.

---

template: prototyping

## Requirements

When creating a clickable prototype, meet the following minimal requirements:

--

- all buttons, links or other user interface components that allow a user to navigate from one screen to another must be functional in the prototype

--

- create as many variations of your existing wireframe diagrams as you need in order to make the prototype look "believable"; give a real sense of how the application flow might work... don't take shortcuts.

--

- your prototypes must be designed to clearly show the way in which a user navigates from one screen to another, as well as how they solve the core use cases and needs your web site is designed to solve.

---

name: reflection

# Reflection

---

template: reflection

## Concept

Reflection is the determination of success or failure.

Once the product or service has been launched, in order to understand whether it is a success or not, clear business goals must have been addressed at the beginning.

---

template: reflection

## Methodology

- User Acceptance Testing (UAT)
- A/B Testing
- End-User interviews / observation

---

name: conclusions

# Conclusions

--

At this point you have a just enough information to get into trouble starting to design experiences, including site/app maps, wireframes, and building clickable prototypes. Go for it!

- Check out an [example of a prototype](https://invis.io/W7W59QSDZSY) that is not yet fully complete.

- Thank you. Bye.
