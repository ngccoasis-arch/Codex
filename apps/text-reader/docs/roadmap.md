# Small implementation roadmap

1. **Check ChatGPT Voice with Juniper.** In ChatGPT Settings → Voice → Voice, select Juniper. Try a Voice conversation and see whether its spoken responses satisfy the user's read-aloud need. The message-level **Read aloud** action has no documented Juniper selector. If the user needs exact Juniper narration of arbitrary posted text, pause implementation until a supported path exists; Android system TTS and the public Speech API do not provide that voice.
2. **Check the existing Android action as an alternative.** In POCO/HyperOS Text-to-speech output settings, choose an engine/voice and speed, play the sample, then try selected-text **Read aloud**. Record whether it follows the selection and what capability is still missing. If it fully meets the need, stop here.
3. **Build the thin vertical slice if an alternative voice is acceptable.** Add an Android `app/` module with a text composer, posted-text display, an Android `TextToSpeech` adapter, and read/stop/replay controls. Keep speech calls behind one interface so the UI is easy to change.
4. **Add voice and speed controls.** Enumerate actual voices, handle missing/default voices, persist a user's voice ID and speed locally, and apply changes on the next play.
5. **Polish playback and accessibility.** Add explicit idle/playing/completed/error states, readable errors, and labelled controls. Consider a pause feature later only if it can resume at the correct position.
6. **Verify on the target device.** Try short and long posts, blank input, rapid successive posts, stop/replay, mixed English/Chinese/Malay text, voice removal, unsupported speeds, and offline use where possible.

**Definition of first release:** a user can post text, choose an available voice and speed, hear the original text, and control playback without creating an account or sending the text to a server.

**Out of scope:** interpreting, summarizing, translating, rewriting, or responding to user text.
