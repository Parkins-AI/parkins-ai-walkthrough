# Walkthrough roadmap

**Scope.** `walkthrough.parkins.ai` and `beta.walkthrough.parkins.ai`: the trip scrapbook
viewer (Workers `walkthrough`, `walkthrough-beta`; R2 `parkins-ai-walkthroughs`). Platform
epic: `parkins-ai-standards/ROADMAP.md`.

## Exceptions

Departures from the platform standards (`parkins-ai-standards/standards/architecture.md`),
each justified as S-ARCH-18 requires.

| Standard | Exception | Why | Ends when | Recorded |
|---|---|---|---|---|
| S-ARCH-12 (beta storage isolated) | `walkthrough-beta` binds the production bucket `parkins-ai-walkthroughs` as `WALKTHROUGHS` | The Worker only reads it (`get`, `head`, `list` in `src/index.js`; no `put` or `delete`). Walkthroughs are written from the Mac by `bin/walkthrough.py`, never through a Worker, so beta cannot change production data, and a beta copy would duplicate ~1.3 GB+ of trip photos for no isolation gain. | The Worker gains any write path (upload, edit, delete), or beta needs content production must not see: then beta gets `parkins-ai-walkthroughs-beta` with a sample walkthrough. | 14 Nov 2026, Eli (Graham's platform phase 2 brief: "record an exception if beta is read-only") |
