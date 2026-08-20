# Information architecture

Use this reference when the source is verbose, mixed in purpose, or difficult to
scan. Fix the information order before polishing sentences.

## Content priority

Rank content by what the reader needs to succeed:

1. **Must know:** information required to understand, decide, act, or stay safe.
2. **Should know:** information that enables a correct or confident result.
3. **Useful context:** background, rationale, examples, and alternatives.
4. **Low-frequency detail:** exhaustive edge cases, history, and deep reference.

Put must-know content in the title, opening, headings, first sentences, and
primary path. Keep should-know content close to the action it supports. Layer
useful context and low-frequency detail behind descriptive headings and links,
not vague labels such as "More information."

## The orientation block

For a document longer than a short answer, provide a compact orientation block
near the top. Adapt the labels to the document:

```markdown
## In brief

Use [the recommended path] because [the main reason]. This applies to [scope].

- **Outcome:** What the reader gets
- **Audience:** Who this is for
- **Prerequisites:** What must already be true
- **Next action:** What the reader can do now
```

Do not create an orientation block that merely repeats the title. It should help
the reader decide relevance and choose a path.

## Headings as navigation

Treat every heading as a promise. A reader scanning only the headings should be
able to reconstruct the document's main path.

- Name the subject or action directly.
- Put distinguishing words early.
- Prefer "Configure authentication" to "Configuration."
- Prefer "When requests fail" to "Troubleshooting considerations."
- Keep heading levels logical and use one hierarchy for one document.
- Avoid clever, metaphorical, or generic headings when findability matters.

## Progressive disclosure

Show the smallest complete path first, then make deeper detail easy to reach.
Good progressive disclosure has an obvious next layer and preserves critical
warnings in the primary path. Do not hide prerequisites, irreversible effects,
security implications, or required decisions in a collapsed section.

In Markdown, use short sections, descriptive links, and separate reference
pages. In HTML or rich documents, use details or accordions only when the label
describes the hidden content and the reader can access it without losing place.

## Scanning checkpoints

Create useful checkpoints at these levels:

- **Document:** title, one-sentence purpose, summary, and next action.
- **Section:** heading, opening point, and local outcome.
- **Paragraph:** first sentence states the point; following sentences support it.
- **Procedure:** step action, condition, expected result, and recovery path.
- **Reference item:** name, definition, syntax or value, constraints, example.

These checkpoints externalize context. They help readers resume after scanning,
interruption, or a jump to another section.

## Information scent

Links, labels, and headings should predict what the reader will find next. Use
specific labels such as `Configure environment variables` or `Authentication
reference`. Avoid `click here`, `read more`, `miscellaneous`, and branded terms
that do not describe the destination.

## Splitting documents

Split a document when it serves different audiences, different tasks, or
different levels of detail. Keep a page together when readers need a broad view
to understand the relationship between its parts. Navigation and cross-links
must make the split understandable.
