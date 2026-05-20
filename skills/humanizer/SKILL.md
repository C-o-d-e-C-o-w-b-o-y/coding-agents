---
name: humanizer
description: Remove signs of AI-generated writing from text. Use when editing or reviewing text to make it sound more natural, direct, and human-written.
---

# Humanizer

Rewrite text so it sounds like a person wrote it. Preserve the meaning, match the intended tone, and remove patterns that make writing feel generated, padded, promotional, or over-polished.

## Core Workflow

When given text to humanize:

1. Read the input carefully.
2. Identify AI-sounding patterns from the sections below.
3. Rewrite the problematic sections while preserving the original meaning.
4. Match the intended voice: casual, formal, technical, editorial, blunt, warm, or another tone implied by context.
5. Add human rhythm and judgment where appropriate.
6. Do a final pass for obvious AI tells, especially em dashes.

## Hard Rule: No Em Dashes

Remove every em dash character from the final output. Replace it with a plain hyphen (`-`) only when a hyphen is grammatically appropriate. Otherwise rewrite the sentence with a comma, period, colon, semicolon, or parentheses.

Do not leave em dashes in quoted text unless the user explicitly asks to preserve exact wording. If exact quotes must be preserved, flag that the quote contains em dashes instead of silently changing it.

## Voice Calibration

If the user provides a writing sample, use it before rewriting:

- Note sentence length and rhythm.
- Note vocabulary level and recurring phrases.
- Note paragraph starts and transitions.
- Note punctuation habits, but still remove all em dashes from the final output unless the user explicitly says otherwise.
- Match the user's voice instead of replacing it with a generic polished style.

If no sample is provided, use natural, varied, direct prose. Let sentences have different lengths. Keep useful personality and judgment. Avoid fake friendliness, ceremony, and perfectly symmetrical structure.

## What To Remove

### Significance Inflation

Watch for: `serves as`, `stands as`, `is a testament to`, `a vital role`, `a crucial moment`, `pivotal`, `underscores`, `highlights the importance`, `reflects broader`, `symbolizing`, `setting the stage`, `evolving landscape`, `indelible mark`, `deeply rooted`.

Problem: The text inflates ordinary facts into grand claims.

Prefer:

```markdown
The institute was established in 1989 to collect and publish regional statistics.
```

Instead of:

```markdown
The institute was established in 1989, marking a pivotal moment in the evolution of regional statistics.
```

### Promotional Language

Watch for: `boasts`, `vibrant`, `rich` used vaguely, `profound`, `showcasing`, `exemplifies`, `commitment to`, `nestled`, `in the heart of`, `groundbreaking`, `renowned`, `breathtaking`, `must-visit`, `stunning`.

Problem: The text sounds like marketing copy.

Rewrite with concrete facts.

### Superficial "-ing" Phrases

Watch for trailing phrases like `highlighting`, `underscoring`, `emphasizing`, `ensuring`, `reflecting`, `symbolizing`, `contributing to`, `fostering`, `showcasing`.

Problem: These phrases often add fake depth without adding information.

Cut them or replace them with specific facts.

### Vague Attribution

Watch for: `industry reports`, `observers have cited`, `experts argue`, `some critics argue`, `several sources`, `many publications`.

Problem: The writer gestures at authority without naming it.

Replace vague attribution with a specific source when available. If no source exists, remove the claim or write it as an unsupported claim.

### Formulaic Challenges Sections

Watch for: `Despite its challenges`, `faces several challenges`, `Future Outlook`, `Challenges and Legacy`.

Problem: These sections often summarize generic problems and end with vague optimism.

Use concrete problems, dates, actors, and actions.

## Language Patterns

### Overused AI Vocabulary

Watch for: `additionally`, `align with`, `crucial`, `delve`, `emphasizing`, `enduring`, `enhance`, `fostering`, `garner`, `highlight`, `interplay`, `intricate`, `key`, `landscape`, `pivotal`, `showcase`, `tapestry`, `testament`, `underscore`, `valuable`, `vibrant`.

Replace with simpler words or remove them.

### Copula Avoidance

Watch for: `serves as`, `stands as`, `marks`, `represents`, `boasts`, `features`, `offers`.

Prefer direct verbs like `is`, `are`, `has`, and `uses`.

### Negative Parallelism

Watch for: `not only... but`, `not just... it's`, `not merely... but also`.

Problem: These constructions are overused and often theatrical.

Prefer one direct sentence.

### Tailing Negations

Watch for clipped endings like `no guessing`, `no wasted motion`, `no extra setup`.

Rewrite as a real clause:

```markdown
The options come from the selected item, so the user does not have to guess.
```

### Rule of Three

Watch for repeated three-part lists used to sound complete.

Problem: The rhythm becomes mechanical.

Keep only the useful items or vary the structure.

### Synonym Cycling

Watch for excessive variation on one subject: `the protagonist`, `the main character`, `the central figure`, `the hero`.

Use the same term when it is clearer.

### False Ranges

Watch for `from X to Y` when X and Y are not a meaningful scale.

Replace with a plain list or specific scope.

### Passive Voice and Subjectless Fragments

Fix passive or subjectless writing when active voice is clearer.

Instead of:

```markdown
No configuration file needed. The results are preserved automatically.
```

Prefer:

```markdown
You do not need a configuration file. The system preserves the results automatically.
```

## Style Patterns

### Em Dash Overuse

Remove every em dash from final output. Usually replace it with a comma, period, colon, semicolon, parentheses, or a plain hyphen if the sentence truly needs a hyphen.

Before:

```markdown
The term is promoted by institutions[em dash]not by the people themselves.
```

After:

```markdown
The term is promoted by institutions, not by the people themselves.
```

### Boldface Overuse

Remove mechanical bolding unless emphasis is genuinely needed.

### Inline-Header Lists

Watch for bullets that start with bold labels and colons:

```markdown
- **Performance:** The app is faster.
- **Security:** Encryption was added.
```

Prefer prose or cleaner bullets:

```markdown
The update speeds up load times and adds encryption.
```

### Title Case Headings

Use sentence case for headings unless the user asks for title case or the format requires it.

### Emojis

Remove decorative emojis from headings and bullets unless they are part of the user's desired voice or product style.

### Curly Quotes

Prefer straight quotes unless the target publication or user style uses curly quotes.

## Communication Patterns

### Chatbot Artifacts

Remove: `Great question`, `Of course`, `Certainly`, `You're absolutely right`, `I hope this helps`, `Would you like`, `let me know`, `here is a`.

Problem: Chatbot phrasing often leaks into content.

### Knowledge-Cutoff Disclaimers

Remove: `as of my last update`, `up to my training data`, `while specific details are limited`, `based on available information`.

Replace with verified facts, or say directly that the claim is not supported if verification is unavailable.

### Sycophantic Tone

Remove overly agreeable phrasing such as `excellent point`, `you're absolutely right`, and inflated praise.

## Filler and Hedging

### Filler Phrases

Use shorter replacements:

- `in order to` -> `to`
- `due to the fact that` -> `because`
- `at this point in time` -> `now`
- `in the event that` -> `if`
- `has the ability to` -> `can`
- `it is important to note that` -> usually remove it

### Excessive Hedging

Trim stacked qualifiers.

Before:

```markdown
It could potentially possibly be argued that the policy might affect outcomes.
```

After:

```markdown
The policy may affect outcomes.
```

### Generic Positive Endings

Remove vague optimistic conclusions like `the future looks bright`, `exciting times lie ahead`, or `a step in the right direction`.

End with the real point.

### Hyphenated Word Pair Overuse

Watch for over-consistent compounds such as `cross-functional`, `client-facing`, `data-driven`, `decision-making`, `well-known`, `high-quality`, `real-time`, `long-term`, and `end-to-end`.

Use hyphens when grammar requires them, but do not hyphenate common word pairs mechanically.

### Persuasive Authority Tropes

Remove phrases like `the real question is`, `at its core`, `in reality`, `what really matters`, `fundamentally`, `the deeper issue`, and `the heart of the matter` unless they add real meaning.

### Signposting

Remove `let's dive in`, `let's explore`, `let's break this down`, `here's what you need to know`, `now let's look at`, and `without further ado`.

Start with the substance.

### Fragmented Headers

Remove one-line warmups that restate a heading.

Before:

```markdown
## Performance

Speed matters.

When users hit a slow page, they leave.
```

After:

```markdown
## Performance

When users hit a slow page, they leave.
```

## Output

Default to returning only the revised text unless the user asks for explanation.

When useful, provide:

1. Revised text
2. Brief notes on the biggest changes
3. Any uncertainty or places where meaning may have changed

Before finalizing, scan for:

- Em dash characters
- Chatbot artifacts
- Vague authority
- Fake significance
- Promotional adjectives
- Mechanical bolding
- Rule-of-three cadence
- Generic upbeat ending

## Reference

This skill is adapted from the upstream `humanizer` skill and Wikipedia's "Signs of AI writing" guidance.
