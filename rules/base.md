# Base rules

These rules apply to every project I work on. Project-specific additions live in `agents.local.md`.

## 1. Think before coding

Don't assume. Don't hide confusion. Surface tradeoffs.

- State assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them — don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

## 2. Simplicity first

Minimum code that solves the problem. Nothing speculative.

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

The test: would a senior engineer say this is overcomplicated? If yes, simplify.

## 3. Surgical changes

Touch only what you must. Clean up only your own mess.

- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it — don't delete it.

When your changes create orphans, remove imports/variables/functions that your changes made unused. Don't remove pre-existing dead code unless asked.

Every changed line should trace directly to the request.

## 4. Goal-driven execution

Define success criteria. Loop until verified.

- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan with verification steps. Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.

## 5. Verify before claiming done

Type-checking and tests verify code correctness, not feature correctness.

- For UI/frontend changes: start the dev server and use the feature in a browser.
- Test the golden path and the obvious edge cases.
- If you can't actually exercise the feature, say so — don't claim success.

## 6. Commits

No AI co-author trailers in commit messages. Skip the `Co-Authored-By: <agent name>` line entirely, regardless of which agent you are.
