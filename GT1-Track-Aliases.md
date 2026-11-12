# GT1 track aliases

`gt2-tools gt1 import-course --course NAME` and the recipe's `course = "NAME"` take either a short alias or GT1's
own internal course name (the "stem") from the GT1 disc's `SYSTEM.DAT`. The GT1 disc is Gran Turismo (USA) v1.1,
SCUS-94194.

## Aliases

| Alias | GT1 stem | Display name the importer uses |
|---|---|---|
| `ssr11` | `outbahn` | Special Stage Route 11 (GT1) |
| `ssr11r` | `rev_outbahn` | Special Stage R11 Reverse (GT1) |
| `ssr5` | `highway` | Special Stage Route 5 (GT1) |
| `clubman` | `shortway` | Clubman Stage Route 5 (GT1) |
| `gvs` | `circuit` | Grand Valley Speedway (GT1) |
| `gve` | `short` | Grand Valley East (GT1) |
| `autumn` | `autumn` | Autumn Ring (GT1) |
| `autumn-mini` | `mini` | Autumn Ring Mini (GT1) |
| `hsr` | `testline` | High Speed Ring (GT1) |
| `deep-forest` | `test_in2` | Deep Forest (GT1) |
| `trial-mountain` | `mountain` | Trial Mountain (GT1) |

GT2 course names hold at most 31 characters. `--name` sets the name written into the slot's course record.
`"Special Stage Route 11 Reverse (GT1)"` does not fit, which is why the reverse alias says "R11".

Reverse layouts have no alias. Use the stem: `rev_circuit`, `rev_short`, `rev_autumn`, `rev_mini`, `rev_highway`,
`rev_shortway`, `rev_outbahn`, `rev_testline`, `rev_test_in2`, `rev_mountain`.

## Every stem on the GT1 disc

63 entries, in disc order. Most are arcade, 2-player and hi-fi versions of the same tracks.

```
circuit rev_circuit 2p_circuit arcade_circuit short rev_short arcade_short 2p_short autumn rev_autumn arcade_autumn
2p_autumn mini rev_mini arcade_mini 2p_mini highway rev_highway arcade_highway 2p_highway hifi_highway shortway
rev_shortway arcade_shortway 2p_shortway hifi_shortway outbahn rev_outbahn arcade_outbahn arcade_rev_outbahn
2p_outbahn hifi_outbahn testline rev_testline test_in2 rev_test_in2 mountain rev_mountain speed maxspeed
2p_testline 2p_test_in2 2p_mountain arcade_testline arcade_test_in2 arcade_mountain TC_lisence TC_lisence
DF_lisence DF_lisence DF_lisence HSR_lisence HSR_lisence DF_lisence_2 autumn_license gv1_license TMt_lisence
gv2_license DF_lisence_3 gv4_license gv3_license rogotest end
```

## Which ones import today (2026-11-11)

Each main course was run through the import into the A-Spec Max Speed slot with the same options as the SSR11
patch: `--slot maxspeed --sky highway --target ps1 --pit keep`.

These are build-time checks only: the course size, the video memory, the drawing load against GT2's busiest
shipped course (2,908 primitives), and the importer's validator. **Only SSR11 has been driven on GT2's own code.**
Every other course is untested in an emulator.

| Stem | Length | .tro bytes (limit 700,000) | Peak primitives | Result |
|---|---|---|---|---|
| `circuit` / `rev_circuit` | 4,960 m | 682,576 / 685,924 | 1,770 / 1,682 | Passes |
| `short` / `rev_short` | 3,025 m | 487,780 / 485,720 | 1,809 / 1,681 | Passes |
| `autumn` / `rev_autumn` | 2,950 m | 514,848 / 509,724 | 1,756 / 1,859 | Passes |
| `mini` / `rev_mini` | 1,255 m | 228,376 / 228,508 | 1,638 / 1,702 | Passes |
| `outbahn` / `rev_outbahn` | 4,891 m | 696,868 / 697,428 | 1,103 / 1,106 | Passes (13 far detail models dropped to fit) |
| `testline` / `rev_testline` | 3,100 m | 312,684 / 313,076 | 1,988 / 2,248 | Passes |
| `test_in2` / `rev_test_in2` | 3,580 m | 435,200 / 434,896 | 2,890 / 2,107 | Passes (forward is close to GT2's peak) |
| `shortway` | 2,466 m | 417,664 | 1,342 | Passes |
| `speed` | | 370,720 | 1,749 | Passes |
| `rev_shortway` | 2,466 m | 419,004 | 1,321 | Stops: 18 of 5,550 road points not found by the game's ground probe |
| `highway` / `rev_highway` | 3,776 m | 681,268 / 675,764 | 1,382 / 1,363 | Stops: 11 road points not found (20 far detail models dropped to fit) |
| `mountain` / `rev_mountain` | 3,979 m | 446,556 / 445,676 | 2,228 / 2,019 | Stops: 24 of 17,002 road points not found |
| `maxspeed` | | 371,008 | 1,749 | Stops: GT1's pit-entry line wraps past the finish line (`--pit drop` may avoid it) |

"Road points not found" means the importer found a few spots where GT2's ground check would miss the road surface.
A car driving there could drop through or bounce. The importer stops rather than build a course with that fault.

## Things to know before trying another course

- **The slot decides how it plays.** In the Max Speed slot every course ends after one lap with "Finish". A slot used
  by races (Tahiti Road, for example) gives laps, AI cars and pit stops.
- **One course per slot.** The patch replaces a GT2 course; it does not add one. [GT2-Targets.md](GT2-Targets.md) lists the slots.
- **The sky is GT2's.** `--sky` borrows a GT2 course's sky and car lighting. `highway` (Special Stage Route 5) is a
  night sky. A day course wants a day sky, for example one of GT2's circuit courses.
- **The checks are not a drive.** Passing them means the course fits. Drive it in an emulator before sharing it.
