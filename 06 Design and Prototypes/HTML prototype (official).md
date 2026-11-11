---
tags: [design, prototype]
updated: 2026-11-06
---
# HTML prototype (official)

Back to [Design and prototypes](Design%20and%20prototypes.md) · Decision: [ADR-34 The HTML prototype is the official design; diagrams as Mermaid in the vault](../10%20Decision%20Log/ADR-34%20The%20HTML%20prototype%20is%20the%20official%20design;%20diagrams%20as%20Mermaid%20in%20the%20vault.md)

**Link:** [Clickable HTML prototype](https://claude.ai/artifact/JoYu88yrzKTxP49N18dp3D). A downloadable copy is kept in the project files as `prototype/supercube-prototype.html`.

This is the official design reference for MechAi (Senne, 6 November 2026). It went through six versions between 6 October and 6 November 2026. The prototype is always light. Since version 6 it uses a light-blue accent; the sidebar colour (a subtle near-black to blue gradient) frames the whole screen and the main window sits inside it with rounded corners, chosen by Senne from a dashboard concept he liked (see [Design and prototypes](Design%20and%20prototypes.md)).

## What you can click through

- **"Who is working?"** profile picker, then a PIN keypad (demo PIN 1234; 5 wrong tries lock the profile). All four roles have their own home screen: operator (Lotte), mechanic, senior mechanic and admin. The 30-minute idle logout works, and "Switch user" signs out.
- **Operator flow:** "Report a problem" with big buttons: pick the kart, pick or say the problem, optional photo. "Take the kart out of the game" is on by default, so sending sets the kart to Broken; for a small issue the operator can switch it off. The mechanics always get an alert.
- **Repair chat** for kart 07 with a broken rear axle bearing: safety level shown first, safety checks, numbered steps with chips for the real handbook sections (4.5.16 page 17, 5.3 pages 38-42, 5.6.2 page 48), and the source page. The page view is a placeholder in the prototype so the handbook stays private; the app shows the real page image.
- **Safety levels:** a battery or charger question shows the high-voltage card (fixed text, handbook pages, a logged confirmation). A question about smoke or fire shows the emergency STOP card, and a red STOP button in the chat header opens it at any time. Neither uses an AI answer.
- **Voice input:** the microphone button in the chat and in the operator report fills in a spoken question (simulated in the prototype).
- **Karts:** tall kart cards with a photo of a real Supercube kart, the four Supercube statuses (Good, Diagnostic, Broken, Permanently broken) and history. In the kart window the status can be changed, which is sent to Supercube.
- **Diagnostics:** Pitlane, Cruise, Boost, High boost and High brake, with a big Stop. Open to everyone, no PIN, every command logged. A "nobody at the kart" check comes first, the kart stops by itself after 60 seconds without a command, and kart 05 is blocked because Tom has an open repair on it. Uses the test client.
- **Stock:** search, a low-stock filter and "Take part" (pick the part from a list; no QR codes).
- **To-dos and notifications**, and the senior's review of a repair note (approved by typing the PIN again).
- **3D view:** a simplified three.js kart that can be turned and zoomed; tapping a part group explodes it, with the bearing highlighted on kart 07. See [3D exploded view](3D%20exploded%20view.md).
- A frame switch for desktop, tablet and phone.

## Version history

| Version | Date | What changed |
| --- | --- | --- |
| 1 | 6 Oct 2026 | First version: icon rail, repair chat, karts, stock, to-dos, user workflow. Navy on white |
| 2 | 16 Oct 2026 | Demo case changed to the broken rear axle bearing on kart 07; content follows supercube.com (AR karting, identical single-seat karts, the gaming floor, headsets) |
| 3 | 16 Oct 2026 | Light only, to match Figma exactly; first 3D view |
| 4 | 16 Oct 2026 | 3D kart modelled from Senne's photos |
| 5 | 16 Oct 2026 | Login and role screens; 3D drivetrain rebuilt from Senne's description |
| 6 | 6 Nov 2026 | Updated to the 6 November decisions: operator role and report flow, Diagnostics, the four Supercube statuses, the three safety levels, microphone button, real handbook sections, QR codes and the Gent venue removed. New look: dark navy sidebar with grouped navigation, light-blue selected pill, breadcrumb, rounded bordered cards that lift on hover. Screens and functions otherwise unchanged. Later the same evening: gradient frame around the whole screen with a rounded main window, and "Diagnostic" removed from the status buttons (the Diagnostics button sets it) |
| 7 | 6 Nov 2026 (evening) | After the AI-assisted review: "nobody at the kart" check, automatic stop and repair block for diagnostics; "Take the kart out of the game" toggle in the operator report; always-visible STOP button in the chat |

## Still open

- The page view shows a placeholder, not the real handbook page, because the prototype can be shared and the handbook is private.
- Voice input and the Supercube connection are simulated. The real versions are built in the app (see [Voice input and hands-free use](../05%20Features/Voice%20input%20and%20hands-free%20use.md) and [Supercube kart status and diagnostics](../05%20Features/Supercube%20kart%20status%20and%20diagnostics.md)).

> [!NOTE]
> A separate full UI design made on 28 October 2026 was rejected by Senne and deleted on 6 November 2026.
