---
tags: [project, pitch]
created: 2026-10-05
author: Senne Clauwaert
updated: 2026-11-06
---
# Pitch & WHY

Back to [Final Work Hub](../Final%20Work%20Hub.md)

## Start with WHY

**Mechanics should spend their time fixing karts, not hunting for answers.**

**Our belief.** A mechanic's work should not depend on who is on shift, which binder holds the right page, or whether a part happens to be on the shelf.

**What goes wrong today.** These are working hypotheses from Senne's daily work as a mechanic at Supercube. We confirm each one with two or three colleagues before the pitch.

| Pain point (hypothesis) | Question to ask colleagues |
| --- | --- |
| Answers live in the handbook and in experienced colleagues' heads | Where do you look first when a kart has a fault you don't know? |
| A kart's repair history is not at hand when you open it | How do you find out what was already fixed on this kart? |
| Missing parts show up only after the diagnosis | How often do you start a repair and then find the part is out of stock? |
| Follow-ups and reminders get lost between shifts | How do you keep track of what still needs doing? |
| Small visible damage is noticed but not reported | When you or an operator see a cracked bumper or loose cable, how do you make sure someone fixes it? |
| Typing on a tablet with dirty hands is not realistic | Would you use a tool you have to type into during a repair? |

**Why now.** Language models combined with search (RAG) can answer from a company's own handbook and point to the exact page. Electric karts carry high-voltage batteries, so answers must be traceable and safety rules must be strict. That is why citations and fixed safety rules are core features, not extras.

**Why us.** Senne works as a mechanic at Supercube. We have a real user, a real problem and access to the real handbook and Supercube's kart system.

**The WHY in one breath**

> We believe mechanics should spend their time fixing karts, not searching for answers. So we bring each kart's status and history, the parts in stock and the manufacturer's handbook together in one assistant that answers by voice, with the page to prove it.

## The solution

One app where a mechanic selects a kart and gets its status and history, the parts in stock and cited repair steps from the handbook, in the same place. The repair assistant is the core; everything else either makes its answers better or acts on them.

| Feature | What it does | When |
| --- | --- | --- |
| Repair assistant (RAG) | Answers from the handbook by voice or text, with the page and page image, and fixed safety rules | Prototype (December) |
| Kart status and history | Status shared with Supercube's system, repairs, issues and alerts per kart | Prototype |
| Operator issue log | The operator reports a problem on a kart and marks it broken | Prototype |
| Parts stock | Parts and stock per shelf; taking a part lowers the stock | Prototype |
| Voice input | Speak the question instead of typing | Prototype |
| Photo issues | Report visible damage with the camera | Prototype if time allows, otherwise semester 2 |
| Supercube connection | Live status and alerts; mark broken or repaired; run diagnostics | Fake data in the prototype, real connection in semester 2 |
| Repair notes as knowledge | Approved notes from colleagues become a source | Semester 2 |
| To-dos and notifications | Open jobs, low stock, unsafe karts | Semester 2 |
| 3D exploded view | Shows where a part sits on the kart | Semester 2 |

Success is measured mainly on the repair assistant: a test set of real mechanic questions with the expected pages, scored on search quality and answer quality. See [Evaluation](../04%20RAG%20and%20AI/Evaluation.md).

## Pitch for Supercube

A short pitch for management, ready to adapt for an email or a two-minute talk.

```text
Subject: MechAi, a repair assistant for Supercube's mechanics

Hi [name],

As you know, I work as a mechanic at Supercube, and together with Nehad I am building my final-year project at Erasmushogeschool Brussel around our workshop. Finding the right information for a fault takes time, and what one mechanic knows is not always available to the next.

MechAi is a workshop assistant. You choose a kart and ask your question out loud. It answers with the steps from the Storm handbook and shows the page, so every answer can be checked. It also shows the kart's history, its status in our own system and whether the parts are in stock, and it logs the repair afterwards. The operators can report a problem on a kart directly from the floor.

What Supercube gets: a working prototype on our own servers, a test report that shows how accurate the answers are, and in the second semester repair notes, to-dos and a full connection with the kart system.

What we need from Supercube:
- Written permission to use the handbook in the app and to send its text to the AI service (OpenAI): the full text once for the search index, then the matching sections per question
- Access to the GraphQL API (a test environment if possible) and a server to run MechAi on
- The fixed safety texts for high-voltage work and emergencies
- About 30 minutes each with two or three colleagues, for interviews and later to test the prototype

Your documents stay yours. They are used only for MechAi and deleted on request. To search and answer, the handbook text is sent to the OpenAI API: the full text once per version to build the search index, and the matching sections for each question. OpenAI does not use API data to train its models. The assistant can be wrong, so every answer shows its source and the mechanic always makes the final call.

Can we meet for 20 minutes to go through it?

Kind regards,
Senne Clauwaert
```

The complete list of questions for Supercube is in [Questions for Supercube](Questions%20for%20Supercube.md).

## Next steps for the pitch

- [ ] Interview two or three mechanics and add one real example per pain point
- [ ] Send the pitch and the questions to Supercube
