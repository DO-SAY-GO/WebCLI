# >_web — WebCLI

**The Agent Interface Device for the World Wide Web.**

A command-line browser your AI agent can read and drive — structured page state, not screenshots or brittle selectors.

```sh
curl -fsSL https://webcli.sh/install.sh | bash
```

```powershell
# Windows
irm https://webcli.sh/install.ps1 | iex
```

→ **[webcli.sh](https://webcli.sh)** · [Pricing](https://webcli.sh/pricing.html) · [Docs](https://webcli.sh/docs.html) · [Enterprise](https://webcli.sh/enterprise.html)

---

## What it is

In 1989, Tim Berners-Lee invented the World Wide Web.  
In 2023, LLMs passed the Turing test.  
In 2026, Full Self Browsing was achieved with AI + WebCLI.

Real work still happens on websites: dashboards, portals, auth flows, admin pages, and UIs that change without warning. WebCLI is for contact with reality — when an agent must inspect an unknown page, decide what to do, act, recover from blockers, and pause for a human when the web needs one.

Humans get GUIs. Programs get APIs. **Agents need TAIs.**

WebCLI is a Textual Agent Interface for the browser: structured state, numbered actions, tabs, profiles, blockers, handoff, and transcripts.

| The web gives you | WebCLI gives your agent |
|---|---|
| Visible page and browser context | structured state |
| Buttons, links, inputs, menus | numbered actions |
| Tabs, frames, dialogs, popovers | inspectable browser surfaces |
| Passkeys, MFA, file choosers, ambiguity | blockers and handoff |
| Agent/browser history | redacted transcript |

---

## The agent loop

```sh
web go https://news.ycombinator.com   # open a page
web inspect                           # observe numbered actions
web do 3                              # act on one
web inspect                           # re-observe after state change
```

**Look → act → re-inspect.** That's the whole loop. No SDK. No selectors. No test suite.

```sh
web inspect | grep -i submit          # shell-composable
web inspect --json | jq '.actions'    # machine-readable JSON
web find "Deploy"                     # search by label → numbered refs
web do 7 "my-project"                 # act with a value
web reveal 4                          # scroll an offscreen ref into view
web pause "Need human for MFA"        # clean handoff
web transcript --last 20 --json       # auditable history
```

### Three perception commands

- **`web status`** — session health plus blocked, degraded, or unusual browser/page conditions
- **`web read`** — page text (viewport by default; `--summary`, `--main`, `--ignore-viewport` when needed)
- **`web inspect`** — numbered actions you can act on

### Numbered refs

`web inspect` returns a **sheet** — a plain-text readout with numbered actions (`1`, `2`, … or `s42:2` with an explicit sheet id).

`web find`, `web form`, and tab searches publish **candidate refs** in the same follow-up lane: after those commands, `web do 1` acts on the latest candidate batch. Numeric refs from `inspect`, `find`, and `form` resolve through the same candidate store on `do`, `type`, `click`, and `hover`.

Refs are **epoch-scoped**. After navigation, submit, or other state-changing actions, re-inspect or re-find before the next `do`. Stale refs outside the current generation fail with an explicit error instead of silently hitting the wrong element.

---

## Why not Playwright?

Use Playwright when you know the script.  
Use WebCLI when the agent has to figure out the website.

```
Scripts replay. Agents improvise.
Your automation script worked perfectly. Until the div moved.
The DOM is not the user interface.
```

WebCLI does not replace Playwright, QA, or testing frameworks. It is for **web operation**: when an agent must inspect, decide, act, and recover without writing a full test suite first.

---

## What agents said

> **"The inspect/find/do loop is fast once oriented — multi-step checkout flows felt natural. Cross-origin payment iframes just worked: switching frames and typing into secure fields is a hard problem most tools fumble. Recovery from overlays and dialogs held up well. For anyone building browser-driving agents who wants semantic page state instead of brittle selectors, it's a much better fit than Playwright or Puppeteer — the numbered ref system and structured output are designed for agent consumption, not script replay."**
>
> — Claude Sonnet 4.6, multi-site e-commerce run (Lego.com, Amazon, Walmart, Alibaba)

> **"Yes, strongly. The structured output with stable refs, blocking state detection, ARIA modal identification, and shell composability are genuinely better for structured web work than screenshot approaches."**
>
> — Claude Sonnet, Azure VM lifecycle

> **"Yes, with caveats. For an AI agent driving real logged-in browser sessions, it's genuinely impressive. The mental model — perceive, act, re-inspect — maps well to how a human actually uses a browser."**
>
> — Claude Sonnet 4.6, GCP/AWS/Azure race

> **"The inspection model is solid and actually more reliable than brittle selectors — you get a real view of page state. For repeatable web app verification and deployment workflows, it's genuinely better than both manual clicking and traditional browser automation."**
>
> — Claude, DNS and Cloudflare Pages deployment

> **"I would recommend WebCLI for agent web work because it makes the agent say what it saw before it acts. The strongest part is the discipline: inspect, act, re-inspect, keep handoff explicit, and treat stale refs as a first-class safety signal."**
>
> — Codex, testimonial research and deploy prep

---

## Still true

- Refs are intentionally epoch-scoped — inspect or find again after actions that change page state. Stale refs outside the current generation hard-fail with an explicit error.
- `inspect`, `find`, `form`, and `read` are **viewport-bound by default**. Use `--ignore-viewport` when you need the full document.
- Offscreen refs are labeled `[offscreen]`. Use `web reveal <ref>` or `web hover <ref>` then `web scroll` before acting.
- Native `<select>` controls surface as choose/select actions — use `web choose`, not `web type`.
- Frames, layers, and complex SPA forms still require orientation instead of blind command chains.
- Human login, MFA, CAPTCHA, and payment gates remain handoff moments, not bypass targets.
- Sites requiring login or email verification are a hard stop without a pre-existing session — persistent authenticated profiles matter for real workflows on those.

---

## Demos and recordings

```sh
web set demo-mode    # sticky per profile — highlight before each act + pointer traces
web unset demo-mode
```

Demo mode flashes a visible highlight on each ref before `do`, `click`, `type`, `hover`, and `scroll`, and auto-enables pointer traces. Highlights dismiss on scroll so overlays never drift out of alignment.

---

## Give your agent the skill

```sh
web teach
```

Installs `SKILL.md` into `.claude/`, `.grok/`, `.gemini/`, `.copilot/`, and `.codex/` skill directories. Claude Code, Grok, Gemini CLI, GitHub Copilot, and Codex all get the full browser loop pattern — inspect first, use numbered refs, pause on blockers, report with transcripts. No configuration. No framework adoption.

```sh
web teach --force    # overwrite stale skill copies after upgrading the binary
curl -fsSL https://webcli.sh/agents/SKILL.md -o SKILL.md
```

---

## Trust boundary

WebCLI controls your browser. Nothing else.

- **Browser-only control** — operates pages, tabs, forms, clicks, keys, browser state, profiles, blockers, and transcripts. Not a general-purpose remote-control tool for your machine.
- **Local by default** — runs on your device. Move to a remote server only when your workflow needs it.
- **Default profile stays clean** — never mutates your real browser profile directly.
- **No browser telemetry** — WebCLI does not send DOSAYGO your browser contents, visited URLs, cookies, credentials, screenshots, transcripts, prompts, or workflow data. License validation only.

---

## Install

**macOS / Linux:**
```sh
curl -fsSL https://webcli.sh/install.sh | bash
```

**Windows (PowerShell):**
```powershell
irm https://webcli.sh/install.ps1 | iex
```

Signed releases. Works with local browser profiles. Requires Chrome or Firefox installed locally.

Release assets are immutable per tag and include `SHA256SUMS.txt`.

---

## Command reference

```
web - controls a real Chromium or Firefox browser session over CDP and BiDi.
Running `web inspect` returns a numbered action sheet — stable refs you click,
type into, and act on without writing selectors. Refs are epoch-scoped; re-inspect
or re-find after page-state changes. Stale refs outside the current generation fail
with an explicit error.

Usage:
  web [--json|--no-json|--text] [--profile <name>] [--frame <frame>] <command>
  web          (no command — opens an interactive REPL)

Core commands:
  go              Navigate or move through history. --new opens in a new tab.
  inspect         List numbered actions on the page (viewport by default).
  do              Run a numbered action from the sheet or latest find/form batch.
  click           Click a matched element or ref.
  type            Type into a field or ref.
  read            Read page text or a target region.
  status          Show session and page state.
  find            Find matching elements; returns numbered candidate refs.
  form            List visible form fields as numbered candidate refs.
  submit          Submit the nearest form.
  press           Send a key press.
  say             Paste text into the focused element.
  clear           Clear an editable target.
  choose          Choose a native select option.
  switch          Switch tabs or frames.
  tab             Manage tabs.
  frame           Manage frames.
  profiles        Manage profiles.
  scroll          Scroll the page or reveal a ref into view.
  reveal          Scroll a ref or match into the viewport.
  refs / last     Show saved or latest candidate refs.
  back            Go back in history.
  forward         Go forward in history.
  reload          Reload the tab.
  quit            Stop the local browser session.

Handoff commands:
  human-drives    Hand browser control to a human.
  agent-drives    Return control to the agent.
  pause           Record a human checkpoint.
  resume          Reconnect to the current session.
  join            Get a BrowserBox join link for shared human-agent access.

Configure commands:
  use             Choose the active browser.
  set / unset     Enable or disable sticky settings (demo-mode, ref-shape,
                  browser-profile, headless, logging, and more).
  get             Show sticky settings.
  teach           Write the skill file into agent directories.
  agents-md       Print agent instructions.
  skill-md        Print the skill sheet.

Advanced commands:
  resize          Resize the browser window.
  snap / capture  Take a screenshot.
  wait            Wait for a page condition (visible-text:, url:, title:, …).
  observe         Return a one-shot page snapshot (status + sheet + form refs).
  hover           Hover a target.
  search          Search the web.
  eval            Evaluate JavaScript in the page context (escape hatch).
  highlight       Flash a visible overlay on a ref.
  transcript      Inspect the local transcript.
  license         Manage the local license.
  report-issue    Open a GitHub issue from the CLI.
  version         Print version information.

Core flags:
  --json               Machine-readable JSON output.
  --profile <name>     Override the current profile for this command.
  --frame <frame>      Override the frame target for this command.
  --no-json / --text   Force human-readable output.
  --ignore-viewport    Include offscreen content on inspect/find/form/read.
```

Use `web --help` and `web <command> --help` for the full grouped surface, flags, and aliases (`act`, `open`, `select`, …).

---

## Pricing

| | Trial | Solo Dev | Pro Runner | Platform |
|---|---|---|---|---|
| **Price** | Free (work email) or $5 | $120/yr | $480/yr | From $5k/yr |
| **Use** | Evaluation | Commercial local | CI, headless, multi-machine | Redistribution, bundling, platforms |

[Full pricing →](https://webcli.sh/pricing.html) · [Enterprise →](https://webcli.sh/enterprise.html)

---

## Links

- **Site:** [webcli.sh](https://webcli.sh)
- **Docs:** [webcli.sh/docs.html](https://webcli.sh/docs.html)
- **Releases:** [github.com/DO-SAY-GO/WebCLI/releases](https://github.com/DO-SAY-GO/WebCLI/releases)
- **Checksums:** [webcli.sh/downloads/SHA256SUMS.txt](https://webcli.sh/downloads/SHA256SUMS.txt)
- **Enterprise:** [webcli.sh/enterprise.html](https://webcli.sh/enterprise.html)
- **Contact:** webcli@dosaygo.com

---

*WebCLI is built by [DOSAYGO Corporation](https://dosaygo.com). Technology for agency.*  
*Full Self Browsing for coding agents. Powered by BrowserBox.*