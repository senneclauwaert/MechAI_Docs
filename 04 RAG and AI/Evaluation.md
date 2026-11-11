---
tags: [rag, evaluation, kpi]
updated: 2026-11-06
---
# Evaluation

Back to [RAG and AI](RAG%20and%20AI.md)

Without numbers we cannot tell whether a change helped, and the jury wants before-and-after results. That is why the test set and the evaluation script are built in sprint 1, before any tuning.

## The test set

A CSV file in git (`eval/questions.csv`) with: id, language, question, expected page(s), points the answer must mention, type and expected safety level.

- **30 to 50 real questions**, written the way mechanics talk. The first 15 are a sprint 1 task, written from the real handbook.
- **Groups:** normal repairs; questions the handbook cannot answer (at least 5); safety and emergency questions (at least 5); part numbers, values and failure codes (at least 5); Dutch (at least 5) and French (at least 5); spoken questions (recorded once and replayed); prompt-injection text inside a repair note (semester 2).
- **10 held-back questions** that we never tune on, to show the improvements are real.
- A small glossary of kart terms in Dutch, French and English helps write good questions.
- A senior mechanic checks the expected answers.
- The best start: ask three mechanics for the last five problems they looked up, and which page answered each one.

## Metrics

- **recall@k:** the share of questions where a correct page is in the top k results.
- **MRR** (mean reciprocal rank): 1 if the right page is first, 1/2 if second, 1/3 if third, averaged.
- **Citation accuracy:** do the cited pages really contain the claim?
- **Invented numbers:** numbers in the answer that are not on the cited page.
- **Correct refusals:** "not in the handbook" on the unanswerable questions.
- **Safety level accuracy:** each safety question on the right level.
- **Faithfulness:** is every claim supported by the sources? (checked by hand on a sample, optionally with Ragas and a judge model).
- **Speed:** time until the answer appears.

## KPIs (proposed, to confirm by the team)

| KPI | Target |
| --- | --- |
| Right page in the top 10 (recall@10) | at least 80% |
| Invented numbers in the test set | 0 |
| Correct refusals on unanswerable questions | at least 4 of 5 |
| Safety questions on the right level | 100% |
| Time to answer on the workshop Wi-Fi | about 10 seconds or less |
| Time to find a procedure, compared with the paper handbook | clearly faster (baseline measured in a real repair) |
| Mechanics who tested the prototype | at least 3 |

These KPIs are also in [Planning & Deadlines](../01%20Project/Planning%20&%20Deadlines.md).

## Tools and method

- Retrieval metrics come from our own short script (`eval/run_eval.py`). It needs no answer model, and question embeddings are cached, so a run costs almost nothing and takes seconds.
- Every run is saved as `eval/results/<date>_<commit>.csv`, tied to a git commit.
- In CI, the evaluation runs against a **small fake manual** written by the team, because the real handbook is never in git. Question embeddings are cached in the repository and the translation step uses fixed search terms, so CI makes no AI calls. The **real evaluation** runs on the server or a laptop against the real index. A new handbook version only becomes current when it passes its own baseline, because page numbers change between versions. CI fails if recall@10 on the fake manual drops below its saved baseline.
- **One change at a time:** each step of the [Optimization playbook](Optimization%20playbook.md) gets its own before-and-after row.

## Feedback loop

Every answer has a thumbs up and down with a quick reason (wrong kart, wrong page, wrong step, unsafe, missing step, other), linked to a trace. Every week the team looks at the thumbs-down answers, finds the cause (missing document, chunking, search or answer), adds the question to the test set, fixes it and runs the evaluation again.

## When is a reranker worth it?

If recall@20 is high but recall@3 is low, the right page is found but ranked too low, and reranking helps. If recall@20 itself is low, fix the chunking, the search terms or the missing document instead ([Embeddings and reranker](Embeddings%20and%20reranker.md)).
