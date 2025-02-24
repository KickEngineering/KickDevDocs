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

We love contributions! Feel free to check out our [CONTRIBUTING.md](https://github.com/KickEngineering/KickDevDocs/blob/main/CONTRIBUTING.md) for more information on submitting improvements or raising issues.

Following many other open-source projects, we will use GitHub as our central point of feedback, bug reports and feature requests for the API. All this documentation is stored within a repository which we will make publicly accessible, to allow the community to contribute to the project. We might even look at publishing a public road map there, but we aren't at that stage yet.

#### Short term feedback

While we’ll be very active on GitHub Issues, we also welcome quick feedback and discussions in our [Discord channel](https://discord.gg/kick). Here, you can ask questions, share your creations, and engage in conversations to help improve the API and the community experience!


## API Roadmap

We're rapidly building a world-class Public API with the following table highlighting the current status of various features available to developers.

Our goals during this phase is to get feedback and iterate quickly. We want to create a well-crafted, stable API that works together seamlessly which means we will be continually improving the API. We will keep you up-to-date with what we are cooking.

### Our Pipeline Currently

🟢 - Stable

🟡 - New

🟠 - Implemented pending changes

🔵 - In development

🔴 - Not yet implemented

| Feature                             | Implemented      | Status              |
| ----------------------------------- | ---------------- | ------------------- |
| GET /users                          | 🟢               | Stable              |
| GET /channels                       | 🟢               | Stable              |
| PATCH /channels                     | 🟢               | Stable              |
| GET /categories/category\_id        | 🟢               | Stable              |
| GET /categories                     | 🟢               | Stable              |
| POST /chat                          | 🟡               | New                 |
| POST /token/introspect              | 🟡               | New                 |
| App Bots                            | 🟡               | New                 |
| App Access Token                    | 🔴               | Not yet implemented |
| Webhook Event-Signature             | 🟢               | Stable              |
| Webhook Event Structure             | 🟢               | Stable              |
| Optional Scopes                     | 🟡               | New                 |
| Chat bot badge                      | 🟡               | New                 |
| Granular scope OAuth consent screen | 🟡               | New                 |
| GET /public-key                     | 🟡               | New                 |

## Changelog

| Date       | Description                                         |
| ---------- | --------------------------------------------------- |
| 24/02/2025 | Kick-Event-Subscription-Id Webhook header           |
| 20/02/2025 | Community Contributors page                         |
| 19/02/2025 | Kick Dev API released                               |
