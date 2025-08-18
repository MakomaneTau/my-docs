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


















