## Git Methodology
- We follow a **main / dev / feature** branching strategy:
    - main: always stable & deployed.
    - dev: integration branch where features are merged.
    - feature/name: each new feature or fix has its own branch.

- **Workflow**:
    1. Switch to latest dev branch
    2. Pull latest dev.
    3. Create a feature/* branch.
    4. Do your changes
    5. Run tests
    6. Stage & Commit(conventional commits)
    7. Pull latest dev to your feature branch
    8. Push changes.
    9. Open a Pull Request (PR) into dev.
    10. After review & testing, merge dev to main.

- **Code Quality Checks**:
    - Run ESLint (npx eslint . --fix) and Jest tests (npm test) before pushing.
    - GitHub Actions runs CI(tests & lint) checks on every PR.
    - After review, merge dev → main for releases

- **Rules**:
    - No direct commits to main.
    - All code goes through PR review.
    - Netlify auto-deploys from main.
