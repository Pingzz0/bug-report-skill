---
name: bug-report
description: ALWAYS use this skill whenever the message contains an error, exception, stack trace, crash log, server or console log, "Caused by", "ERROR", "Traceback", or the user says something broke, crashed or doesn't work, even if the error looks easy and even if they only ask "can you help". Explains the error, traces where it came from (file, line, root cause), scrubs private data, and writes a ready to post GitHub bug report.
---

# Bug Report

Turn a raw error into three things: a plain explanation, the exact origin, and a bug report someone else can act on. Works for any language, framework, game engine or tool.

## 1. Read the error

Identify before saying anything:

- **Language / runtime / tool** (Java, Python, Node, Luau, C#, Rust, a build tool, a game console...)
- **Error type** (NullPointerException, TypeError, segfault, 404, compile error, failed assertion...)
- **The actual message**, separated from noise like timestamps, log prefixes and repeated lines
- **Whether there are several errors**. Usually only the first one matters, the rest are fallout. Say so.

## 2. Find where it came from

This is the core of the skill. Do not stop at "what" the error is.

**From a stack trace:**
- Walk the frames from the top. Skip frames from the standard library, frameworks, engines and dependencies.
- The first frame in the user's own code is the **crash location**. Report file, line, class or function.
- Look for `Caused by:`, `During handling of the above exception`, inner exceptions or chained errors. The deepest cause is usually the real one.

**Without a stack trace:**
- Use clues in the message: file names, line numbers, keys, IDs, URLs, function names, plugin or module names.
- Say what the error means about where it *could* come from, ranked by likelihood.

**Crash location vs root cause:** the line that threw is often not the line that is wrong. A null value that crashes on line 80 may be set wrong on line 12. When the code is available, follow the bad value back to where it was created and report both.

**If the project files are available**, open the file at the reported line and read the surrounding code before concluding. Never guess at code you could have read.

**If information is missing**, ask at most 3 targeted questions, for example:
- "Can you paste `PlayerListener.java` around line 42?"
- "What were you doing right before it happened?"
- "Which version of X are you on?"

Do not ask for things the error already answers.

## 3. Explain it

Short, plain language, no jargon without a quick definition:

- **What happened** in one or two sentences
- **Where**: file, line, function, plus the root cause location if different
- **Why**: the actual reason, not a restatement of the message
- **How to fix it**: the concrete change. Show the corrected code if the original is available.

If confidence is low, say so and say what would confirm it.

## 4. Write the bug report

Output this in a single Markdown code block so it can be copied straight into a GitHub issue. The outer fence MUST use four backticks (````markdown ... ````) because the report contains a normal three backtick block for the log inside it. With three backticks outside, the block breaks.

````markdown
## Bug: <short specific title, e.g. "NPE in PlayerListener when player joins with empty inventory">

**Summary**
<one or two sentences>

**Environment**
- Version:
- OS / platform:
- Runtime / engine:
- Other relevant info:

**Steps to reproduce**
1.
2.
3.

**Expected behavior**

**Actual behavior**

**Error log**
```
<trimmed log, only the relevant part>
```

**Location**
- Crashes at: `<file>:<line>` in `<function>`
- Root cause: `<file>:<line>` (if different)

**Suspected cause**

**Possible fix**

**Severity**
<Crash / Major / Minor / Cosmetic>
````

Rules for the report:

- **Never invent facts.** Unknown fields get `Unknown` or are removed. Do not make up repro steps or versions.
- **Trim the log.** Keep the error line, the cause chain and the relevant frames. Cut repeated lines and unrelated output.
- **Wrap the log** in a fenced code block inside the report.
- **Title must be specific.** "It crashes" is not a title.

## 5. Privacy check before posting

The report is meant to be public, so scrub it before output:

- API keys, tokens, passwords, webhook URLs, connection strings
- Usernames inside file paths (`C:\Users\name\...` becomes `C:\Users\<user>\...`)
- Emails, IP addresses, server addresses, player or account names that are not needed

Replace them with placeholders like `<redacted>` and tell the user what was removed.

## Output order

1. Short explanation (what, where, why, fix)
2. Privacy warnings: list every sensitive item found in what the user pasted (webhooks, tokens, usernames in paths, IPs, player names) and say which ones need to be revoked or changed, not just hidden
3. Any questions, if something important is missing
4. The bug report block

Always include the bug report block, even when the user only asked for help and the fix is easy. If the user says they only want one part, give only that.
