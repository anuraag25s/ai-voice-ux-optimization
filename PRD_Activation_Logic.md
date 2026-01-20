# Feature Spec: Local Wake-Word State Machine

## Objective
Enable hands-free activation with zero network latency and 100% privacy preservation.

## Technical Constraints
* **Privacy:** Wake word detection must happen **on-device**. No audio is streamed to the cloud until the "Active" state is triggered.
* **Battery:** Background listening service must consume <1% CPU on idle.

## State Machine Logic

```mermaid
graph TD
    A[Idle State] -->|Microphone listening buffer 2s| B{Wake Word Detected?}
    B -- No --> A
    B -- Yes ('Wake Phrase') --> C[Active State]
    C -->|Haptic Feedback| D[Stream Audio to Cloud]
    D --> E[LLM Processing]
    E --> F[Text Injection]
    F --> A
