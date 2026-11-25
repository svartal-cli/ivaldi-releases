# Change a conversation's provider

Use the conversation's model picker to choose a model on another configured provider. The choice applies when you send the next message. Until then, the existing session continues to own the conversation. The same conversation, displayed history, workspace, files, plans, and checkpoints remain available.

Provider changes are available on web, desktop, and mobile; older app versions that predate the feature keep their previous picker. A provider change waits for a safe boundary: finish or stop active work and resolve pending approvals or questions first. Native subagent transcripts cannot change providers independently.

## What the new provider receives

Ivaldi starts a fresh destination session on the same conversation, workspace, and stored history. The new provider does not receive the entire transcript. It begins with a short preview of the conversation's original and most recent context, plus a pointer to the exact point in the stored history where your new message continues.

From there, the new provider can read the rest of the conversation itself: earlier messages and tool records a bounded page at a time or one specific record at a time, and original images through the attachment tool as viewable images. Other attached files remain available through chunked reads. Historical tool data stays historical — recorded calls are a record of what happened, not instructions to execute them again, though the provider may still rerun a command when its own work calls for it. Nothing is rewritten, shortened, or summarized before the new provider starts.

The transfer is not a native session import. Provider-private reasoning such as hidden thinking, internal caches, live tools, and native subagent state do not transfer. Tool output that Ivaldi never persisted cannot be reconstructed. Images whose originals are missing cannot be recovered. The switch is recorded in the timeline.

## Cost and preparation

The starting preview stays short no matter how large the conversation is, so a long history no longer triggers any summarizing pass. The new provider works from the preview and looks further back only as its task requires; history it retrieves is processed as ordinary conversation input, so normal usage costs still apply. Completed preparation is retained for safe retries rather than repeated.

## Failed or interrupted switches

If preparation fails, the original session stays available. Correct the credential or provider problem and use **Retry provider switch**. A rejection confirmed before the destination accepted the message can be retried — a Codex rejection, for example; other failures may not be. If a failure happens after the original session has stopped, the app retains its recovery information.

If Ivaldi cannot determine whether the destination received the message, it reports uncertain delivery and never sends the message again automatically. Use **Reset provider switch** to end the uncertain attempt while keeping your history intact, then inspect any work the destination may already have performed before retrying. Reset is available on web, desktop, and mobile.

Brokered credentials require a worker that supports conversation handoff. A remote broker reaches the destination through Ivaldi's existing scoped bridge rather than a local file path, and reachability is checked before the original session stops. External OpenCode servers are currently ineligible because they cannot install that scoped connection. Locally managed OpenCode sessions are supported.
