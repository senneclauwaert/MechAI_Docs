---
tags: [analysis]
researched: 2026-10-16
updated: 2026-11-17
---
# Market & Competitor Analysis

Back to [Analysis](Analysis.md)

> [!NOTE]
> Researched on 16 October 2026. Prices are list prices found online and can change; sources are linked at the bottom. Four kinds of tools come close to what Supercube needs: karting software, maintenance software (CMMS), AI assistants for technicians, and general "chat with your documents" tools. None combines all of them.

## Competitors

| Tool | What it does | Price | Why not good enough for Supercube |
| --- | --- | --- | --- |
| **Apex Timing – kart maintenance module** | Karting software with fleet tracking: kart status, maintenance schedules and alerts, history, spare parts | Not published (quote) | Says *that* a kart needs a repair, not *how* to fix it; no repair guidance or AI; built around timing for rental tracks |
| **SODISCAN (SODIKART)** | Live monitoring of SODI electric karts: which are on track, charging, offline; battery level, temperature, alerts | Comes with SODI karts | Only for SODI karts; monitoring, no repair help, no stock or history |
| **BMI Leisure / timing systems** | Race control, timing, assigning karts to bookings | Quote | About customers and races; nothing on maintenance found |
| **MaintainX** (CMMS) | Work orders, assets, preventive maintenance, parts inventory. Its AI assistant searches an asset's manuals and links to the source pages | Free basic plan; \$20 and \$65 per user per month; the manual-search AI is **Enterprise only** | The useful AI part sits in the most expensive plan; generic, no kart-specific safety rules; data in a US SaaS |
| **Limble** (CMMS) | Work orders, assets, inventory, preventive maintenance | Free basic plan; paid plans by quote | No repair assistant over a private manual found; per-user cost; generic |
| **UpKeep** (CMMS) | Work orders, assets, inventory; four plans (Lite, Starter, Professional, Business Plus) | Paid per user (exact prices not confirmed) | Same as other CMMS: tracking, not answering repair questions from the manual |
| **MECH AI** | AI diagnostics for car repair: OEM wiring diagrams, service bulletins, trouble-code help | Free to \$249.99 per month | Built on car OEM data; knows nothing about Supercube's karts or its book |
| **Aquant** | Enterprise AI for service teams: learns from manuals, service logs and technician knowledge | Enterprise only, no public price, no free plan | Far too expensive and heavy for a small karting company; weeks of setup |
| **Custom RAG for a car OEM (Valcon case)** | RAG chatbot over technical manuals for 14,000 technicians in 3,000 garages, 3 languages | Consulting project | Proves the idea works at scale, but is a custom build for a large OEM |
| **NotebookLM (Google)** | Upload documents and chat with them; answers cite the exact passage | Free (50 sources per notebook); paid plans from \$4.99 per month | No kart, stock or history; no safety rules or refusal logic; company book on a consumer Google account; no control over the pipeline to show the jury |
| **ChatGPT / Copilot with a file upload** | General chat with an uploaded PDF | Free to paid plans | No guaranteed page citations, can invent numbers, no safety layer, no integration with the workshop |

## Comparison of features

| Feature | Karting software | CMMS (MaintainX etc.) | AI technician tools | NotebookLM / ChatGPT | **MechAi** |
| --- | --- | --- | --- | --- | --- |
| Repair answers from our own manual | No | Enterprise only | Yes (expensive) | Yes | **Yes** |
| Page citation and page image | No | Enterprise only | Varies | Citation, no image | **Yes** |
| HV safety rules, refusals, number check | No | No | Partly | No | **Yes** |
| Kart status and history | Yes | Yes | Partly | No | **Yes** |
| Photo issues linked to history and to-dos | No | Photos on work orders | No | No | **Yes** |
| Stock per location | Parts | Yes | No | No | **Yes** |
| Approved repair notes as knowledge | No | No | Yes | No | **Yes** |
| NL / FR / EN | Varies | Partly | Varies | Yes | **Yes** |
| Runs on Supercube's own server | No | No | No | No | **Yes** |
| Mark karts broken and run diagnostics in Supercube's system | No | No | No | No | **Yes** |
| Cost for Supercube | Quote | \$0–65 per user per month | High | Low | **Mistral API usage only (about €5 to €10 a month expected)** |

## Conclusion

- **The gap:** karting software and CMMS tools track *that* something needs fixing; AI tools answer *how* to fix it. Small companies like Supercube can't afford a tool that does both, and no tool knows Supercube's own book, karts and safety procedure.
- **Our position:** a small, focused platform that combines the repair assistant with the fleet, photo issues, stock and task basics, built around safety (fixed safety texts, refusals, number checks, senior approval). It runs on Supercube's own server and talks to Supercube's own kart system.
- **What we learn from the market:** MaintainX and NotebookLM show that citing the source page is now expected; Aquant shows that capturing technician knowledge (our repair notes) is valuable; the Valcon case shows RAG over manuals works for technicians in several languages.
- **Honest limit:** for a large fleet a commercial CMMS would be the safer long-term choice; our platform could integrate with one later instead of replacing it.

## Sources

- [Apex Timing – kart maintenance](https://apex-timing.com/en/rental-karting-software-solution-c24.html)
- [SODISCAN for SODI electric karts](https://www.sodikart.com/en-gb/news/informations/sodiscan-software-for-sodi-electric-karts-69.html)
- [BMI Leisure – timing software for karting](https://www.bmileisure.com/en/features/timing-software-for-karting)
- [MaintainX vs Limble pricing (Reliamag)](https://reliamag.com/cmms/maintainx-vs-limble/)
- [MaintainX – search asset manuals with AI](https://help.getmaintainx.com/search-asset-manuals-with-maintainx-copilot)
- [UpKeep pricing guide (Fabrico)](https://www.fabrico.io/blog/upkeep-pricing-guide-2026-costs-plan-limits-hidden-fees/)
- [MECH AI on Capterra](https://www.capterra.com/p/10044904/MECH-AI/)
- [Aquant pricing (Costbench)](https://costbench.com/software/field-service-management/aquant/)
- [Valcon – RAG chatbot for 14,000 technicians](https://valcon.com/case-studies/driving-accuracy-and-speed-with-an-enterprise-rag-chatbot-for-14000-technicians/)
- [NotebookLM free vs paid (FreeAcademy)](https://www.freeacademy.ai/blog/notebooklm-free-vs-plus-2026)
