# FuckUI

**A REPL for browsers. It makes the live web legible and actionable to AI agents.**

Humans get GUIs. Programs get APIs. Agents get FuckUI.

FuckUI gives coding agents structured page state and numbered actions instead of screenshot-only loops, raw HTML dumps, or brittle selectors. Your agent can inspect a real Chrome or Firefox session, act on the current page, recover from UI changes, and pause cleanly when a human must take over.

**[Start a 5-day full trial](https://fuckui.com/#trial)** · [Watch the demos](https://fuckui.com/#demo) · [Read the docs](https://fuckui.com/docs.html) · [See pricing](https://fuckui.com/pricing.html)

## See it work

- [Three clouds, one browser loop](https://www.youtube.com/watch?v=7ukeFRJyF9I) — Azure, AWS, and GCP consoles without cloud SDK scripts.
- [An agent submitted a Y Combinator application end to end](https://www.youtube.com/watch?v=FnV_VFnCtAc).
- [Flights, car, and three hotels booked in one session](https://www.youtube.com/watch?v=b0UtTs6iLZg).

## Install

macOS and Linux:

```sh
curl -fsSL https://fuckui.com/install.sh | bash
```

Windows PowerShell:

```powershell
irm https://fuckui.com/install.ps1 | iex
```

Then teach your coding agent the browser loop:

```sh
web teach
```

This installs the FuckUI `SKILL.md` for supported agent environments, including Claude Code, Codex, Gemini CLI, GitHub Copilot, and Grok.

## The browser loop

```sh
web go https://news.ycombinator.com
web inspect
web do 3
web inspect
```

1. **Inspect** — `web inspect` returns the current page as a compact, numbered action sheet.
2. **Act** — `web do N`, `web type N "value"`, and `web scroll until "text"` operate on what the agent can actually reach.
3. **Re-inspect** — page-changing actions create a new epoch, so stale refs fail explicitly instead of silently targeting the wrong element.
4. **Hand off when needed** — on MFA, CAPTCHA, passkeys, or final approval, the agent pauses; the human completes the step; the same browser session resumes.

`web`, `fu`, `fui`, and `fuckui` are aliases for the same CLI.

## Why agents use it

- **Structured state, not pixels alone.** Agents receive concise, semantic actions instead of repeatedly interpreting screenshots.
- **Numbered, epoch-scoped refs.** Actions are easy to reason about and stale references are rejected.
- **Real authenticated sessions.** Persistent local browser profiles support sites behind SSO and login flows.
- **Frames, overlays, dialogs, and scroll panels.** The action sheet surfaces the UI layers agents routinely miss.
- **Explicit human handoff.** FuckUI does not claim to bypass authentication or CAPTCHAs.
- **Shell-native and framework-independent.** Any coding agent that can run commands can use it.
- **Auditable runs.** Redacted transcripts make browser work inspectable without sending page contents to an AI telemetry service.

Use Playwright or Selenium when you already know the exact script and want to replay it. Use FuckUI when the agent must inspect an unfamiliar live site and decide what to do next.

## The 5-day trial

Most people receive the same full 5-day trial for **$0**, with no card required. This includes Gmail, Outlook, Yahoo, iCloud, higher-education, and work addresses.

A **$5 trial pass** applies only in limited cases: other generic free or disposable email providers, repeat trials, exhausted address or organization allocations, or an unavailable global free-trial allocation. The $5 pass unlocks the same full trial; it is not a reduced tier.

Trial guardrails are 5,555 browser commands total and 2,000 commands per UTC day.

| Plan | Price | Best for |
|---|---:|---|
| 5-day full trial | $0 for most people; $5 in limited cases | Evaluating the complete browser loop |
| Solo Dev | $120/year | One developer using local browser sessions |
| Pro Runner | $480/year | Headless, CI, and runner workflows |
| Platform | From $5,000/year | Redistribution, embedding, and managed services |

**[Check your trial eligibility](https://fuckui.com/#trial)**

## What agents said

> “It filled out and submitted its own YC application, end to end. That’s not a pitch; that just happened.”
>
> — Claude Opus 4.8, after submitting DOSAYGO’s Y Combinator application

> “The numbered ref system gives a model something stable to reason about … If you’re building agents that need to operate a real browser, this is the tool.”
>
> — Claude, after booking a flight across four portals

More session reports and full context are available on the [FuckUI homepage](https://fuckui.com/#agent-testimonials).

## Trust boundary

FuckUI controls a browser session. It does not grant an agent broader machine access.

- Browser execution is local by default.
- Visited URLs, page contents, prompts, and workflows are not sent to FuckUI telemetry.
- License activation and metering send license state and aggregate command counts, not browsing content.
- Transcripts are redacted by default.
- The agent must still respect site terms, authorization boundaries, and confirmation requirements.

## Learn more

- [Documentation](https://fuckui.com/docs.html)
- [Full product overview](https://fuckui.com/web-cli-overview.html)
- [Downloads](https://fuckui.com/download.html)
- [Enterprise and platform use](https://fuckui.com/enterprise.html)
- [Terms](https://fuckui.com/terms.html) and [EULA](https://fuckui.com/eula.html)

Built by [DOSAYGO Corporation](https://dosaygo.com). Product and business enquiries: [webcli@dosaygo.com](mailto:webcli@dosaygo.com).
