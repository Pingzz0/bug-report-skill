# bug-report

A Claude skill that turns any error into something useful.

Paste an error message, stack trace or crash log and Claude will:

1. **Explain it** in plain language
2. **Find where it came from**: file, line, function, and the real root cause if it's somewhere else
3. **Warn you about leaked secrets** like webhook URLs, tokens, usernames in paths and IPs
4. **Write a clean bug report** ready to paste into a GitHub issue, with private data scrubbed

Works with any language, framework or engine.

## Example

You paste:

```
[WARN]: [MyPlugin] Unknown key 'messages.welcom' in config.yml, ignoring
[ERROR]: Could not pass event PlayerJoinEvent to MyPlugin v1.0.0
Caused by: java.lang.NullPointerException: Cannot invoke "String.replace(...)" because "template" is null
	at com.example.util.MessageUtil.format(MessageUtil.java:27)
	at com.example.listener.JoinListener.onJoin(JoinListener.java:41)
```

Claude tells you the crash is at `MessageUtil.java:27`, but the real cause is the typo `welcom` in your config, shows you the fix, and gives you a finished GitHub issue.

## Install

### Claude app

1. Download this repo as a ZIP, or grab `bug-report.zip` from Releases
2. Make sure the zip contains the `bug-report` folder with `SKILL.md` inside
3. Upload it as a custom skill in your Claude settings

### Claude Code

Copy the `bug-report` folder into one of these:

| Location | Scope |
|---|---|
| `~/.claude/skills/` | all your projects |
| `.claude/skills/` in a project | only that project |

## Usage

Just paste the error, or type `/bug-report` first to make sure it loads.

If something important is missing, Claude asks up to 3 quick questions before writing the report. It never makes up versions or repro steps.

## Tips

If Claude answers without using the skill, you probably have a lot of skills enabled. When there are too many, some only show up by name without their description, so Claude doesn't know when to use them. Turn off skills you don't need, or use `/bug-report`.

## License

[MIT](LICENSE)
