# Text Reader / Read-Aloud Agent

A small app for posting text and hearing it read aloud in a chosen voice at a chosen speed.

## First user flow

1. Type or paste text into a composer and tap **Read aloud**.
2. The app shows the posted text and starts speech without changing its wording.
3. Pick an available voice and a speed; play, pause/resume, stop, or replay.
4. Post new text to read it next. For the first version, a new post stops the previous reading.

The first version should work without an account, language model, or backend. Use a speech engine available on the selected device/platform. Voice and language availability will depend on that engine.

## Proposed structure

```text
apps/text-reader/
  README.md
  docs/
    requirements.md       Product scope and acceptance criteria
    roadmap.md            Small milestones and open platform choice
  src/                   UI and speech adapter (after platform choice)
  tests/                 Focused speech-state and UI tests (after code exists)
```

The docs are committed now. `src/` and `tests/` are proposed paths, not empty tracked directories or a claim that the app exists.

## Decisions to retain

- Read the user's posted text as written; do not generate a response to it.
- Let the user select a voice from voices actually available on the device, with a sensible system default.
- Default speed to 1.0× and offer 0.75×, 1.0×, 1.25×, 1.5×, and 2.0× where supported.
- Keep text on the device for the initial version; do not send it to an external speech service by default.
- Keep the implementation platform open until the target (Android app or browser app) is chosen.

See [requirements](docs/requirements.md) and [roadmap](docs/roadmap.md).
