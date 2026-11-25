# Install Ivaldi

Ivaldi runs coding agents on your computer and lets you control them from its
desktop, web, or mobile app. Set up the machine where the agents will work first.

## Requirements

You need an installed, authenticated provider before starting a thread. You can
launch Ivaldi and configure providers afterwards.

## Command line

Install the `ivaldi` command with npm (needs Node.js for `npx`):

```bash
npx ivaldi@latest install
```

This installs the `ivaldi` command to `~/.local/bin`. If that folder is not on your
`PATH` yet, add it. If an `ivaldi` that Ivaldi or the desktop app did not create is
already there, it leaves that one alone and stops. To pin an exact version, run
`npx ivaldi@<version> install`.

| Task                                  | Command                                                                     |
| ------------------------------------- | --------------------------------------------------------------------------- |
| Start the server and open the web app | `ivaldi`                                                                    |
| Start the server without a browser    | `ivaldi serve`                                                              |
| Use it from your other devices        | `ivaldi up` ([details](./remote-access.md))                                 |
| Keep it running in the background     | `ivaldi service install` ([details](./background-service.md))               |
| Move to the newest release            | `ivaldi update`                                                             |
| Reclaim database space                | `ivaldi doctor` ([details](./background-service.md#reclaim-database-space)) |
| Remove it again                       | `ivaldi uninstall`                                                          |

Run `ivaldi help` or `ivaldi --help` for the full reference. To start in a new working
directory, use an explicit path such as `ivaldi ./my-project`. A bare directory name
is accepted only if it already exists.

If `ivaldi` or `ivaldi start` reports an already running server, run the `ivaldi pair`
command it names and open the pairing URL to connect to that server. Stop it
before starting a replacement, or use a different `--base-dir` for an
independent server.

To try Ivaldi once without installing it, run `npx ivaldi@latest` instead (needs
Node.js for `npx`). It offers to install the `ivaldi` command first. If you say no,
it asks again at the next minor release, and `npx ivaldi install` installs it later.
`npx ivaldi` always runs the version npm picked, even when an `ivaldi` is installed. On
the nightly train, run your installed `ivaldi` (for example `ivaldi connect`), not
`npx ivaldi`, which runs the latest stable release.

### Intel Macs

There is no `ivaldi` executable for Intel Macs. Release archives of the command
exist for macOS on Apple silicon, Linux x86_64, and Windows x64.

## Desktop app

Download the desktop app from [svartal.com/ivaldi](https://svartal.com/ivaldi) or from
[GitHub Releases](https://github.com/svartal-cli/ivaldi-releases/releases). Builds are
published for macOS on Apple silicon (`.dmg`), Windows x64, and Linux x86_64 (AppImage).

### Linux

To launch the AppImage, open a terminal in its download folder. Replace
`Ivaldi.AppImage` below with the exact filename you downloaded:

```bash
chmod +x ./Ivaldi.AppImage
./Ivaldi.AppImage
```

### The `ivaldi` command

The desktop app includes the `ivaldi` command-line tool. A new install sets it up
on first launch; after an update, or any time, choose **Install** next to
**ivaldi command** in **Settings → About**. On macOS and Linux it adds an `ivaldi` link
in `~/.local/bin` (or `~/bin`); on Windows it adds the app's command folder to
your `PATH`. Open a new terminal afterwards. If the folder is not on your
`PATH`, **Add to PATH** on the Welcome page or in **Settings → About** adds one
line to your shell's startup file. **Remove** takes it off, and the app does not
add it again. If you already have another `ivaldi`, it stays as it is.

### Windows Subsystem for Linux

Choose a WSL distro in **Settings → Sharing & access** to run agents and projects
there. Install the provider CLIs inside that distro. Ivaldi installs its own
server runtime there automatically; the first launch after an app update can
take longer.

### Open a project from a terminal

With the desktop app already running on the same machine:

```bash
ivaldi app
```

This opens a new thread for the current directory, adding the project if needed.
Pass a path, such as `ivaldi app ../my-project`, to open another directory. It requires
the desktop app, so a standalone server or an SSH session is not enough. If the
command cannot reach the app, start or update the desktop app and try again.

### Drop a folder on the sidebar

Drag one or more folders from Finder, Explorer, or your file manager onto the
sidebar. Each one opens as a project on this computer, the same as `ivaldi app`.
Files dropped on a thread still attach to that thread. Browsers do not share
folder paths, so in the web app use **Add project** instead.

## Mobile app

Ivaldi is not in the App Store or Google Play. On a phone or tablet, open
[ivaldi.svartal.com](https://ivaldi.svartal.com) in the browser and add it to your
home screen: Ivaldi offers **Install** where the browser supports it, and on iPhone
and iPad you tap Share in Safari, then **Add to Home Screen**. It then opens like an
app, without a browser bar.

The phone connects to a server on another machine. Follow
[remote access](./remote-access.md) to link it through Svartal Connect or a pairing URL.

## Providers

Open **Settings → Providers** in the web or desktop app, select the environment,
and enable the provider you want. Installation, login, and configuration belong
to that environment's machine, even when you connect from a phone or another
computer.

| Provider    | Install and authenticate                                                                                                                                  |
| ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Codex       | [Connect with ChatGPT](./providers-codex.md#connect-with-chatgpt), or install [Codex CLI](https://developers.openai.com/codex/cli) and run `codex login`. |
| Claude      | Install [Claude Code](https://claude.com/product/claude-code), then run `claude auth login`.                                                              |
| Cursor      | Install [Cursor CLI](https://cursor.com/cli), then run `agent login`.                                                                                     |
| Grok Build  | Install [Grok Build CLI](https://x.ai/cli), then run `grok login`.                                                                                        |
| Kiro        | Install [Kiro CLI](https://kiro.dev/docs/cli/), then run `kiro-cli login`.                                                                                |
| OpenCode    | Install [OpenCode](https://opencode.ai), then run `opencode auth login`.                                                                                  |
| Antigravity | Install and sign in with Google from Ivaldi's provider settings.                                                                                          |
| Pi          | Install [Pi](./providers-pi.md#set-up-pi) with Node.js 22.19 or newer, then run `pi` and `/login`.                                                        |
| Muse Code   | Install [Muse Code](https://dev.meta.ai/docs/muse-code) on the server, run `muse login`, then enable it in Settings → Providers.                          |
| fx          | Install [fx](https://fx.sh) with `curl -fsSL https://fx.sh/setup.sh \| bash`, then run `fx login`.                                                        |

Provider CLIs must be on the server's `PATH`. If Ivaldi cannot find one, set its
**Binary path** in provider settings, especially when using a version manager.
Cursor's executable is `cursor-agent`, although its login command is
`agent login`. Codex connected through ChatGPT and Antigravity can use their
managed runtimes without a `PATH` entry.

Ivaldi warns when a provider version has known compatibility problems with your
release. Check **Settings → Providers** on that environment for the recommended
version or range. When its package manager supports installing a specific version,
you can install the recommendation there. Otherwise use the provider's installer
on the environment's machine. An unlisted version is unverified.

When a provider CLI is behind its latest release, its provider card shows the
available version. **Update now** runs the installer that owns the CLI
(Homebrew, mise, or a global npm, pnpm, Yarn, Bun, Volta, or Vite+ install), or
the CLI's own update command when Ivaldi cannot tell. Claude, Codex, and
OpenCode installs Ivaldi cannot identify stay manual: update them through the
installer you used. Ivaldi runs `mise upgrade`
only for a tool your mise config requests as `latest` when the provider's binary
path is a mise shim or under the tool's `installs/<tool>/latest` link; update a
pinned version, or a path into one version's directory, through mise yourself.
Update a CLI installed with Nix through Nix.
Cursor and Antigravity update with Ivaldi. Homebrew and Chocolatey installs
compare against the version their package manager offers, which can trail the
npm release; update Claude installed with Chocolatey through Chocolatey.

The managed runtimes for Antigravity and for Codex connected through ChatGPT
first install the release Ivaldi tested. When Ivaldi finds a newer compatible
release, their setup in **Settings → Providers** offers an update.

Add another provider instance for a separate account or configuration. Each
instance can have its own environment variables, such as API keys or a custom
base URL. Mark secret values as sensitive; after saving, Ivaldi does not display
their original values.

For provider-specific setup and accounts, see [Codex](./providers-codex.md),
[Claude](./providers-claude.md), [OpenCode](./providers-opencode.md),
[Antigravity](./providers-antigravity.md), [Kiro](./providers-kiro.md),
[Pi](./providers-pi.md), [Muse Code](./providers-muse.md), and [fx](./providers-fx.md).

### Provider check timeouts

If a provider works in its CLI but Ivaldi reports a timeout while checking it,
allow more time in the Ivaldi server's environment. For example, give Codex and
Claude readiness checks 60 seconds:

```bash
T3CODE_CODEX_PROBE_TIMEOUT_MS=60000 T3CODE_CLAUDE_PROBE_TIMEOUT_MS=60000 ivaldi serve
```

For a remote environment, set these on the machine running the Ivaldi server.
Keep them in your launcher or service configuration to retain them across
updates, then restart the server. For systemd, add
`Environment=T3CODE_CODEX_PROBE_TIMEOUT_MS=60000` under `[Service]` in a service
override, reload systemd, and restart the service. Provider instances can also
set their own overrides in Settings → Providers.

Each variable extends that provider's readiness-probe deadlines; a phase whose
default is already longer keeps its default. Providers with several phases can
take longer than one deadline in total. Values must be whole milliseconds no
greater than 2147483647; unset or invalid values keep the defaults.

| Provider            | Environment variable                   |
| ------------------- | -------------------------------------- |
| Codex               | `T3CODE_CODEX_PROBE_TIMEOUT_MS`        |
| Claude              | `T3CODE_CLAUDE_PROBE_TIMEOUT_MS`       |
| Cursor              | `T3CODE_CURSOR_PROBE_TIMEOUT_MS`       |
| Antigravity         | `T3CODE_ANTIGRAVITY_PROBE_TIMEOUT_MS`  |
| Grok                | `T3CODE_GROK_PROBE_TIMEOUT_MS`         |
| Kiro                | `T3CODE_KIRO_PROBE_TIMEOUT_MS`         |
| fx                  | `T3CODE_FX_PROBE_TIMEOUT_MS`           |
| Pi                  | `T3CODE_PI_PROBE_TIMEOUT_MS`           |
| Muse Code           | `T3CODE_MUSE_PROBE_TIMEOUT_MS`         |
| OpenCode            | `T3CODE_OPENCODE_PROBE_TIMEOUT_MS`     |
| ACP Registry agents | `T3CODE_ACP_REGISTRY_PROBE_TIMEOUT_MS` |

Longer deadlines also take longer to report a stalled check. These overrides
cover readiness and discovery, including OpenCode server startup. Usage and
config enrichment retain their own shorter limits. Turn execution, package
installation, update checks, and shutdown limits keep their existing behavior.

## Next steps

- [Working with threads](./thread-sidebar.md): start tasks and organize parallel work.
- [Permission modes](./permission-modes.md): choose when agents ask before acting.
- [Remote access](./remote-access.md): connect from another device.
- [Running in the background](./background-service.md): keep a host available.
- [Updating Ivaldi](./updating.md): update the app and connected servers.
- [Managed policy](./managed-policy.md): configure Ivaldi for everyone on a machine.
