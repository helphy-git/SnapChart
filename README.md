# SnapChart
A flowchart as code with timeline

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