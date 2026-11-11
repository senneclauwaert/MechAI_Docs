---
tags: [design, 3d]
updated: 2026-11-06
---
# 3D exploded view

Back to [Design and prototypes](Design%20and%20prototypes.md) · Feature: [3D exploded view of the kart](../05%20Features/3D%20exploded%20view%20of%20the%20kart.md)

This note describes how the 3D kart sketch in the HTML prototype is built and how a real model could be made. The 3D view is a **semester 2** feature. The December prototype uses the handbook's own exploded drawings, shown as page images in the chat.

## What the prototype model shows

The model is hand-built in three.js. All positions and sizes are estimates from photos and descriptions, not measurements.

**Modelled from Senne's photos (version 4):** wrap-around bumpers, a tube frame with battery trays, the nose with the "SUPERCUBE 07" print, a roll bar with a headset hook, the seat, batteries, the motor controller, the network switch, the motor with chain drive, the rear brake disc and the pedals.

**Drivetrain from Senne's description of the real kart (version 5):**

- **Rear axle, from the left:** the tyre and hub, a bearing with a lock collar, the brake disc with its hydraulic caliper and pads, a second bearing with a lock collar, then the differential. The right axle is longer and has the same parts mirrored.
- **Drive:** the motor sits above the axle behind the seat and drives the differential by chain. Behind it on the right are the motor controller and the seatbelt controller.
- **Batteries:** two on each side of the seat.
- **Electronics:** the converter and the network switch sit left of the seat, with network cables to every controller.
- **Front:** the steering wheel with the main controller (a PC) in its hub, and the steering rack. An audio cable runs from the wheel to the headset on top of the seat.
- Tapping a part group zooms in and explodes it. On kart 07 the bearing is highlighted.

## How a real model could be made (checked 24 October 2026)

- **AI image-to-3D tools** (for example Meshy or TRELLIS) produce one fused, inaccurate mesh. That is not good enough for tappable parts.
- **Hunyuan3D's** licence excludes the EU, so it cannot be used in Belgium.
- **glif.app** has no 3D output.

**Plan:** first ask Supercube for CAD files of the kart ([Questions for Supercube](../01%20Project/Questions%20for%20Supercube.md)). Otherwise, model the tappable parts in Blender (free) as separate named objects and export one GLB file. Each part is named after its part number, so tapping it can open the stock and the handbook page.
