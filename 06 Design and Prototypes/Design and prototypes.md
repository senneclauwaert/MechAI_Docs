---
tags: [design, index]
updated: 2026-11-16
---
# Design and prototypes

Back to [Final Work Hub](../Final%20Work%20Hub.md)

This folder describes what has been made so far that you can click or look at. None of it is the real app yet: the data in these prototypes is example data.

| Note | What it is | State |
| --- | --- | --- |
| [HTML prototype (official)](HTML%20prototype%20%28official%29.md) | The clickable HTML prototype with the profile picker, repair chat, karts, stock and a 3D kart sketch | **The official design reference** |
| [Figma Prototype](Figma%20Prototype.md) | The Figma file: page "v0.7 prototype" has every screen of the official prototype (tablet, desktop, phone); page "Prototype" is the older design | v0.7 page current (16 Nov 2026); old page is history |
| [Diagrams](Diagrams.md) | The analysis diagrams (architecture, pipeline, data, flows, states, timeline) as Mermaid in this vault | Current |
| [3D exploded view](3D%20exploded%20view.md) | How the 3D kart sketch is built and how a real model could be made | Semester 2 |

## Design rules

- **The HTML prototype is the official design** ([ADR-34 The HTML prototype is the official design; diagrams as Mermaid in the vault](../10%20Decision%20Log/ADR-34%20The%20HTML%20prototype%20is%20the%20official%20design;%20diagrams%20as%20Mermaid%20in%20the%20vault.md)).
- **Colours (changed 6 November 2026 by Senne):** white cards on a cool light-grey background, a sidebar on a subtle gradient from near-black to deep blue that runs around the whole screen, the main window inset in it with rounded corners, and a light-blue accent (#1679C9 for text and buttons, #5AB4F5 for the selected item). Status colours stay green, amber and red. Light mode only. The earlier navy-on-white Figma palette is history.
- **Look and motion:** rounded cards with a thin border and a soft shadow, a filled pill for the selected item, cards that lift slightly on hover, dashed borders for "add" or "report" actions, and a breadcrumb above each page title.
- **Built for dirty hands:** big buttons, quick picks, voice input and photos instead of typing ([ADR-31 Hands-free design- voice input, quick picks, big buttons](../10%20Decision%20Log/ADR-31%20Hands-free%20design-%20voice%20input,%20quick%20picks,%20big%20buttons.md)).
- **No QR codes** anywhere.
- **Every kart works the same.** Kart 07 is only the example used in the demo.

## Updates planned for the prototype

The prototype was made before the decisions of 6 November 2026. To match them, it still needs:

- the operator role and its "report a problem" flow;
- the Diagnostics screen (Pitlane, Cruise, Boost, High boost, High brake, Stop) and Supercube's four kart statuses;
- the three safety levels, the microphone button and the handbook page images in the chat;
- the real handbook sections instead of invented page numbers;
- removal of the QR buttons and of the Gent venue.

These are listed in [To Do](../09%20To%20Do/To%20Do.md).
