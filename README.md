# SnapChart
A flowchart as code with timeline

# Enhancements for next version

I think at that next step we really start to get into a more full-fledged application.  Things such as UNDO, REDO ; Probably a side window of the code but the tricky part is delivering an experience where if someone knows the code they could easily modify there (and copy paste within it)  but the ability to add/insert objects with mouse ; insert arrows with mouse ; click on links and add text all of those things would really bring it to a pretty polished state
Possibly real time collaboration



Considerations
What you're describing is a split-pane diagram IDE. Left side: live visual canvas with mouse interactions. Right side: the code/text representation. Both stay in sync — edit the code, diagram updates; click-drag on canvas, code updates. That's exactly what Mermaid.live does and why it felt closer to a real tool — the code pane is your power-user escape hatch, the canvas is your human interface, and neither is the "real" version.
The interaction primitives you listed:

Undo/redo — fundamental, can't ship without it
Click node to select, double-click to rename — already partially there
Drag to move nodes
Click-drag between nodes to draw edges
Click edge to add label
Code pane — editable, live-syncing, copyable
Add node via canvas (not just a bottom button)

That's roughly a 3-4 week build to do properly. Not a one-session applet anymore — it's an application.

The collaboration idea is interesting and not as far as it sounds. The simplest version isn't real-time sync (which is genuinely hard — CRDTs, conflict resolution, websockets). The simplest version is what Git already does: each person has a named snapshot, and a "compare" view renders them side by side or diff-highlighted. You already have the timeline infrastructure for exactly this. Instead of snapshots being "2024-01 → 2024-04", they're "Matt's version → Alex's version → Sarah's version." The overlay rendering where each person's divergent nodes get a colour-coded tint is very achievable.
The Figma model of "multiplayer cursors + shared canvas" is the full version and is a different class of problem entirely.

My honest suggestion on sequencing:
Rather than adding more to the self-contained HTML applet, this is the point where the right move is probably to stop building one-shot HTML files and think about what the actual stack should be. A proper split-pane diagram IDE wants:

A persistent data store (even just flat files + the manifest model)
A proper component structure (React makes the split-pane sync much cleaner)
Served from your nginx stack like the other tools

Which means the next session probably shouldn't be "let me add undo/redo to the HTML file" — it should be scoping what the v1 application architecture looks like and building the first real version of it properly.





#v2



Interactive editing: The lightest useful version is:

Click any node label to rename it inline
The ⊕ expand button on a node opens a simple panel to define the sub-flow (or link to an existing one)
A small "add node" button at the bottom of each flow
Changes auto-save to the active FLOWS snapshot
The two features interact nicely — you edit the current snapshot, which gets recorded as a new version on the timeline. So the editing produces the timeline history rather than it being hand-authored.




Timeline slider — bottom bar with four dots plus a "live" dot. Click any dot or use ←/→ arrow keys to scrub through the four snapshots:

2024-01 — just a linear pipeline, no sub-flows
2024-04 — classify becomes expandable, basic classification flow appears
2024-07 — quarantine becomes its own drillable sub-flow
2024-10 — vendor flow added, full system
live — editable working copy
Watch the root diagram — in 2024-01 "Classify email" is a plain process node. By 2024-04 it has the ⊕ drill indicator. That's the versioning concept made visible.

Inline editing (live mode only):

Double-click any process node to rename it inline — an input appears positioned over the node, Enter commits, Esc cancels
"+ add step" button at the bottom of any flow adds a new process node and immediately opens it for naming
"⊕ Snapshot" button in the header commits the current state as a new timeline entry
When viewing history the "History view" badge appears and editing is disabled. "Return to live ↑" snaps back.

On next steps — the most natural beta test would be: replace the email example with one of your actual network flows. The routing or firewall zone logic would be a good candidate. Drop your real node labels in and see if the drill-down structure actually matches how you think about the problem. That'll surface what the tool needs that it doesn't have yet.

#v1 
- Basic flowchart with ability to drill into a child node for subprocess