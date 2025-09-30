<!-- ## Architecture & Data Model

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

--- -->


## Database Documentation

**Choice of Database** : 
We used Firebase Firestore as our project’s database.

- Justification: Firestore was chosen because it is a flexible, cloud-based NoSQL
database that integrates seamlessly with Firebase Authentication and other
Firebase services. It provides real-time data synchronization, which is essential
for responsive user experiences. In addition, Firestore’s scalability and
serverless nature reduce the need for manual database management.




- Docs: https://firebase.google.com/docs/firestore


**Database Schema** :

Our schema is organized into collections and documents rather than relational tables.
Below is the current structure:


- Chats Collection
```NoSQL
chats collection
{
    "chatID": "string",
    "createdAt": timestamp,
    "messages": (array)[
        {
            "delaySeconds": number,
            "deliveryTime": number,
            "sender": "string",
            "sentAt": number,
            "text": "string"
        },
        {
            "delaySeconds": number,
            "deliveryTime": number,
            "sender": "string",
            "sentAt": number,
            "text": "string"
        },
        {
            "delaySeconds": number,
            "deliveryTime": number,
            "sender": "string",
            "sentAt": number,
            "text": "string"
        }
    ],
    "users": [
        "string",
        "string"
    ]
}
```

- Match Collection
```NoSQL
match collection
{
    "matchID": "string",
    "user1": "string",
    "user2": "string",
}
```


- Profiles Collection

```NoSQL
profiles collection
{
    "avatarUrl": "string-Generated via DiceBear",
    "hobbies": "array",
    "intro": "string",
    "languages": "string",
    "timezone": "string",
    "userID": "string"
}
```


- Reports Collection
```NoSQL
reports collection
{
    "chatID": "string",
    "message": {
        "delaySeconds": "number",
        "deliveryTime": "number",
        "sender": "string",
        "sentAt": "number",
        "text": "string"
    },
    "reason": "string",
    "reportedAt": "number",
    "reporter": "string",
    "status": "string",
}
```


- Users Collection

```NoSQL
users collection
{
    "userID": "string",
    "createdAt": "timestamp",

}
```





**Deployment Information**

- Frontend Deployment:

```bash
o Hosted on Netlify for fast global delivery.
o Frontend communicates with backend via API calls to Railway.
```

- Backend Deployment:
```bash
o Hosted on Railway.
o Backend (Express.js) connects to Firestore using the Firebase Admin SDK.
```

- Database Deployment:
```bash
o Firestore is fully managed in the cloud by Firebase.
o No manual server provisioning is needed.
o Authentication and security rules are managed through Firebase Console.
```












