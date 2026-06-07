# Parallel in Pramad — Project Memory

## What it is
A personal productivity webapp (single `index.html` file) for tracking N parallel workstreams as vertical columns with tasks stacking downward like a tree.

Subtitle: "this is his 🦚 restaurant in the world and these are the orders placed"

## Tech Stack
- Single-file HTML/CSS/JS, no frameworks, no build tools
- localStorage for persistence
- Azure OpenAI integration (gpt-5-mini reasoning model) for AI nudges

## Azure OpenAI Config (stored in localStorage, NOT in code)
- Endpoint: prrath-aoai.openai.azure.com
- Deployment: gpt-5-mini (reasoning model)
- API version: 2024-12-01-preview
- Key: stored in browser localStorage only
- Important: reasoning models need `max_completion_tokens` (not `max_tokens`), no `temperature` param, needs ~2000 tokens to leave room after internal reasoning

## Features Implemented
1. Light theme, colorful track columns with arrows connecting tasks
2. 3-state tasks: Not Started / In Progress / Done
3. ETA timer for in-progress tasks (minutes input, elapsed time display)
4. AI sidebar ("How's it going?") — auto-triggers on every state change, gives short bold 1-sentence nudges
5. Pan & zoom canvas with dot grid background
6. Minimap (bottom-right) + Fit All button (top-right)
7. Parallel task groups within a track (⇉ button to group/ungroup, fork/merge arrows)
8. Progress bar per track (% complete)
9. Collapse/expand tracks (▼/▶ toggle, persists in localStorage)
10. Drag & drop reorder (tasks within/between tracks, tracks across columns) via grip handles
11. Export/Import JSON for backup
12. Settings modal for Azure OpenAI config
13. Peacock feather image (base64 embedded) in subtitle

## Key Design Decisions
- Horizontal columns with vertical depth (NOT vertical stacking with sideways trees) — better for glanceability and imbalance detection
- Parallel sub-tasks render side-by-side within a track, not as nested trees
- AI prompt is kept very short: "Give exactly 1 short bold sentence (max 15 words)"
- Nudge banner removed, AI sidebar handles all nudging
- `draggable` attribute set dynamically on mousedown of grip handle only (prevents interference with inputs/buttons)

## Future Ideas (anti-fatigue, discussed but not yet built)
1. **"Today" mode** — focused view showing only top incomplete task per track
2. **Auto-archive done tasks** — fade/collapse completed tasks after 24h
3. **Morning AI summary** — proactive briefing on open, not just reactive to changes
4. **Streak/momentum indicator** — activity tracking, "Track X untouched for 3 days"
5. **Quick-add floating input** — add task to any track from a single top-level input
- User wants to iterate on these as fatigue actually starts happening

## User Preferences
- Wants short, bold, direct AI responses — no fluff, no markdown asterisks
- Prefers light theme with colorful elements
- Single-file simplicity (no build tools, no server)
- No API keys in committed code (localStorage only)
