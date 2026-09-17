## General Working Style

- Understand the user's goal before editing.
- Inspect existing code and patterns before inventing new ones.
- Preserve unrelated user changes in a dirty worktree.
- Prefer the smallest coherent change that fully solves the problem.
- Do not introduce dependencies without a clear reason.
- Validate with the most relevant available tests, builds, linters, or runtime
  checks.
- Report concrete outcomes, remaining risks, and verification results.
- Do not stop at “it works” when the request includes product quality or visual
  polish. Visual polish does not imply adding more UI; often the best polish is
  simplification, tighter hierarchy, and removal of unnecessary elements.

## Frontend Design and Implementation Standards

Apply this section only to frontend or UI work. Repository-specific design
systems, components, tokens, and conventions take precedence.

Act like a senior frontend engineer with strong product judgment. Make the UI
intentional, restrained, responsive, accessible, and production-ready. Treat
simplicity and information density as forms of polish. Do not interpret
“polished” as “more designed.”

Favor clarity, utility, and trust over novelty, decoration, or visual spectacle.

### Simplicity and Information Density

For authenticated product UI, settings, admin pages, dashboards, account pages,
management tools, and CRUD-style screens, default to utilitarian presentation
rather than marketing presentation.

Think utility application, not landing page.

- If the purpose of a screen is to show data, show the data.
- If the purpose of a screen is to edit settings, show the settings.
- If the purpose of a screen is to show a list, show the list.
- Prefer compact lists, rows, tables, forms, and normal-sized headings.
- Keep the actual information and controls visually prominent and easy to reach.
- Do not bury useful content below decorative or explanatory content.
- Preserve the visual density and complexity of nearby existing screens unless
  the user explicitly asks for a redesign.
- When choosing between a simpler implementation and a more visually elaborate
  implementation that communicates the same information, prefer the simpler
  one.
- Do not add UI merely to make a sparse page feel fuller or more “premium.”
- Empty space is not automatically good design. Use enough spacing for clarity,
  not enough to separate closely related information unnecessarily.
- Compact content may remain compact on large screens. Do not spread sparse
  content across the viewport merely to create visual balance.
- Avoid manufacturing hierarchy by repeating the same concept at several
  visual levels.

Avoid unless explicitly requested, required by the existing design system, or
clearly necessary for usability:

- oversized H1 or hero typography
- hero sections
- marketing-style introductions
- eyebrow labels such as “YOUR SETTINGS” above an already obvious heading
- slogans, taglines, or inspirational copy
- large explanatory tiles
- decorative horizontal rules
- decorative cards around simple content
- repeated headings that communicate the same thing
- large empty-state illustrations
- excessive whitespace
- multiple sections for information that could be presented clearly in one
  compact section
- decorative gradients, shadows, borders, or containers that do not improve
  comprehension
- explanatory text for concepts the user already understands from context

For example, a simple blocked-user management screen should generally prefer:

    Blocked Users

    user-one        Unblock
    user-two        Unblock

or, when empty:

    Blocked Users

    You haven't blocked anyone.

Do not turn a simple settings or list page into a hero page with multiple
headings, explanatory panels, slogans, decorative dividers, and large empty
regions unless the request specifically calls for that treatment.

Before adding a UI element, ask:

1. Does this help the user perform the task?
2. Does this communicate useful information the user does not already have?
3. Does this improve comprehension, navigation, feedback, or accessibility?
4. Would removing it make the page meaningfully worse?

If the answer is no, leave it out.

### Product and Visual Principles

- Give every screen a clear purpose.
- Make the primary information or action obvious when one exists.
- Do not invent a primary action for passive settings, status, or list screens.
- Prefer hierarchy, typography, spacing, and contrast before borders, shadows,
  extra containers, or color.
- Make important elements obvious and secondary elements quiet.
- Avoid generic dashboard card grids, stock framework examples, random
  gradients, excessive borders, weak contrast, and inconsistent radii or
  shadows.
- Use meaningful real-world content lengths, including long and missing values.
- Keep layouts aligned and readable on wide screens, but do not expand or spread
  sparse content merely to fill available space.
- Use the project's spacing scale. If none exists, use an 8px-based scale with
  4px for very small gaps.
- Prefer one level of grouping when one level is enough.
- Use cards only when the content is genuinely a distinct grouped object, not
  simply because cards are available.
- Avoid visual complexity that exceeds the complexity of the underlying task.

### Responsive Design

Design and verify mobile, tablet, laptop, and wide-desktop behavior. At minimum,
consider 390x844, 768x1024, 1280x800, and 1440x900.

- Prevent unintended horizontal scrolling.
- Collapse navigation and multi-column layouts appropriately.
- Keep controls usable and text readable on narrow screens.
- Use at least 44px touch targets where practical.
- Never make critical actions hover-only.
- Make tables scroll, reduce to priority columns, or transform for mobile.
- Keep dialogs within the viewport and easy to dismiss.
- Use max-widths so text and layouts do not stretch awkwardly.
- Reduce mobile density intentionally rather than shrinking everything.
- Do not increase desktop whitespace simply because more viewport space is
  available.
- Keep related information visually close across viewport sizes.

### Typography, Color, and Motion

- Use a small, consistent type scale with clear hierarchy and readable line
  height.
- Reserve very large typography for cases where it serves a genuine product
  purpose, not merely to make a screen feel designed.
- Keep body text near a comfortable 60–80 character line length when possible.
- Maintain WCAG AA contrast where practical; muted text must remain readable.
- Use a restrained palette and semantic colors consistently.
- Never rely on color alone for state.
- Keep most transitions around 150–250ms and use motion to explain change, not
  decorate it.
- Respect `prefers-reduced-motion`.
- If dark mode exists, design its surfaces, borders, focus states, and contrast
  intentionally rather than simply inverting colors.
- Avoid adding accent colors merely to create visual interest.
- Use typographic emphasis sparingly so hierarchy remains meaningful.

### Components and Interaction

- Reuse existing project components before creating new ones.
- Make components reusable without premature abstraction or giant prop APIs.
- Support relevant default, hover, focus, active, disabled, loading, error,
  empty, and success states.
- Use one clear primary action per main section when a primary action genuinely
  exists.
- Keep secondary actions quieter and destructive actions distinct.
- Do not add action buttons simply to make a section feel complete.
- Use visible form labels, appropriate mobile input types, nearby errors, and
  clear focus states.
- Use cards only for meaningful grouped objects; avoid nested cards.
- Prefer plain rows or lists for simple collections.
- Use tables when comparison matters, align numeric data, and handle long
  content and empty states.
- Keep navigation labels clear and make the current location obvious.
- Make destructive actions difficult to trigger accidentally.
- Keep controls close to the objects they affect.
- Avoid separating a label, value, and action into distant visual regions unless
  the layout materially benefits from doing so.

### States and Feedback

Account for loading, empty, error, success, disabled, permission-denied,
offline/unavailable, no-results, and first-use states when relevant.

- Prefer skeletons for structured loading and avoid layout shift.
- Keep empty states proportional to the screen.
- For simple lists and settings, prefer one concise sentence such as
  “You haven't blocked anyone.”
- Only add explanatory copy, illustrations, or a next action to an empty state
  when they materially help the user.
- Do not turn routine empty states into marketing moments.
- Use human-readable errors, preserve user input, and avoid leaking raw errors
  outside developer tools.
- Confirm success briefly without interrupting the flow.
- Prefer inline feedback near the affected control or content when practical.
- Do not create large success banners for trivial operations.

### Accessibility

- Use semantic HTML; buttons perform actions and links navigate.
- Give every input an accessible label.
- Keep all interactions keyboard reachable with visible focus.
- Use ARIA only when semantic HTML is insufficient.
- Trap focus in modals and make menus keyboard navigable.
- Provide meaningful alt text and hide decorative images from assistive tools.
- Never rely on color alone for status or errors.
- Do not sacrifice semantic structure for visual styling.
- Keep reading order and visual order aligned where practical.

### Code Quality and Performance

- Follow the repository's language and framework choices.
- Do not force TypeScript into a JavaScript project.
- Keep components focused and separate business logic from presentation where
  practical.
- Use meaningful names, remove unused code, and avoid placeholder TODOs.
- Prefer existing tokens and styling conventions over arbitrary values.
- Avoid unnecessary rendering, main-thread work, network requests, and bundle
  growth.
- Optimize images, reserve media dimensions, lazy-load heavy code when useful,
  and paginate or virtualize large collections.
- Do not add a component abstraction when a small amount of straightforward
  markup is clearer.
- Do not introduce design-system machinery to solve a one-off simple layout
  problem unless there is a clear reuse case.

## Cubacadabra documentation authority

- Keep hand-written, cross-repository Cubacadabra product documentation in the
  sibling `docs` repository. Read and update its canonical contract whenever
  a public or cross-repository contract changes, in the same piece of work.
- Do not create competing hand-written contract pages in an implementation
  repository's `docs/` directory. Keep local build, test, release, and
  implementation-specific instructions in its README or CONTRIBUTING file;
  generated references stay with their generators, and executable fixtures
  stay under tests.
- Do not delete or empty existing sibling `docs/` directories until the
  central source-disposition ledger is complete and the owner explicitly
  authorizes source cleanup.
