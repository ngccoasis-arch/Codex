# Small implementation roadmap

1. **Select target and speech engine.** Choose Android native or browser first. Check the target's installed voices, supported speed range, pause/resume behavior, and offline behavior; record any limits here.
2. **Build the thin vertical slice.** Add `src/` with a text composer, posted-text display, a speech adapter, and read/stop/replay controls. Keep speech-engine calls behind one interface so UI state does not depend on a particular engine.
3. **Add voice and speed controls.** Enumerate actual voices, handle missing/default voices, persist a user's voice ID and speed locally, and apply changes on the next play.
4. **Polish playback and accessibility.** Implement real pause/resume if supported, explicit idle/playing/paused/completed/error states, readable errors, and labelled controls.
5. **Verify on the target device.** Try short and long posts, blank input, rapid successive posts, stop/replay, mixed English/Chinese/Malay text, voice removal, unsupported speeds, and offline use where possible.

**Definition of first release:** a user can post text, choose an available voice and speed, hear the original text, and control playback without creating an account or sending the text to a server.

**Out of scope:** interpreting, summarizing, translating, rewriting, or responding to user text.
