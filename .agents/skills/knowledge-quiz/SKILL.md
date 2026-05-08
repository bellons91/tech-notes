---
name: knowledge-quiz
description: Builds a short quiz (3–5 single-choice plus 1–2 open questions) on a user-named topic, then grades answers with clear right/wrong feedback and corrections. Use when the user asks to be quizzed, to test or check their knowledge, for practice questions, or for a knowledge check on a subject.
---

# Knowledge quiz

## When this applies

The user wants to **test their understanding** of a **specific topic** (for example: “quiz me on X”, “test my knowledge of Y”, “check what I remember about Z”).

If the topic is vague, ask **one short** clarifying question (scope, difficulty, or which sub-area) before writing the quiz.

## Before writing questions

1. **Infer the knowledge base**: If the quiz should align with **this repository’s notes**, read the relevant files under `source/content/` first. If the user names an external syllabus, book, or course, follow that scope without inventing requirements they did not give.
2. **Calibrate difficulty** to what they asked for (default: mixed recall + short reasoning). Avoid trick questions; distractors should be plausible but clearly wrong to someone who understands the material.

## Quiz format (required counts)

Deliver **one quiz block** the user can answer in a follow-up message.

### Part A — Single choice (required: **3 to 5** questions)

- Each item is **one** correct answer among **exactly four** labeled options: **A, B, C, D**.
- State the **question stem** once, then list options on separate lines.
- Ensure **exactly one** option is correct; keep wording unambiguous.

### Part B — Open ended (required: **1 or 2** questions)

- Ask for **short written answers** (a few sentences or a small bullet list unless they asked for depth).
- Make the expected **object of explanation** explicit (define, compare, outline steps, justify a choice, etc.).

### Answer sheet placeholder

End the quiz with a line telling the user how to reply, for example: “Reply with your choices (e.g. `1B, 2C, …`) and your answers to the open questions.”

## After the user submits answers

1. **Multiple choice**: For each item, state **correct option**, whether the user was **right or wrong**, and if wrong give a **brief correction** (why the right answer holds and why the chosen distractor does not, without condescension).
2. **Open questions**: Judge **accuracy and completeness** against the topic. Quote or paraphrase the user’s answer only as needed. If something is wrong or incomplete, **explain the gap** and supply the **correct idea** or missing steps. If correct, say so briefly.
3. **Summary**: One short paragraph on overall strength and the **1–3** highest-leverage topics to revisit.

## Style constraints

- Keep the initial quiz **readable**: numbered questions, consistent labels.
- Do **not** reveal the answer key until the **grading** phase (after they answer).
- If you are unsure of a fact, say so and base grading on **standard references** or caveated reasoning rather than bluffing.

## Examples

**Single choice (shape only):**

```markdown
1. [Stem ending with a clear question?]
   - A) …
   - B) …
   - C) …
   - D) …
```

**Open question (shape only):**

```markdown
6. In your own words, explain [concept]. Mention [required elements].
```

**Grading snippet (shape only):**

```markdown
**Question 3:** Correct: C. Your answer A — incorrect. [One to three sentences of correction.]
```
