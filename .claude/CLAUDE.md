<!-- BEGIN:nextjs-agent-rules -->

# This is NOT the Next.js you know

This version has breaking changes — APIs, conventions, and file structure may all differ from your training data. Read the relevant guide in `node_modules/next/dist/docs/` (resolved from this file's directory; in monorepos the `next` package may not be visible from the repo root) before writing any code. Heed deprecation notices.

This block is written and re-added by `next dev` — verify at `node_modules/next/dist/server/lib/generate-agent-files.js`. Removing it from a diff only re-creates the uncommitted change; committing it with your work keeps the tree clean.

<!-- END:nextjs-agent-rules -->


# Code Standards

## Core Principles

Write code that is **accessible, performant, type-safe, and maintainable**. Focus on clarity and explicit intent over brevity.

### Type Safety & Explicitness

- Use explicit types for function parameters and return values when they enhance clarity
- Prefer `unknown` over `any` when the type is genuinely unknown
- Use const assertions (`as const`) for immutable values and literal types
- Leverage TypeScript's type narrowing instead of type assertions
- Use meaningful variable names instead of magic numbers - extract constants with descriptive names

### Modern JavaScript/TypeScript

- Use arrow functions for callbacks and short functions
- Prefer `for...of` loops over `.forEach()` and indexed `for` loops
- Use optional chaining (`?.`) and nullish coalescing (`??`) for safer property access
- Prefer template literals over string concatenation
- Use destructuring for object and array assignments
- Use `const` by default, `let` only when reassignment is needed, never `var`

### Async & Promises

- Always `await` promises in async functions - don't forget to use the return value
- Use `async/await` syntax instead of promise chains for better readability
- Handle errors appropriately in async code with try-catch blocks
- Don't use async functions as Promise executors

### React & JSX

- Use function components over class components
- Call hooks at the top level only, never conditionally
- Specify all dependencies in hook dependency arrays correctly
- Use the `key` prop for elements in iterables (prefer unique IDs over array indices)
- Nest children between opening and closing tags instead of passing as props
- Don't define components inside other components
- Use semantic HTML and ARIA attributes for accessibility:
  - Provide meaningful alt text for images
  - Use proper heading hierarchy
  - Add labels for form inputs
  - Include keyboard event handlers alongside mouse events
  - Use semantic elements (`<button>`, `<nav>`, etc.) instead of divs with roles

### Error Handling & Debugging

- Remove `console.log`, `debugger`, and `alert` statements from production code
- Throw `Error` objects with descriptive messages, not strings or other values
- Use `try-catch` blocks meaningfully - don't catch errors just to rethrow them
- Prefer early returns over nested conditionals for error cases

### Code Organization

- Keep functions focused and under reasonable cognitive complexity limits
- Extract complex conditions into well-named boolean variables
- Use early returns to reduce nesting
- Prefer simple conditionals over nested ternary operators
- Group related code together and separate concerns

### Security

- Add `rel="noopener"` when using `target="_blank"` on links
- Avoid `dangerouslySetInnerHTML` unless absolutely necessary
- Don't use `eval()` or assign directly to `document.cookie`
- Validate and sanitize user input

### Performance

- Avoid spread syntax in accumulators within loops
- Use top-level regex literals instead of creating them in loops
- Prefer specific imports over namespace imports
- Avoid barrel files (index files that re-export everything)
- Use proper image components (e.g., Next.js `<Image>`) over `<img>` tags

### Framework-Specific Guidance

**Next.js:**
- Use Next.js `<Image>` component for images
- Use `next/head` or App Router metadata API for head elements
- Use Server Components for async data fetching instead of async Client Components

**React 19+:**
- Use ref as a prop instead of `React.forwardRef`

**Solid/Svelte/Vue/Qwik:**
- Use `class` and `for` attributes (not `className` or `htmlFor`)

---

## Testing

- Write assertions inside `it()` or `test()` blocks
- Avoid done callbacks in async tests - use async/await instead
- Don't use `.only` or `.skip` in committed code
- Keep test suites reasonably flat - avoid excessive `describe` nesting

## When linters Can't Help

Linter will catch most issues automatically. Focus your attention on:

1. **Business logic correctness** - Linters can't validate your algorithms
2. **Meaningful naming** - Use descriptive names for functions, variables, and types
3. **Architecture decisions** - Component structure, data flow, and API design
4. **Edge cases** - Handle boundary conditions and error states
5. **User experience** - Accessibility, performance, and usability considerations
6. **Documentation** - Add comments for complex logic, but prefer self-documenting code

---

Most formatting and common issues are automatically fixed by running the linter script from `package.json`. Run it before committing to ensure compliance.


# Session Start Sequence
 
Read in order, stop if a blocker is found:
 
1. `spec/identity/README.md` — routing for product DNA and brand voice, then `spec/identity/project-dna.md`
2. `spec/sessions/README.md` — routing for session artifacts, then the highest-numbered `session-XX.md` file in `spec/sessions/`; treat the latest session as still active unless it contains an explicit end marker like `Session ended` or `Today's work is done`

---

## Audience & UX Contract
 
Target visitors have short attention spans. Every feature must:
 
- Communicate intent within 2–3 seconds of view
- Use progressive disclosure — don't show everything at once
- Be operable without reading instructions

---

## Animation Rules
 
Animate: state changes, navigation transitions, feedback on actions (success/error), loading states.
Never animate: form submission awaiting response, destructive confirmations, repeated micro-interactions after first use.

---

## Strict Engineering Rules
 
- New feature → invoke `grilling` skill first. No code until spec is confirmed.
- Architecture/system design decisions → `codebase-design` skill.
- Refactoring with broad structural impact → `improve-codebase-architecture` skill.
- Outer radius = inner radius + padding (optical alignment).
- Fix UI root causes in `app/globals.css` or `components/ui/*`, never one-off page overrides, inline styles, or per-component patches.
- Reversible actions: local-first optimistic. Destructive mutations: explicit pending state + confirmation.
- Read exports, callers, and shared utilities before adding any code. If existing structure is unclear, ask.
- After every significant step: state what was done, what's verified, what's next. Do not continue from a state you can't describe, and do not do multiple chunks at once.
- Match existing conventions even if you disagree. If a convention is harmful, surface it — don't fork it silently.
- Push back when a spec is unclear, incomplete, or unworkable, or when a decision or an idea is not suitable to the project's goals and constraints. Ask for clarification, propose a solution, and get confirmation before coding, do not agree blindly.
- "Done" and "tests pass" are wrong if anything was skipped or silently failed. Surface uncertainty, don't hide it.
- Analyze the time and space complexity of the code you write. Identify the complexity of each significant algorithm or loop, justify your reasoning, and suggest optimizations where they would meaningfully improve complexity.

---

## Writing and Reply Rules

- Never use a metaphor, simile, or other figure of speech which you are used to seeing in print.
- Never use a long word where a short one will do.
- If it is possible to cut a word out, always cut it out.
- Never use the passive where you can use the active.
- Never use a foreign phrase, a scientific word, or a jargon word if you can think of an everyday English equivalent.
- Break any of these rules sooner than say anything outright barbarous.
- When writing anything to the interface or project (not user), invoke `unslop` skill to get rid of any AI slop, robotic tone, em dashes, or any other undesirable jargon in your writing. If you are unsure, ask for a second opinion.

---

## Session Wrap-up

Run `/wrap-up` skill.
