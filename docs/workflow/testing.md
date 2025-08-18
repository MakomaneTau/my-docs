# Testing & CI

- **Jest** for unit and integration tests  
    Jest is a fast and reliable JavaScript testing framework. We use it because it provides a simple API, excellent performance, and built-in support for mocking and coverage analysis. It helps ensure our code works as expected and catches regressions early.

- **Testing Library** for React component tests  
    Testing Library encourages testing components from the user's perspective, focusing on accessibility and real-world usage. It helps us write maintainable tests that verify UI behavior without relying on implementation details.

- **GitHub Actions** for CI/CD  
    GitHub Actions automates our build, test, and deployment workflows directly in our repository. It provides seamless integration with GitHub, enabling us to run tests and deploy code on every push or pull request, ensuring code quality and reducing manual effort.

- **Codecov** for code coverage reporting  
    Codecov integrates with our CI pipeline to track code coverage metrics. It gives us insights into which parts of our codebase are tested, helping us identify gaps and maintain high test coverage over time.

---