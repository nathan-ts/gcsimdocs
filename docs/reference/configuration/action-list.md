---
sidebar_position: 2
title: Action Lists
---

Action lists are purely priority lists (modelled after WoW [simulationcraft](https://github.com/simulationcraft/simc), but differing syntax). The sim will scan down the list of actions starting with the first one and continuing until the first available is found. This is the action that will be executed. If nothing is found, nothing will be executed this frame and the list will be checked again the next, and so on.

Below is an example - the rest of the page dives into the syntax details, but a practical guide on how to build an action list starting from scratch can be found [here](../../guide/practical_guide.md). In particular see the "Simming New Teams (Creating/Modifying Action Lists)" section.

```
raidenshogun attack:4,dash,attack:4,dash,attack:4,dash,attack:2,charge +if=.status.raidenburst>0;

# Additional check to reset at the start of the next rotation
raidenshogun skill +if=.status.xianglingburst==0&&.energy.xingqiu>70&&.energy.xiangling>70;
raidenshogun skill +if=.status.raidenskill==0;

# Skill is required before burst to activate Kageuchi. Otherwise ER is barely not enough
# For rotations #2 and beyond, need to ensure that Guoba is ready to go. Guoba timing is about 300 frames after XQ fires his skill
xingqiu skill[orbital=1],burst[orbital=1],attack +if=.cd.xiangling.skill<300;

# Bennett burst goes after XQ burst for uptime alignment. Attack to proc swords
bennett burst,attack,skill +if=.status.xqburst>0&&.cd.xiangling.burst<180;

# Only ever want to XL burst in Bennett buff and after XQ burst for uptime alignment
xiangling burst,attack,skill,attack,attack +if=.status.xqburst>0&&.status.btburst>0;
# Second set of actions needed in case Guoba CD comes off while pyronado is spinning
xiangling burst,attack +if=.status.xqburst>0&&.status.btburst>0;
xiangling skill ;

# Raiden must burst after all others. Requires an attack to allow Bennett buff to apply
raidenshogun burst +if=.status.xqburst>0&&.status.xianglingburst>0&&.status.btburst>0;

# Funnelling
bennett attack,skill +if=.status.xqburst>0&&.energy.xiangling<70 +swap_to=xiangling;
bennett skill +if=.energy.xiangling<70 +swap_to=xiangling;
bennett skill +if=.energy.xingqiu<80 +swap_to=xingqiu;
bennett attack,skill +if=.status.xqburst>0 +if=.energy.raidenshogun<90 +swap_to=raidenshogun;

xingqiu attack +if=.status.xqburst>0;
xiangling attack +is_onfield;
bennett attack +is_onfield;
xingqiu attack +is_onfield;
raidenshogun attack +is_onfield;
```

## Syntax


Each line typically follows the following structure

`<char or command> <list of abilities> <flags>`

For example

`bennett skill,attack,burst,attack /if=.xx.xx.xx>1 /swap=xiangling /onfield /limit=1 /try=1 /timeout=100 /noswap=50`


## Starting line

Each line needs to start either with a character name (i.e. `albedo`, `amber`, etc...) or a command

The following are valid commands

- `chain` (and the related `<macro>:`)
- `wait_for`
- `reset_limit`
- `wait` (calc mode only)


### `char`

This specifies a list of abilities to be executed by the character. 

**IMPORTANT**: Note that all the abilities in the list **must be ready** before this line can be executed. The exception to this is if they `+try` flag is set.

See list of abilities below for valid abilities.

### `wait_for`

`wait_for` tells the simulator to until certain conditions are met before executing the next action. The length of wait depends on the flags set. You can use `wait_for` in a standalone fashion as in the below examples, but they are generally much more useful when you chain them with other actions. Please see the `chain` section below for details.

Examples:
```
# wait
wait_for mods value=.xiangling.bennett-buff==1 max=100;
wait_for particles value=xiangling max=100;
wait_for time max=10;
wait_for time max=100 +filler=attack[param=1];
```

The `wait_for` command is followed by one of the three options

- `mods`: for conditional vs a character stat mod being active
- `particles`: for conditional upon receiving a particle
- `time`: for waiting for a set amount of time

The `value` field is required for either `mods` or `particles`. `value` is either in the format of `.character.buffname` for `mods` OR `source` for `particles`

The `max` field must also be set. This is the maximum length the simulator will wait. For example, if `max` is set to 100, then regardless of the condition, the maxmium duration the simulator will wait is 100 frames. You can set `max` to -1 if there is no max.

There is also an optional flag `+filler`. Example: `+filler=attack[param=1]`. Filler is an action that the simulator will try and execute while waiting. This action can be any of the valid actions (**except `swap`**). There should only be one action followed by `filler`. Note that if you try to fill with `burst`, nothing may happen as `burst` may not be ready.

### `chain`

`chain` allow you to execute a list of macros.

Macro are a way to shortcut a certain sequence of actions. Macros can only be used in `chain`.

All macros must be declared **before** they are used in a chain. Otherwise the configuration file will not run.

Macros starts with an `identifier` representing the name of the macro as is followed by `:`. Examples:

```
xq_seq:xingqiu skill[orbital=1],burst[orbital=1],attack;
bt_seq:bennett burst,skill;
```

Macros can also be commands

```
wait_for_bt:wait_for particles value=bennett max=100;
startover:reset_limit  # Not sure why you would want to chain a reset_limit but it's acceptable.
```

Macros **should not** include any optional flags. Doing so may cause undefined behavior in your simulation.


The chain command itself is subject to the same format as any regular line - below is an example using the above commands, which uses Bennett burst + skill, then waits on Bennett until he collects his particles before swapping to Xingqiu. After the entire sequence is over it then swaps to Xiangling.

`chain bt_seq,wait_for_bt,xq_seq,startover +if=.xx.xx.xx>1 +swap_to=xiangling +limit=1 +try=1;`

By default, if the `+try` flag is not set then every ability in each macro must be ready before this chain will be executed. Other wise only the first action of the first ability in the chain needs to be ready.

Note that the following flags cannot be assigned to `chain` as they wouldn't make sense:

- `+is_onfield`


### `reset_limit`

`reset_limit` resets all lines with `/limit` flag (i.e. set their usage count to 0)

### `wait` **CALC MODE ONLY**

This is a calc mode only command. It can set one of the following 2 ways:

- `wait 10;` This tells the simulator in calc mode to wait for 10 frames
- `wait until 1000;` This tells the simulator to wait until frame 1000

This command has no effect in regular simulations


## List of abilities

This should be a comma separated list of abilities. Params can be passed into each ability via square brackets. For example:

`skill[orbital=1],attack,burst[orbital=1]`

`:x` can be used as a short form to repeat certain abilitiy. For example:

`attack[travel=50]:4`

This will repeat attack, with params `[travel=50]` 4 times. Common usage would be something like:

`raidenshongun attack:4,charge,attack:4,charge`

Which is basically N4C N4C.

**DO NOT WRITE `skill:4` UNLESS THE SKILL CAN BE USED 4 TIMES WITH NO COOLDOWN**. Otherwise the simulator will set there waiting for the next time skill comes back up. Similarly don't do this with `burst`. 

Following is valid list of abilities

- `skill`
- `burst`
- `attack`
- `charge`
- `high_plunge`
- `low_plunge`
- `proc`
- `aim`
- `dash`
- `jump`
- `swap`

## Flags

These are additional key words that can be added after the list of abilities that modify how the action is executed. Most of these key words can be used by simply adding them after a command, such as `zhongli attack +if=.cd.xingqiu.burst<120 +limit=1`.

- `+if`: condition that must be fulfiled before this line can be executed. See conditionals section below
- `+swap_to`: forcefully swap to another char after this line has finished. **DO NOT USE together with `+swap_lock=`, your character will sit there and do nothing for the `swap_lock` duration**
- `+swap_lock`: force the sim to stay on this character for x frames. **DO NOT USE together with `+swap_to=`, your character will sit there and do nothing for the `swap_lock` duration**
- `+is_onfield`: this line can only be used if this character is already on field (does not work in `chain`). Does not have a value, so just use it like `zhongli attack +is_onfield`
- `+label`: a name for this line; can't have duplicated labels
- `+needs`: this line can only be executed if the previous action is the referred to label
- `+limit`: number of times this line can be executed (replaces once)
- `+timeout`: this line cannot be executed again for x number of frames
- `+try`: if this flag is set, then this line will execute as long as first ability in the list is executable. If flag is set to `wait`, then if the sim will keep trying to execute the next ability in the list even if it's not ready (even if it means waiting forever). If flag is set to `drop`, then if the next ability is not ready immediately after the previous ability, the next ability along with the rest of the sequence will be dropped.



## Conditionals

Conditions can be specified for each action. Conditions consists of two parts, the condition itself, and the logical operators linking multiple conditions

In general, `+if` follows the following structure

`+if=.field1.field2.field3<operator><int value>`

For example

`+if=.tags.albedo.elevator==1`


Conditions are specified in the following format `.field1.field2.field3<op><val>`. Fields are as follows:

| field1 | field2 | field3 | field4 | description |
| --- | --- | --- | --- | --- |
| `energy` | `any char name` | none | none |specified char's current energy |
| `cd`| `any char name` | `skill` `burst`|none | cooldown remaining on skill/burst in frames |
| `stam`| none | none | none |player's current stamina |
| `status` | see each character | none | none |these are character specialized statuses, usually used to keep track of buffs |
| `tags` | `any char name` | see each character none || these are character specialized tags as defined by each character|
| `debuff` | `res` or `def` | `t1` or `t2` etc...| `debuff tag` | specific debuffs, see debuff section below on currently acceptable tags|
| `element` | `pryo` `hydro` `cryo` `electro` `frozen` `ec` | `t1` or `t2` etc... | `1` if the specified element exists, `0` otherwise|
| `ready`| `any char name` | `skill` `burst`|none | shorthand to check both cooldown and energy is ready |

`<op>` can be any one of the following: `==` `!=` `>` `>=` `<` `<=`

`<val>` is always a non-decimal number

Conditions can be chained together using the following logical operators:

- and `&&`
- or `||`

Brackets are also accepted to specify the order of operations. Example as follows:

`xingqiu skill +if=.cd.xingqiu.burst<120&&(.energy.xingqiu<80||.energy.xiangling<80)`

This will execute the conditions of `(.energy.xingqiu<80||.energy.xiangling<80)` first
