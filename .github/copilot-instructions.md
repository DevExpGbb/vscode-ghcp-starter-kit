# Tech Stack and Style Guide for TypeScript/JavaScript Projects

## Tech Stack
- **Language:** TypeScript (preferred), JavaScript (ES2020+)
- **Package Manager:** npm or yarn (choose one and use consistently)
- **Build Tool:** tsc (TypeScript Compiler)
- **Linting:** ESLint with Airbnb or Google style guide
- **Formatting:** Prettier
- **Testing:** Jest (unit/integration), with ts-jest for TypeScript
- **Type Checking:** Enabled strict mode in tsconfig.json
- **Version Control:** Git (main branch protection enabled)
- **CI/CD:** GitHub Actions

## Style Guide
- Use 2 spaces for indentation.
- Prefer `const` and `let` over `var`.
- Use arrow functions for anonymous functions.
- Always use semicolons.
- Use single quotes for strings.
- Enforce explicit return types for functions.
- Organize imports: external, internal, then relative.
- Use PascalCase for types and interfaces, camelCase for variables and functions.
- Document public functions and exported types with JSDoc.
- Avoid using `any`; prefer explicit types.
- No unused variables or imports.
- All code must pass linting and formatting checks before merging.

## General Practices
- Write unit tests for all business logic.
- Use feature branches and submit pull requests for review.
- Keep dependencies up to date and avoid deprecated packages.
- Review and follow security best practices for npm packages.
