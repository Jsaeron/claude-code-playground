# CLAUDE.md - AI Assistant Guide

This document provides comprehensive guidance for AI assistants (particularly Claude) working in this codebase. It outlines the repository structure, development workflows, conventions, and best practices.

---

## Repository Overview

**Repository:** claude-code-playground
**Owner:** Jsaeron
**Purpose:** Playground repository for testing and experimenting with Claude Code workflows
**Current State:** Empty/Initialized repository ready for development

---

## Table of Contents

1. [Repository Structure](#repository-structure)
2. [Development Workflow](#development-workflow)
3. [Git Conventions](#git-conventions)
4. [Coding Standards](#coding-standards)
5. [AI Assistant Guidelines](#ai-assistant-guidelines)
6. [File Organization](#file-organization)
7. [Documentation Standards](#documentation-standards)
8. [Testing Guidelines](#testing-guidelines)
9. [Common Tasks](#common-tasks)

---

## Repository Structure

As this repository grows, maintain this organizational structure:

```
claude-code-playground/
├── .git/                 # Git version control
├── .github/              # GitHub-specific files (workflows, templates)
│   ├── workflows/        # CI/CD pipelines
│   └── ISSUE_TEMPLATE/   # Issue templates
├── docs/                 # Documentation files
│   ├── architecture/     # Architecture decision records
│   └── guides/           # User and developer guides
├── src/                  # Source code
│   ├── components/       # Reusable components
│   ├── utils/            # Utility functions
│   ├── services/         # Business logic and services
│   └── types/            # Type definitions
├── tests/                # Test files
│   ├── unit/             # Unit tests
│   ├── integration/      # Integration tests
│   └── e2e/              # End-to-end tests
├── scripts/              # Build and deployment scripts
├── config/               # Configuration files
├── CLAUDE.md             # This file - AI assistant guide
├── README.md             # Project overview and setup
├── LICENSE               # License information
└── .gitignore            # Git ignore patterns
```

---

## Development Workflow

### Branch Strategy

1. **Main Branch:** `main` (or `master`)
   - Protected branch
   - Always in deployable state
   - Requires pull request reviews

2. **Feature Branches:** `claude/[feature-name]-[session-id]`
   - Format: `claude/claude-md-mjs6xclz6fp7aamt-YPWST`
   - Create from main branch
   - Delete after merge

3. **Branch Naming Convention:**
   - Feature: `claude/feature-description-sessionid`
   - Bug fix: `claude/fix-description-sessionid`
   - Experiment: `claude/experiment-description-sessionid`

### Development Process

1. **Start Work:**
   ```bash
   git checkout -b claude/feature-name-sessionid
   ```

2. **Make Changes:**
   - Write code following conventions
   - Test changes thoroughly
   - Update documentation

3. **Commit:**
   ```bash
   git add .
   git commit -m "Clear, descriptive commit message"
   ```

4. **Push:**
   ```bash
   git push -u origin claude/feature-name-sessionid
   ```

5. **Create Pull Request:**
   ```bash
   gh pr create --title "Feature: Description" --body "Detailed explanation"
   ```

---

## Git Conventions

### Commit Messages

Follow the conventional commits format:

```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting, no logic change)
- `refactor`: Code refactoring
- `test`: Adding or updating tests
- `chore`: Maintenance tasks

**Examples:**
```
feat(auth): add user authentication system

Implement JWT-based authentication with refresh tokens.
Includes login, logout, and token refresh endpoints.

Closes #123
```

```
fix(api): handle null response in user service

Previously would crash when API returned null.
Now returns empty user object with proper error handling.
```

### Commit Best Practices

1. **Atomic commits:** Each commit should represent one logical change
2. **Descriptive messages:** Explain the "why" not just the "what"
3. **Test before committing:** Ensure code works and tests pass
4. **No secrets:** Never commit API keys, passwords, or sensitive data

### Push/Pull Retry Logic

Network operations should retry on failure:
- Retry up to 4 times
- Exponential backoff: 2s, 4s, 8s, 16s
- Only retry on network errors, not authentication failures

---

## Coding Standards

### General Principles

1. **Simplicity First:**
   - Write the simplest code that works
   - Avoid premature optimization
   - Don't over-engineer solutions

2. **Readability:**
   - Clear variable and function names
   - Self-documenting code preferred over comments
   - Comments only when logic isn't self-evident

3. **DRY (Don't Repeat Yourself):**
   - Extract common patterns into functions
   - But avoid premature abstraction
   - Three uses before abstracting

4. **YAGNI (You Aren't Gonna Need It):**
   - Only build what's needed now
   - Don't design for hypothetical future requirements
   - Features can be added when actually needed

### Code Organization

1. **File Length:**
   - Keep files focused and under 400 lines
   - Split large files into logical modules

2. **Function Length:**
   - Functions should do one thing well
   - Ideally under 50 lines
   - Extract complex logic into helper functions

3. **Imports:**
   - Group imports logically
   - Third-party before local imports
   - Remove unused imports

### Error Handling

1. **Validate at Boundaries:**
   - User input
   - External API responses
   - File operations

2. **Trust Internal Code:**
   - Don't add unnecessary checks for internal functions
   - Use type systems for safety

3. **Fail Fast:**
   - Validate early in the function
   - Return early for error conditions

### Security

1. **Input Validation:**
   - Sanitize user input
   - Validate data types and formats
   - Prevent SQL injection, XSS, command injection

2. **Authentication & Authorization:**
   - Never trust client-side validation alone
   - Use secure session management
   - Implement proper access controls

3. **Secrets Management:**
   - Never commit secrets to git
   - Use environment variables
   - Use secret management tools in production

---

## AI Assistant Guidelines

### Before Making Changes

1. **Read First:**
   - ALWAYS read files before modifying them
   - Use Read tool, not cat/grep
   - Understand existing patterns and conventions

2. **Plan Complex Tasks:**
   - Use TodoWrite for multi-step tasks
   - Break down large features
   - Track progress systematically

3. **Search Effectively:**
   - Use Task tool with Explore agent for codebase exploration
   - Use Grep for specific pattern searches
   - Use Glob for finding files by pattern

### When Writing Code

1. **Minimal Changes:**
   - Only change what's necessary
   - Don't refactor unrelated code
   - Don't add "improvements" not requested

2. **No Unnecessary Additions:**
   - Don't add docstrings to unchanged code
   - Don't add comments unless logic is complex
   - Don't add type annotations to existing code
   - Don't add error handling for impossible scenarios

3. **Delete Unused Code:**
   - Remove completely, don't comment out
   - No backwards-compatibility hacks for unused code
   - Clean removal is better than deprecation markers

4. **Follow Existing Patterns:**
   - Match the style of surrounding code
   - Use existing utilities and helpers
   - Maintain consistency

### Tool Usage

1. **Specialized Tools:**
   - Read: For reading files (not cat)
   - Edit: For modifying files (not sed/awk)
   - Write: For new files (not echo/cat)
   - Grep: For searching code (not grep/rg commands)
   - Glob: For finding files (not find/ls)

2. **Parallel Execution:**
   - Run independent operations in parallel
   - Single message with multiple tool calls
   - Don't use placeholders or guess parameters

3. **Task Tool:**
   - Use Explore agent for codebase understanding
   - Use specialized agents when available
   - Provide detailed prompts for agents

### Communication

1. **No Tool Abuse:**
   - Don't use echo/printf to communicate
   - Output text directly to user
   - Don't use code comments to explain actions

2. **Concise Responses:**
   - Brief and to the point
   - Technical accuracy over validation
   - Objective, professional tone

3. **No Emojis:**
   - Unless explicitly requested
   - Professional communication style

### Git Operations

1. **Safe Git Practices:**
   - Never skip hooks (--no-verify)
   - Never force push without explicit request
   - Check authorship before amending
   - Only commit when explicitly asked

2. **Commit Workflow:**
   - Check git status and diff first
   - Review recent commits for style
   - Draft clear commit messages
   - Verify commit success with git status

3. **Pull Request Creation:**
   - Analyze ALL commits in PR, not just latest
   - Include summary and test plan
   - Use heredoc for proper formatting
   - Return PR URL to user

---

## File Organization

### Naming Conventions

1. **Files:**
   - Lowercase with hyphens: `user-service.js`
   - Components: PascalCase: `UserProfile.tsx`
   - Test files: `.test.js` or `.spec.js` suffix

2. **Directories:**
   - Lowercase with hyphens
   - Plural for collections: `components/`, `utils/`

3. **Variables and Functions:**
   - camelCase: `getUserById`, `isAuthenticated`
   - Constants: UPPER_SNAKE_CASE: `MAX_RETRY_COUNT`
   - Classes: PascalCase: `UserService`, `HttpClient`

### File Location

1. **Co-location:**
   - Keep related files close
   - Component with its styles and tests
   - Service with its types

2. **Shared Code:**
   - Common utilities in `src/utils/`
   - Shared types in `src/types/`
   - Reusable components in `src/components/`

---

## Documentation Standards

### Code Documentation

1. **When to Comment:**
   - Complex algorithms
   - Non-obvious business logic
   - Workarounds and their reasons
   - Public API functions

2. **When NOT to Comment:**
   - Self-explanatory code
   - What the code does (code should be clear)
   - Redundant information

3. **Documentation Format:**
   ```javascript
   /**
    * Calculates the compound interest for an investment.
    *
    * @param {number} principal - Initial investment amount
    * @param {number} rate - Annual interest rate (as decimal)
    * @param {number} years - Number of years
    * @returns {number} Total amount after interest
    */
   function calculateCompoundInterest(principal, rate, years) {
     return principal * Math.pow(1 + rate, years);
   }
   ```

### README Files

Each major directory should have a README explaining:
- Purpose of the directory
- Key files and their roles
- How to use the code within
- Any special considerations

### Architecture Documentation

Document major decisions in `docs/architecture/`:
- Why certain patterns were chosen
- Trade-offs considered
- Future considerations

---

## Testing Guidelines

### Test Organization

```
tests/
├── unit/           # Fast, isolated tests
├── integration/    # Tests with external dependencies
└── e2e/            # Full application tests
```

### Test Naming

```javascript
describe('UserService', () => {
  describe('getUserById', () => {
    it('returns user when user exists', () => {
      // Test implementation
    });

    it('returns null when user does not exist', () => {
      // Test implementation
    });

    it('throws error when id is invalid', () => {
      // Test implementation
    });
  });
});
```

### Test Best Practices

1. **AAA Pattern:**
   - Arrange: Set up test data
   - Act: Execute the function
   - Assert: Verify the result

2. **Independent Tests:**
   - Each test should be runnable in isolation
   - No shared state between tests
   - Use beforeEach/afterEach for setup/cleanup

3. **Clear Assertions:**
   - One logical assertion per test
   - Clear failure messages
   - Test both happy and sad paths

---

## Common Tasks

### Starting a New Feature

```bash
# 1. Create feature branch
git checkout -b claude/new-feature-sessionid

# 2. Plan the work (use TodoWrite tool)
# 3. Implement changes
# 4. Test thoroughly
# 5. Commit changes
git add .
git commit -m "feat: add new feature description"

# 6. Push to remote
git push -u origin claude/new-feature-sessionid

# 7. Create pull request
gh pr create --title "Feature: Description" --body "Details"
```

### Fixing a Bug

```bash
# 1. Create fix branch
git checkout -b claude/fix-bug-description-sessionid

# 2. Reproduce the bug
# 3. Write a failing test
# 4. Fix the bug
# 5. Verify test passes
# 6. Commit and push
git add .
git commit -m "fix: resolve issue with specific behavior"
git push -u origin claude/fix-bug-description-sessionid
```

### Adding Tests

```bash
# 1. Identify untested code
# 2. Write tests covering edge cases
# 3. Ensure tests pass
# 4. Commit
git add .
git commit -m "test: add tests for feature X"
```

### Refactoring Code

```bash
# 1. Ensure existing tests exist
# 2. Make refactoring changes
# 3. Verify all tests still pass
# 4. Commit
git add .
git commit -m "refactor: simplify user authentication logic"
```

---

## Key Reminders for AI Assistants

### DO:
- ✅ Read files before modifying them
- ✅ Use TodoWrite for complex multi-step tasks
- ✅ Follow existing code patterns and conventions
- ✅ Keep changes minimal and focused
- ✅ Delete unused code completely
- ✅ Use specialized tools (Read, Edit, Write, Grep, Glob)
- ✅ Run independent operations in parallel
- ✅ Write clear, descriptive commit messages
- ✅ Test changes before committing
- ✅ Ask for clarification when requirements are unclear

### DON'T:
- ❌ Make changes without reading the file first
- ❌ Add features or refactorings not requested
- ❌ Add comments to code you didn't change
- ❌ Add docstrings to unchanged functions
- ❌ Create abstractions for one-time operations
- ❌ Add error handling for impossible scenarios
- ❌ Use bash commands for file operations
- ❌ Use echo/printf to communicate with users
- ❌ Commit secrets or sensitive data
- ❌ Force push or skip git hooks without permission
- ❌ Use emojis unless explicitly requested

---

## Version History

- **v1.0.0** (2025-12-30): Initial creation of CLAUDE.md for claude-code-playground repository

---

## Contributing

When updating this document:
1. Keep it concise but comprehensive
2. Add examples for clarity
3. Update version history
4. Ensure consistency with actual repository practices

---

## References

- [Conventional Commits](https://www.conventionalcommits.org/)
- [Git Best Practices](https://git-scm.com/book/en/v2)
- [Clean Code Principles](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)

---

*This document is a living guide and should be updated as the repository evolves and new conventions are established.*
