# FAQ

## Is Ivaldi a harness?

No. A harness is what turns an LLM into an agent: it gives the model tools, a way to call them, runs them, and hands the results back. Claude Code is an interface (the TUI, the Code tab in the desktop app) plus a harness underneath (the Anthropic Agent SDK). Codex has the same split: the app plus the Codex App Server. Ivaldi uses those harnesses. It is not a harness, and it does not work without one.

Bring your own: Claude Code, Codex, Cursor, Grok Build, OpenCode, Google Antigravity, Kiro, Pi, Muse Code, or fx. [Provider setup](./install.md#providers)

## Why use Ivaldi instead of Claude Code or the Codex app?

- Use the subscriptions you already have. Claude, Codex, and the other supported providers work side by side.
- Remote work. Run `ivaldi up` on any machine and drive it from your other devices.
- One app on desktop, web, and phone.

[Install](./install.md)

## Can I use Ivaldi with my Claude Code subscription?

Yes. [Claude](./providers-claude.md)

## How do I use Ivaldi remotely?

Your agents run wherever the Ivaldi server runs: your desktop, a server, a VPS. You connect to it from your other devices. Run `ivaldi up` on that machine. Svartal Connect is the easiest path. LAN pairing and Tailscale work too, and [ivaldi.svartal.com](https://ivaldi.svartal.com) is the web client. [Remote access](./remote-access.md)

## How do I use Ivaldi on my phone?

Open [ivaldi.svartal.com](https://ivaldi.svartal.com) on the phone, add it to your home screen, and connect it to your computer with Svartal Connect or a pairing link. The phone is a remote. Your computer does the work and needs to stay on. [Mobile setup](./install.md#mobile-app) · [Remote access](./remote-access.md)

## Why does Svartal Connect keep disconnecting?

Svartal Connect is Ivaldi's built-in alternative to Tailscale for remote connections. If it keeps dropping, open **Settings > Environments**, find the machine, and select **Details**. The first part marked as failed is the cause. Tailscale or a LAN pairing also work as a fallback. [Svartal Connect troubleshooting](./connect-troubleshooting.md)

## Can I add a bunch of accounts for one provider?

Ivaldi is not the place to rotate a pool of accounts. It does not switch between accounts to stretch usage limits, and doing so can break a provider's terms.

A separate work account is fine. Setup for two: [Codex](./providers-codex.md#use-multiple-accounts) · [Claude](./providers-claude.md#separate-accounts-or-configurations). If you already run a CLIProxyAPI hub outside Ivaldi, Ivaldi can show its pooled limits under Usage. [Connect a hub](./usage.md#connect-a-cliproxyapi-hub)

## Can I use an API key or OpenRouter instead of a subscription?

Yes. Add another provider instance in Settings and give it its own keys and endpoint. Claude has a full OpenRouter recipe. Your subscription setup stays untouched. [OpenRouter](./providers-claude.md#openrouter) · [Provider instances](./install.md#providers)

## Does my code go to Svartal's servers?

No. Your code and prompts go from your machine to your provider (Anthropic, OpenAI, and so on). With Svartal Connect, Svartal checks your sign-in and the host's link, and traffic reaches the host through a Cloudflare tunnel (`cloudflared` on the host). Product usage events are off unless the server is started with them turned on; they never include prompts or file contents. [Product usage data](./telemetry.md)

## Worktrees are eating my disk. How do I clean them up?

Open **Settings → Worktrees → Cleanup** and turn on automatic worktree cleanup. You can also run it now from there. [Storage cleanup](./project-settings.md#storage-cleanup)

## Is there voice input?

Yes. Web and desktop require you to choose an environment first. The transcript goes into your draft for review. See [Voice input](./voice-input.md).

## Does it work on Windows, Mac, and Linux?

Yes. The desktop app and the `ivaldi` command are available for macOS on Apple silicon, Windows x64, and Linux x86_64. There is no `ivaldi` command for Intel Macs. On Windows you can also run agents inside WSL. [Install](./install.md)

## Why is my provider not showing up?

Usually the CLI is not installed or not on the `PATH` of the machine that runs the server (the computer, not your phone). Log in on that machine first, for example with `codex login` or `claude auth login`. Still missing? Point **Binary path** at it in provider settings. Version managers often cause this. [Provider setup](./install.md#providers)
