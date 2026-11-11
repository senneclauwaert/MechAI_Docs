---
tags: [parked, rag, video]
created: 2026-10-10
updated: 2026-11-06
status: parked
---
# Repair videos

Back to [Parked and future ideas](Parked%20and%20future%20ideas.md) · Decision: [ADR-11 Repair videos parked](../10%20Decision%20Log/ADR-11%20Repair%20videos%20parked.md)

> [!NOTE]
> Parked on 10 October 2026 to keep the scope small, and confirmed on 6 November 2026: maybe a few videos later if there is time, not now. The research below stays valid.

**The question:** can we film short repair videos (for example changing a rear axle bearing), let the AI write the steps, store the videos and have the assistant find the right one?

**Short answer:** yes, it is realistic. The AI writes a *draft*, and a senior mechanic approves it, exactly like [Repair notes as knowledge](../04%20RAG%20and%20AI/Repair%20notes%20as%20knowledge.md). The assistant never searches the video itself: it searches the approved text steps, and each step remembers where it is in the video.

## Turning a video into steps

1. **Sound to text.** The mechanic talks while filming ("now I loosen the four bolts"). Speech-to-text turns it into text with timestamps.
2. **Video to pictures.** `ffmpeg` saves one frame every few seconds at 1280×720.
3. **Pictures and transcript to steps.** The worker sends the frames and the timestamped transcript to a vision-capable model and asks for numbered steps in JSON, each with a start time, tools, parts and warnings.
4. **Review.** The draft goes to the senior mechanic's review screen. Only approved steps become searchable.

**Why narration matters:** from pictures alone a model guesses. It cannot reliably read a torque value or see whether the high-voltage system is really switched off. Talking while filming gives it the facts.

## Cost (rough estimate)

A two-minute video gives about 40 frames and a short transcript, roughly 50,000 tokens for a small vision model: a few cents at most per video. Thirty videos stay well under a few euros. Prices must be re-checked when the feature is built.

## Storing and finding the videos

- One file per video on the `files` volume, behind the `storage` module. The worker first re-encodes phone video to 720p H.264 (roughly 10 to 20 MB per minute; estimate). Thirty two-minute videos take about 1 GB.
- Every approved step is a chunk in pgvector like any other source, with the extra fields `video_id` and `start_seconds`. An answer can then cite "Video: rear axle bearing, step 3 (0:42)", and the app plays the video from that second (an HTML5 video with `#t=42`).

## How it fits the architecture

Everything runs in the existing worker: upload, re-encode, speech-to-text, frames, model, draft and review. No new services are needed.

| Piece | Difficulty |
| --- | --- |
| Upload and storage | Easy |
| Frames and transcript | Easy to medium |
| Draft steps as JSON | Medium (prompt work) |
| Review screen and search with timestamps | Medium; reuses the repair-note flow |

**Advice:** build the repair-note flow first, then one test video end to end.

## Open points

- Supercube's permission to film and store videos, and whether faces may appear.
