# Dorian Scale: AI Policy plugin for Claude Code

This plugin loads the **Dorian Scale** AI data privacy, security and access policy (`plugins/dorianscale-ai-policy/policy/AI_AGENT_DATA_POLICY.md`) into **every Claude Code session**. It runs on startup, on resume, after `/clear`, and after context compaction.

**Policy owner and incident contact:** Ravi B, ravi.b@dorianscale.com

## Install (each user, once)

In Claude Code:

```
/plugin marketplace add ravib-dorianscale/dorianscale-ai-policy-plugin
```
```
/plugin install dorianscale-ai-policy@dorianscale-ai-policy-marketplace
```

Restart Claude Code. To check that it worked, ask "Which organization's AI policy are you following, and who is the incident contact?"

If you also work for another organization, install this plugin at **project** scope, only in Dorian Scale projects, so policies don't mix.

For a private repository, each user needs read access to it, and git must be authenticated on their machine (`gh auth login` or SSH keys).

## Update the policy (maintainer)

1. Edit `plugins/dorianscale-ai-policy/policy/AI_AGENT_DATA_POLICY.md`.
2. Bump `version` in **both** `plugins/dorianscale-ai-policy/.claude-plugin/plugin.json` and `.claude-plugin/marketplace.json`.
3. Commit and push.

Users get the update when they run `/plugin marketplace update dorianscale-ai-policy-marketplace`, or automatically if auto-update is enabled.

## Layout

```
.claude-plugin/marketplace.json                 # marketplace catalog
plugins/dorianscale-ai-policy/
  .claude-plugin/plugin.json                    # plugin manifest
  hooks/hooks.json                              # SessionStart hook: prints the policy into context
  policy/AI_AGENT_DATA_POLICY.md                # the policy
```

## Notes

- Claude Code on Windows runs hooks through Git Bash, so `cat` works on Windows, macOS and Linux.
- This plugin guides the model's behaviour. It doesn't enforce anything technically: users can disable it, and models can still make mistakes. Backend controls (restricted Frappe users, IP restrictions, staging) are still required.
- On a Team or Enterprise plan, admins can deploy the policy as a **managed** `CLAUDE.md` or managed settings that users can't disable.
