## Tech Stack & Ralational Database

**Frontend**

  - **Next.js:** Modern UI Library with hooks and context
    Youtube reference:
    - Why next.js over react - https://www.youtube.com/watch?v=msJicleNHkA
      - **Routing:** Next.js provides a built-in file-based routing system that automatically maps files in the pages directory to URLs, making navigation intuitive without extra configuration.
      - **Code-Splitting:** It automatically splits JavaScript by page, so users only download the code needed for the page they’re viewing, improving load times.
      - **Pre-Rendering:** Next.js can generate HTML for each page at build time (SSG) or on request (SSR), boosting SEO and performance compared to client-side rendering
      - **API Support:** It allows you to create serverless API routes directly in the same project, removing the need for a separate backend for simple server-side logic

- **Tailwind CSS:** Utility-first CSS framework
    Youtube reference:
    - Why tailwind css - https://www.youtube.com/watch?v=pKrPeUQiDu4
    - **Utility-First Styling:** Tailwind offers a wide range of low-level utility classes that let you style elements directly in your markup without writing separate CSS files.
    - **Customization:** It’s highly configurable via a single config file, allowing you to define colors, spacing, typography, and breakpoints to match your design system.
    - **Responsive Design:** Built-in responsive variants make it easy to create designs that adapt seamlessly across different screen sizes.
    - **Performance:** Tailwind automatically purges unused CSS in production, keeping file sizes small and load times fast.
- React Query
- React Context API

**Backend**

- Next.js API routes  
- **Firebase**
  - Backend-as-a-Service Platform
    - **Firebase Auth**: Firebase Authentication provides ready-to-use sign-in methods (email, password, social logins) with secure session management, reducing the need to build auth from scratch.
    - **Firestore**: A scalable NoSQL database that syncs data in real-time across clients, making it ideal for dynamic and collaborative apps.  
- **Express.js**
  - **Minimal and Flexible:** Express provides a lightweight core with the flexibility to add only the middleware and features you need.
  - **Routing:** Offers a simple yet powerful routing system to handle different HTTP methods and URL patterns.
  - **Middleware Support:** Easily integrates third-party or custom middleware to handle requests, responses, authentication, and more.
  - **REST API Development:** Well-suited for building robust and scalable RESTful APIs quickly with minimal boilerplate..

**Deployment**

- **Netlify** 
    - **Continuous Deployment:** Automatically builds and deploys your site whenever you push changes to your Git repository.
    - **Global CDN:** Delivers your site through a fast, globally distributed content delivery network for low-latency access worldwide
    - **Serverless Functions:** Allows you to run backend logic without maintaining a server, ideal for lightweight APIs and dynamic features.
    - **Instant Rollbacks:** Lets you revert to any previous deploy instantly, ensuring quick recovery from issues.

**Development Infrastructure**

- GitHub for version control  
- GitHub Actions for CI (test.yml)
    - Jest for unit testing
    - Codecov for Code Coverage
- Hosting: Netlify (One-click deployment)
- Secrets & Environment management: Github Secrets & Netlify Environment Variables
- Docs site: GitHub Pages (MkDocs)
