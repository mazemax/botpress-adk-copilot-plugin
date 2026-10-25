# Update, rollback, duplicate installs, and uninstall

Back up any host configuration you change and record the current package version, install source, and upstream SHA. Update one host at a time and verify in a fresh session. The procedures below are documented host flows, not observed compatibility results for this release candidate.

## Copilot CLI

For a direct local-path install, reinstall from the desired source revision with `copilot plugin install ./botpress-adk-copilot-plugin`; official documentation notes that direct installs are cached. For an installed source that supports updates, use:

```bash
copilot plugin update botpress-adk-community
copilot plugin list
```

Uninstall with:

```bash
copilot plugin uninstall botpress-adk-community
```

Use the manifest `name`, not the local directory name. Start a fresh session and inspect both skills and the `/` command picker. VS Code + Copilot behavior requires separate verification and is not inferred from these CLI commands.

## VS Code + GitHub Copilot

For a direct Git installation, use the same interface where it was installed. In a supported Copilot harness, `/plugin list`, `/plugin update botpress-adk-community`, and `/plugin uninstall botpress-adk-community` are the documented operations; command completion can provide the installed identity. The Agent Customizations editor and installed-plugins view also provide update/uninstall controls.

VS Code documents that direct Git installations cannot be enabled or disabled; uninstall to stop using one. The `/plugin` command inventory and Agent Customizations editor inventory are separate, so do not assume an operation in one manages an installation from the other. Reload/restart and start a fresh session before checking the six skills and 12 commands.

## Rollback

Use a previously tested immutable tag/commit rather than an arbitrary branch tip. Reinstall or select that source using the verified host flow, restart/reload, and repeat skill/command discovery plus the golden path. A rollback must not silently change the upstream ADK snapshot: compare both `UPSTREAM.json` files and review generated-command and side-effect differences.

## Duplicate installations

Use one intentional installation source per host profile where practical. Inspect CLI-installed, VS Code direct, marketplace, personal, project, and plugin components for duplicate names and remove stale copies through their owning interface. Record precedence/cache behavior from actual host evidence instead of guessing.

## Verification after update or removal

Confirm package version, expected six-skill and 12-command inventory (or absence after removal), fresh-conversation activation, and any remaining host configuration/cache entries. Update `docs/compatibility.md` only with observed results. The distribution's own scripts never modify host installation or global configuration.
