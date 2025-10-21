# Meetings

## Sprint 1 meeting evidence

- **Tech stack:**
    - **Frontend:**
        - **Next.js:**
            - Youtube reference: [Why next.js over react](https://www.youtube.com/watch?v=msJicleNHkA)
            - Routing – Next.js provides a built-in file-based routing system that automatically maps files in the pages directory to URLs, making navigation intuitive without extra configuration.
            - Code-Splitting – It automatically splits JavaScript by page, so users only download the code needed for the page they’re viewing, improving load times.
            - Pre-Rendering – Next.js can generate HTML for each page at build time (SSG) or on request (SSR), boosting SEO and performance compared to client-side rendering.
            - API Support – It allows you to create serverless API routes directly in the same project, removing the need for a separate backend for simple server-side logic.
        - **Tailwind CSS:**
            - Youtube reference: [Why tailwind css](https://www.youtube.com/watch?v=pKrPeUQiDu4)
            - Utility-First Styling – Tailwind offers a wide range of low-level utility classes that let you style elements directly in your markup without writing separate CSS files.
            - Customization – It’s highly configurable via a single config file, allowing you to define colors, spacing, typography, and breakpoints to match your design system.
            - Responsive Design – Built-in responsive variants make it easy to create designs that adapt seamlessly across different screen sizes.
            - Performance – Tailwind automatically purges unused CSS in production, keeping file sizes small and load times fast.
    - **Backend and database:**
        - **Firebase:**
            - Authentication – Firebase Authentication provides ready-to-use sign-in methods (email, password, social logins) with secure session management, reducing the need to build auth from scratch.
            - Cloud Firestore – A scalable NoSQL database that syncs data in real-time across clients, making it ideal for dynamic and collaborative apps.
        - **Express.js:**
            - Minimal and Flexible – Express provides a lightweight core with the flexibility to add only the middleware and features you need.
            - Routing – Offers a simple yet powerful routing system to handle different HTTP methods and URL patterns.
            - Middleware Support – Easily integrates third-party or custom middleware to handle requests, responses, authentication, and more.
            - REST API Development – Well-suited for building robust and scalable RESTful APIs quickly with minimal boilerplate.
    - **Deployment:**
        - **Netlify:**
            - Continuous Deployment – Automatically builds and deploys your site whenever you push changes to your Git repository.
            - Global CDN – Delivers your site through a fast, globally distributed content delivery network for low-latency access worldwide.
            - Serverless Functions – Allows you to run backend logic without maintaining a server, ideal for lightweight APIs and dynamic features.
            - Instant Rollbacks – Lets you revert to any previous deploy instantly, ensuring quick recovery from issues.

- **Development Guides:**
    - **Next.js:**
        1. Install Node.js (LTS version recommended).
        2. Create the app: `npx create-next-app@latest my-app` then `cd my-app`
        3. Run the development server: `npm run dev`
        4. Open in browser → Go to http://localhost:3000.
        5. Start building → Edit files in the pages/ or app/ directory.
    - **GitHub repo:**
        1. Create a new repo on GitHub (choose name, description, public).
        2. In VSCode terminal Initialize Git in your project: `git init`
        3. Add remote origin: `git remote add origin https://github.com/USERNAME/REPO-NAME.git`
        4. Stage and commit files: `git add .` then `git commit -m "Initial commit"`
        5. Push to GitHub: `git branch -M main` then `git push -u origin main`
    - **GitHub Pages:**
        1. Have a GitHub repo with your project code.
        2. Push code to main branch (or another branch if you prefer).
        3. Enable GitHub Pages: Go to Settings → Pages in your repo. Under Source, select the branch (main) and folder (/root or /docs).
        4. Save settings → GitHub will give you a live URL.
        5. Access your site once the deployment finishes.
    - **Netlify Deployment:**
        1. Create a Netlify account (or log in).
        2. Connect your GitHub repo: Click New Site → Import from Git → Select your repo.
        3. Configure build settings: Build command: `npm run build`, Publish directory: `out` (for Next.js static export) or `build` (for React).
        4. Deploy site → Netlify will build and give you a live URL.
        5. Optional → Set up custom domain in Netlify settings.
    - **Firebase auth:**
        1. Create a Firebase project at Firebase Console.
        2. Add a web app → Get Firebase config (apiKey, authDomain, etc.).
        3. Install Firebase SDK in your project: `npm install firebase`
        4. Initialize Firebase in your project:
            ```js
            import { initializeApp } from "firebase/app";
            import { getAuth } from "firebase/auth";
            const firebaseConfig = { /* your config */ };
            const app = initializeApp(firebaseConfig);
            const auth = getAuth(app);
            ```
        5. Enable auth methods in Firebase Console → Authentication → Sign-in method (Email/Password, Google, etc.).
        6. Use Firebase Auth to register, login, and manage users in your app.
    - **Firestore:**
        1. Create a Firebase project (or use an existing one).
        2. Enable Firestore in the Firebase Console → Firestore Database → Create database.
        3. Install Firebase SDK (if not already done).
        4. Initialize Firestore in your project:
            ```js
            import { getFirestore } from "firebase/firestore";
            const db = getFirestore(app); // app is your initialized Firebase app
            ```
        5. Use Firestore to read/write data:
            - Add document: `addDoc(collection(db, "users"), { name: "John" })`
            - Get documents: `getDocs(collection(db, "users"))`
            - Update document: `updateDoc(doc(db, "users", docId), { age: 30 })`
            - Delete document: `deleteDoc(doc(db, "users", docId))`

- **Project Management:**
    - As a group, we have chosen Agile Scrum as our project management methodology. Scrum is an iterative and collaborative framework that divides the project into short, manageable cycles called sprints. Each sprint produces an incremental release, allowing us to continuously improve the product, respond to feedback, and adapt to changing requirements throughout the development process.
    - **Key Roles:**
        - Product Owner: Responsible for defining the product vision and prioritizing features. Our Product Owner is our client, Nathan.
        - Scrum Master: Facilitates the Scrum process, leads meetings, and ensures the team stays on track. Our Scrum Master is Diana.
        - Team: The group of individuals who develop, test, and support the product. Our team members include: Keevon, Toure’, Ponani, Smiso, and Vuthu.
    - **Three Key Artifacts in Scrum:**
        - Product Backlog: A comprehensive list of all desired features and requirements for the product, including items planned for future sprints.
        - Sprint Backlog: A prioritized list of features and tasks selected from the product backlog for completion during the current sprint.
        - Burn Down Chart: A visual representation of progress, showing how much work remains in the sprint backlog over time.
    - **Three Main Ceremonies:**
        - Sprint Planning: All team members meet to discuss user stories, define sprint goals, and estimate the effort required for each task.
        - Weekly Scrum (Daily Stand-up): Team members briefly share what they have completed, what they are currently working on, and any obstacles they are facing.
        - Sprint Review / Retrospective: Held at the end of each sprint. The team demonstrates progress to the client (Nathan) and reflects on what went well and what can be improved in future sprints.
    - **Sequence of our project management methodology:**
        - Product Backlog → Sprint Planning → Sprint Backlog → Sprint → Sprint Review → Sprint Retrospective

    - **Evidence of sprint methodology:**
        - Meeting notes, task boards, and progress charts are maintained in Trello and GitHub throughout the project.

## Sprint 2 meeting evidence
- **Product Backlog:** Maintained and updated in Trello for Sprint 2.
- **Sprint Planning Meeting (Meeting 1):** Discussed user stories, defined sprint goals, and estimated tasks for Sprint 2.
- **Design Implementation & Estimates (Meeting 2):** Reviewed UI/UX designs and provided time/effort estimates for new features.
- **Random Matchmaking Development & GitHub Merge (Meeting 3):** Developed and merged the random matchmaking feature, resolved merge conflicts.
- **Testing Strategy & User Feedback (Meeting 4):** Outlined testing approach and gathered user feedback for improvements.
  
  ![Microsoft Teams Meeting Screenshot](../images/online-meeting2.png)

- **Stakeholder Review:** Presented sprint outcomes to stakeholders and collected feedback for the next sprint.

## Sprint 3 meeting evidence
- **Product Backlog:** Updated with new requirements and feedback from previous sprints.
- **Sprint Planning Meeting (Meeting 1):** Prioritized tasks and set sprint goals for Sprint 3.
- **Design Implementation & Estimates (Meeting 2):** Finalized design changes and estimated development time for remaining features.
- **Random Matchmaking Development & GitHub Merge (Meeting 3):** Enhanced matchmaking logic and ensured successful integration.
- **Testing Strategy & User Feedback (Meeting 4):** Conducted comprehensive testing and reviewed user feedback for final adjustments.
  
  ![Microsoft Teams Meeting Screenshot](../images/online-meeting4.png)

- **Stakeholder Review:** Demonstrated completed features and discussed next steps with stakeholders.












