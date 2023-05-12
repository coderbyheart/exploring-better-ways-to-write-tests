# Exploring better ways to write tests

![Publish](https://github.com/coderbyheart/exploring-better-ways-to-write-tests/workflows/Publish/badge.svg?branch=saga)

Slides for my talk about exploring better ways to write tests

- [Markdown](./slides.md)
- [Interactive](https://coderbyheart.github.io/exploring-better-ways-to-write-tests/index.html)

## Abstract

Very often we focus on improving the way we write tests within our test
frameworks. I on the other hand invest time into building new test frameworks.
Over the last years I have worked on
[end-to-end testing cloud native applications](#it-does-not-run-on-my-machine-integration-testing-a-cloud-native-application),
which lead to the development of a BDD feature runner. This year I took the idea
even further with a focus on coming closer to the goal of living documentation:
the test files are now written in Markdown. In addition I started to work on
fixing another big issue that we encounter often:
[our inability to provide good architecture documentation](/twitter/status/1381512195612246018)
... what we need is not big, huge architecture diagrams for entire systems (like
we get when we use C4, Arc42), but diagrams that are context-sensitive. BDD is
actually a great source for these kinds of diagrams and this is what I want to
share in this talk.

### Key take-aways

- that testing, developing and documentation go hand in hand
- that we as people working on these system need to look at our tools and find
  ways to improve them
- ideas on how to build living, understandable, up-date architecture diagrams
- new ideas about the features of GitHub Actions, traceability and automated
  diagram generation

## Viewing

An up-to-date version is published to
[GitHub pages](https://coderbyheart.github.io/exploring-better-ways-to-write-tests/index.html).

Press `s` to show the speaker notes.

### Locally

Open the project using
[Dev Container](https://code.visualstudio.com/docs/remote/containers).

Open two shells:

1. `npm run watch`
2. `npm start`

You can now view the slides at <http://127.0.0.1:8000>.

## Building

Render to reveal.js:

    make build

Render to PowerPoint (useful for copying to a PowerPoint template):

    make public/slides.pptx
