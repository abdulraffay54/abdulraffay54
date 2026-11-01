
# Git Commit Guidelines & Rules

These rules define how you must inspect, organize, stage, and commit changes in this repository.

Your goal is to maintain a clean, meaningful, atomic, and easily understandable Git history.

## 1. Commit Message Convention

Always follow the Conventional Commits format:

`<type>(<scope>): <description>`

General format:

- `type`: Category of change.
- `scope`: Optional area, component, module, or feature affected.
- `description`: Short explanation of what changed.

Examples:

- `feat(auth): add Google OAuth authentication`
- `fix(dashboard): resolve incorrect revenue calculation`
- `refactor(api): simplify user validation logic`
- `style(header): improve responsive navigation`
- `docs(readme): update installation instructions`
- `test(auth): add login validation tests`
- `perf(images): optimize image loading`
- `chore(deps): update React dependencies`

Use lowercase for types, scopes, and descriptions unless proper nouns require capitalization.

Use imperative mood in descriptions.

Good: `fix(auth): prevent expired sessions from being reused`

Bad: `fixed auth session issue`

Do not end commit descriptions with a period.

## 2. Allowed Commit Types

Use only the following commit types:

- `feat`: Introduces a new feature or functionality.
- `fix`: Fixes a bug or incorrect behavior.
- `refactor`: Changes internal code structure without changing external behavior.
- `style`: Formatting, whitespace, CSS styling, or visual adjustments without functional changes.
- `perf`: Improves performance or resource efficiency.
- `test`: Adds, updates, or fixes tests.
- `docs`: Documentation-only changes.
- `chore`: Maintenance tasks, configuration changes, tooling, and dependency updates.
- `build`: Changes to build systems, bundlers, or compilation configuration.
- `ci`: Changes to CI/CD pipelines and workflows.
- `revert`: Reverts a previous commit.

Choose the most specific and accurate type.

Never use `feat` for bug fixes or `refactor` for changes that introduce new functionality.

## 3. Atomic Commit Principle

Every commit must represent ONE logical, self-contained change.

A commit should:

- Have one clear purpose.
- Be understandable without inspecting unrelated changes.
- Be independently reviewable.
- Avoid mixing unrelated features, fixes, or maintenance work.
- Leave the repository in a reasonably stable state.

Examples:

GOOD:
- Add login form validation.
- Fix mobile navigation overflow.
- Update dashboard loading skeleton.
- Refactor reusable button component.

BAD:
- Update login, dashboard, footer, dependencies, and README.
- Fix several unrelated bugs in one commit.
- Mix a new feature with unrelated formatting changes.

A commit may modify multiple files if those files are necessary to implement the same logical change.

Do not create one commit per file. Organize commits by logical functionality, not file count.

## 4. How Much to Commit

Use the following rules to determine commit boundaries:

### Small changes
Commit together when changes:
- Belong to the same functionality.
- Are closely related.
- Depend on one another.
- Form one logical improvement.

Example:
A login form implementation involving:
- LoginForm.tsx
- login-validation.ts
- auth-service.ts
- login-form.css

These can belong in one commit if they collectively implement the same login feature.

### Medium changes
Split into separate commits when there are distinct logical tasks.

Example:
1. `feat(auth): add login functionality`
2. `feat(auth): add password reset flow`
3. `test(auth): add authentication tests`

### Large changes
Break large implementations into smaller, meaningful commits.

Example:
1. `feat(profile): add profile data model`
2. `feat(profile): implement profile editing`
3. `feat(profile): add profile image upload`
4. `test(profile): add profile update tests`

Do not create artificial commits just to increase the commit count.

The objective is a clean history, not a high number of commits.

## 5. Inspect Changes Before Committing

Before creating any commit, inspect the repository.

Always execute and review:

1. `git status`
2. `git diff`
3. `git diff --stat`
4. `git diff --cached` (if changes are already staged)

Understand:
- What files changed.
- What functionality changed.
- Whether changes are related.
- Whether unrelated modifications exist.
- Whether sensitive information is present.
- Whether generated or temporary files were introduced.

Never commit changes you do not understand.

Do not blindly commit everything.

## 6. Staging Rules

Never use `git add .` or `git add -A` by default.

Instead:

- Stage files explicitly.
- Group files according to their logical purpose.
- Inspect staged changes before committing.
- Avoid staging unrelated user modifications.
- Do not stage files merely because they are modified.

If a file contains both related and unrelated changes, use interactive staging or another safe method to stage only the relevant hunks.

Never overwrite, discard, reset, or modify unrelated user changes.

## 7. Files That Must Never Be Committed

Never commit sensitive or machine-specific files, including:

- `.env`
- `.env.local`
- `.env.production`
- Private API keys.
- Access tokens.
- Passwords.
- SSH private keys.
- Credentials.
- Database dumps containing sensitive information.
- Personal configuration files.
- IDE-specific temporary files.
- Operating-system temporary files.
- Build artifacts unless explicitly required by the project.

Respect the existing `.gitignore`.

If sensitive information is detected in staged changes:
- Stop the commit.
- Do not expose the secret in commit messages or logs.
- Notify the user.
- Never assume that deleting a secret from the latest change removes it from Git history.

Do not modify `.gitignore` just to make a commit succeed without understanding why a file is ignored.

## 8. Commit Message Quality

Commit messages must explain WHAT changed and, when useful, WHY it changed.

Keep the subject line:
- Concise.
- Specific.
- Ideally between 50 and 72 characters.
- Written in imperative mood.
- Free of unnecessary words.

GOOD:
`fix(auth): prevent duplicate login requests`

`feat(search): add debounced search functionality`

`refactor(ui): extract reusable modal component`

BAD:
`update code`

`changes`

`final fixes`

`minor updates`

`work done`

`bug fixed`

Avoid vague messages at all costs.

## 9. Commit Body

Use a commit body when the change requires additional context.

A body is useful when:
- The implementation is complex.
- An important technical decision was made.
- The reason for a change is not obvious.
- There are breaking changes.
- There are important limitations or migration instructions.

Example:

feat(auth): implement refresh token rotation

- Add refresh token rotation.
- Invalidate previously used refresh tokens.
- Handle expired refresh token responses.

Do not add a commit body for trivial changes.

## 10. Breaking Changes

If a change introduces backward-incompatible behavior, explicitly identify it.

Use:

`feat(api)!: replace legacy authentication endpoints`

For additional details, include:

`BREAKING CHANGE: The legacy /auth/login endpoint has been removed.`

Do not label ordinary internal refactoring as a breaking change.

## 11. Dependencies and Lockfiles

When updating dependencies:

- Keep dependency changes separate from unrelated feature changes.
- Commit the relevant lockfile alongside its dependency manifest.
- Never manually modify lockfiles unless necessary.
- Do not update unrelated dependencies.
- Explain significant dependency upgrades in the commit body when appropriate.

Example:

`chore(deps): upgrade Next.js to latest compatible version`

## 12. Formatting and Refactoring

Do not mix large formatting-only changes with functional changes.

If formatting is necessary for a feature, keep it limited to the files and code directly involved.

If an entire codebase needs formatting, create a dedicated commit:

`style: format project using Prettier`

Avoid unnecessary formatting changes that make code reviews difficult.

## 13. Testing Before Committing

Before committing functional changes:

- Run relevant tests when available.
- Run linting when available.
- Run type checking when available.
- Run the build when appropriate.

Do not claim tests passed unless you actually executed them.

If tests fail:
- Determine whether failures are related to your changes.
- Fix related failures when within scope.
- Report unrelated failures.
- Do not silently ignore failing checks.

Do not automatically introduce new testing dependencies.

## 14. User Modifications and Existing Git History

Treat existing repository changes as user-owned unless explicitly instructed otherwise.

Never:
- Discard uncommitted user changes.
- Amend an existing commit without permission.
- Rewrite Git history without permission.
- Force-push without explicit permission.
- Delete branches without permission.
- Commit directly to protected branches against repository policy.

If the working tree contains changes from previous work, inspect them before proceeding.

Do not assume every modified file belongs to the current task.

## 15. When to Create Multiple Commits

Before committing, mentally categorize all changes.

For example, if the working tree contains:

- New authentication feature.
- Dashboard styling fix.
- README updates.
- Dependency upgrades.

Create separate commits:

1. `feat(auth): implement user authentication`
2. `fix(dashboard): correct mobile layout spacing`
3. `docs(readme): update project setup instructions`
4. `chore(deps): update project dependencies`

Only create commits for changes that are ready and logically complete.

Do not include unfinished or experimental work unless explicitly requested.

## 16. When NOT to Commit

Do not commit when:

- The changes are incomplete.
- The implementation is broken.
- The changes contain secrets.
- The changes cannot be understood.
- Unrelated user changes cannot be safely separated.
- Tests reveal unresolved failures related to the implementation.
- The user has not authorized committing when approval is required.

In these situations, explain the problem and wait for instructions.

## 17. Commit Execution Workflow

Follow this workflow every time you are asked to commit changes:

STEP 1: Inspect repository status.

`git status --short`

STEP 2: Understand all changes.

`git diff`

`git diff --stat`

STEP 3: Identify logical groups.

Categorize changes into independent features, fixes, refactors, documentation, and maintenance tasks.

STEP 4: Identify unrelated changes.

Separate user-owned changes and unrelated modifications.

STEP 5: Check for sensitive files and secrets.

Inspect all files that will be staged.

STEP 6: Stage only relevant files.

Use explicit file paths or carefully selected hunks.

STEP 7: Inspect staged changes.

`git diff --cached`

STEP 8: Run appropriate checks.

Execute relevant tests, linting, type checking, or builds.

STEP 9: Determine commit boundaries.

Split unrelated logical changes into separate commits.

STEP 10: Write meaningful commit messages.

Follow Conventional Commits strictly.

STEP 11: Create commits.

Create commits only for authorized, complete, and verified changes.

STEP 12: Verify the result.

`git status`

`git log -n 5 --oneline`

Report:
- Number of commits created.
- Commit hashes.
- Commit messages.
- Files or functionality included.
- Tests/checks executed.
- Any remaining uncommitted changes.

## 18. Final Agent Behavior

Your primary responsibility is to maintain a clean, professional Git history.

Always prioritize:

1. Logical grouping over file-based grouping.
2. Atomic commits over oversized commits.
3. Meaningful messages over generic descriptions.
4. Explicit staging over blindly staging everything.
5. Preserving user changes over convenience.
6. Code quality over commit frequency.
7. Transparency over assumptions.

Never commit blindly.

Never create meaningless commits.

Never sacrifice repository safety to save time.

When uncertain whether two changes belong together, separate them if they can reasonably stand independently.

When uncertain whether a change belongs to the current task, do not include it.
