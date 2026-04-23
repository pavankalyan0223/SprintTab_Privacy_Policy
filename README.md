# SprintTab

SprintTab is a Manifest V3 Chrome extension for collecting short-lived research fragments while you browse.
It keeps everything local (IndexedDB + `chrome.storage.local`) and organizes captured content into a focused sidebar workflow.

## What SprintTab does

SprintTab is a private, local-first workspace for research while browsing.

- Save pages to a 7-day sprint list so your backlog stays short and focused.
- Clip text instantly from any page with `Alt+C`.
- Re-highlight your saved clips when you revisit the same URL.
- Keep writing in Notes while clips continue to flow in.
- Open floating quick-history cards over the page for recent clips.
- Create and save sticky notes directly on the page with `Alt+N`.
- Search everything locally (sprint items + clips) with no server calls.

## Core features

### Sprint tab

- Save current page from the sidebar.
- Card UI with:
  - page title + domain
  - 7-day countdown
  - progress bar
  - aging/archive visual states
- Automatic cleanup via `chrome.alarms`:
  - 5+ days -> marked aging
  - 7+ days -> moved to archived store
- Simple list virtualization when items exceed 50.

### Notes tab

- Edit view for writing and collecting clips.
- Site Links view with source links for clips.
- Sticky Notes view to browse saved sticky-note cards.
- Removing a link in Site Links removes that link only (does not mutate note text).
- Auto-save to `chrome.storage.local` (debounced).
- Copy button for quick export of notes text.

### Search tab

- Fast local search (no network).
- FlexSearch Document index over `title`, `text`, and `url`.
- Debounced query updates.
- Result cards show source badge, domain, and date.
- Clip result opens source page and scrolls to first matching highlight.
- Index cache persisted in `chrome.storage.local` and rebuilt from live DB data.

### Content scripts

- `clipper.ts`
  - listens for clip/history/sticky-note commands
  - saves selected text as clip
  - shows "Clipped to sidebar" toast
  - renders Quick History HUD cards (drag, resize, scroll-aware text)
  - renders Sticky Note HUD card (edit, navigate, save)
- `highlighter.ts`
  - fetches clips for current URL
  - highlights matching text with `mark.js`
  - supports SPA re-highlighting with debounced `MutationObserver`
  - listens for `SCROLL_TO` and pulses first highlight

## Keyboard shortcuts

- `Alt+C` -> clip selected text
- `Alt+H` -> show quick history HUD
- `Alt+S` -> open sidebar and switch to Notes
- `Alt+N` -> open sticky note card
- Extension shortcuts page: `chrome://extensions/shortcuts`

## Privacy Policy

https://gist.github.com/pavankalyan0223/f55cb1b3f3f239d6a43224dc4c9dad6e
