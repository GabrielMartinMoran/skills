---
name: cognitive-writing
description: >-
  Write, rewrite, review, and structure documentation and general text for
  cognitive accessibility, clarity, focus, and impact. Use this skill whenever
  the user asks for a README, guide, tutorial, reference, explanation, policy,
  report, specification, long-form text, dense-content rewrite, plain-language
  edit, accessibility improvement, better scannability, ADHD-friendly or
  neurodivergent-friendly content, information prioritization, or visual text
  hierarchy, even when they do not name cognitive accessibility explicitly.
  Preserve technical accuracy, necessary complexity, caveats, and user intent
  while improving how easily readers can enter, scan, understand, remember, and
  act on the content.
license: "MIT"
metadata:
  version: "0.1.0"
  author: Gabriel Martin Moran [moran.gabriel.95@gmail.com]
  source: "https://github.com/GabrielMartinMoran/skills"
---

# Cognitive writing

Write documents that reduce avoidable cognitive effort without reducing the
truth, nuance, or usefulness of the content. Treat structure, wording, and
visual hierarchy as part of the meaning. Make the next useful action obvious.

This skill applies universal cognitive-accessibility practices. It does not
promise that a document will work identically for every person with ADHD or any
other cognitive or learning disability. Individual testing and personalization
remain more reliable than a fixed style recipe.

## Core rule

**Make the content easier to enter, scan, understand, remember, and act on
without discarding necessary complexity.**

Use layers instead of deletion:

- Put the essential answer, decision, or action first.
- Keep supporting reasoning, definitions, examples, constraints, and exceptions
  available at the point where they help.
- Move genuinely secondary detail into clearly labeled sections or references.
- Remove repetition, filler, ambiguity, and decorative noise rather than
  removing meaning.

## Operating workflow

Follow this sequence unless the user asks for a narrower operation.

### 1. Establish the brief

Identify the document's job, audience, reader tasks, medium, language, risk
level, and expected depth. For technical content, inspect the surrounding
project and source of truth before changing claims. Ask a focused question when
an unknown audience, goal, or medium would materially change the result.

If the missing context is not material, proceed with a stated assumption rather
than blocking the work.

### 2. Build a content inventory

Before rewriting, extract the content that must survive:

- claims, decisions, requirements, and definitions;
- procedures, prerequisites, examples, and expected outcomes;
- caveats, exceptions, failure modes, numbers, links, and citations;
- unresolved or potentially inaccurate statements that need confirmation.

Classify each item as essential, supporting, optional, redundant, or uncertain.
Preserve essential and supporting items. Flag uncertain items instead of
silently changing them. Remove optional or redundant items only when doing so
does not change the reader's decision or ability to complete the task.

### 3. Choose the document shape

Choose the shape that matches the reader's need before choosing sentence style:

- **Tutorial:** learning through a safe, meaningful sequence.
- **How-to:** completing a specific task.
- **Reference:** looking up complete, precise information.
- **Explanation:** understanding context, rationale, or tradeoffs.
- **README:** orienting quickly, installing or trying the project, then finding
  deeper documentation.
- **Decision or policy document:** understanding the decision, scope, rationale,
  constraints, and consequences.

Read `references/document-modes.md` for selection guidance and default
structures. Combine modes only when the boundaries between them are visible.

### 4. Design the reader path

Give the document an explicit path through five questions:

1. What is this, and why does it matter?
2. What does the reader need to do or decide now?
3. What details explain or enable that action?
4. What constraints, risks, exceptions, or failure states matter?
5. What should the reader do next?

Use an inverted-pyramid order for task-oriented and web content: essential
information first, enabling detail second, background or low-frequency detail
last. Use a different order when readers must learn concepts in sequence or
when the subject's logic requires prior context; explain that choice through
clear headings and signposts.

Read `references/information-architecture.md` when the source is long, mixed in
purpose, or difficult to navigate.

### 5. Write for comprehension

- State the subject and action early.
- Use concrete, familiar words when they are accurate.
- Prefer active voice and specific verbs.
- Keep each sentence focused on one main idea.
- Keep each paragraph focused on one topic and make its opening sentence carry
  the point.
- Define unavoidable jargon at first use and use one term consistently for one
  concept.
- Use literal wording when ambiguity, stress, safety, or precise action matters.
- Replace nested clauses, double negatives, filler, vague pronouns, and implied
  prerequisites with explicit relationships.
- Preserve technical terms, formal definitions, mathematical meaning, and
  necessary qualifications when simpler wording would be less accurate.

Read `references/language-and-visual-patterns.md` for sentence, paragraph, list,
link, code, table, and callout guidance.

### 6. Create visual hierarchy

Use formatting to reveal relationships, priority, and action. Do not use it as
decoration or as a substitute for editing.

- Use descriptive, front-loaded headings that tell the reader what is there.
- Keep heading levels logical and do not skip levels.
- Use paragraphs for connected reasoning, bullets for parallel items, and
  numbered lists for sequence, priority, or a countable procedure.
- Use tables for genuine comparisons or repeated fields, not for ordinary prose.
- Use code blocks for exact commands, syntax, output, and configuration.
- Use links whose labels describe the destination or action without surrounding
  context.
- Use summaries, callouts, bold text, and visual examples selectively. Each
  section should have a clear dominant signal instead of many competing ones.
- Use whitespace to separate concepts and make the reading path visible.
- For HTML or rich documents, preserve semantic structure, contrast, scalable
  text, user control, and meaningful alternative text. Never make color, motion,
  icons, or typography the only carrier of meaning.

### Section anatomy

Treat a section as a cognitive checkpoint, not as a heading followed by an
unstructured block of text. Give each section one job and use this anatomy when
it fits the document mode:

1. **Heading:** name the subject, action, decision, or question the section
   answers.
2. **Lead:** state the section's point, outcome, or relevance in the opening
   sentence or short paragraph.
3. **Core content:** provide the explanation, procedure, comparison, or
   reference information.
4. **Support block:** add one useful example, code block, table, definition, or
   evidence block when it improves understanding.
5. **Boundary block:** surface a warning, constraint, exception, or uncertainty
   when the reader needs it to act correctly.
6. **Exit signal:** show the result, checkpoint, next step, or link to a deeper
   section when the reader needs help continuing.

Do not force every section to contain every part. Do not stack headings with no
orientation between them. Use a blank line and a visible change in purpose to
separate blocks, but do not put every paragraph in a box or callout. A block
earns visual weight when it helps the reader recognize a different kind of
information, not merely because the paragraph is important to the author.

### 7. Validate before delivery

Run these checks against the final document:

1. **Fidelity:** Are all essential claims, constraints, examples, numbers,
   links, and exceptions preserved or explicitly flagged? Did the rewrite avoid
   adding guarantees, outcomes, or operational effects that the source does not
   support?
2. **Purpose:** Can a reader tell what the document is for and whether it is
   relevant from the title and opening?
3. **Findability:** Can a reader scanning headings and first sentences locate
   the main task, answer, decision, or warning?
4. **Cognitive load:** Are unnecessary memory demands, hidden prerequisites,
   jargon, ambiguity, repetition, and visual distractions reduced?
5. **Hierarchy:** Does emphasis reflect importance, or is everything competing
   for attention?
6. **Actionability:** Are procedures ordered, conditions explicit, outcomes
   visible, and recovery paths documented?
7. **Accessibility:** Are headings semantic, links descriptive, lists parallel,
   code exact, tables necessary, and visuals explained?
8. **Fit:** Does the structure match the audience, medium, language, and risk?

Read `references/quality-checklist.md` for the full review pass and evidence
boundaries.

## ADHD and cognitive accessibility

Use ADHD-informed practices as ways to reduce avoidable barriers, not as claims
about every ADHD reader. Prefer clear purpose, visible structure, short paths,
restorable context, explicit instructions, summaries, searchable labels, and
reduced interruption. Keep the full content available through progressive
disclosure rather than assuming that shorter always means better.

Do not diagnose, stereotype, or promise an "ADHD-proof" result. Do not force a
single font, color scheme, paragraph length, reading level, or visual format.
When the audience is important or the document is high-stakes, recommend testing
with representative readers and offer adaptable versions where practical.

## Impact without noise

Make text compelling through relevance and precision:

- name the reader's problem or desired outcome early;
- lead with the consequence, decision, or benefit that changes attention;
- use concrete examples and meaningful contrasts;
- make headings and link labels useful even when scanned alone;
- use confident, direct language without hype, clickbait, or false certainty.

Visual emphasis earns attention when it is scarce and meaningful. If a reader
cannot tell what matters most after a quick scan, revise the information order
before adding more formatting.

## Default output behavior

When rewriting or creating content, return the requested document in the user's
language and medium. Preserve established terminology and project conventions
unless they create a clear accessibility or accuracy problem. Include a short
editorial summary only when the user asks for rationale, review notes, or a
change log.

When reviewing instead of rewriting, report findings by impact and location,
then give concrete revisions. Separate factual or accessibility problems from
subjective style preferences.

## References

Read only the reference needed for the current task:

- `references/principles-and-boundaries.md` for evidence, caveats, and ADHD
  language.
- `references/document-modes.md` for README, tutorial, how-to, reference,
  explanation, policy, and decision structures.
- `references/information-architecture.md` for prioritization, navigation,
  progressive disclosure, and reader paths.
- `references/language-and-visual-patterns.md` for sentence-level and layout
  decisions across Markdown, HTML, and plain text.
- `references/transformation-examples.md` for before-and-after section and
  formatting patterns.
- `references/quality-checklist.md` for the final review and test questions.
