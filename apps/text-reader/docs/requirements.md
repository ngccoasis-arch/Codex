# Core requirements and interaction decisions

## Scope

**Voice constraint discovered:** The user wants ChatGPT's Juniper voice. ChatGPT Voice lists Juniper, but Android's installed TTS voices and the public Speech API do not expose it as a selectable voice for a separate app. The Android prototype described below would therefore use an alternative voice, subject to the user's choice. Do not present it as a Juniper implementation. ChatGPT's Android **Read aloud** action is documented, but a Juniper selector for that action is not documented.

The app speaks text that the user posts in its own composer. It displays that original text while reading. It is a read-aloud tool, with no analysis, summary, translation, correction, chatbot response, or content generation.

### Must have for the first usable version

| Area | Behavior | Acceptance check |
| --- | --- | --- |
| Input | Accept pasted or typed Unicode text, including English, Chinese, Malay, punctuation, and line breaks. | Posting nonempty text displays the same text and starts speech; blank/whitespace-only input does not start speech. |
| Playback | Read the submitted text with Android's installed speech engine. | Read/replay and stop work; finished/error/cancelled states are visible. |
| Voice | List voices exposed by the installed speech engine with readable name and language; default to the system voice. | A selected available voice is used for the next reading; if it disappears, revert to the system default and inform the user. |
| Speed | Start at 1.0×; offer 0.75×, 1.0×, 1.25×, 1.5×, 2.0× within the engine's supported range. | A selected speed affects the next reading; unsupported values are disabled or clamped visibly. |
| New post | Keep only one active reading. | Posting new text cancels the current utterance before reading the new one. |
| Privacy | Keep text and settings locally in the first version. | No account, analytics payload, or app-managed text upload is needed; choose an offline voice if reading must stay on the device, since some installed voices use network synthesis. |
| Accessibility | Label the input, voice, speed, and playback controls; show status in text. | Controls work with keyboard/touch and an assistive reader; playing state is distinguishable without sound. |

### Voice and speed details

- Show only voices Android's installed TTS engine reports as available; label voices that require a network connection, and let the user choose an offline voice when available.
- Store a stable voice identifier when the engine provides one; retain the system default as a fallback.
- A voice change during playback takes effect on replay or the next post, avoiding a surprising restart mid-sentence.
- Speed is a playback multiplier, not a rewrite of text. The selected speed likewise takes effect on replay or the next post.
- Use the posted text's original characters for speech. Platform TTS may pronounce punctuation and mixed languages differently; test English, Chinese, Malay, and mixed-script samples on the chosen target.
- Android `TextToSpeech` has stop but no native pause/resume method. The first version offers stop and replay, with no misleading pause control.

### Constraints and later ideas

The first version has one active post and no saved chat history. Offline reading is desirable where an installed voice supports it, but available voices may require downloads or network access; expose that limitation honestly. Sharing text from another app, background playback, file import, voice downloads, audio export, and synchronization can be evaluated after the basic reading flow works.

## Platform and decision gate

The target is an Android app. First verify whether the phone's selected-text **Read aloud** action already supports the desired engine, voice, and speed through system Text-to-speech output settings. The custom app should proceed when a specific gap remains, such as a convenient post-and-replay flow or independent per-app voice controls. The app cannot force a particular voice into another app's selected-text menu.
