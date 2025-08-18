# GlobeTalk — Virtual Pen Pals 🌍✉️

**GlobeTalk** is a privacy-first, anonymous pen-pal platform that connects people around the world for friendly, cultural, asynchronous “letter” exchanges. It recreates the charm of postal pen pals using modern web tech: random matchmaking, delayed message delivery, short cultural profiles, and moderation — text-only and anonymous by design.

---

[![codecov](https://codecov.io/gh/MakomaneTau/GlobeTalk/branch/main/graph/badge.svg)](https://codecov.io/gh/MakomaneTau/GlobeTalk)
![License](https://img.shields.io/badge/license-MIT-blue)

## Table of contents
1. [Quick summary](#quick-summary)
2. [Features](#features)  
3. [Tech stack](#tech-stack)  
4. [Architecture & data model](#architecture--data-model)  
5. [API endpoints](#api-endpoints)  
6. [Local setup & development](#local-setup--development)  
7. [Testing & CI](#testing--ci)  
8. [Sprint 1 deliverables](#sprint-1-deliverables-rubric-aligned)  
9. [Privacy, safety & moderation](#privacy-safety--moderation)  
10. [Contributing](#contributing)  
11. [Contact & support](#contact--support)  
12. [License](#license)

---

## Quick summary
- **Purpose:** Help users make anonymous, cross-cultural connections via delayed text letters.  
- **Key constraints:** Text-only (no file/media), anonymous (no names/emails published), moderation/reporting, OAuth-based sign-in for account protection.  
- **Target users:** Curious learners, language learners, students, and anyone seeking low-pressure cultural exchange.

## Features
- **Random Matchmaking** — pair users globally with optional filters (language, region/time-zone).  
- **Asynchronous Messaging** — write a “letter”, schedule a delivery delay (e.g., 12 hours).  
- **Cultural Profiles** — short, anonymous fields (age range, hobbies, region, languages).  
- **Inbox / Compose** — thread-based UI for reading and writing letters.  
- **Moderation** — reporting, moderation logs, blocking.  
- **Settings & Safety** — block/report, toggle match preferences, delete account.

## Tech stack

### Frontend

#### Nextjs

Youtube reference:
Why next.js over react - https://www.youtube.com/watch?v=msJicleNHkA

* Routing - Next.js provides a built-in file-based routing system that automatically
maps files in the pages directory to URLs, making navigation intuitive without extra
configuration.
* Code-Splitting – It automatically splits JavaScript by page, so users only download
the code needed for the page they’re viewing, improving load times.
* Pre-Rendering – Next.js can generate HTML for each page at build time (SSG) or on
request (SSR), boosting SEO and performance compared to client-side rendering.
* API Support – It allows you to create serverless API routes directly in the same
project, removing the need for a separate backend for simple server-side logic

#### Tailwind CSS
Youtube reference:
Why tailwind css - https://www.youtube.com/watch?v=pKrPeUQiDu4

* Customization – It’s highly configurable via a single config file, allowing you to
define colors, spacing, typography, and breakpoints to match your design system
* Utility-First Styling – Tailwind offers a wide range of low-level utility classes that let
you style elements directly in your markup without writing separate CSS files.
* Responsive Design – Built-in responsive variants make it easy to create designs
that adapt seamlessly across different screen sizes
* Performance – Tailwind automatically purges unused CSS in production, keeping
file sizes small and load times fast.




### Backend

#### Firebase

* Authentication – Firebase Authentication provides ready-to-use sign-in methods
(email, password, social logins) with secure session management, reducing the
need to build auth from scratch.
* Cloud Firestore – A scalable NoSQL database that syncs data in real-time across
clients, making it ideal for dynamic and collaborative apps.

#### Express.js

* Minimal and Flexible – Express provides a lightweight core with the flexibility to add
only the middleware and features you need.
* Routing – Offers a simple yet powerful routing system to handle different HTTP
methods and URL patterns.
* Middleware Support – Easily integrates third-party or custom middleware to handle
requests, responses, authentication, and more.
* REST API Development – Well-suited for building robust and scalable RESTful APIs
quickly with minimal boilerplate.


### Deployment

#### Netlify
* Continuous Deployment – Automatically builds and deploys your site whenever
you push changes to your Git repository.
* Global CDN – Delivers your site through a fast, globally distributed content
delivery network for low-latency access worldwide
* Serverless Functions – Allows you to run backend logic without maintaining a
server, ideal for lightweight APIs and dynamic features.
* Instant Rollbacks – Lets you revert to any previous deploy instantly, ensuring
quick recovery from issues.



<!-- **Development Infrastructure**
- GitHub for version control  
- GitHub Actions for CI (test.yml)
    - Jest for unit testing
    - Codecov for Code Coverage
- Hosting: Netlify (One-click deployment)
- Secrets & Environment management: Github Secrets & Netlify Environment Variables
- Docs site: GitHub Pages (MkDocs)

## Architecture & data model

### High-level components
- Frontend (Next) — UI, auth redirect, profile flow  
- Backend API — matchmaking, messaging, moderation  
- Database — persistent storage for users, matches, messages, logs  
- Worker / Scheduler — processes delayed deliveries

### Minimal DB schema (NoSQL)
```NoSQL
users
{
  "uid": "uid_abc123",
  "anonId": "G-42a7",
  "createdAt": "<Firestore Timestamp>",
  "lastSeenAt": "<Firestore Timestamp>",
  "authProvider": "google",
  "settings": {
    "receiveEmail": false
  }
}

profiles
{
  "anonId": "G-42a7",
  "ownerUid": "uid_abc123",
  "region": "South Africa",
  "languages": ["English","Zulu"],
  "hobbies": ["music","soccer"],
  "bio": "22-28 • interested in culture & language exchange",
  "createdAt": "<Firestore Timestamp>"
}

matches
{
  "id": "match_ab12",
  "userA": "uid_abc123",
  "userB": "uid_def456",
  "matchedAt": "<Firestore Timestamp>",
  "longTerm": false,
  "state": "active"
}

messages
{
  "id": "msg_x001",
  "senderId": "uid_abc123",
  "body": "Hello from South Africa! What are your local holidays like?",
  "createdAt": "<Firestore Timestamp>",
  "deliveryTime": "<Firestore Timestamp>",
  "delivered": false,
  "deliveredAt": null,
  "flagged": 0
}

moderation logs
{
  "id": "report_0001",
  "reporterId": "uid_xyz789",
  "messageRef": "/matches/match_ab12/messages/msg_x001",
  "reason": "abusive language",
  "status": "pending",
  "createdAt": "<Firestore Timestamp>",
  "handledBy": null,
  "actionTaken": null
}
```
-->
### API Endpoints

> See [docs/api.md](docs/api.md) for full request/response examples.

#### Auth
- `GET /auth/oauth/login` — Redirect user to OAuth provider.
- `POST /auth/oauth/callback` — Exchange provider code for app JWT.

#### Profiles
- `POST /profiles` — Create or update a profile.
- `GET /profiles/:anonId` — Retrieve a profile by public anon ID.

#### Matchmaking
- `POST /match` — Request a new match (with optional filters).
- `GET /matches` — List active matches for the current user.

#### Messaging
- `POST /messages` — Write a letter (delayed delivery).  
- `GET /messages/:matchId` — Get delivered messages for a match.

#### Moderation
- `POST /moderation/report` — Report a message.  
- `GET /moderation/reports` — Moderator-only list of reports.  
- `POST /admin/moderation/:reportId/action` — Moderator resolves report.  
- `DELETE /users/:uid` — Delete user account (self or admin).

---


### Testing & CI

- **Jest** for unit and integration tests
- **Testing Library** for React component tests
- **GitHub Actions** for CI/CD
- **Codecov** for code coverage reporting

---

## Sprint 1 Deliverables (Rubric-aligned)
- [x] User authentication (email, Google OAuth)
- [x] Anonymous profile creation
- [x] Responsive UI (Next.js + Tailwind CSS)
- [x] Netlify deployment

---

### Privacy, Safety & Moderation

- No personal info shared between users
- All messages are text-only, no media
- Moderation tools for reporting/blocking
- Data stored securely in Firebase
- Users can delete their account at any time

---

### Contributing

1. Fork the repo and clone locally
2. Create a new branch (`git checkout -b feature/my-feature`)
3. Commit your changes (`git commit -m 'Add feature'`)
4. Push to GitHub and open a Pull Request

See CONTRIBUTING.md for more details.

---

### Contact & Support

- Issues: [GitHub Issues](https://github.com/MakomaneTau/GlobeTalk/issues)
- Email: [pontshotau09@gmail.com](mailto:pontshotau09@gmail.com)

---

### License

This project is licensed under the MIT License. See [`LICENSE`](LICENSE) for details.

---

### MkDocs Quick Reference

For full documentation visit [mkdocs.org](https://www.mkdocs.org).

### Useful Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs -h` - Print help message and exit.

### Project layout

```
mkdocs.yml    # The configuration file.
docs/
    index.md  # The documentation homepage.
    ...       # Other markdown pages, images and other