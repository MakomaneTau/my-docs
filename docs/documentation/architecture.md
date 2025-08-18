## Architecture & Data Model

### High-Level Components
- **Frontend (Next):** UI, authentication redirect, profile flow  
- **Backend API:** Matchmaking, messaging, moderation  
- **Database:** Persistent storage for users, matches, messages, logs  
- **Worker / Scheduler:** Processes delayed deliveries

### Minimal DB Schema (NoSQL)
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
    "languages": ["English", "Zulu"],
    "hobbies": ["music", "soccer"],
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

moderation_logs
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

### API Endpoints

> See [docs/api.md](docs/api.md) for full request/response examples.

#### Auth
- `GET /auth/oauth/login` — Redirect user to OAuth provider
- `POST /auth/oauth/callback` — Exchange provider code for app JWT

#### Profiles
- `POST /profiles` — Create or update a profile
- `GET /profiles/:anonId` — Retrieve a profile by public anon ID

#### Matchmaking
- `POST /match` — Request a new match (with optional filters)
- `GET /matches` — List active matches for the current user

#### Messaging
- `POST /messages` — Write a letter (delayed delivery)
- `GET /messages/:matchId` — Get delivered messages for a match

#### Moderation
- `POST /moderation/report` — Report a message
- `GET /moderation/reports` — Moderator-only list of reports
- `POST /admin/moderation/:reportId/action` — Moderator resolves report
- `DELETE /users/:uid` — Delete user account (self or admin)

---
