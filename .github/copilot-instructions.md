# Copilot instructions

## Project shape

- This repository is a self-contained Japanese space-exploration quiz. `index.html` contains the complete app: markup, styles, question data, and runtime behavior.
- Keep the page usable directly from `file://`; the quiz currently has no package manager, build step, server, or external runtime dependencies.

## Architecture and quiz behavior

- The page switches between the `#quiz` and `#result` views. A bottom-of-file JavaScript IIFE owns the quiz state and the `renderQuestion`, `chooseAnswer`, and `showResult` transitions.
- Quiz content is the `questions` array. Each entry has a Japanese `question`, four `answers`, a zero-based `correct` index, and an `explanation`. New or edited entries must preserve those fields and answer-index semantics.
- The UI currently assumes 10 questions. If that changes, keep the static copy and accessibility metadata in sync with `questions.length`, including the question count, progress-bar maximum, and result denominator.
- Answer buttons are built in `renderQuestion`; keep answer text as text content, and preserve their accessible labels and `aria-keyshortcuts`. `chooseAnswer` locks choices, updates the score and live feedback, and moves focus to the next action. The document-level `1`–`4` shortcuts, next-question flow, and restart focus are part of the keyboard interaction.
- `showResult` applies the celebratory presentation at 8 or more correct answers; retain the separate perfect-score treatment and the calmer lower-score results.

## UI conventions

- All styling is inline. Theme colors are CSS custom properties in `:root`, with dark-theme overrides under `prefers-color-scheme: dark`. Reuse these tokens when changing UI colors.
- Keep the narrow responsive layout, mission-control question panel, and animated starfield in CSS. Motion must remain suppressed for `prefers-reduced-motion: reduce`, including result decorations.
- Preserve semantic question headings, the labelled answer group, progress-bar values, live feedback/announcements, and visible keyboard focus styles when changing markup or focus behavior.

## Run and verify

- Open `index.html` directly in a browser; no server is required.
- For interaction changes, smoke-test both correct and incorrect answers, score/progress updates, the 8/10 result threshold, keyboard navigation and restart, and the dark/light and reduced-motion styles in a browser.
- If a Playwright MCP server is configured, use it for browser-level smoke tests; keep the quiz itself dependency-free and runnable directly from `file://`.
