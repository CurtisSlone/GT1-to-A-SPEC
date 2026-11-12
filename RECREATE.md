# Recreate the SSR11 patch from your own discs

`gt2-tools` builds the patch from two disc images you own. The steps give the same bytes every time, so you can check
your result against the published patch.

## What you need

- `Gran Turismo 2 A-Spec (v1.2.1).cue` and `.bin`: SHA-256 `94866e3dbcf666cfc3dc2275c8dba1fa415a626a44ed7a80600238cefa1a599f`.
- `Gran Turismo (USA) (v1.1).cue` and `.bin` (SCUS-94194): the .bin's SHA-256 is
  `e1ba7def96b7f213637fa82658b53c34a3a5f6c54df7d7e5ab9c3f53a2d41f03`.
- `gt2-tools.exe` (Windows, `tools/windows`) or `gt2-tools` (Linux x86-64, `tools/linux`).
- About 4 GB of free space.

Put the tool, both .cue/.bin pairs and `aspec-ssr11.toml` (from `recipe/`) in one folder, for example
`C:\ssr11`, and open PowerShell there. On Linux, use `./gt2-tools` in place of `.\gt2-tools.exe`.

## The short way: one command

```
.\gt2-tools.exe disc extract "Gran Turismo (USA) (v1.1).cue" --out gt1
.\gt2-tools.exe patch build aspec-ssr11.toml --base "Gran Turismo 2 A-Spec (v1.2.1).cue" --source gt1\disc\files --out out
```

The first command copies the GT1 disc's files out of the image. The second runs every step below in order and
writes `out\Gran Turismo 2 A-Spec (v1.2.1) SSR11.bin`, its `.cue`, the `.xdelta`, and `out\report.txt` with every
hash. It stops with an error if your A-Spec image is not the expected one.

## Step by step

### 1. Extract the A-Spec image

```
.\gt2-tools.exe disc extract "Gran Turismo 2 A-Spec (v1.2.1).cue" --out aspec --expect-hash 94866e3dbcf666cfc3dc2275c8dba1fa415a626a44ed7a80600238cefa1a599f
```

This checks the image's SHA-256, then writes its files to `aspec\disc` and unpacks GT2.VOL (33,699 files) to
`aspec\data\gt2vol`.

### 2. Extract the GT1 disc

```
.\gt2-tools.exe disc extract "Gran Turismo (USA) (v1.1).cue" --out gt1
```

This writes GT1's files to `gt1\disc\files`. The course is in `COURSE.DAT`, its name in `SYSTEM.DAT`. GT1 has no
GT2.VOL, so the tool says so and stops there.

### 3. Convert SSR11 into the Max Speed slot

```
.\gt2-tools.exe gt1 import-course --disc gt1\disc\files --course ssr11 --data aspec\data --out ssr11 --slot maxspeed --sky highway --target ps1 --pit keep --name "Special Stage Route 11" --mod SSR11
```

| Option | What it does |
|---|---|
| `--course ssr11` | GT1's Special Stage Route 11 (`outbahn` on the GT1 disc) |
| `--slot maxspeed` | Written under Max Speed's file names and course record, so Machine Test > Max Speed loads it |
| `--sky highway` | GT2's night sky and car lighting from Special Stage Route 5 |
| `--target ps1` | The stock game: GT1's textures packed into the course's video memory, GT2's limits enforced |
| `--pit keep` | GT1's pit lines stay |
| `--name` | The name in the game's records, at most 31 characters |

It writes the patch folder `ssr11\mods\SSR11` (the course files and the course table) and prints what it did:
the 13 far detail models it dropped to fit, the texture packing, and the budget check.

### 4. Check it against the stock game's limits

```
.\gt2-tools.exe course check ssr11\mods\SSR11 --slot maxspeed --budget ps1 --data aspec\data
```

The last line should read `within the stock game's limits`. The check covers:
- the course memory (700,000 bytes);
- the video memory region every course load overwrites;
- the drawing load against GT2's busiest shipped course;
- the pit lines.

### 5. Build the new disc image

```
.\gt2-tools.exe disc build --base "Gran Turismo 2 A-Spec (v1.2.1).cue" --data aspec\data --mod ssr11\mods\SSR11 --out "Gran Turismo 2 A-Spec (v1.2.1) SSR11.bin" --cue "Gran Turismo 2 A-Spec (v1.2.1) SSR11.cue"
```

This replaces 4 files in GT2.VOL: the course table, the map, and the two course files. GT2.VOL grows by 121
sectors, so MUSIC.DAT and FAULTY.PSX move. Then the tool rewrites the disc's file table and the CD error
correction, and checks every sector. Every other sector is the A-Spec image's.

### 6. Make the patch and check it

```
.\gt2-tools.exe patch make "Gran Turismo 2 A-Spec (v1.2.1).bin" "Gran Turismo 2 A-Spec (v1.2.1) SSR11.bin" "GT2-A-Spec-SSR11.xdelta"
.\gt2-tools.exe patch verify "Gran Turismo 2 A-Spec (v1.2.1).bin" "GT2-A-Spec-SSR11.xdelta" "Gran Turismo 2 A-Spec (v1.2.1) SSR11.bin"
```

`patch make` writes a standard xdelta (VCDIFF) that xdelta3 and xdelta front ends apply. `patch verify` applies it
to your A-Spec image and compares the result byte for byte.

## Check your result

| File | SHA-256 |
|---|---|
| `Gran Turismo 2 A-Spec (v1.2.1) SSR11.bin` (709,527,840 bytes) | `a155f2619cae12c60c6df80346eb9270db3ffa5ffdcdaf08c33b254aab7cde46` |
| `GT2-A-Spec-SSR11.xdelta` (2,956,164 bytes) | `7654bc1f62a424728985d72b4bd64b7de94afd21ae072d6bdb12dc2a7e4e9f0a` |

In PowerShell: `Get-FileHash "Gran Turismo 2 A-Spec (v1.2.1) SSR11.bin"`. On Linux: `sha256sum`.

## Other slots

The slot is one line in the recipe. A copy of `aspec-ssr11.toml` with `slot = "tahiti_t"` puts SSR11 in place of
Tahiti Road, where races and pit stops work. That version is built the same way and passes the same checks. It has
not been tested in an emulator yet.

Other GT1 courses: set `course = "..."` in the recipe to an alias or a GT1 stem from [GT1-Track-Aliases.md](GT1-Track-Aliases.md), which also lists which courses pass the checks today.
