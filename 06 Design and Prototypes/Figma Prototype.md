---
tags: [design, figma]
updated: 2026-11-16
---
# Figma Prototype

Back to [Design and prototypes](Design%20and%20prototypes.md)

**Link:** [Figma "Prototype"](https://www.figma.com/design/hWB597CW9ZjhYQPv3eu5DG), in Senne's Figma team "Final work".

The file has two pages:

- **"v0.7 prototype (6 Nov 2026)"** ([open the page](https://www.figma.com/design/hWB597CW9ZjhYQPv3eu5DG?node-id=72-793)), added on 16 November 2026. It holds every screen of the [HTML prototype (official)](HTML%20prototype%20%28official%29.md) version 0.7 in its current look. This page matches the official design.
- **"Prototype"**, the original page from 6 October 2026. It uses the first palette (white, navy #0B45B8) and is kept as design history.

## Page "v0.7 prototype (6 Nov 2026)"

The 68 screens were rebuilt from the HTML prototype as editable layers: text in Poppins (and IBM Plex Mono for part numbers), vector icons, cards with their borders and shadows. They are grouped in sections:

| Section | Screens |
| --- | --- |
| Sign in | Who is working?, enter PIN, wrong PIN, logged out after 30 minutes idle |
| Home per role | Mechanic, senior mechanic, operator and admin home |
| Repair assistant | Pick the kart, pick the problem, thinking, safety checks lock the plan, plan unlocked, cited answers, high-voltage level (fixed text and confirmed), emergency STOP card, not in the handbook, voice input |
| Karts | All karts, needs attention, kart detail (mechanic and operator), 3D view |
| Diagnostics | Check nobody is at the kart, speed modes with STOP, blocked by someone else's open repair |
| Stock | All parts, low stock, part detail, take a part (pick the part, pick the kart) |
| To-dos and alerts | Open and done to-dos, notifications |
| Sources | Handbook page, exploded view drawing, approved repair note, high-voltage handbook page |
| Repair notes | Log repair, senior review, approve with PIN, wrong PIN, mechanic cannot approve |
| Report a problem | Operator report: empty, listening, filled (set to Broken), small issue (stays in the game) |
| Desktop | Senior home, repair assistant, karts (1440 × 900) |
| Phone | 15 phone screens (390 × 844), including the bottom tab bar, the two drawers and pop-ups as bottom sheets |
| User workflow | The workflow board from the prototype |

Tablet screens are 1180 × 800. The 3D view shows a still image of the 3D kart, because Figma cannot show interactive 3D. The kart photo on the kart cards is an image. All names, numbers and handbook pages are example data, as in the prototype.

When the HTML prototype changes, these screens must be updated too.

## Page "Prototype" (design history)

- A user-workflow board: eight steps, each naming its screen.
- Twelve tablet screens (six of them pop-up states): the assistant, the cited repair plan, Karts, Stock, To-dos and Notifications, the handbook page source, log repair, kart history, taking a part and senior review.
- Four phone screens with a bottom tab bar.
- Components (button, chip, navigation rail, bottom navigation) and a "Supercube colors" variable collection.
- A clickable flow: press Present and pick "Mechanic flow (tablet)".
- A row "Login and role screens" (16 October): profile picker, PIN keypad, and the mechanic, senior and admin home screens.

## Known gaps

- The old "Prototype" page still shows QR buttons and a note about an outside login; both were dropped. Use the v0.7 page instead.
- The v0.7 screens are static: they have no clickable Present-mode flow yet. The clickable version is the HTML prototype.
- Figma cannot do interactive 3D, so the turning and zooming 3D view exists only in the HTML prototype.
- Senne has a View seat on the Figma team and needs an Editor seat to edit.
