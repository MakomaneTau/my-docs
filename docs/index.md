# GlobeTalk — Virtual Pen Pals 🌍✉️

**GlobeTalk** is a privacy-first, anonymous pen-pal platform that connects people around the world for friendly, cultural, asynchronous “letter” exchanges. It recreates the charm of postal pen pals using modern web tech: random matchmaking, delayed message delivery, short cultural profiles, and moderation — text-only and anonymous by design.

---

[![codecov](https://codecov.io/gh/MakomaneTau/GlobeTalk/branch/main/graph/badge.svg)](https://codecov.io/gh/MakomaneTau/GlobeTalk)

![License](https://img.shields.io/badge/license-MIT-blue)

## Table of contents

1. Quick summary
2. Team member roles
3. Project Management Methodology
4. Features
5. Tech stack
6. Git Methodology
7. Architecture & data model
8. API endpoints
9. Local setup & development
10. Development Guide 
11. Testing & CI
12. Sprint 1 deliverables
13. Privacy, safety & moderation
14. Contributing
15. Contact & support
16. License
---

## Quick summary
- **Purpose:** Help users make anonymous, cross-cultural connections via delayed text letters.  
- **Key constraints:** Text-only (no file/media), anonymous (no names/emails published), moderation/reporting, OAuth-based sign-in for account protection.  
- **Target users:** Curious learners,language learners, students, and anyone seeking low-pressure cultural exchange.

## Team member roles
- **Product Owner & Client:**Nathan (Responsible for defining the product vision and prioritizing features.)
- **Scrum Master:**Diana (Facilitates the Scrum process, leads meetings, and ensures the team stays on track.)
- **Team:**The group of individuals who develop, test, and support the product, include:
    - Keevon Jacobs
    - Makomane Tau
    - Ponani Ngobeni
    - Khethani Vhuthuhawe
    - Smiso Ndlovu
    - Diana Bingani

## Project Management Methodology
  Youtube reference:
  Introduction to scrum - https://www.youtube.com/watch?v=9TycLR0TqFA&t=10s
  
  Online Book Source
  The 2020 Scrum Guide by Schwaber & Sutherland - https://scrumguides.org/scrum-guide.html

- We have chosen **Agile Scrum** as our project management methodology. Scrum is an iterative and collaborative framework that divides the project into short, manageable cycles called sprints. Each sprint produces an incremental release, allowing us to continuously improve the product, respond to feedback, and adapt to changing requirements throughout the development process.

- **Three Key Artifacts in Scrum**
    - Product Backlog: A comprehensive list of all desired features and requirements for the product, including items planned for future sprints.
    - Sprint Backlog: A prioritized list of features and tasks selected from the product backlog for completion during the current sprint.
    - Burn Down Chart: A visual representation of progress, showing how much work remains in the sprint backlog over time.

- **Three Main Ceremonies**
    - Sprint Planning: All team members meet to discuss user stories, define sprint goals, and estimate the effort required for each task.
    - Weekly Scrum (Daily Stand-up): Team members briefly share what they have completed, what they are currently working on, and any obstacles they are facing
    - Sprint Review / Retrospective: Held at the end of each sprint. The team demonstrates progress to the client and reflects on what went well and what can be improved in future sprints.
                    
- **Sequence of our project management methodology**
    1. Product Backlog
    2. Sprint Planning
    3. Sprint Backlog
    4. Sprint 
    5. Sprint Review 
    6. Sprint Retrospective

## Features
- **Random Matchmaking** — pair users globally with optional filters (language, region/time-zone).  
- **Asynchronous Messaging** — write a “letter”, schedule a delivery delay (e.g., 12 hours).  
- **Cultural Profiles** — short, anonymous fields (age range, hobbies, region, languages).  
- **Inbox / Compose** — thread-based UI for reading and writing letters.  
- **Moderation** — reporting, moderation logs, blocking.  
- **Settings & Safety** — block/report, toggle match preferences, delete account.

## Tech Stack

See [getting-started/tech-stack.md](getting-started/tech-stack.md) for full details on our frontend, backend, deployment, and development infrastructure choices.

## Git Methodology

See [workflow/git-methodology.md](workflow/git-methodology.md) for our full branching strategy, workflow, code quality checks, and PR rules.

## Architecture & Data Model

See [documentation/architecture.md](documentation/architecture.md) for full details.

## Initial Designs

See the link below for our design prototypes for the core features of the system.
https://www.figma.com/proto/9nLRwWxWq9rGt9MRAzd8gs/Virtual-pen-pals?node-id=29-6&t=iS525tzkq7e2lfdT-1&scaling=min-zoom&content-scaling=fixed&page-id=0%3A1&starting-point-node-id=29%3A6

## GitHub repository link

Access our GitHub repository.
https://github.com/usmiso/GlobeTalk.git

**Summary:**  
GlobeTalk uses a modular architecture with a Next.js frontend, a backend API for matchmaking and messaging, a NoSQL database for storing users, profiles, matches, and messages, and a worker/scheduler for delayed message delivery. The data model is privacy-focused, with anonymous IDs and moderation logs to ensure safety.


# Development Guide

## 1. Introduction
This guide explains how to set up, develop, and contribute to the GlobeTalk web application. It is intended for developers working on the project, both current team members and future contributors.

---

## 2. Prerequisites
Ensure the following tools are installed:

- Node.js (v18+)
- npm (comes with Node.js) or Yarn
- Git
- Code editor (VS Code recommended)
- Firebase CLI (if working with Firestore/Storage)

---

## 3. Installation & Setup

1. **Clone the repository:**
```bash
git clone https://github.com/MakomaneTau/GlobeTalk.git
cd GlobeTalk

2. **Install dependencies:**
```bash
npm install

3. **Set up envirinment variables**
Set up environment variables:

Copy .env.example → .env.local

Add Firebase config, API keys, or other credentials

Project Structure

4. **Project Structure**
/pages → Next.js page routes
/components → Reusable UI components
/styles → Tailwind or global styles
/lib → Helper functions and utilities
/public → Static assets (images, icons)
/tests → Unit and integration tests


5. **Development Workflow**
- **Branching strategy:**
  - `main` → production
  - `develop` → staging/dev
  - `feature/*` → feature branches
- **Commit conventions:**  
  Use clear commit messages, e.g., `feat: add login form`
- **Linting & formatting:**
```bash
npm run lint

6. **Running & Testing**
```bash
# Run development server
npm run dev

# Build for production
npm run build
npm start

# Run tests
npm run test

7. **Deployment**
```bash
# Hosted on Vercel (optimized for Next.js)

# Production deployment
# Push changes to main branch to trigger deployment

# Staging deployment
# Push changes to develop branch to trigger staging

# Note: Make sure all required environment variables are set in the hosting platform

8. **Troubleshooting**

- **Port 3000 already in use:**  
  Run `npm run dev -- -p 4000` to use a different port.

- **Missing environment variables:**  
  Check your `.env.local` file and make sure all required variables are present.

- **Build errors:**  
  Run `npm run lint` and fix any issues reported.

- **Firebase connection issues:**  
  Ensure credentials in `.env.local` match your Firebase project.

---

9. **Codebase Overview**

- **Frontend:** Next.js pages and components (`/pages`, `/components`)  
- **Backend/API:** API routes within `/pages/api`  
- **Styles:** Tailwind CSS or global styles in `/styles`  
- **Utilities:** Helper functions in `/lib`  
- **Static assets:** Stored in `/public`  
- **Tests:** Unit and integration tests in `/tests`  
- **Configuration:** `package.json`, `.eslintrc`, `next.config.js`  





## Testing & CI

See [workflow/testing.md](workflow/testing.md) for full details on our testing strategy, tools, and CI/CD setup.

- **Jest** for unit and integration tests  
- **Testing Library** for React component tests  
- **GitHub Actions** for CI/CD  
- **Codecov** for code coverage reporting  

---

## Sprint 1 Deliverables
- [x] User authentication (email, Google OAuth)
- [x] Responsive UI (Next.js + Tailwind CSS)
- [x] Netlify deployment

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
- Email: [pontshotau097@gmail.com](mailto:pontshotau097@gmail.com)

---

### License

This project is licensed under the MIT License. See [`LICENSE`](LICENSE) for details.
