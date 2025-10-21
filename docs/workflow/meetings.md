# Meetings

## Sprint 1 Meeting Evidence

- **Meeting 1: Technology Stack & Team Agreements**
  - **Date:** 05 August 2025  
  - **Venue:** In-person
  - **Agenda & Discussions:**
    - Selected technology stack: Next.js, Tailwind CSS (frontend); Firebase, Express.js (backend); Vercel/Netlify (deployment)
    - Tools: GitHub, Trello, WhatsApp, Discord, Figma
    - Team agreement: each member tests their own code
  - **Decisions Made:**
    - GitHub repo under Toure
    - Explore GitHub Pages (Smiso & Diana), test automation (all)
    - Future: folder structure, automation, code coverage

- **Meeting 2: Task Allocation & Progress Review**
  - **Date:** 6 August 2025  
  - **Venue:** Online
  - **Agenda & Discussions:**
    - Assigned roles:
      - Ponani & Vuthu: Sign Up UI & Login UI
      - Keevon & Smiso: Login, Signup backend
      - Smiso & Toure: Forgot Password backend
      - Ponani & Diana: Homepage UI & responsiveness
    - Set internal deadlines; confirmed all features for Sprint 1
  - **Decisions Made:**
    - Clear task ownership
    - Test features before merging
    - Next sprint: refine features
  - ![Microsoft Teams Meeting Screenshot](../images/online-meeting2.png)

- **Meeting 3: UI Design & Initial Development**
  - **Date:** 11 August 2025  
  - **Venue:** In-person
  - **Agenda & Discussions:**
    - Reviewed Figma designs (Login, Sign Up, Forgot Password, Homepage)
    - Responsiveness requirements
    - Task breakdown: UI development, functionality implementation
  - **Decisions Made:**
    - Finalized UI designs for Sprint 1
    - Assigned UI vs functionality responsibilities

- **Meeting 4: Repository & Collaboration Setup**
  - **Date:** 15 August 2025  
  - **Venue:** Online
  - **Agenda & Discussions:**
    - Addressed repo cloning/pulling issues
    - Defined branching strategy (feature branches, naming scheme)
    - Created Sprint1-Combination branch for integration
    - Established PR/peer review workflow
  - **Decisions Made:**
    - Finalized branch naming
    - Always merge to Sprint1-Combination first
  - ![Microsoft Teams Meeting Screenshot](../images/online-meeting4.png)

## Sprint 2 Meeting Evidence

- **Meeting 1: Sprint Planning**
  - **Date:** 20 August 2025  
  - **Venue:** Online
  - **Agenda & Discussions:**
    - Features for Sprint 2: Profile, Random Matchmaking
    - Profile page: select page range, region (pending client), intro, avatar/username generator
    - Random Matchmaking: button to find pen pal, send/receive letters, inbox, one-time vs long-term (pending client)
    - Early testing
    - Assigned frontend/backend split
  - **Decisions Made:**
    - Focus on Profile & Random Matchmaking for demo
    - Integrate avatar/username APIs
    - Await client input on region & pen pal messaging
    - Initial frontend/backend split
  - ![Sprint Planning Teams Meeting](../images/online-meeting2.png)

- **Meeting 2: Design Implementation & Estimates**
  - **Date:** 25 August 2025  
  - **Venue:** In-person
  - **Agenda & Discussions:**
    - Assigned user story estimates
    - Finalized/began implementing designs (Homepage, Profile, Edit Profile, Avatar & Username, Dashboard)
    - Implemented Profile page functionality
    - Reviewed design decisions
  - **Decisions Made:**
    - Finalized designs, began implementation
    - User story estimates completed
    - Prepared for avatar/username API integration

- **Meeting 3: Random Matchmaking Development & GitHub Merge**
  - **Date:** 27 August 2025  
  - **Venue:** Online
  - **Agenda & Discussions:**
    - Began matchmaking algorithm
    - Merge conflicts from local versions
    - Team-wide merging session: consolidate, resolve conflicts, sync environments
  - **Decisions Made:**
    - Merged branches, consistent codebase
    - Continued matchmaking development
  - ![Teams Merge Session](../images/online-meeting4.png)

- **Meeting 4: Testing Strategy & User Feedback**
  - **Date:** 1 September 2025  
  - **Venue:** Online
  - **Agenda & Discussions:**
    - Distributed automation testing tasks
    - User feedback: formal questionnaires, printed forms, collection process
  - **Decisions Made:**
    - Assigned automation testing
    - Adopted questionnaire feedback system
    - Distributed/collected forms

## Sprint 3 Meeting Evidence

- **Meeting 1: Sprint Planning**
  - **Date:** 4 September 2025  
  - **Venue:** Online
  - **Agenda & Discussions:**
    - Features: Improvements to Profile, Random Matchmaking, Chatting System, Cultural Explorer
    - Chatting System: data model, Firestore collections, REST endpoints, moderation, dashboard, real-time updates, security, extensibility
    - Cultural Explorer: country profiles (REST API), country facts (manual dataset)
  - **Decisions Made:**
    - Focus on Chatting System & Cultural Explorer for demo
    - Explorer: country profiles (API), facts (dataset)
    - Chat system: Firestore collections

- **Meeting 2: Designs for Implementation & Estimates**
  - **Date:** 10 September 2025  
  - **Venue:** In-person
  - **Agenda & Discussions:**
    - Assigned user story estimates
    - New UI designs for Cultural Explorer, Profile, Edit Profile, Chat System, Dashboard
  - **Decisions Made:**
    - Finalized designs, began implementation
    - User story estimates completed
    - Updated database schema

- **Meeting 3: In-person Team Coding Session**
  - **Date:** 19 September 2025  
  - **Venue:** In-person
  - **Agenda & Discussions:**
    - Checked progress on frontend/backend tasks
    - Chatting System: Firestore setup, REST endpoints, frontend integration, moderation
    - Cultural Explorer: API integration, dataset creation, mapping logic
  - **Decisions Made:**
    - Merge completed chat/explorer components
    - Assign debugging tasks
    - Set deadline for unfinished features

- **Stakeholder Interaction Meeting**
  - **Date:** 23 September 2025  
  - **Venue:** Online
  - **Agenda & Discussions:**
    - Presented new design, deliverables
    - Clarified API documentation, database, testing, public API endpoint
  - **Decisions Made:**
    - API docs: clear/structured
    - Add changes to schema
    - Document all tests
    - Prove at least 1 public API endpoint

- **Meeting 4: Testing Strategy & User Feedback**
  - **Date:** 25 September 2025  
  - **Venue:** Online
  - **Agenda & Discussions:**
    - Distributed automation testing tasks
    - Continued formal feedback approach
    - Printed forms, collection process
  - **Decisions Made:**
    - Assigned automation testing
    - Continued questionnaire feedback system
    - Distributed/collected forms

## Sprint 4 Meeting Evidence

- **Meeting 1: Sprint Planning (Admin & Moderation Scope)**
  - **Date:** 29 September 2025  
  - **Venue:** Online (Google Meet)
  - **Agenda & Discussions:**
    - Defined the scope for Sprint 4: Admin Moderation, Reports Dashboard, and Core Safety Features.
    - Outlined user-facing moderation tools: Report (with reasons like "Spam", "Harassment"), Block, and Unblock.
    - Discussed user data deletion upon account removal.
    - Planned the "Reports Page" as the central admin dashboard, accessible only to authorized admin emails.
    - Initial discussion on backend persistence: all reports, blocks, and admin actions must be logged in Firestore.
  - **Decisions Made:**
    - Prioritize the "Reports Page" as the primary deliverable.
    - Task allocation:
      - Backend: Create admin-only access middleware, design Firestore schema for reports and the blocked_users collection, build initial endpoints for "Validate" and "Invalidate".
      - Frontend: Build the Reports Page UI, including the main table structure and admin-only page guard.

- **Meeting 2: Backend Architecture & Security**
  - **Date:** 02 October 2025  
  - **Venue:** Online (WhatsApp Group Call)
  - **Agenda & Discussions:**
    - Reviewed security and supply chain requirements.
    - Discussed implementation of automated scripts (scan-compromised.js/py) for CI.
    - Emphasized best practices: pinning versions, running audits, and secret scanning.
    - Defined the API for admin actions: "Validate" and "Invalidate" must update the report status in Firestore.
    - Planned the audit trail for blocking: must store admin email, time, and source (e.g., "reports_page").
    - Confirmed health checks and Open API (Swagger) docs are needed for all new admin endpoints.
  - **Decisions Made:**
    - Backend team to implement security scripts and CI guardrails.
    - Finalized the Firestore schema for the blocked_users collection to include audit info.
    - All admin moderation endpoints (block, validate, invalidate) will be developed.

- **Meeting 3: Reports Page UI & Data Flow**
  - **Date:** 06 October 2025  
  - **Venue:** In-person
  - **Agenda & Discussions:**
    - Reviewed UI mockups for the Reports Page table.
    - Finalized table columns: Report ID, Offense, Reporter, Reported User, Message, Date, Status, Severity, Actions.
    - Discussed "Severity" logic: how to automatically tag reports (e.g., "harassment" = High, "spam" = Low).
    - Planned the data flow for the frontend: fetching the report list from the backend.
    - Discussed empty/error state handling for the reports table.
  - **Decisions Made:**
    - Frontend will implement the table layout and static action buttons (Validate/Invalidate).
    - Backend will create the endpoint to fetch all reports and include the calculated severity level in the response.
    - The "Message" content will be displayed for context.

- **Meeting 4: Polling and Real-time Updates (Sprint Fine Touches)**
  - **Date:** 10 October 2025  
  - **Venue:** Online (Google Meet)
  - **Agenda & Discussions:**
    - Addressed the "Fine Touch" requirement for real-time updates.
    - Evaluated WebSockets vs. polling; decided on polling for simplicity and robustness.
    - Discussed the polling mechanism: auto-refresh the report list every 5 seconds.
    - Planned for failure: polling should pause or back off if there are repeated API failures.
    - Reviewed frontend implementation of "Validate" and "Invalidate" actions and their connection to the backend API.
  - **Decisions Made:**
    - Implement a 5-second polling interval on the Reports Page.
    - The page will include an on-demand "Refresh" button as a fallback.
    - Frontend team to add feedback (e.g., "Success", "Error") for all admin actions.

- **Meeting 5: Violation Count & Block Threshold Integration**
  - **Date:** 15 October 2025  
  - **Venue:** In-person (Paired Programming Session)
  - **Agenda & Discussions:**
    - Focused on integrating violation counts (a "Fine Touch" feature).
    - Backend: Create logic to count validated violations for each user.
    - Frontend: Display the "Violation Count" for the reported user in each report row.
    - Implemented the core "Block User" threshold logic: If a user has $\geq 3$ violations and is not already blocked, the "Block User" button must appear.
    - Tested the end-to-end flow: Admin clicks "Block User" $\rightarrow$ API call $\rightarrow$ user profile updated $\rightarrow$ blocked_users collection updated $\rightarrow$ button text changes to "Blocked" or disappears.
  - **Decisions Made:**
    - The violation count is successfully pulled and displayed.
    - The conditional "Block User" button logic is implemented and tied to the backend block endpoint.
    - Confirmed that a block action prevents the user from appearing in matchmaking and sending messages.

- **Meeting 6: Final Review, Sorting, & Error Handling**
  - **Date:** 19 October 2025  
  - **Venue:** Online (Google Meet)
  - **Agenda & Discussions:**
    - Conducted a full demo of the Reports Page.
    - Implemented "Fine Touch": enhanced sorting for the reports table (by Severity, Date, Status).
    - Reviewed and tested all backend and frontend error handling (e.g., API failures, invalid permissions).
    - Confirmed admin-only access control is secure.
    - Verified all moderation actions (validate, invalidate, block) are correctly logged and persisted in Firestore with full traceability.
  - **Decisions Made:**
    - The Reports Page and all associated moderation logic are feature-complete.
    - Sorting and polishing are finalized.
    - The feature is ready for final QA and deployment.

---

### Stakeholder Meeting Decisions & Agreements
- Trial period for matched users, max two rematches.
- Region is defined as country + time zone + language.
- Users can preview cultural profiles before matching.
- Messaging types: one-time vs long-term correspondence.
- Action items:
    - Adjust matchmaking logic to support profile previews.
    - Document and finalize trial period rules in requirements.
    - Update region-based preferences in the database schema.
    - Prepare prototype screens reflecting these changes for the next review.
- Next steps: Implement discussed changes into the next sprint.

- Schedule follow-up with stakeholder to present updated prototype












