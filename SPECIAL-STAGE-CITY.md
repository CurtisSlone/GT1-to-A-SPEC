# Special Stage City for GT2 A-Spec v1.2.1

This patch joins Special Stage Route 5 (GT2) and Special Stage Route 11 Reverse (GT1) into one course, about 8.4 km
long, joined at the hairpin the two courses share. It replaces all three Special Stage Route 5 slots. The reverse slot becomes Special Stage City driven the other way.

The course is road and sky only: the road, the walls, the street lamps, and SSR5's night skyline. The buildings are
left out so the course fits the stock game's limits.

It is a fan project, not affiliated with Sony
Interactive Entertainment or Polyphony Digital. No disc images are included. Not approved by any GT2 modder, ever.

## What you need

- `Gran Turismo 2 A-Spec (v1.2.1).bin`, the same file as for the SSR11 patch (README.md has its hashes).
- xdelta3, or an xdelta front end (Delta Patcher, xdelta UI).
- DuckStation.

## Apply the patch

```
xdelta3 -d -s "Gran Turismo 2 A-Spec (v1.2.1).bin" project-biege-special-stage-city.xdelta "Gran Turismo 2 A-Spec (v1.2.1) Special Stage City.bin"
```

Put `Gran Turismo 2 A-Spec (v1.2.1) Special Stage City.cue` next to the new .bin and open the .cue in DuckStation.

The patched .bin should be exactly:

| | |
|---|---|
| Size | 709,245,600 bytes |
| SHA-256 | `56993b77fcd645ba56e444a0890adc114d9ddaff76561fe35f528b727429d6bd` |
| CRC-32 | `fe7a5821` |

| Patch file | Size | SHA-256 |
|---|---|---|
| `project-biege-special-stage-city.xdelta` | 4,118,936 bytes | `6583bcbc3c80b59762e4eb460d6fd7040ddeca62ff3d798c0eb2961413baba38` |

## Where to drive it

The GT Mode events that use Special Stage Route 5 now load Special Stage City (the menus still show SSR5's picture).

## Known limits

- 391 sections and 8.4 km: longer than any course GT2 ships (most sections: 229; longest: Pikes Peak, 6,972 m).
  The build checks pass, but nothing checks section count or lap length.
- The menus' course pictures till say Special Stage Route 5.
- No pit lane. Where would I put it?!
