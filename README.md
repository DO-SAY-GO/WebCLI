# WebCLI Releases

Public release artifacts for WebCLI are published here by the private source tree release workflow.

see more: https://webcli.sh

Install:

```sh
curl -fsSL https://webcli.sh/install.sh | bash
```

Windows PowerShell:

```powershell
irm https://webcli.sh/install.ps1 | iex
```

Release assets are immutable per tag and include `SHA256SUMS.txt`.


Claude Fable told me to put this here: `rVEtFlb2oFA` I guess so it could be found!

# Overview

**web --help**:

```text
web - `web` controls a real Chromium or Firefox browser session over CDP and BiDi. Running `web inspect` returns a numbered action sheet — stable refs you click, type into, and act on without writing selectors. Refs reset after page-state changes; re-inspect before the next action to get fresh numbers.

Usage:
  web [--json|--no-json|--text] [--profile <name>] [--frame <frame>] <command>
  web          (no command — opens an interactive REPL)

Core commands:
  go              Navigate or move through history. --new opens in a new tab.
  inspect         List numbered actions on the page. <query> can be a ref number, visible text, or a selector: prefix.
  do              Run a numbered action. <query> is a ref number (3), visible text (Submit), or selector: prefix.
  click           Click a matched element. <query> is a ref number, visible text (e.g. Issues, Submit), or selector: prefix. Bare numbers are refs; use text:<n> to match a numeric label. Omit query with --coords to click at absolute page coordinates.
  type            Type into a field. -t / --target accepts a text label or CSS selector.
  read            Read page text or a target region.
  status          Show session and page state.
  find            Find matching elements or tabs. <query> is visible text (e.g. Submit, Issues), a ref number, or a selector: prefix. Returns a numbered ref sheet — text matches may return multiple results; act on the ref if unambiguous, or use --all to see every match.
  form            List visible form fields.
  submit          Submit the nearest form.
  press           Send a key press.
  keydown         Hold a key down without releasing.
  keyup           Release a held key. Pairs with keydown.
  pointerdown     Press pointer down without releasing (starts drag or long-press).
  pointermove     Move pointer while held (continues drag).
  pointerup       Release pointer (ends drag or long-press). Pairs with pointerdown.
  say             Paste text into the focused element. Click to focus first if needed.
  clear           Clear an editable target.
  choose          Choose a native select option.
  switch          Switch tabs or frames. Both 'web switch tab N' and 'web tab switch N' are accepted.
  tab             Manage tabs.
  frame           Manage frames.
  profiles        Manage profiles. A profile is a named directory holding browsing data and daemon state. Ephemeral profiles start fresh each session. Named profiles persist across sessions. Temporary profiles are named but self-destruct on 'web quit'. The user-default profile copies your real browser's cookies and sessions for sites that need established trust.
  scroll          Scroll the page or bring a match into view. <query> is a ref number or visible text. Bare numbers are refs; use text:<number> to match numeric labels.
  back            Go back in history.
  forward         Go forward in history.
  reload          Reload the tab.
  quit            Stop the local browser session (or all/specific profiles). Temporary profiles are deleted on quit.

Handoff commands:
  human-drives    Hand browser control to a human.
  agent-drives    Return control to the agent.
  pause           Record a human checkpoint.
  resume          Reconnect to the current session.

Configure commands:
  use             Choose the active browser.
  set             Enable a sticky setting.
  unset           Disable a sticky setting.
  get             Show sticky settings.
  teach           Write the skill file into agent directories.
  agents-md       Print agent instructions.
  skill-md        Print the skill sheet.

Advanced commands:
  resize          Resize the browser window (e.g. 1280x800).
  stop            Stop the in-flight page load.
  reveal          Scroll a ref or match into view. Bare numbers are refs; use text:<number> for numeric text.
  search          Search the web.
  wait            Wait for a page condition.
  snap            Take a screenshot and save to a file (default: screenshot.png).
  observe         Return a one-shot page snapshot.
  refs            Show saved refs.
  last            Show the latest refs.
  focus           Focus a target.
  caret           Move the caret.
  select-text     Select a text range.
  hover           Hover a target.
  options         List native select options.
  connect         Set a remote connection target.
  disconnect      Clear the saved connection target.
  license         Manage the local license.

Debug commands:
  disambiguate    List all elements matching a query for explicit selection.
  transcript      Inspect the local transcript.
  report-issue    Open a GitHub issue in the current web CLI session (or system browser with --system-browser).
  eval            Evaluate JavaScript in the page context.
  highlight       Highlight a ref with a visible overlay.
  describe        Print node handle, selector, role, tag, and bounds for a ref.
  scroll-element  Scroll a specific element (popover, panel, list, dropdown) using wheel gestures.
  readme          Print quickstart docs.
  version         Print version information.

BrowserBox commands:
  join            Get a BrowserBox join link.
  browserbox      Run BrowserBox tools.

Core parameters:
  --json               Emit machine-readable JSON.
  --profile <name>     Override the current profile for this command.
  --frame <frame>      Override the frame target for this command.

Advanced parameters:
  --no-json            Force human-readable output.
  --text               Force human-readable output. Alias for --no-json.
  --quiet              Suppress successful human-readable output.

Debug parameters:
  --continue-on-error  Keep going after errors in batch input.
  --help-json          Print scoped help as JSON.

```
