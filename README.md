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

Hey there! Welcome to the KICK Dev Docs 👋

We’re excited to launch KICK’s Public API and officially welcome third-party developers into the KICK ecosystem.

Our first release contains a number of endpoints that cover a wide range of functionality on KICK.

We have more in the pipeline and are eager to collaborate with the community to better understand your top priorities.

We’ve made it easy to submit feedback and contribute. Our team is listening to the feedback to guide our next steps.

### Feedback

We love contributions! Feel free to check out our [CONTRIBUTING.md](CONTRIBUTING.md) for more information on submitting improvements or raising issues.

Following many other open-source projects, we will use GitHub as our central point of feedback, bug reports and feature requests for the API. All this documentation is stored within a repository which we will make publicly accessible, to allow the community to contribute to the project. We might even look at publishing a public road map there, but we aren't at that stage yet.

#### Short term feedback

While we’ll be very active on GitHub Issues, we also welcome quick feedback and discussions in our [Discord channel](https://discord.gg/SvyWXP5aWb). Here, you can ask questions, share your creations, and engage in conversations to help improve the API and the community experience!

## API Roadmap

We're rapidly building a world-class Public API with the following table highlighting the current status of various features available to developers.

Our goals during this phase is to get feedback and iterate quickly. We want to create a well-crafted, stable API that works together seamlessly which means we will be continually improving the API. We will keep you up-to-date with what we are cooking.

Check out our Public Roadmap [here](https://github.com/orgs/KickEngineering/projects/3).

## Changelog

| Date       | Description                                                    |
|------------|----------------------------------------------------------------|
| 02/12/2025 | Added delete app functionality                                 |
| 02/12/2025 | Added DELETE /chat/:message_id endpoint                        |
| 27/11/2025 | Added pinned_time_seconds field to kicks.gifted event payload  |
| 25/11/2025 | Made refresh tokens reusable/flexible                          |
| 25/11/2025 | Added tags and viewer_count to GET /categories/:id             |
| 21/11/2025 | Added custom_tags to GET /livestreams                          |
| 21/11/2025 | Added custom_tags to GET /channels                             |
| 27/10/2025 | Added GET /kicks/leaderboard endpoint                          |
| 21/10/2025 | Added kicks.gifted webhook event                               |
| 20/08/2025 | Added replies_to field on chat message sent event              |
| 28/07/2025 | Allow multiple broadcaster_user_id params on livestreams       |
| 22/07/2025 | Added created_at to chat message payload                       |
| 23/05/2025 | Added moderation banned webhook event                          |
| 21/05/2025 | Added moderation endpoints                                     |
| 05/05/2025 | Added livestream metadata webhook event                        |
| 15/04/2025 | Added reply chat message                                       |
| 08/04/2025 | Added get channels by slug                                     |
| 08/04/2025 | Added thumbnail to channels response                           |
| 07/04/2025 | Added expires_at to channel subscriptions payload              |
| 07/04/2025 | Added identity object to chat sender payload                   |
| 01/04/2025 | Added livestreams endpoint                                     |
