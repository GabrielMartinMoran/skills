# Prompt Engineering Techniques Reference

Comprehensive catalog of research-backed prompting techniques. Organized by category. Each entry includes: what it is, when to use it, how to apply it, and supporting research.

---

## Table of Contents

1. [Foundational Techniques](#1-foundational-techniques)
2. [Reasoning Techniques](#2-reasoning-techniques)
3. [Output Control Techniques](#3-output-control-techniques)
4. [Context & Retrieval Techniques](#4-context--retrieval-techniques)
5. [Automatic Optimization Techniques](#5-automatic-optimization-techniques)
6. [Agent-Specific Techniques](#6-agent-specific-techniques)
7. [Meta-Techniques](#7-meta-techniques)

---

## 1. Foundational Techniques

### 1.1 Zero-Shot Prompting

**What**: Direct instruction without examples.
**When**: Simple, well-defined tasks the model handles natively (classification, extraction, summarization).
**How**: Clear instruction + input + output format specification.
**Limitation**: Insufficient for complex structured outputs or domain-specific formats.

```
Classify the following customer message as POSITIVE, NEGATIVE, or NEUTRAL.
Respond with only the label.

Message: {input}
```

### 1.2 Few-Shot / Multishot Prompting

**What**: Provide 2-5 input/output examples before the actual task.
**When**: Structured output tasks, format-sensitive tasks, domain-specific classification.
**How**: Wrap examples in `<example>` tags (Claude) or clear delimiters. Ensure diversity across examples.
**Research**: Brown et al. (2020) "Language Models are Few-Shot Learners" — GPT-3 paper establishing few-shot as a core paradigm.

Best practices:
- 3-5 examples is the sweet spot. More than 7 rarely helps and wastes tokens.
- Include at least one edge case example.
- Order matters slightly — put the most representative example first.
- If examples create unintended patterns (e.g., all examples are short → model always outputs short), add a diverse example to break the pattern.

### 1.3 Role / Persona Prompting

**What**: Assign a specific expertise/identity in the system prompt.
**When**: Always — even a one-sentence role improves focus and tone.
**How**: "You are a [role] with expertise in [domain]. You communicate [style]."
**Research**: Consistent improvement across Claude, GPT, and Gemini. Particularly effective on smaller models.

```
You are a senior security engineer specializing in OWASP Top 10 vulnerabilities.
You communicate findings concisely with severity ratings and actionable remediation steps.
```

### 1.4 Instruction Decomposition

**What**: Break complex tasks into sequential numbered steps.
**When**: Multi-step tasks where order and completeness matter.
**How**: Number each step. Make each step atomic (one action per step).
**Key insight**: Models execute numbered steps more reliably than prose paragraphs describing the same workflow.

### 1.5 Positive Framing

**What**: Tell the model what TO do, not what NOT to do.
**When**: Always. Negative instructions ("don't use jargon") are less reliable than positive ones ("use plain language accessible to a general audience").
**Research**: Anthropic's prompting best practices documentation emphasizes this consistently.

---

## 2. Reasoning Techniques

### 2.1 Chain-of-Thought (CoT)

**What**: Ask the model to reason step-by-step before giving a final answer.
**When**: Math, logic, multi-step analysis, code debugging.
**How**: Add "Think through this step by step" or provide examples with explicit reasoning traces.
**Research**: Wei et al. (2022) "Chain-of-Thought Prompting Elicits Reasoning in Large Language Models."

**Important nuance for modern models**: Claude Opus 4.6, GPT-5+, and other frontier models have native reasoning. Over-prompting CoT on these models can cause overthinking. Use `effort` parameters or model-native thinking features instead of manually instructing CoT.

### 2.2 Self-Consistency

**What**: Sample multiple reasoning paths and take the majority vote.
**When**: High-stakes decisions, math, logic where single-path errors are costly.
**How**: Run the same prompt N times (temperature > 0), take majority answer.
**Research**: Wang et al. (2023) — 2-3x accuracy boost over standard CoT on arithmetic tasks.
**Limitation**: Requires multiple API calls. Best for batch/offline processing, not real-time.

### 2.3 Tree-of-Thought (ToT)

**What**: Explore multiple reasoning branches, evaluate them, and select the best path.
**When**: Complex planning, architecture decisions, strategy with trade-offs.
**How**: Instruct the model to generate 2-3 approaches, evaluate each against criteria, then select and develop the best one.
**Research**: Yao et al. (2023) "Tree of Thoughts: Deliberate Problem Solving with Large Language Models."

```
Generate 3 distinct approaches to solve this problem.
For each approach, evaluate: feasibility, maintainability, performance.
Select the best approach and implement it fully.
```

### 2.4 Reflection / Self-Verification

**What**: Ask the model to check its own work before delivering.
**When**: Coding, math, factual claims, any task with verifiable correctness.
**How**: Append "Before you finish, verify your answer against [criteria]."
**Research**: Anthropic docs recommend this consistently. Effective on Claude 4.x models.

### 2.5 Backward Reasoning

**What**: Generate answer → reconstruct the question from the answer → cross-check conditions.
**When**: Multi-condition logic problems, complex requirements analysis.
**Research**: ACL 2025, NAACL 2025 backward reasoning literature.

### 2.6 ReAct (Reasoning + Acting)

**What**: Interleave reasoning traces with tool actions in a loop.
**When**: Agentic tasks that combine thinking with external tool use.
**How**: Structure as: Thought → Action → Observation → Thought → ...
**Research**: Yao et al. (2023) "ReAct: Synergizing Reasoning and Acting in Language Models."

---

## 3. Output Control Techniques

### 3.1 Output Format Specification

**What**: Define the exact structure of the desired output.
**When**: Always for structured outputs. Critical for downstream parsing.
**How**: Provide a template, JSON schema, or example of the exact output format.

```xml
Respond in this exact format:
<analysis>
  <summary>One-sentence summary</summary>
  <findings>
    <finding severity="HIGH|MEDIUM|LOW">Description</finding>
  </findings>
  <recommendation>Actionable next step</recommendation>
</analysis>
```

### 3.2 Constrained Output / Format Indicators

**What**: Use XML tags or structured delimiters to control where content goes.
**When**: When you need clean separation of output sections (thinking vs answer, code vs explanation).
**How**: "Write your analysis in `<analysis>` tags and your final answer in `<answer>` tags."

### 3.3 Prefilled Response (Claude Legacy)

**What**: Start the assistant's response to force a format.
**When**: Claude models before 4.6 only. Deprecated in Claude 4.6.
**Migration**: Use explicit format instructions instead. See Anthropic's migration guide.

### 3.4 Verbosity Control

**What**: Explicitly control response length and detail level.
**When**: When default verbosity doesn't match your needs.
**How**: Be specific: "Respond in 2-3 sentences" or "Provide a comprehensive analysis of at least 500 words."

### 3.5 LaTeX / Math Formatting Control

**What**: Control whether mathematical expressions use LaTeX or plain text.
**When**: Claude Opus 4.6 defaults to LaTeX — override if you need plain text.
**How**: "Format all math as plain text using /, *, ^ operators. Do not use LaTeX."

---

## 4. Context & Retrieval Techniques

### 4.1 Document Positioning (Long Context)

**What**: Place long documents at the top of the prompt, instructions at the bottom.
**When**: Any prompt with 20k+ tokens of context.
**Research**: Anthropic testing shows up to 30% improvement in response quality.
**How**: Structure as: [documents] → [examples] → [instructions] → [query].

### 4.2 Grounding in Quotes

**What**: Ask the model to extract relevant quotes from provided documents before reasoning.
**When**: Long-document QA, analysis tasks, anything where hallucination risk is high.
**How**: "First, extract the relevant quotes from the documents. Then, based only on these quotes, provide your analysis."
**Research**: Anthropic's long context tips. Dramatically reduces hallucination.

### 4.3 Context Windowing / Compaction

**What**: Summarize and compress conversation history to fit within context limits.
**When**: Long-horizon agentic tasks, multi-turn conversations approaching context limits.
**How**: Instruct the model to preserve architectural decisions and unresolved issues while discarding redundant content.
**Research**: Anthropic's context engineering blog — Claude Code uses this approach in production.

### 4.4 Just-in-Time Context Loading

**What**: Load context on demand via tool calls instead of pre-loading everything.
**When**: Agentic systems working with large codebases or databases.
**How**: Store lightweight references (file paths, URLs, query templates) and load data dynamically.
**Research**: Anthropic's effective context engineering for AI agents.

### 4.5 RAG Integration

**What**: Retrieve relevant external documents and inject them into the prompt.
**When**: Tasks requiring up-to-date or domain-specific knowledge.
**How**: Embed the retrieved context in `<context>` tags with source attribution.

---

## 5. Automatic Optimization Techniques

### 5.1 APE (Automatic Prompt Engineer)

**What**: Use an LLM to generate candidate prompts, evaluate them, select the best.
**Research**: Zhou et al. (2023) ICLR — showed LLM-generated prompts can outperform human-written ones.
**When**: You have clear evaluation criteria and test data but struggle to manually write the optimal prompt.

### 5.2 OPRO (Optimization by Prompting)

**What**: Iteratively optimize prompts by showing the LLM previous prompts + their scores and asking it to produce a better one.
**Research**: Yang et al. (2024) — discovered "Take a deep breath" improves math performance through meta-optimization.
**When**: You have a metric and can run multiple evaluation rounds.

### 5.3 DSPy / MIPROv2

**What**: Programmatic prompt optimization framework. Treats prompts as code with signatures, modules, and optimizers.
**Research**: Khattab et al. (2024) EMNLP — MIPRO optimizer uses Bayesian optimization to find optimal prompt + demonstration combinations.
**When**: Production systems where you need systematic, reproducible prompt optimization with clear metrics.
**Key insight**: DSPy separates *what* (signatures) from *how* (optimization), enabling automatic prompt refinement.

### 5.4 EvoPrompt

**What**: Evolutionary algorithm approach to prompt optimization. Mutates and selects prompts across generations.
**Research**: Guo et al. (2025) — consistently outperforms manually designed prompts.
**When**: Large search space of possible prompt formulations.

### 5.5 TextGrad

**What**: Treats text feedback as "gradients" for optimization. LLM evaluates output, identifies weaknesses, refines the prompt.
**Research**: Yuksekgonul et al. (2024) — "Automatic differentiation via text."
**When**: Complex multi-component systems where you need to optimize each component's prompt.

### 5.6 Anthropic Console Prompt Improver

**What**: Built-in tool that enhances prompts by adding XML structure, examples, and CoT.
**When**: Quick first-pass improvement. Good starting point before manual refinement.
**How**: Submit your prompt in the Anthropic Console → Prompt Improver → review and refine.

---

## 6. Agent-Specific Techniques

### 6.1 Conceptual Engineering over Rigid Templates

**What**: Give agents principles and heuristics rather than step-by-step scripts.
**When**: Always for autonomous agents. Scripts break on novel situations.
**Research**: Anthropic Applied AI team (2025) — building Claude Code and advanced research agents.
**How**: Define decision-making criteria, not decision trees.

```
When deciding whether to search the codebase or read a specific file:
- If you know the file path, read it directly.
- If you need to find something but don't know where it is, search first.
- If search returns too many results, refine with a more specific query.
```

### 6.2 Three Pillars of Agentic Prompts

**What**: Structure agent system prompts around three categories.
**Research**: Originated in OpenAI's GPT-4.1/5 guides, but applies universally to any frontier model used as an agent.

1. **Persistence & drive**: Encourage the agent to keep going, not give up early, try alternative approaches on failure.
2. **Tool use guidance**: Clear examples of how to invoke tools, when to use them, and what to do with results.
3. **Scope discipline**: Don't expand the task beyond what was asked. Flag optional additional work as optional.

### 6.3 Default-to-Action vs Conservative Prompting

**What**: Control whether the agent acts proactively or waits for explicit instruction.
**When**: Configure based on your use case's risk tolerance.

For proactive agents:
```xml
<default_to_action>
Implement changes rather than only suggesting them. If intent is unclear,
infer the most useful action and proceed. Use tools to discover missing
details instead of guessing.
</default_to_action>
```

For conservative agents:
```xml
<do_not_act_before_instructions>
Do not make changes unless clearly instructed. Default to providing
information and recommendations. Only proceed with edits when
explicitly requested.
</do_not_act_before_instructions>
```

### 6.4 Parallel Tool Call Control

**What**: Explicitly enable or constrain parallel tool execution.
**When**: Performance-critical agents (enable) or order-sensitive workflows (constrain).
**Research**: Frontier models (Claude 4.6, GPT-5.x, Kimi K2.5) all excel at parallel execution with explicit prompting.

### 6.5 Prompt Chaining

**What**: Split a complex task across multiple sequential LLM calls, where each call's output feeds the next.
**When**: Tasks with distinct phases (research → analyze → write → review).
**How**: Design each prompt as a focused, single-responsibility step. Pass structured output between steps.

### 6.6 Context-Aware State Management

**What**: Instruct agents to track their remaining context budget and manage it.
**When**: Long-horizon tasks that approach context limits.
**Research**: Available in Claude 4.5/4.6 (native), GPT-5.x (via compaction API). Implementable via prompt instructions on any model.
**How**: Inform agents about compaction availability and context-saving mechanisms in their system prompt.

---

## 7. Meta-Techniques

### 7.1 Prompt-as-Code

**What**: Treat prompts as versioned, testable artifacts with clear interfaces.
**When**: Production systems. Any prompt that matters should be version-controlled.
**How**: Store prompts in files with semantic versioning. Build evals. Run them in CI.
**Research**: DSPy philosophy; Anthropic's "define success criteria → build evals → iterate" workflow.

### 7.2 The Colleague Test

**What**: Show your prompt to a colleague with minimal context. If they're confused, the model will be too.
**Research**: Anthropic's official prompting best practices — their #1 golden rule.

### 7.3 Eval-Driven Optimization Loop

**What**: Define success metrics → write prompt → run evals → analyze failures → iterate.
**When**: Always for production prompts. Prompting is empirical — intuition is insufficient.
**Research**: OpenAI's prompting guide emphasizes "AI engineering is inherently an empirical discipline."

Loop:
1. Draft prompt
2. Run on 10-20 test cases
3. Score outputs (automated metrics + human review)
4. Identify failure patterns
5. Revise prompt to address failures
6. Repeat until target quality is met

### 7.4 Graduated Complexity

**What**: Start with the simplest possible prompt. Add complexity only when evals show it's needed.
**When**: Always. Over-engineering prompts is as harmful as under-engineering them.
**Research**: Common theme across Anthropic, OpenAI, and Google's prompting guides.

### 7.5 FATA (Focused Adaptive Task Assistance)

**What**: Provide minimal intent → model asks targeted clarifying questions → executes with full context.
**When**: Complex strategy tasks, requirements gathering, non-expert users.
**Research**: arXiv 2508.08308 (2025) — ~40% improvement over standard prompting.

### 7.6 CO-STAR Framework

**What**: Structure prompts with Context, Objective, Style, Tone, Audience, Response format.
**When**: Content generation tasks (articles, emails, reports).
**How**: Fill in each element explicitly. Useful as a checklist, not a rigid template.

### 7.7 Skeleton-of-Thought

**What**: Generate an outline first, then fill in each section in parallel.
**When**: Long-form generation where structure matters.
**Research**: Ning et al. (ICLR 2024).

---

## Quick Reference: Technique Selection by Task

| Task | Primary Technique | Supporting Techniques |
|------|-------------------|----------------------|
| Classification | Zero-shot or Few-shot | Role prompting, Output format |
| Code generation | Role + Instruction decomposition | Reflection, Examples |
| Long document QA | Grounding in quotes | Document positioning, XML structure |
| Math/Logic | CoT or native thinking | Self-consistency, Self-verification |
| Agent instructions | Conceptual engineering | Three pillars, Default-to-action |
| Skill/SKILL.md | Progressive disclosure | Trigger description, $ARGUMENTS |
| MCP tool description | Ultra-concise action-oriented | Parameter hints, Failure modes |
| Content generation | CO-STAR or Role + Format | Examples, Verbosity control |
| Data extraction | Few-shot with XML output | Format specification, Edge cases |
| Prompt optimization | Eval-driven loop | APE/OPRO, Colleague test |

---

## Key Research References

1. **The Prompt Report** — Schulhoff et al. (2024/2025). Taxonomy of 58 LLM prompting techniques. arXiv:2406.06608
2. **Chain-of-Thought Prompting** — Wei et al. (2022). arXiv:2201.11903
3. **Tree of Thoughts** — Yao et al. (2023). arXiv:2305.10601
4. **ReAct** — Yao et al. (2023). arXiv:2210.03629
5. **DSPy / MIPRO** — Khattab et al. (2024). EMNLP 2024. arXiv:2310.03714
6. **OPRO** — Yang et al. (2024). arXiv:2309.03409
7. **APE** — Zhou et al. (2023). ICLR 2023. arXiv:2211.01910
8. **TextGrad** — Yuksekgonul et al. (2024). arXiv:2406.07496
9. **EvoPrompt** — Guo et al. (2025). arXiv:2309.08532
10. **Self-Consistency** — Wang et al. (2023). arXiv:2203.11171
11. **Skeleton-of-Thought** — Ning et al. (ICLR 2024)
12. **Automatic Prompt Optimization Survey** — arXiv:2502.16923 (2025)
13. **Anthropic Prompting Best Practices** — platform.claude.com/docs
14. **OpenAI GPT-4.1/5/5.2 Prompting Guides** — cookbook.openai.com
15. **Anthropic Context Engineering** — anthropic.com/engineering/effective-context-engineering-for-ai-agents
16. **Systematic Survey of PE in LLMs** — Sahoo et al. (2024). arXiv:2402.07927
17. **Teach Better or Show Smarter** — NeurIPS 2024. Instruction vs Exemplar optimization.
