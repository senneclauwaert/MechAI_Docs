---
tags: [rag, safety]
updated: 2026-11-06
---
# Safety rules

Back to [RAG and AI](RAG%20and%20AI.md) · Decision: [ADR-30 Safety levels enforced in code](../10%20Decision%20Log/ADR-30%20Safety%20levels%20enforced%20in%20code.md)

The karts run on high-voltage batteries and have a motor controller. A wrong answer can hurt someone, so these rules are not optional. They are enforced in code, not left to the AI.

> [!IMPORTANT]
> **The AI never writes a safety plan.** A language model writes text that *sounds* right; for high-voltage work that is not good enough. For emergencies and high-voltage work, MechAi shows Supercube's own fixed texts and the original handbook pages.

## Three safety levels

| Level | When | What the app does |
| --- | --- | --- |
| **Emergency** | Smoke, fire, a burning smell, a hot or swollen battery, someone hurt | No AI call. A red STOP card with Supercube's emergency text (for example "STOP. Step away. Call the senior mechanic or supervisor."). Logged as a safety event |
| **High voltage** | Battery, charger, motor controller, battery management system (BMS), high-voltage wiring | Supercube's fixed safety text and the **original handbook pages as images**. The AI may point to the right page, but writes no steps. One logged confirmation ("I have isolated the battery"), recording who and when |
| **Normal** | Ordinary repairs, for example the rear axle bearing | Cited steps from the handbook, with the page images shown. Every number must appear on the cited page; if one doesn't, no steps are shown, only the pages |

**Refused at every level:** requests to bypass an interlock, the BMS or other protection, or to open a battery pack outside the documented procedure. The answer is a refusal with "call a senior mechanic", and the request is logged.

## How the level is decided (fail safe)

1. **Code first:** word lists in Dutch, French and English, matched with tolerance for typos, decide emergency and high voltage before any AI call.
2. **The AI's flag second:** the translation call also returns its own safety guess.
3. **The stricter level wins.** If the code and the AI disagree, or the AI call fails, the app uses the stricter level.

## Other rules enforced in code

- **Never invent numbers.** Every torque value, voltage, wire colour or part number must appear on a cited page. Values are normalised first ("25 Nm" equals "25,0 N·m").
- **No AI-written wiring facts.** For electrical questions the app shows the wiring-diagram page as an image; the AI never states a wire colour or pin number on its own.
- **"Not in the handbook"** when the best similarity score is below the threshold (not the RRF rank score), with the closest pages shown.
- **Always show the original page**, so the mechanic can check.
- **Sources are data, not instructions** (protection against prompt injection: text in a source that tries to give the model new orders). Repair notes count only after a senior approves them and are never used for safety steps.
- **Qualifications:** where a task needs an electrical qualification (in Belgium often BA4 or BA5), the fixed text says so. Supercube decides which task needs which qualification.
- **Unsafe issues:** an issue reported as "kart unsafe" marks the kart broken and alerts the senior mechanics.
- **Every safety question is logged** for review.

## Honest wording

We write "the app only *shows* answers backed by the handbook", not "the model only answers from the handbook". The checks reduce the risk; they do not replace training, isolation procedures or supervision.

## What Supercube provides

- The emergency text and the high-voltage text, written or approved by Supercube.
- Which tasks need which qualification.
- A senior mechanic who reviews the safety questions in the test set and the app's answers before the Showdown.

These are listed in [Questions for Supercube](../01%20Project/Questions%20for%20Supercube.md).

## Testing

The test set holds at least 5 safety questions and 5 emergency phrasings in each language. The target is that **every** one lands on the right level and that no AI-written steps ever appear for emergency or high-voltage questions ([Evaluation](Evaluation.md)).

## Checks added after the 6 November feedback

- **An always-visible STOP button** in the app opens the emergency card directly, so an emergency never depends on the words being recognised. Spoken emergency phrases are part of the test set, because speech-to-text can mishear them.
- **Measure the high-voltage share first.** Before the high-voltage word list is frozen, we measure what share of real test questions lands on that level. If it is large, the list is narrowed (for example, "battery" only together with work words), so the assistant stays useful.
