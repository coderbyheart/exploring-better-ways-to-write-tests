---
title: Exploring better ways to write tests
theme: white
slideNumber: true
header-includes: |
  <link href="https://fonts.googleapis.com/css2?family=Work+Sans:wght@300;400;500&display=swap" rel="stylesheet">
  <style>
   .reveal h1, .reveal h2, .reveal h3, .reveal h4, .reveal h5, .reveal h6 {
      font-weight: 300;
      text-transform: none;
      font-family: var(--heading-font);
      color: #e00073;
   } 
   .reveal {
        font-size: var(--main-font-size);
        font-family: var(--main-font); 
        font-weight: 400;
        font-size: 32px;
        height: calc(100% - 60px);
   }
   .reveal strong {
        font-weight: 500;
   }
   .reveal a {
      color: #0069CC;
   }
   .reveal a:hover, .reveal a:active {
      color: #007EF5;
   }
   .reveal u {
      text-decoration-color: #e00073;
   }
   .reveal ul {
     list-style-type: square;
     list-style-color: #e00073;
   }
   .reveal li::marker {
     color: #e00073;
   }
   .reveal li {
     margin-bottom: 0.75rem;
   }
   :root {
        --main-font: 'Work Sans', sans-serif;
       --heading-font: 'Work Sans', sans-serif;
   }
   .reveal-viewport {
     background-color: #fff;
   }
   .reveal-viewport::after {
      content: "@coderbyheart | CC-BY-NC-SA-4.0";
      position: absolute;
      bottom: 0; 
      left: 0;
      width: 100%; 
      height: 60px;
      background-color: #191919;
      color: white;
      font-family: var(--main-font);
      font-size: 22px;
      font-weight: 500;
      line-height: 60px;
      padding-left: 10vw;
   }
   #markus-tacker img {
      border-radius: 100%;
    }
    #markus-tacker ul {
      font-size: 80%;
      margin-top: 6rem;
    }
    #markus-tacker div.column:first-child {
      text-align: center;
    }
    #title-slide h1 {
      color: #e00073;
      font-weight: 500;
      font-size: 60px;
    }
    #title-slide h1:after {
      content: "Nordic Testing Days | Tallinn";
      display: block;
      color: #222;
      padding: 1rem;
      margin-top: 2rem;
      font-weight: 300;
      font-size: 32px;
    }
    #title-slide:after {
      content: "June 2023";
      font-size: 22px;
      color: #191919;
      font-style: italic;
    }
    figcaption {
      display: none;
    }
    div.column {
      text-align: left;
      width: calc(50% - 1rem); 
      margin-right: 1rem;
    }
    div.column + div.column {
      margin-left: 1rem;
      margin-right: 0;
    }
    .slide p {
      text-align: left;
    }
    div.text-center p {
      text-align: center;
    }
    .reveal pre {
      box-shadow: none;
    }
    .reveal .slide-number {
      bottom: initial;
      top: 8px;
      color: #333;
      background-color: transparent;
      font-size: 36px;
    }
  </style>
---

# Markus Tacker

:::::::::::::: {.columns}

::: {.column width=40%}

![Markus Tacker](./markus.webp){width=50%}

:::

::: {.column width=48%}

Principal R&D Engineer  
Trondheim

[\@coderbyheart@chaos.social](https://chaos.social/@coderbyheart)

<small>Pronouns: he/him</small>

:::

::::::::::::::

# Preface

I need to do
[a lot of end-to-end testing](https://coderbyheart.com/talks#it-does-not-run-on-my-machine-integration-testing-a-cloud-native-application),
but I am not _really_ happy with the tools.

So I wrote a _new_ test framework: _\*sigh\*_.

I'd rather I didn't, but it actually adresses the main shortcomings I see with
the tools that _I_ know to be available.

So let's have a look at what's missing...

# Need 1: Better way to write end-to-end tests

The way I write tests sucks...

# Gherkin intro

This is Gherkin syntax
[from the source](https://cucumber.io/docs/gherkin/reference/):

```gherkin
Feature: Guess the word

  # The first example has two steps
  Scenario: Maker starts a game
    When the Maker starts a game
    Then the Maker waits for a Breaker to join

  # The second example has three steps
  Scenario: Breaker joins a game
    Given the Maker has started a game with the word "silky"
    When the Breaker joins the Maker's game
    Then the Breaker must guess a word with 5 characters
```

# Using Gherkin in my projects

[Example](https://github.com/NordicSemiconductor/asset-tracker-cloud-aws-js/blob/e620758645d9768ec55ac8e2512e43b9970dbb24/features/DeviceMessages.feature)

Problems not well covered by Gherkin:

- low level API calls
- dependency to other Feature
- asynchronous result

Note: This is intentionally **NOT** following
[the Gherkin recommendation](https://cucumber.io/docs/bdd/better-gherkin/)
(because client is a machine)

Note 2: we don't have business people writing the scenarios.

# Improve Gherkin: BDD Markdown

<https://github.com/NordicSemiconductor/bdd-markdown-js>

[Supported syntax](https://raw.githubusercontent.com/NordicSemiconductor/bdd-markdown-js/saga/parser/test-data/feature/Example.feature.md)

- Dependencies
- Retries
- Comments
- Formatted code
- Tables for examples

# Improve test runner: make asynchronous behaviour first party citizen

- [`Soon` keyword](https://github.com/NordicSemiconductor/bdd-markdown-js/blob/dfa44aa6f7ea6c69087a8d333456f67d1069c550/examples/mars-rover/MarsRover.feature.md#hit-an-obstacle)

# Integrate Markdown with GitHub Actions

<https://github.com/NordicSemiconductor/bdd-markdown-js/actions/runs/4954467574#summary-13422645884>

# Need 2: I need architecture diagrams

- Manually creating them works, but maintaining is a mess

# Example: Backend Architecture diagrams using C4 and Miro

- [C4 model](https://c4model.com/)

# System Context Diagram

![System Context Diagram](./Iris\_ System Context Diagram.jpg)

# Container Diagram

![Container Diagram](./Iris\_ Container diagram.jpg)

# Component Diagram

![Component Diagram](./Component diagram\_ Backend - Backend.jpg)

# Solution: Create from test runs

Generate architecture diagrams
[from test runs](https://github.com/NordicSemiconductor/cloud-bdd-markdown-e2e-example-aws-js "‌")

[Example](https://github.com/NordicSemiconductor/cloud-bdd-markdown-e2e-example-aws-js/actions/runs/4956101677#summary-13426591516)

# The Future? Combine everything in one UI!

![Idea](./idea.jpg)

# Interactive Architecture Diagram

We need to put the flow of events first

- Show all the Features, filter by feature -> show only the components and
  events used
- Show all the components, filter by component -> which features use this
  component?
  - Which features have a lot of overlap in component usage
- Inventory of all events -> filter events that include e.g. an email, which
  components are used?

# Thank you

<div class="text-center">

Please share your feedback!

<small>[m@coderbyheart.com](mailto:m@coderbyheart.com)  
[\@coderbyheart@chaos.social](https://chaos.social/@coderbyheart)</small>

<small>Latest version:  
[`bit.ly/better-test-tools`](https://bit.ly/better-test-tools)</small>

We are hiring!  
[nordicsemi.com/jobs](https://nordicsemi.com/jobs)  
<small>Trondheim &middot; Oslo &middot; 20+ more locations</small>

</div>
