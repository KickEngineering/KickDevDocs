---
icon: hand-wave
cover: .gitbook/assets/hero (1).png
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Welcome

Hey there! Welcome to the Kick Developer Docs 👋

You will find a range of features and documentation on how to integrate with the Kick API.

## A letter to the Developers

Hi :wave: Just want to let you know what we are working on in this closed-beta phase, to keep you up to date with what might be changing during this phase, what is stable and what is to come.

## API Roadmap

We're rapidly building a world-class Public API, the following table highlights the current status of various features available to developers.

Our goals during this phase is to get feedback and iterate quickly. We want to create a well crafted, stable API that works together seamlessly which means we will be continually improving the API over the Closed BETA period based on your feedback.

### Feedback

Following many other open source projects, we will use Github as our central point of feedback, bug reports and feature requests for the API. All this documentation is stored within a repository which we will make publicly accessible, to allow the community to contribute to the project. We might even look at publishing a public road map there, but we aren't at that stage yet.

#### Short term feedback

Although we will be extremely active on the Github Issues on the documentation repository, we will also provide a means for shorter feedback and discussion via a Discord channel. Here you can ask questions, have discussions with the devs that have created the API. We are pretty opinionated people so I think there should be some great discussions on how to make this API and the community around it the best it can be!

### Our Pipeline Currently

:green\_circle: - Stable

:orange\_circle: - Implemented pending changes

:blue\_circle: - In development

:red\_circle: - Not yet implemented

| Feature | Implemented | Status |
|---------|------------|---------|
| GET /users | 🟢 | Stable |
| GET /channels | 🟠 | Subject to change. Moving the query parameter from streamer_id to broadcaster_user_id |
| PATCH /channels | 🟢 | Stable |
| GET /categories/category_id | 🟢 | Stable |
| GET /categories | 🟢 | Stable |
| POST /chat | 🔵 | In progress |
| App Bots | 🔵 | In progress |
| App Access Token | 🔵 | In Progress |
| Webhook Event-Signature | 🔵 | In Progress |
| Webhook Event Structure | 🟠 | Will remove Channel ID from all events |
