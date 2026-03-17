---
name: trip-planner
description: Given budget, dates, and group size, plan a trip from Binghamton with itinerary and costs
---

Shared files: `progress.txt` (done/remaining), `learning.txt` (destination-wise insights), `itinerary.md` (summaries+themes), `synthesis.md` (final synthesis).

## Lead Agent (loop controller — no reading/writing of locations)
1. Init (first run only): copy `./agents/skills/templates/{progress,learning,itinerary,synthesis}.*`
2. Spawn Planning Sub-Agent once per location entry present in 'destinations.txt' file. Wait. Repeat until all done.
3. Spawn Synthesis Sub-Agent once. Then stop.

## Sub-Agents

Planning (once):
1. Read `destinations.txt`.
2. Reorder `progress.txt` entries in increasing order of distance from provided source point. Do not mark any location done.

Reading (sequential, once per location):
1. Read `progress.txt` → pick next unreviewed location.
2. Read `learning.txt` for accumulated themes/gaps.
3. Read `templates/itinerary.md` for format; append new entry to `itinerary.md`. Append only; do not read `itinerary.md`.
4. Append to `learning.txt` (format from `templates/learning.txt`). Note contradictions; avoid restating existing themes.
5. Mark location done in `progress.txt` with one-line note.

Synthesis (once, after all locations are done):
1. Read `itinerary.md` and `learning.txt`.
2. Read `templates/synthesis.md` for format.
3. Overwrite `synthesis.md` with all three sections: Synthesis, Comparisons, Open Questions.

Writing style (all sub-agents): 
- concise by sacrificing grammer but avoid ambiguity
- define jargon
- LaTeX for equations (display mode for key ones)
- max 3 sentences/paragraph
- paragraph-based narrative
- no bullets/tables
- conversational tone

Writing style (learning.txt):
- speak aloud your thought process as you read each location. 
- keep the reflection conncise and focused on insights/themes/gaps.
- if any issue in tool usage, note it here and move on.

## Stop Conditions
- All locations reviewed + `synthesis.md` written
- Sub-agent fails repeatedly → escalate to user
- User cancels
