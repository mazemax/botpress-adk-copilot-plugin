# GitHub Copilot quickstart

**Release candidate:** `1.0.0-rc.1`. This is a verification protocol based on official host documentation, not a claim that the steps passed on your host. See `docs/compatibility.md`.

## Prerequisites

- A supported VS Code + GitHub Copilot or Copilot CLI installation and the required account/configuration.
- For VS Code, enable `chat.plugins.enabled`; an organization policy may control it.
- Git for a local source install.
- For ADK workflows: the official Botpress ADK CLI, a compatible ADK environment, and a dedicated non-production Botpress workspace when a live dev bot is required.
- A disposable ADK project directory and synthetic data.
- Node.js 24+ only when running this repository's maintainer tooling; it is not a plugin runtime dependency.

Read `docs/side-effects.md` before invoking workflows. No Botpress token is needed for repository validation.

## Candidate installation: VS Code + GitHub Copilot

This direct-source flow is documented by VS Code but has **not been run in this implementation environment**:

1. Open the Command Palette and run **Chat: Install Plugin From Source**. Alternatively, use **Install Plugin from Source** on the **Plugins** page of the Agent Customizations editor.
2. Enter `https://github.com/mazemax/botpress-adk-copilot-plugin` and review the source before installing.
3. Start a fresh Copilot session and inspect the installed plugin, skills, and `/` command picker. In a supported Copilot harness, `/plugin list` is the documented inventory command.
4. Record the exact VS Code, Copilot harness, plugin, and package versions plus the installed source revision.

A direct Git installation can be updated or uninstalled but cannot be enabled/disabled in VS Code. Manage it in the same interface used to install it; VS Code documents separate inventories for `/plugin` commands and the Agent Customizations editor. Do not infer VS Code behavior from Copilot CLI results.

Official reference: [Agent plugins in VS Code](https://code.visualstudio.com/docs/agent-customization/agent-plugins).

## Candidate installation: Copilot CLI

Install directly from the public GitHub repository:

```bash
copilot plugin install mazemax/botpress-adk-copilot-plugin
copilot plugin list
```

For local maintainer testing, clone and install a real directory instead:

```bash
git clone https://github.com/mazemax/botpress-adk-copilot-plugin.git
copilot plugin install ./botpress-adk-copilot-plugin
copilot plugin list
```

Start a new interactive session and use `/skills list` to inspect skills and the `/` picker to inspect commands. Reinstall a direct local copy after changing it because the CLI caches installed components. These CLI steps do not verify VS Code + Copilot.

Official references: [Creating a plugin for Copilot CLI](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/plugins-creating) and [Copilot CLI plugin reference](https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-plugin-reference).

## Five-minute discovery verification

1. Use a clean host profile and the intended package revision.
2. Restart/reload and start a fresh conversation.
3. Confirm the six skills are discoverable: `adk`, `adk-debugger`, `adk-dev-console`, `adk-docs`, `adk-evals`, and `adk-frontend`.
4. Open the `/` picker and confirm all 12 command IDs from `docs/workflows.md`. Select entries by their actual displayed labels; do not assume an unverified qualified namespace.
5. Check for duplicate personal/project/plugin skills or commands with the same names.
6. Use a read-oriented prompt first: “Explain what a Botpress ADK action is and show one small example from the official ADK references.”
7. Record host/version, OS, model, package version, upstream SHA, expected result, and actual result in the host checklist.

Do not begin with `adk-ship`, credentials, a production workspace, or a destructive test. Direct source installation does not mean this plugin is listed in Awesome Copilot or reviewed by GitHub/Botpress.

## First disposable ADK workflow

After discovery succeeds, use `docs/workflows.md` and the manual checklist to inspect or initialize a disposable project, build one small primitive, validate it, and run a synthetic dev-only test. Review every proposed file and workspace mutation. Do not deploy.

## If verification fails

Use `docs/troubleshooting.md` and open the appropriate issue template with sanitized evidence. An installation, command-discovery, or activation failure should be recorded as a release-blocking finding for the declared support matrix, not silently omitted. A natural-language fallback can complete a task, but it does not make a failed command-discovery check pass.
