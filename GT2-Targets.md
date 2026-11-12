# GT2 targets: the course slots a patch can replace

A patch replaces one GT2 course. `--slot` (or `slot = "..."` in a recipe) names it. The new course loads wherever
the game loads that slot: its GT Mode events, licence tests, or Machine Test runs. This list is read from
Gran Turismo 2 A-Spec v1.2.1 (126 courses). The retail Simulation disc has the same slots, but A-Spec moved some
events between courses.

How to read it:

- **Every slot takes the same course size and video memory.** A GT1 course that passes the checks fits any slot,
  so the slot only decides where and how the course is driven.
- **Laps, AI cars, pit rules and licence targets belong to the events, not the course.** A 2-lap event set up for a
  5 km track runs 2 laps of whatever you put there.
- **Each variant is its own slot.** Forward, reverse (`rev_`, `_rev`), 2-player (`2p`) and night versions are
  separate files. Replacing `tahiti_t` leaves `tahiti_t_rev` and `tahiti_t_2p` as they were.
- **Menu pictures and some menu text stay GT2's.** The race itself, the course map and the course record's name
  change. Event pages may still show the old track's picture.
- **Old records stay.** Records saved under the slot's old course stay in the list.
- **Random events.** 92 GT Mode events draw their course from GT2's random-course list (`none`). That list was not
  read here, so some slots below may also come up there.

Flags: `night` uses night car lighting, `dirt` uses rally rules and tires, `2-player` is the split-screen version,
`reverse` runs the other way, `hill climb` is Pikes Peak's point-to-point mode, `no boards` skips the trackside
sponsor boards, and `0x02` is a bit whose meaning is not known yet. The Sky column is the sky file the slot uses
today. `--sky` can borrow any GT2 course's sky.

Tested so far: `maxspeed` was driven with SSR11 on GT2's own code. `tahiti_t` was built and passed the checks but
has not been driven. Every other slot is untested.

## Race slots (the best targets for a circuit)

Tarmac courses with GT Mode races: laps, AI cars, and pit stops where an event allows them.

| Slot (`--slot`) | Name in the game | Flags | Sky | GT Mode events | Licence tests |
|---|---|---|---|---|---|
| `autumn` | Autumn Ring | no boards | `au` | 4: F1EECHAMP0504, GCC0003, SUPERCAR03, TCN0001 |  |
| `circuit` | Grand Valley Speedway | no boards | `gv_sky` | 4: EGV0001, EPL0002, F1EECHAMP0501, GTC0002 |  |
| `grindel` | Grindelwald | - | `noon` | 4: CBM0002, HTC0003, TCN0002, WOS0002 | LIS04 |
| `highway` | Special Stage Route 5 | night, no boards | `dawn` | 7: 80S0002, ES50001, FRC0002, GTA0002, SLS0002, TCT0001 (+1) |  |
| `laguna` | Laguna Seca Raceway | no boards | `lagunasky` | 14: 4WD0003, ELS0001, GT30502, GT50501, GTA0005, GTW0502 (+8) | LIS06 |
| `mountain` | Trial Mountain Circuit | no boards | `mskyX` | 11: 80S0001, ETM0001, FFC0003, GBL0001, GBL0002, GBL0003 (+5) |  |
| `new_parmaS` | Apricot Hill Speedway | - | `new_parmas_sky` | 6: EPL0001, EPS0001, GT30505, GT50505, GTW0503, STT0001 | LIS09 |
| `parma` | Midfield Raceway | - | `parma_sky` | 10: F1EECHAMP0505, FFC0002, FRC0003, GJL0001, GJL0002, GJL0003 (+4) | LIS03 |
| `parma_rev` | Midfield Raceway | reverse | `parma_sky` | 1: FPS0001 |  |
| `rev_test_in2` | Deep Forest Raceway | reverse, no boards, 0x02 | `tl_sky2` | 1: SUPERCAR01 |  |
| `roma` | Rome Circuit Full Course | - | `roma_sky` | 11: CBM0003, EPL0003, ERM0001, F1EECHAMP0502, GIL0001, GT50503 (+5) | LIS05 |
| `roma_night` | Rome-Night | night | `romadark_sky` | 2: GIL0002, SUPERCAR02 | LIS08 |
| `roma_short` | Rome Short Course | - | `roma_sky` | 4: CBM0001, GCC0001, WGN0001, WLK0001 |  |
| `s_speed` | Super Speedway | - | `speedsky` | 3: GT50502, GTA0001, WGN0002 |  |
| `seatt_s` | Seattle Short Course | - | `sea_ha_e` | 4: 4WD0001, GCC0002, MSC0001, WLK0002 |  |
| `seattle` | Seattle Circuit Full Course | - | `sea_ha_e` | 4: 4WD0002, 80S0004, EST0001, MSC0002 | LIS01 |
| `short` | Grand Valley East Section | no boards | `gv_sky` | 2: GT30501, MRC0001 |  |
| `shortway` | Clubman Stage Route 5 | night, no boards | `dawn` | 1: FRC0001 |  |
| `speed` | Test Course | no boards | `mskyX` | 2: FPM0001, TCT0002 |  |
| `sprint2` | Red Rock Valley Speedway | 0x02 | `cloudtest` | 5: GTA0003, GTC0001, MRC0003, PFL0002, SND0003 |  |
| `tahiti_t` | Tahiti Road | - | `t_sky` | 9: 80S0005, FFC0001, GFL0001, GFL0002, HTC0001, LIS00 (+3) | LIS00 |
| `test_in2` | Deep Forest Raceway | no boards, 0x02 | `tl_sky2` | 9: 80S0003, F1EECHAMP0503, GGL0001, GGL0002, GGL0003, GT30503 (+3) |  |
| `testline` | High Speed Ring | no boards | `tl_sky4` | 3: MRC0002, SLS0003, SND0002 |  |

## Dirt and hill climb slots

Rally events use dirt rules and dirt tires. A tarmac course here drives like a rally stage on the wrong surface.

| Slot (`--slot`) | Name in the game | Flags | Sky | GT Mode events |
|---|---|---|---|---|
| `SMtN_License1` | L_smokeymountain1 | dirt | `mskyX_2` | 1: LIB00 |
| `nn_dirt_2` | Smokey Mountain South | dirt | `mskyX_2` | 3: DO20001, DO20002, DO20003 |
| `nn_dirt_3` | Green Forest Roadway | dirt | `mskyX_2` | 3: DO30001, DO30002, DO30003 |
| `no_name_dirt` | Smokey Mountain North | dirt | `mskyX_2` | 3: DON0001, DON0002, DON0003 |
| `no_name_dirt_rev` | Smokey Mountain North | dirt, reverse | `mskyX_2` | 3: DRN0001, DRN0002, DRN0003 |
| `pikes` | Pikes Peak Hill Climb | dirt, hill climb | `lagunasky` | 3: DOC0001, DOC0002, DOC0003 |
| `pikes_rev` | Pikes Peak Downhill | dirt, reverse, hill climb | `lagunasky` | 3: DRC0001, DRC0002, DRC0003 |
| `tahiti_d_new` | Tahiti Dirt Route 3 | dirt | `t_sky` | 3: DOT0001, DOT0002, DOT0003 |
| `tahiti_d_new_rev` | Tahiti Dirt Route 3 | dirt, reverse | `t_sky` | 3: DRT0001, DRT0002, DRT0003 |
| `tahiti_test7` | Tahiti Maze | dirt | `t_sky` | 3: DO70001, DO70002, DO70003 |

## Machine Test slots

`maxspeed` is the SSR11 patch's slot: one lap, then "Finish". `TC_lisence` is shared: Machine Test's 0-400 m and
0-1000 m and several licence tests all load it, so replacing it changes all of them.

| Slot (`--slot`) | Name in the game | Flags | Sky | Uses |
|---|---|---|---|---|
| `TC_lisence` | L_start&stop | no boards | `mskyX_2` | G1000, G400, LJA00, LJB00, LJB01, LJB02 |
| `maxspeed` | Max Speed Attack | no boards | `mskyX` | GMAX |

## Licence test slots

Short test layouts. Replacing one changes that licence test, and its target times no longer make sense.

| Slot (`--slot`) | Name in the game | Flags | Sky | Licence tests |
|---|---|---|---|---|
| `L_pikes_climb` | L_pikes_climb | dirt | `lagunasky` | LIA04 |
| `L_pikes_down` | L_pikes_down | dirt | `lagunasky` | LIA05 |
| `L_tahiti_dirt` | L_tahiti_dirt | dirt | `t_sky` | LIB01 |
| `SMtN_License2` | L_smokeymountain2 | dirt | `mskyX_2` | LIA03 |
| `circle30` | L_circle30 | - | `circle30sky` | LJB03 |
| `circle80` | L_circle80 | - | `circle80sky` | LIA00, LJB04 |
| `l_mid1` | L_mid1 | - | `parma_sky` | LIC06, LIC07 |
| `l_mid2` | L_mid2 | - | `parma_sky` | LIA07 |
| `l_plam` | L_plam | - | `new_parmas_sky` | LIA02 |
| `l_screw` | L_screw | - | `lagunasky` | LIA08, LIB09 |
| `lic_seattle` | L_seattle | - | `sea_ha_e` | LIC09 |
| `license_roma` | L_Rome | - | `roma_sky` | LIA06, LIC08 |
| `spL1` | spL1 | 0x02 | `cloudtest` | LIC05 |
| `spL2` | spL2 | 0x02 | `cloudtest` | LIC04 |
| `spL3` | spL3 | 0x02 | `cloudtest` | LIB08 |
| `test_20` | L_slalom20 | - | `speedsky` | LIB05 |
| `test_40` | L_slalom40 | - | `speedsky` | LIB07 |
| `test_cb` | L_corner-brake | no boards | `licen_sky` | LJA01 |
| `test_hs1` | L_Eau-Rouge | - | `licen_sky` | LIA01, LIA09 |
| `test_j1` | L_J-turn1 | - | `speedsky` | LIC00, LIC01 |
| `test_ko` | L_box | - | `speedsky` | LIC02 |
| `test_ko_brind` | L_box_brind | - | `speedsky` | LIC03 |
| `test_l2` | L_L-turnL | - | `tesr_l2sky` | LJA04, LJA05 |
| `test_s1` | L_S-corner1 | - | `licen_sky` | LJB08, LJB09 |
| `test_s2` | L_S-corner2 | - | `licen_sky` | LIB02, LIB03, LJA06, LJA07 |
| `test_ul1` | L_U-turnL | - | `licen_sky` | LJB05, LJB06 |
| `test_ur1` | L_U-turnR | - | `licen_sky` | LJA02, LJA03, LJB07 |
| `test_w1` | L_double1 | - | `speedsky` | LIB04 |
| `test_w2` | L_double2 | - | `speedsky` | LIB06 |
| `test_z` | L_crank | - | `speedsky` | LJA08, LJA09 |

## Not reached in GT Mode

No GT Mode event or licence test on this disc loads these slots (unless the random list does). This covers the
2-player and reverse versions, the night and short variants without events, and test and check courses left on the
disc. Replacing one is safe, but on the Simulation disc you cannot pick a track freely, so the player would not
reach it without editing an event.

| Slot (`--slot`) | Name in the game | Flags | Sky |
|---|---|---|---|
| `2p_autumn` | Autumn Ring | 2-player, no boards | `au` |
| `2p_circuit` | Grand Valley Speedway | 2-player, no boards | `gv_sky` |
| `2p_highway` | Special Stage Route 5 | night, 2-player, no boards | `dawn` |
| `2p_mini` | Autumn Ring Mini | 2-player, no boards | `au` |
| `2p_mountain` | Trial Mountain Circuit | 2-player, no boards | `mskyX` |
| `2p_roma` | Rome Circuit Full Course | 2-player | `roma_sky` |
| `2p_roma_night` | Rome-Night | night, 2-player | `romadark_sky` |
| `2p_roma_short` | Rome Short Course | 2-player | `roma_sky` |
| `2p_seatt_s` | Seattle Short Course | 2-player | `sea_ha_e` |
| `2p_seattle` | Seattle Circuit Full Course | 2-player | `sea_ha_e` |
| `2p_short` | Grand Valley East Section | 2-player, no boards | `gv_sky` |
| `2p_shortway` | Clubman Stage Route 5 | night, 2-player, no boards | `dawn` |
| `2p_sprint2` | Red Rock Valley Speedway | 2-player, 0x02 | `cloudtest` |
| `2p_test_in2` | Deep Forest Raceway | 2-player, no boards, 0x02 | `tl_sky2` |
| `2p_testline` | High Speed Ring | 2-player, no boards | `tl_sky4` |
| `Gtest` | Grindelwald | 2-player | `noon` |
| `Rhighway` | Special Stage Route 5 | night, reverse, no boards | `dawn` |
| `Rshortway` | Clubman Stage Route 5 | night, reverse, no boards | `dawn` |
| `bill_checker` | billboard-check | no boards, 0x02 | `cloudtest` |
| `cart` | Motor Sports Land | - | `cartsky` |
| `cart2p` | Motor Sports Land | 2-player | `cartsky` |
| `checker` | check | - | `licen_sky` |
| `dart_test2` | dart_test2 | - | `tl_skyG` |
| `l_20` | l_20 | - | `cartsky` |
| `laguna2` | Laguna Seca Raceway | 2-player | `lagunasky` |
| `laguna2p` | Laguna Seca Raceway | 2-player, no boards | `lagunasky` |
| `lagunareverse` | Laguna Seca Raceway | reverse, no boards | `lagunasky` |
| `mini` | Autumn Ring Mini | no boards | `au` |
| `new_parmaS_2p` | Apricot Hill Speedway | 2-player | `new_parmas_sky` |
| `new_parmaS_rev` | Apricot Hill Speedway | reverse | `new_parmas_sky` |
| `nn_dirt_2_2p` | Smokey Mountain South | dirt, 2-player | `mskyX_2` |
| `nn_dirt_2_rev` | Smokey Mountain South | dirt, reverse | `mskyX_2` |
| `nn_dirt_3_2p` | Green Forest Roadway | dirt, 2-player | `mskyX_2` |
| `no_name_dirt_2p` | Smokey Mountain North | dirt, 2-player | `mskyX_2` |
| `parma_2p` | Midfield Raceway | 2-player | `parma_sky` |
| `pikes_2p` | Pikes Peak Hill Climb | dirt, 2-player, hill climb | `lagunasky` |
| `pikes_2p_rev` | Pikes Peak Downhill | dirt, 2-player, reverse, hill climb | `lagunasky` |
| `rev_autumn` | Autumn Ring | reverse, no boards | `au` |
| `rev_circuit` | Grand Valley Speedway | reverse, no boards | `gv_sky` |
| `rev_mini` | Autumn Ring Mini | reverse, no boards | `au` |
| `rev_mountain` | Trial Mountain Circuit | reverse, no boards | `mskyX` |
| `rev_roma` | Rome Circuit Full Course | reverse | `roma_sky` |
| `rev_roma_night` | Rome-Night | night, reverse | `romadark_sky` |
| `rev_roma_short` | Rome Short Course | reverse | `roma_sky` |
| `rev_short` | Grand Valley East Section | reverse, no boards | `gv_sky` |
| `rev_speed` | Test Course | reverse, no boards | `mskyX` |
| `rev_sprint2` | Red Rock Valley Speedway | reverse, 0x02 | `cloudtest` |
| `rev_testline` | High Speed Ring | reverse, no boards | `tl_sky4` |
| `reverse` | Grindelwald | reverse | `noon` |
| `seatt_s_r` | Seattle Short Course | reverse | `sea_ha_e` |
| `seattle_r` | Seattle Circuit Full Course | reverse | `sea_ha_e` |
| `speed2p` | Super Speedway | 2-player | `speedsky` |
| `speedreverse` | Super Speedway | reverse | `speedsky` |
| `tahiti_d_new_2p` | Tahiti Dirt Route 3 | dirt, 2-player | `t_sky` |
| `tahiti_t_2p` | Tahiti Road | 2-player | `t_sky` |
| `tahiti_t_rev` | Tahiti Road | reverse | `t_sky` |
| `test_20a` | test_20 | - | `speedsky` |
| `test_30a` | test_30 | - | `licen_sky` |
| `test_40a` | test_40 | - | `speedsky` |
| `test_hs2` | test_hs2 | - | `licen_sky` |
| `test_l1` | L_L-turnR | - | `circle80sky` |
