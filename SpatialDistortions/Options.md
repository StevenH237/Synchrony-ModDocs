This is a simple guide to the options of Spatial Distortions.

There are both [Options](#options) and [Custom Rules](#custom-rules).

# Options
**Final floor warning text**: Controls whether or not a warning label should appear on the final floor (as in the order played) of the dungeon.

# Custom Rules
## Floor order
* **Forward**: Forces each floor (per zone) to appear in order, i.e. x-1 MUST appear before x-2 can appear. The various zones may still mix with each other.
* **Reverse**: Same, but in reverse order, i.e. x-4 MUST appear before x-3.
* **Random** (default): This constraint does not apply.

## Zone order
* **Forward**: Forces each floor to not appear until the same floor in the previous zone has appeared, i.e. 1-2 MUST appear before 2-2. The floors may still mix with each other, i.e. 2-1 may appear anywhere around 1-2 and 2-2.
* **Reverse**: Same, but in reverse order, i.e. 4-2 MUST appear before 3-2.
* **Random** (default): This constraint does not apply.

## Clustering
* **Zone**: Once a floor appears, all floors from the same zone must immediately follow (in any order) before any other floors appear; i.e. 1-1, 1-2, 1-3, and 1-4 must all appear consecutively (but not necessarily in that order).
* **Level**: Same, but cluster the floors of a zone instead; i.e. 1-1, 2-1, 3-1, 4-1, and (if you're playing Amplified) 5-1 must all appear consecutively (but not necessarily in that order).
* **None** (default): This constraint does not apply.

## Preserve boss alignment
If checked, bosses will appear in the same locations as before the dungeon is randomized.

## Force single final boss
If checked, in a run with multiple bosses at the end of the final depth, one boss will be chosen at random to be 5-4 with the remaining boss floors discarded.

Even if not checked, the following combinations of settings will force it anyway:
* Zone order isn't Random
* Clustering is by Level
* Clustering is by Zone, with Preserve Boss Alignment enabled