# Text Reader / Read-Aloud Agent

A planned Android app for posting text and hearing it read aloud in a chosen voice at a chosen speed.

## Juniper and the app decision

The requested voice is **Juniper in ChatGPT**, selected under **ChatGPT Settings → Voice → Voice**. POCO's Google text-to-speech settings do not select ChatGPT voices. ChatGPT's documented Juniper choice is for Voice conversations; OpenAI does not document a Juniper selector for the Android message action **Read aloud**. Before building an Android app, confirm whether ChatGPT Voice with Juniper meets the need. A standalone app using Android `TextToSpeech` cannot offer that exact ChatGPT voice, and Juniper is not listed among the public Speech API voices. This project is paused at documentation until a supported voice path and the remaining gap are clear. See [ChatGPT Voice](https://help.openai.com/en/articles/20001274-chatgpt-voice), [ChatGPT Android actions](https://help.openai.com/en/articles/8142208-chatgpt-android-app-faq), and [Speech API voices](https://developers.openai.com/api/docs/guides/text-to-speech).

## Try the phone's reader first

On POCO/HyperOS, open **Settings → Additional settings → Languages & input → Text-to-speech output**. Select the preferred engine and open its settings to inspect available voices; adjust language and speech rate, play the sample, and then try the selected-text **Read aloud** action again. Menu names may vary by software version. This only checks the phone's own voices, not Juniper. If that provides an acceptable alternative voice and speed, a separate app may add little value. If it does not, record which voice/control is missing before implementing the app. See [Xiaomi's settings path](https://www.mi.com/my/support/article/KA-06461/) and [Android's TTS settings guide](https://support.google.com/accessibility/android/answer/6006983).

## First user flow

1. Type or paste text into a composer and tap **Read aloud**.
2. The app shows the posted text and starts speech without changing its wording.
3. Pick an available voice and a speed; read, stop, or replay.
4. Post new text to read it next. For the first version, a new post stops the previous reading.

The first version should work without an account, language model, or backend. Use Android's [`TextToSpeech` API](https://developer.android.com/reference/android/speech/tts/TextToSpeech) and installed engine. Voice and language availability will depend on that engine. The API has no native pause/resume method, so that control is not promised for the first version.

## Proposed structure

```text
apps/text-reader/
  README.md
  docs/
    requirements.md       Product scope and acceptance criteria
    roadmap.md            Small Android milestones and decision gate
  app/src/main/           Android UI, speech adapter, and resources (future)
  app/src/test/           Focused playback-state tests (future)
```

The docs are committed now. `app/` is a proposed path, not a tracked directory or a claim that the app exists.

## Decisions to retain

- Read the user's posted text as written; do not generate a response to it.
- Let the user select a voice from voices actually available on the device, with a sensible system default.
- Default speed to 1.0× and offer 0.75×, 1.0×, 1.25×, 1.5×, and 2.0× where supported.
- Avoid app-managed uploads. Prefer offline voices when available, and tell the user when a selected voice needs network synthesis.
- Target an Android app, subject to checking whether the phone's built-in reader already meets the need.

See [requirements](docs/requirements.md) and [roadmap](docs/roadmap.md).
