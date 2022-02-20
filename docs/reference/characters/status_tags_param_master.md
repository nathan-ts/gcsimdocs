---
sidebar_position: 1
title: Character Statuses, Parameters, and Tags Master List
---

# Characters

Please see Discord readme channel for latest update on which characters are not yet implemented.

## Statuses

Statuses are tags that can be conditioned upon on the action list. The are referenced by `.status.<status name>` The following are valid statuses:

<!-- prettier-ignore -->
| character | status | description |
| --- | --- | --- |
| Albedo | `albedoc2` | Albedo C2 remaining duration |
| Beidou | `beidouc4` | Beidou C4 (active effect) remaining duration |
| Beidou | `beidoua4` | Beidou A4 (active effect) remaining duration |
| Beidou | `beidouburst` | Beidou burst (active effect) remaining duration |
| Bennett | `btburst` | Bennett burst (active effect) remaining duration |
| Chongyun | `chongyunfield` | Chongyun skill field duration |
| Diluc | `dilucc4` | Diluc C4 duration |
| Diluc | `dilucq` | Diluc C4 duration |
| Diona| `dionaburst` | Diona burst (active effect) remaining duration |
| Eula | `eulaq` | Eula burst active duration; if > 0, then her burst is currently active and acquiring stacks |
| Fischl | `fischloz` | Fischl oz active duration (i.e. how many more frames Oz will be onfield for) |
| Ganyu | `ganyuc6` | Ganyu C6 (active effect) remaining duration (i.e. if this value > 0 then the next CA will be "instant") |
| Gorou | `generalwarbanner` | Gorou E buff |
| Gorou | `generalglory` | Gorou Q buff |
| Hutao | `paramita` | Hutao Paramita duration |
| Hutao | `htbb` | Hutao Blood Blossom duration |
| Jean | `jeanq` | Jean burst field duration |
| Keqing | `keqinginfuse` | Keqing E infuse duration |
| Klee | `kleeq` | Klee burst duration |
| Kokomi | `kokomiskill` | Kokomi skill duration |
| Kokomi | `kokomiburst` | Kokomi burst duration |
| Lisa | `lisaburst` | Lisa burst duration |
| Ningguang | `ningguangskillparticleICD` | Ningguang particle ICD (i.e. 6 sec before her E will generate particles again) |
| Noelle | `noelleq` | Noelle burst (active effect) remaining duration |
| Raiden | `raidenskill` | Raiden skill (active effect) remaining duration |
| Raiden | `raidenburst` | Raiden burst (active effect) remaining duration |
| Rosaria | `rosariaburst` | Rosaria burst duration |
| Sara | `sarabuffx` | Sara buff or character; **Replace x with character name** For example `sarabuffraidenshogun` `sarabuffbennett` etc...|
| Shenhe | `shenhequill` | Shenhe quill (timer only) remaining duration |
| Shenhe | `shenheburst` | Shenhe burst (active effect) remaining duration |
| Sucrose | `sucrosea4` | Sucrose A4 (active effect) remaining duration |
| Sucrose | `sucroseburst` | Sucrose burst (active effect) remaining duration |
| Xiangling | `xianglingguoba` | Xiangling skill (active effect) remaining duration |
| Xiangling | `xianglingburst` | Xiangling burst (active effect) remaining duration |
| Xiangling | `xlc6` | Xiangling C6 (active effect) remaining duration |
| Xiao | `xiaoburst` | Xiao burst duration |
| Xiao | `xiaoc6` | Xiao C6 icd |
| Xingqiu | `xqorb` | Xingqiu sword orbital (active effect) remaining duration |
| Xingqiu | `xqburst` | Xingqiu burst (active effect) remaining duration |
| Yanfei | `yanfeiburst` | Yanfei burst duration |
| Yun Jin | `yunjinburst` | Yun Jin burst duration |
| Yoimiya | `yoimiyaskill` | Yoimiya skill (active effect) remaining duration |
| Yoimiya | `aurous` | Yoimiya burst (active effect) remaining duration |
| Yoimiya | `aurousicd` | Yoimiya burst internal cooldown (i.e. if this value > 0 then attacks will not trigger Yoimiya burst damage) |
| Yoimiya | `yoimiyaa2` | Yoimiya A2 (active effect) remaining duration |

## Tags

Tags are also additional status that can be condition upon in the action list. However these are character specific and are referenced by `.tags.<char name>.<tag name>`

<!-- prettier-ignore -->
| character | tag | description |
| --- | --- | --- |
| Albedo | `elevator` | `1` if elevator is active, otherwise `0` |
| Albedo | `c2` | number of stacks for c2 |
| Eula | `grimheart` | number of grimheart stacks |
| Lisa | `stack` | number of E stacks |
| Ningguang | `jade` | number of jades |
| Shenhe | `quills_{character name}` | Number of quill stacks remaining depending on the character. For example, .tags.shenhe.quills_ganyu |
| Sucrose | `eCharge` | number of charges on her skill |
| Xiao | `a4` | number of a4 stacks |
| Xiao | `eCharge` | number of charge on his skill |
| Yanfei | `seal` | number of seals |
| Yun Jin | `burststacks_{character name}` | Number of burst stacks remaining depending on the character. For example, .tags.yunjin.burststacks_zhongli |
| Zhongli | `shielded` | whether or not his shield (from hold E) is active; `1` if active |

## Params

Params are additional info that can be passed to individual attack/skill/burst etc..

<!-- prettier-ignore -->
| character | ability | param | description |
| --- | --- | --- | --- |
| albedo | `burst` | `bloom` | number of bloom hits. default 2 |
| aloy | `attack` | `travel` | projectile travel time. default 10 frames |
| aloy | `aim` | `weakspot` | Hit weakspot with aimed shot. default 0 (false), 1 for true  |
| aloy | `skill` | `bomblets` | default 2 |
| aloy | `skill` | `bomblet_coil_stacks` | default 2 |
| aloy | `skill` | `delay` | default 0 |
| amber | `attack` | `travel` | projectile travel time. default 10 frames  |
| amber | `aim` | `travel` | projectile travel time. default 10 frames  |
| amber | `aim` | `bunny` | shoot the bunny (for C2+ only). default 0 (false). no damage if 1 (true) |
| amber | `aim` | `weakspot` | Hit weakspot with aimed shot. default 0 (false), 1 for true  |
| amber | `skill` | `hold` | frames to hold bunny for (for throwing). default 0 |
| beidou | `skill` | `counter` | number of counter hits. default 0. 2 for perfect counter. does not affect frames |
| bennett | `skill` | `hold` | default 0 for skill tap. 1 for short hold, 2 for long hold |
| diluc | `burst` | `dot` | number of dot ticks. default 2 |
| diluc | `burst` | `explode` | if explode from burst hits. default 0 (no hit) |
| diona | `attack` | `travel` | projectile travel time. default 10 frames  |
| diona | `aim` | `travel` | projectile travel time. default 10 frames  |
| diona | `skill` | `travel` | projectile travel time. default 10 frames  |
| diona | `skill` | `hold` | default 0 for skill tap. 1 for hold |
| eula | `skill` | `hold` | default 0 for skill tap. 1 for hold |
| fischl | `attack` | `travel` | projectile travel time. default 10 frames  |
| ganyu | `attack` | `travel` | projectile travel time. default 10 frames  |
| ganyu | `aim` | `travel` | projectile travel time. default 10 frames  |
| ganyu | `aim` | `weakspot` | Hit weakspot with aimed shot. default 0 (false), 1 for true  |
| ganyu | `skill` | `bloom` | bloom delay from projectile landing default 20 frames |
| ganyu | `burst` | `radius` | radius of the targets. default 1m |
| gorou | `aim` | `weakspot` | Hit weakspot with aimed shot. default 0 (false), 1 for true  |
| hutao | `burst` | `targets` | number of targets to simulate burst hitting for healing purposes. actual number of target in sim ignored |
| jean | `skill` | `hold` | hold duration for Jean skill. default 0. require > 60 to trigger C1 |
| jean | `skill` | `enter` | number of times enemy enters field. default 0 |
| jean | `skill` | `delay` | number of frames to wait before enemy enters. default 10 |
| kazuha | `high_plunge` | `collide` | does collide dmg on plunge apply; default 0 (no) |
| kazuha | `skill` | `hold` | default 0 for tap. 1 for hold |
| keqing | `skill` | `c1` | number of hits for c1 (since explosion caused at both start and end). default 1 |
| klee | `attack` | `travel` | projectile travel time. default 10 frames  |
| klee | `skill` | `walk` | if set (any value), attack counter will reset to simulate walk cancel |
| klee | `charge` | `travel` | projectile travel time. default 10 frames |
| klee | `skill` | `bounce` | number of bounce hits that lands. default 1 |
| klee | `skill` | `mine` | number of mines that hits. default 2 |
| kokomi | `skill` | `travel` | projectile travel time. default 10 frames  |
| lisa | `charge` | `hits` | number of targets hit by charge attack. default 1 |
| lisa | `skill` | `hold` | default 0 for skill tap. 1 for hold |
| ningguang | `attack` | `travel` | projectile travel time. default 10 frames  |
| ningguang | `charge` | `travel` | projectile travel time. default 10 frames  |
| ningguang | `burst` | `travel` | projectile travel time. default 10 frames  |
| rosaria | `skill` | `nobehind` | default 0. 1 for striking behind for A2 purposes |
| sara | `attack` | `travel` | projectile travel time. default 10 frames  |
| sara | `aim` | `travel` | projectile travel time. default 10 frames  |
| sara | `aim` | `weakspot` | Hit weakspot with aimed shot. default 0 (false), 1 for true  |
| sara | `skill` | `wave_cluster_hits` | use numbers in each slot to control the # of hits. So for center hit, then 3 hits from each wave, set wave_cluster_hits=33331 |
| sara | `skill` | `waveAttackProcs` | used to determine which waves proc the attack buff. same format as wave_cluster_hits |
| shenhe | `skill` | `hold` | 0 for press (default), 1 for hold |
| tartaglia | `attack` | `travel` | projectile travel time. default 10 frames (range mode only) |
| tartaglia | `aim` | `travel` | projectile travel time. default 10 frames (range mode only) |
| tartaglia | `aim` | `weakspot` | Hit weakspot with aimed shot. default 0 (false), 1 for true  |
| tartaglia | `charge` | `hitWeakPoint` | hit weak point for charge attack in melee mode. default 0 (false) |
| venti | `attack` | `travel` | projectile travel time. default 10 frames  |
| venti | `aim` | `travel` | projectile travel time. default 10 frames  |
| venti | `aim` | `weakspot` | Hit weakspot with aimed shot. default 0 (false), 1 for true  |
| venti | `skill` | `hold` | default 0 for skill tap. 1 for hold |
| xiao | `high_plunge` | `plunge_hits` | determine how many plunge falling hits you do on the way down. default 0 |
| xiao | `low_plunge` | `plunge_hits` | determine how many plunge falling hits you do on the way down. default 0 |
| xingqiu | `skill` | `orbital` | whether or not orbital is in contact with target (resulting in hydro app). default 0 |
| xingqiu | `burst` | `orbital` | whether or not orbital is in contact with target (resulting in hydro app). default 0 |
| yanfei | `attack` | `travel` | projectile travel time. default 10 frames  |
| yoimiya | `attack` | `travel` | projectile travel time. default 10 frames  |
| yunjin | `skill` | `a1` | set this to 1 for A1 skill effect using skill press frame count (i.e., the minimum frames possible) |
| yunjin | `skill` | `hold` | default 0 for skill press, 1 for first charge level, and 2 for second charge level, using the appropriate frame counts. |
| zhongli | `skill` | `max` | max number times resonance can hit (simulate maybe out of range of a construct) |
| zhongli | `skill` | `hold` | default 0 for skill tap. 1 for hold |
| zhongli | `skill` | `hold_nostele` | default 0. if 1 no stele will be created (i.e. shield only). `hold` will take precedence over this |
