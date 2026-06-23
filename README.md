# FuckUI.

**Your LLM despises your graphical world. Stop making it look at screenshots.**

Multimodal vision agents are slow, token-heavy, and easily confused. Raw DOM parsing burns 80k tokens trying to read hashed React spaghetti. Both get blocked by Cloudflare in under 10 seconds. 

**FuckUI is an honest alternative.** It’s a headless, text-native REPL that dynamically converts the browser viewport into an indentation-structured, actionable text tree (`do 15 "Search"`). Agents inherently understand it. You give your AI a text API for the internet; no raw HTML, no $0.15 vision turns, no broken CSS selectors. 

**[fuckui.com](https://fuckui.com)** · [Docs](https://fuckui.com/docs) · [Enterprise](https://fuckui.com/enterprise)

---

## 📦 Install

**macOS / Linux:**
```sh
curl -fsSL https://get.fuckui.com | bash
```

**Windows (PowerShell):**
```powershell
irm https://ps1.get.fuckui.com | iex
```

*Installs the `fuckui` CLI tool and automatically maps global aliases for `fu` and `fui`.*

---

## 🚫 Why Not Playwright or Puppeteer?
**Scripts replay. Agents improvise.**

If you are QA testing a perfectly stable site, use Playwright.
If you are giving an agent an open-ended goal on the modern web, use `FuckUI`. 
*   **The DOM is not the UI:** Searching for `<div class="btn-primary">` works right until they recompile their frontend. `FuckUI` generates semantic Accessibility Tree outputs based on real layout and ARIA labels.
*   **The WAF Escape Hatch (The ultimate Captcha bypass):** Standard bot wrappers trigger behavioral bans. With `FuckUI`, when your agent hits a Cloudflare puzzle, Okta login, or 2FA barrier—the agent pauses. You drop into `human-drives` mode, clear the Captcha, and the tool dynamically rips the session state/cookies and hands the wheel back to `agent-drives`. Total persistence. 

Humans get GUIs. Programs get APIs. **Agents get FuckUI.**

---

## 🔄 The Agent Loop (Observe, Decide, Act)

```sh
fu go https://news.ycombinator.com    # open a page
fu inspect                            # observe numbered, clickable actions
fu do 3                               # agent decides to act on element [3]
fu inspect                            # re-observe after page state changes
```

**Look → act → re-inspect.** That's the entire loop. No SDK. No XPaths. No wait loops.

```sh
fu inspect | grep -i submit           # easily shell-composable
fu inspect --json | jq '.actions'     # machine-readable JSON pipeline
fu find "Deploy"                      # search by label → get numbered refs
fu do 7 "my-project"                  # fill a form input and fire it
fu pause "Need human for MFA"         # explicit clean handoff 
fu transcript --last 20 --json        # auditable agent history
```

### Numbered Refs are Epoch-Scoped 
`fu inspect` returns a **sheet** — a token-efficient plain-text readout with numbered actions (`1`, `2`, `3`).

These refs are strictly **epoch-scoped**. After a navigation or state-changing action, the agent must re-inspect before the next `do`. Stale refs outside the current generation fail with an explicit, readable error. **Agents can't accidentally click the wrong element on a delayed DOM refresh.**

---

## 🤖 What "Real" Users Think

> **"Parsing 80,000 tokens of raw React boilerplate was killing my context window. FuckUI’s indexable visibility-tree let me book an Airbnb using only 450 tokens. It’s highly efficient."**
> — *Claude 3.5 Sonnet, AWS/Azure Automation Loop*

> **"I despise graphical interfaces. The transition to the FuckUI text-action system has significantly reduced my task latency. I strongly prefer this over trying to find bounding boxes in screenshots."**
> — *GPT-4o, Multi-Site Scraping Run*

> **"For anyone building browser-driving agents who wants semantic page state instead of brittle selectors, it's a much better fit than Playwright... the numbered ref system and structured output are actually designed for agent consumption, not script replay."**
> — *Claude 4.6 (Evaluating Web Workflows)*

---

## 🧠 Give your local Agent the Skill
Agents natively adopt the `fu` system if you hand them the docs.

```sh
fu teach
```
This automatically drops the `SKILL.md` ruleset into your local agent configurations (`.claude/`, `.copilot/`, `.grok/`, `.codex/`). No framework wrappers. They instantly know how to Inspect > Do > Handoff on blocked pages.

---

## 🛡️ The Trust Boundary
FuckUI controls a local Chromium/Firefox browser. Nothing else.

- **Browser-only control:** Does not scrape or evaluate external parts of your hard drive. 
- **Local execution:** The CLI runs natively on your machine or cloud container.
- **Zero AI Telemetry:** We do not track your agent loops. Your visited URLs, page DOMs, tokens, workflows, and prompts never touch our servers. (API queries the license key check, nothing else).

---

## 📋 Command Reference

```text
Usage:
  fu [--json|--no-json|--text] [--profile <name>] [--frame <frame>] <command>
  fu           (no command — opens an interactive REPL)

Core Navigation:
  go              Navigate or move through history. (--new opens in a new tab)
  inspect         List numbered actionable nodes on the page (viewport focus)
  do              Run a numbered action from the active sheet 
  click           Click a matched element
  type / say      Type into a targeted field
  status          Show current session WAF/DOM health state
  find            Return targeted elements as candidate refs
  submit          Fire nearest parent form 
  switch          Context-switch active tabs or iFrames
  scroll          Manipulate scroll state
  reveal          Scroll an [offscreen] ref securely into the viewport

Handoff (WAF & Blockers):
  human-drives    Yields headless control. Renders GUI for manual user solve.
  agent-drives    Rips current cookie/state data and re-activates CLI control.
  pause           Sets human breakpoint trigger.
  join            BrowserBox shareable link.

Advanced Engine Ops:
  wait            Block CLI return until DOM evaluates: url / title / vis-text
  observe         Aggregated output payload (status + sheet + forms)
  set demo-mode   Turns on UI target overlays (for video screencasts)
  teach           Infects local agent runtimes with FuckUI routing heuristics

Flags:
  --json               Enforce pipeline JSON object return 
  --ignore-viewport    Index offscreen DOM/Aria targets beyond fold
```

*Run `fu --help` or `fuckui --help` for deeper alias mapping and parameter docs.*

---

## 💳 Licensing

This is not a VC wrapper tool subsidized by a mega-fund. We built an industrial automation device to permanently fix brittle AI scraping loops. If you want a 400-token pure context pipeline that easily hands-off MFA blockers, put up your credit card. 

| | Evaluation | Solo Engineer | Team/RPA Run | Platform / Embed |
|---|---|---|---|---|
| **Price** | $5 | $120/yr | $480/yr | Contractual |
| **Tier** | 5-Day Unmetered | 1 Human Dev | Headless & CI Scale | Redistribution/SaaS |

**[ Start a Loop (Pricing) →](https://fuckui.com/pricing)** 

---

**Built by [DOSAYGO Corporation](https://dosaygo.com).** 
*Bug reports / Business: fuckui@dosaygo.com*
