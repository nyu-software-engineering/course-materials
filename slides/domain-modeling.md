---
layout: presentation
title: Domain Modeling
permalink: /slides/domain-modeling/
---

class: center, middle

# Domain Modeling

Identifying the entities existent in a problem space.

---

# Agenda

1. [Overview](#overview)
2. [Entities](#entities)
3. [Relationships](#relationships)
4. [Entity-Relationship Diagrams](#er-diagrams)
5. [Conclusions](#conclusions)

---

class: center, middle
name: overview

# Overview

---

# Overview

Developing and documenting a conceptual model of the _things_ that exist within the domain of the project, and the interrelationships among those _things_.

Domain models help break down and understand the _problem space_ within which work will be performed.

---

# Overview

Whereas use cases and user stories help understand the users and their interactions with the system, domain modeling helps understand the internals of the system to be built.

---

# Overview

## Living documentation

Domain models are _living documents_. They are continually refined as needed.

They are never _done_ and never _exhaustive_. They are _conversational_ in nature.

They provide only as much information as is useful to those involved in a project.

---

# Overview

## Living documentation

As you work on a project, your understanding of the domain expands.

Keeping an up-to-date domain model can help all involved agree on the details of the domain.

---

class: center, middle
name: entities

# Entities

---

# Entities

Entities are the _things_ that exist in the domain of a project that must be documented.

Entities may be people, processes, system components, databases, or any other _noun_.

---

# Entities

## Process

Identifying _entities_ is easy (if you have written documentation of the project).

- Go through all existing documentation and write down all the _nouns_.
- Consolidate any synonyms that describe the same _thing_.
- Remove any _nouns_ that are, in fact, attributes or properties of other _nouns_ - these are not entities.

---

# Entities

## Diagramming

Domain models follows a standardized modeling style defined by the Unified Modeling Language (UML), a commonly-used diagramming language.

- Entities are placed in rectangles.

---

# Entities

## Example

![Entities example](https://knowledge.kitchen/mediawiki/images/2/24/Identifying_entities_in_a_domain_model.png)

---

class: center, middle
name: relationships

# Relationships

---

# Relationships

Once _entities_ are established, document the _relationships_ or _interactions_ among them.

- How many of each _entity_ are involved in the relationship? This is the _multiplicity_ of the relationship

---

# Relationships

## Diagramming

Domain models follows a standardized modeling style defined by the Unified Modeling Language (UML), a commonly-used diagramming language.

- Relationships are drawn as lines between the related entities.
- The _multiplicity_, or how many instances of each entity are involved in a given relationship, are notated next to the relevant entity.

---

# Relationships

## Example

![Simple relationships example](https://knowledge.kitchen/mediawiki/images/0/09/Domain_model_simple_example.png)

---

# Relationships

## Example

This example contains additional details about each _entity_:
![More complex relationships example](https://knowledge.kitchen/mediawiki/images/0/09/Domain_model_example.png)

---

class: center, middle
name: er-diagrams

# Entity-Relationship Diagrams

---

# Entity-Relationship Diagrams

In database design, very similar diagrams are created, called Entity-Relationship Diagrams (ERD).

- The two are done for different purposes, but the style of diagram is very similar.

---

class: center, middle
name: conclusions

# Conclusions

---

# Conclusions

Thank you. Bye.
