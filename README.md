# Special Stage Route 11 for GT2 A-Spec v1.2.1 (proof of concept)

This patch puts Special Stage Route 11 from Gran Turismo (GT1) into Gran Turismo 2 A-Spec v1.2.1.
It replaces the course of Machine Test > Max Speed. Nothing else in the game changes.
The course runs on GT2's own code: the A-Spec v1.2 executable and 2 MB of RAM, with no emulator tricks.

This is a fan project. It is not affiliated with Sony Interactive Entertainment or Polyphony Digital.
No disc images are included. You need your own copy of A-Spec v1.2.1 and Gran Turismo (USA) (v1.1)

# GT2 Modding Community
Can we be friends now? I'm ready to break bread. You know where to find me.

## What you need

- `Gran Turismo 2 A-Spec (v1.2.1).bin`, exactly this file:

| | |
|---|---|
| Size | 709,243,248 bytes |
| MD5 | `eff86e0d22ee44395c0a19a72f2ba0fc` |
| SHA-1 | `280f047b149426830bf793d1b4d39bb8e200df8f` |
| SHA-256 | `94866e3dbcf666cfc3dc2275c8dba1fa415a626a44ed7a80600238cefa1a599f` |
| CRC-32 | `66383d3d` |

- xdelta3, or an xdelta front end (Delta Patcher, xdelta UI).
- DuckStation.

## Apply the patch

1. Check that your A-Spec .bin matches the hashes above.
2. Apply the patch:

   ```
   xdelta3 -d -s "Gran Turismo 2 A-Spec (v1.2.1).bin" "GT2-A-Spec-SSR11.xdelta" "Gran Turismo 2 A-Spec (v1.2.1) SSR11.bin"
   ```

3. Make `Gran Turismo 2 A-Spec (v1.2.1) SSR11.cue` next to the new .bin with these three lines:

   ```
   FILE "Gran Turismo 2 A-Spec (v1.2.1) SSR11.bin" BINARY
     TRACK 01 MODE2/2352
       INDEX 01 00:00:00
   ```

4. Load the .cue in DuckStation.

## Play it

GT Mode > Machine Test (on the city map) > Max Speed > Start. You need a car in your garage.

- Special Stage Route 11 at night, with GT1's own textures at their original resolution.
- The sky and car lighting are GT2's own, from Special Stage Route 5.
- Max Speed rules on a circuit: the clock runs with no time limit. The run ends when you cross the line after one
  lap. Then you get the replay, name entry, and the results page with your top speed.
- GT1's pit lane is kept. Take the pit entry before the last corner and you get "Limited Speed" in the lane.
  Machine Test does not stop the car in the pits, so it shows "Skipped Pit Stop".


## Make it yourself

The patch is built by `gt2-tools` from your own A-Spec and GT1 discs, the same bytes every time.
See [RECREATE.md](RECREATE.md). The tools are in `tools/`, and the recipe is `recipe/aspec-ssr11.toml`.

Other GT1 courses: [GT1-Track-Aliases.md](GT1-Track-Aliases.md) lists the names the tool takes and which courses pass its checks today.

GT2 slots a patch can replace: [GT2-Targets.md](GT2-Targets.md) lists all 126, with the events and licence tests that load each one.
