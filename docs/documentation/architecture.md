## Database Documentation

**Choice of Database** : 
We used Firebase Firestore as our project’s database.

- **Justification**: Firestore was chosen because it is a flexible, cloud-based NoSQL
database that integrates seamlessly with Firebase Authentication and other
Firebase services. It provides real-time data synchronization, which is essential
for responsive user experiences. In addition, Firestore’s scalability and
serverless nature reduce the need for manual database management.




- **Docs:** [https://firebase.google.com/docs/firestore](https://firebase.google.com/docs/firestore)


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

### Data

**Production vs Testing Data**:
Most of the current data is for testing purposes.

Total records: [fill in number]

Production data: [fill in number or percentage]

Testing data: [fill in number or percentage]

**Notes**:
Even with a small amount of production data, Firestore’s real-time sync and validation rules ensure that data integrity is maintained.



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


### Database Structure and Best Practices

1. Structure:
The database is organized using collections and documents, following Firestore best practices:

    - Group related data logically into collections (e.g., chats, users, reports).

    - Store repeated or nested data in arrays when appropriate (e.g., messages within chats).

    - Avoid deeply nested structures to maintain performance and query simplicity.

2. Best Practices Implemented:

    - Real-time updates handled efficiently with Firestore listeners.

    - Security rules restrict read/write access based on user authentication.

    - Timestamps and unique IDs ensure data integrity and traceability.

    - References between collections (e.g., userID in profiles and chats) are used instead of duplicating data.







