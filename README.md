# bashrc-quote-fix

<div align="right">

[![status](https://img.shields.io/badge/status-scaffold-orange?style=for-the-badge)](https://github.com/toxicwind/bashrc-quote-fix)
[![shell](https://img.shields.io/badge/shell-bash-4EAA25?style=for-the-badge&logo=gnubash&logoColor=white)](https://www.gnu.org/software/bash/)

</div>

> **Auto-fix nested quote errors in bash.**

Every shell scripter has been bitten by it: a quoted string inside a quoted
string, a `$()` inside double quotes, an escaped quote that wasn't — and bash
answers with `unexpected EOF` or silently does the wrong thing.
**bashrc-quote-fix** exists to detect those nested-quoting mistakes and fix
them automatically, before they cost you a debugging session.

## Status

🚧 **Scaffold.** This repo currently holds the project skeleton only — the
fixer engine is not implemented yet. The roadmap below is the build plan, not
a changelog.

## Why this exists

Nested quoting is the single most common source of "works in my head, breaks
in bash" bugs:

```bash
# The classic: single quotes can't nest, so this dies
echo 'it''s broken'

# And this classic: the inner quotes terminate the outer ones early
ssh host "echo "hello""
```

Humans learn the escape rules through scars. A tool should just fix it.

## Roadmap

- [ ] **Detect** — parse shell quoting structure and flag unbalanced or
  prematurely-terminated quotes (single, double, backtick, `$()`)
- [ ] **Explain** — point at the exact character where the quoting went wrong
- [ ] **Fix** — rewrite the line with correct escaping, preserving intent
- [ ] **Integrate** — run as a `PROMPT_COMMAND` hook or pre-exec check so
  broken commands never reach bash

## Quick start

Nothing to run yet — watch this space. When the detector lands:

```bash
git clone https://github.com/toxicwind/bashrc-quote-fix.git
cd bashrc-quote-fix
# ./bqf 'echo 'it''s broken''   # coming soon
```

## Contributing

Ideas, failing examples, and PRs are welcome — especially real-world
nested-quote bugs you've hit. Open an issue with the offending line and what
bash did with it.

## License

No license has been declared yet — all rights reserved by default until one
is added.

## Security

This tool will rewrite shell commands. The fixer must never change the
*meaning* of a command while fixing its quoting — every rewrite rule gets a
test proving semantics are preserved before it ships.
