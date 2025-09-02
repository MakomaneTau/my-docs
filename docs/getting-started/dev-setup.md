# Development Guides

### Next.js
1. Install Node.js (LTS version recommended).
2. Create the app:

```bash
npx create-next-app@latest my-app
cd my-app
```
3. Run the development server
```bash
npm run dev
```
4. Open in browser
```bash
Go to http://localhost:3000
```
5. Start building → Edit files in the pages/ or app/ directory.






### GitHub repo
1. Create a new repo on GitHub (choose name, description, public)
2. In VScode terminal Initialize Git in your project
```bash
git init
```
3. Add remote origin
```bash
git remote add origin https://github.com/USERNAME/REPO-NAME.git
```
4. Stage and commit files
```bash
git add .
git commit -m "Initial commit"
```
5. Push to GitHub
```bash
git branch -M main
git push -u origin main
```


### GitHub pages
1. Have a GitHub repo with your project code
2. Push code to main branch (or another branch if you prefer).
3. Enable GitHub Pages
```bash
Go to Settings → Pages in your repo.
Under Source, select the branch (main) and folder (/root or /docs)
```
4. Save settings → GitHub will give you a live URL
5. Access your site once the deployment finishes


### Netlify Deployment
1. Create a Netlify account (or log in).
2. Connect your GitHub repo
```bash
Click New Site → Import from Git → Select your repo
```
3. Configure build settings
```bash
Build command: npm run build
Publish directory: out (for Next.js static export) or build (for React)
```
4. Deploy site → Netlify will build and give you a live URL.
5. Optional → Set up custom domain in Netlify settings.


### Firebase auth

1. Create a Firebase project at Firebase Console.
2. Add a web app → Get Firebase config (apiKey, authDomain, etc.).
3. Install Firebase SDK in your project:
```bash
npm install firebase
```
4. Initialize Firebase in your project:
```bash
import { initializeApp } from "firebase/app";
import { getAuth } from "firebase/auth";
const firebaseConfig = { /* your config */ };
const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
```
5. Enable auth methods in Firebase Console → Authentication → Sign-in method
(Email/Password, Google, etc.).
6. Use Firebase Auth to register, login, and manage users in your app.


### Firestore
1. Create a Firebase project (or use an existing one).
2. Enable Firestore in the Firebase Console → Firestore Database → Create database.
3. Install Firebase SDK (if not already done)
4. Initialize Firestore in your project:
```bash
import { getFirestore } from "firebase/firestore";
const db = getFirestore(app); // app is your initialized Firebase app
```
5. Use Firestore to read/write data:
```bash
Add document: addDoc(collection(db, "users"), { name: "John" })
Get documents: getDocs(collection(db, "users"))
Update document: updateDoc(doc(db, "users", docId), { age: 30 })
Delete document: deleteDoc(doc(db, "users", docId))
```

### Next.js + Express for a simple API
1. Install dependencies (if not done already):
```bash
npm install express firebase-admin
```
2. Create server.js in your project root:
```bash
import express from "express";
import { initializeApp, applicationDefault } from "firebase-admin/app";
import { getFirestore } from "firebase-admin/firestore";

const app = express();
app.use(express.json()); // for parsing JSON bodies

// Initialize Firebase Admin
initializeApp({
  credential: applicationDefault(),
});

const db = getFirestore();

// Example API route: GET all users
app.get("/api/users", async (req, res) => {
  try {
    const snapshot = await db.collection("users").get();
    const users = snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
    res.json(users);
  } catch (err) {
    res.status(500).json({ error: err.message });
  }
});

// Example API route: POST a new user
app.post("/api/users", async (req, res) => {
  try {
    const { name, age } = req.body;
    const docRef = await db.collection("users").add({ name, age });
    res.status(201).json({ id: docRef.id, name, age });
  } catch (err) {
    res.status(500).json({ error: err.message });
  }
});

// Start server
const PORT = process.env.PORT || 3001;
app.listen(PORT, () => console.log(`Server running on port ${PORT}`));

```
3. Run your server:
```bash
node server.js
```
GET users: http://localhost:3001/api/users and POST new user: Send JSON { "name": "John", "age": 30 } to the same URL.
 

## Third Party Code Documentation

Our project makes use of several third-party libraries and APIs to improve efficiency,
provide essential functionality, and ensure maintainability. Below is a list of all
important third-party code used, with documentation links and justifications.

**Frontend(Next.js+React)**

- Next.js (v14)
```bash
o Docs: https://nextjs.org/docs
o Justification: Next.js was chosen for its powerful server-side rendering
and routing features. It simplifies building scalable web applications and
provides built-in optimizations for performance.
```
- React (v18)
```bash
o Docs: https://react.dev/
o Justification: React is the core library for building reusable UI
components. It enables efficient state management and component-
driven development.
```
- Tailwind CSS (v3)
```bash
o Docs: https://tailwindcss.com/docs
o Justification: Tailwind CSS provides a utility-first approach to styling,
making it faster to build and maintain consistent user interfaces.
```
- Next.js built-in modules:
```bash
o next/link (routing between pages)
o next/navigation (client-side navigation APIs)
o next/image (optimized image rendering)
o Docs: Next.js Components
o Justification: These built-in features streamline navigation, routing, and
image optimization within the app.
```

**APIs / External Services**

- DiceBear Avatars API
```bash
o Docs: https://www.dicebear.com/styles/
o Justification: Used for generating random avatars for users, improving
personalization and user experience without needing manual uploads.
```
- RandomUser API (randomuser.me)
```bash
o Docs: https://randomuser.me/documentation
o Justification: Used to generate random user profiles during testing and
development, ensuring realistic test data
```

**Backend (Node.js + Express)**

- Express.js (v4)
```bash
o Docs: https://expressjs.com/
o Justification: Express provides a lightweight and flexible framework for
building backend REST APIs, handling routes, and connecting to the
frontend
```
- CORS
```bash
o Docs: https://www.npmjs.com/package/cors
o Justification: Ensures secure cross-origin communication between
frontend and backend, preventing browser security errors.
```
- Firebase Admin SDK
```bash
o Docs: https://firebase.google.com/docs/admin/setup
o Justification: Provides secure access to Firebase services such as authentication and Firestore database management from the backend.
```












