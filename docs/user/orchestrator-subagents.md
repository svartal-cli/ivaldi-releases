# Orchestrator subagents

Delegated tasks run as child conversations, potentially using a different provider
and model from the parent. They appear alongside native subagents in the agent
panel and remain accessible under their parent in the sidebar. The panel shows
startup and progress, provider/model, routing, and the final response or failure.
Open the child conversation to inspect its full transcript or answer an
approval/input request. Completed entries remain available after reload.

## Delegating work

An agent hands a self-contained task to a subagent with the `delegate_task` MCP
tool. The child cannot see the parent's conversation, so the task text carries
everything it needs: the goal, which files it owns, and acceptance checks.
`orchestrator_capabilities` lists the providers and models available for
delegation.

Delegation returns immediately by default; when the child finishes, the parent
is woken for its next turn, so there is nothing to poll. When the current turn
needs the result, the agent passes `mode: "wait"`. Agents sharing a checkout
must not edit overlapping files concurrently; `isolation: "worktree"` gives a
child its own prepared checkout.

`task_status({ taskId })` reads a child's progress and final result, and
`task_cancel({ taskId })` stops it, including anything still queued behind it.
Follow-up messages on an idle child go through `t3_thread_send` with its
`childThreadId`. Stopping the parent also interrupts its active children, and
reloading or disconnecting the UI does not cancel delegated work.

## Routing by task type

A workspace can declare, in `.t3code/orchestrator.json`, the kinds of work it
delegates (task types), the models on offer with a 1–5 rating per task type,
and rules that pin a task type to a model. When the workspace declares task
types, agents pass `taskType` on `delegate_task` and routing picks the target;
`orchestrator_routing` shows the live table and which config file produced it.
In a Knit bundle, a `repo` on the call or a repo rule in the config routes by
repository. An explicit `target` on the call overrides routing for one task.
Settings → Orchestrator edits the app-wide default config; the workspace file
is merged over it.

## Threads on another environment

Agents can also open a new thread on one of your other Ivaldi environments
linked to the same account: `environment_list` shows them, with a live status
per environment. `environment_project_list` lists the projects of one, and
`environment_thread_launch` opens the thread, either as a normal project thread
(`project`) or on a Knit bundle (`knit`). The new thread cannot run with broader
permissions than the thread that asked for it, and both environments must be
linked to your Svartal account.

An environment that receives these launches controls them in
**Settings → Connections**: allow any access, cap what incoming threads may do,
or turn them off entirely. The default is full access.
