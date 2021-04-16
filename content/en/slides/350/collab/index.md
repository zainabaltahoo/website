---
title: Collaboration
summary: How to utilize available tools to enable developers to work together
authors: []
tags: [isom350]
categories: []
date: "2021-04-16T13:12:50Z"
slides:
  # Choose a theme from https://github.com/hakimel/reveal.js#theming
  theme: moon
  # Choose a code highlighting style (if highlighting enabled in `params.toml`)
  #   Light style: github. Dark style: dracula (default).
  #   Available highlight themes listed in: https://highlightjs.org/static/demo/
  #   Use lower case names and replace space with hyphen '-'
  highlight_style: dracula

  diagram: true
  diagram_options:
    # Mermaid diagram themes include: default,base,dark,neutral,forest
    theme: base

  # RevealJS slide options.
  # Options are named using the snake case equivalent of those in the RevealJS docs.
  reveal_options:
    controls: true
    progress: true
    slide_number: c/t  # true | false | h.v | h/v | c | c/t
    center: true
    rtl: false
    mouse_wheel: true
    transition: concave  # none/fade/slide/convex/concave/zoom
    transitionSpeed: default  # default/fast/slow
    background_transition: slide  # none/fade/slide/convex/concave/zoom
    touch: true
    loop: false
    menu_enabled: true
    chalkboard_enabled: true
    history: true
---


# ISOM 350
## Business Application Development

Mohammad AlMarzouq

Collaboration in Software Development

---

## Types of Collaboration

- Synchronous
- Asynchronous

---

## Synchronous Collaboration

- Developer working together on the same file at the same time
- Enabled using replit.com multiplayer repls
- Great for knowledge sharing
  - A form of eXprogramming

--- 

## Synchronous Collaboration Limitation

- Requires time scheduling
- Limited number of participants (Usually 2)
- Member contribution not tracked

---

## Asynchronous Collaboration

- Developers working together over time
- Enabled using Git and GitHub
  - Integrated with replit.com
- Requires agreement on workflow
- Better fit for large group collaboration and effort tracking

---

## Asynchronous Collaboration Limitations

- Steep learning curve
- Overhead to using the tools
  - Greater benefits with larger groups
  - Still useful for individuals
- Benefit of using collaboration tools might not be clear
- Success dependent on choice from endless workflows

--- 

## Class Workflow

```mermaid
graph TD
    A[Find new Task]
    B[Create New Branch]
    C[Work on Task]
    D[Commit Work Done]
    E[Send Pull Request to Project Manager]
    A --> B
    B --> C
    C --> D
    D -- Bug Exists --> C
    D -- Task or Fix Complete --> E
    E --> A
```
