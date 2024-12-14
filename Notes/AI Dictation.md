---
tags:
- speech
video-url: https://www.youtube.com/watch?v=loIvdOpqn5Q&list=WL&index=17
---

## AI Dictation Overview

In this video, Robert introduces the growing use of AI-powered dictation tools, focusing on their ability to save time by converting [[Speech to Text]]—especially when paired with language models (LLMs). He reviews three popular applications for dictation: **MacWhisper**, **WhisperFlow**, and **Super Whisper**, along with their key features, limitations, privacy concerns, and workflows. Additionally, he provides a guide for free offline dictation using **iCo**, **LM Studio**, and **Shortcuts**.

### Key AI Dictation Tools

#### 1. Transcription and Language Models

- **Two-Step Process**: AI dictation tools typically involve transcription (speech-to-text) followed by [[LLM]] processing to improve grammar, translation, and summarization.
- **Whisper AI**: This model significantly enhances transcription accuracy, especially when combined with LLMs like [[GPT]], allowing for more seamless dictation.

#### 2. MacWhisper

- **Overview**: An early adopter of Whisper AI, focusing on transcription with both local and cloud models.
- **Pros**: Excellent transcription quality, flexible for advanced use, supports local models.
- **Cons**: Bugs with punctuation and translations, limited user experience (UX), lacks a history feature, requires API tokens for advanced features.

#### 3. WhisperFlow

- **Overview**: A newer app, specifically designed for dictation with voice-triggered commands.
- **Pros**: Fast, intuitive commands, strong transcription and AI assistant features, supports formatting without manual settings.
- **Cons**: Privacy concerns (online-only), data collection transparency issues, subscription-based model.

#### 4. Super Whisper

- **Overview**: Offers extensive customization options with different modes for dictation, AI assistance, coding, and more.
- **Pros**: Supports both cloud and local models, integrates with tools like **Alfred** and **Keyboard Maestro**.
- **Cons**: Steep learning curve, high cost ($250 for a lifetime license), developed by a single person.

#### 5. Free Offline Dictation with iCo and LM Studio

- **Solution**: Combines **iCo** with **LM Studio** for a free, offline transcription tool.
- **Setup**: Download LM Studio, set up a local server for models like Lama, and connect with iCo using Shortcuts or **Keyboard Maestro** for offline transcription.
- **Limitations**: Can time out for lengthy audio files; may need to bypass Shortcuts for complex tasks.

---

### Guide to Setting Up Free Offline Dictation

1. **Download iCo and LM Studio**

    - **iCo**: A free app using Whisper for transcription.
    - **LM Studio**: Allows downloading open-source AI models (e.g., Lama) and running a local server for offline use.
2. **Create a Shortcut**

    - Configure iCo and LM Studio for local dictation, using either local models (via LM Studio) or cloud models with an API token.
    - Adjust the system prompt based on the task, such as translation or cleanup.
3. **Use Keyboard Maestro**

    - Recommended for longer dictations to avoid Shortcuts app time limits, offering flexibility for managing large audio files.
4. **Testing and Debugging**

    - If processing times out, files are saved in the Shortcuts folder for backup.
    - For extended recordings, consider bypassing Shortcuts and using **Keyboard Maestro** exclusively.

---

### Conclusion and Recommendations

- **Super Whisper**: Most versatile, suited for advanced users.
- **MacWhisper**: Ideal for simple transcription tasks.
- **WhisperFlow**: Shows potential but has privacy concerns.
- **Offline Solution**: Use the **iCo + LM Studio** setup

[[AI Avatars]]   [[Speech to Text]]  [[AI Agents]]