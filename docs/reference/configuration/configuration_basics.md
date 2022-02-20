---
sidebar_position: 1
title: Configuration Basics
---

## Configuration File

The configuration file can be roughly broken into 3 parts:

- character data
- enemy data
- rotation data

The config file is read by the sim line by line. Each configuration line **must be terminated** with a `;`. This is so that a single configuration can span multiple lines to allow easier readability.

For example, instead of writing:

`xingqiu char lvl=70/80 cons=2 talent=6,8,8;`

We can write

```
xingqiu char
   lvl=70/80
   cons=2
   talent=6,8,8;
```

White spaces are ignored as well so the following is equally valid.

```
xingqiu char
   lvl = 70 / 80
   cons = 2
   talent = 6, 8, 8;
```

## Run options

You can specify run options directly in the config file

`options iteration=5000 duration=90 workers=24 mode=sl`

## Comments

Any text following a `#` is treated as a comment and will be ignored until the end of the line. There are no multiline comments

## Character

Character data can be roughly broken into 4 parts:

- `<name> char` data such as level, base stats, cons, talents, etc..
- `<name> add weapon=<weapon name>` data such as weapon base stats, refine
- `<name> add set=<set name>` or artifact data, for set bonuses
- `<name> add stats` for any character stats

For example:

```
bennett char lvl=70/80 cons=2 talent=6,8,8 +params=[a=1];
bennett add weapon="favoniussword" refine=1 lvl=90/90 +params=[b=2];
bennett add set="noblesseoblige" count=4 +params=[c=1];
bennett add stats hp=4780 atk=311 er=0.518 pyro%=0.466 cr=0.311 ; #main
bennett add stats hp=717 hp%=0.058 atk=121 atk%=0.635 def=102 em=42 er=0.156 cr=0.128 cd=0.265 ; #subs
```

An optional param flag may be added to the character, the weapon, or the set via the `+params` flag. This optional param is defined by each character and may include things such as Serpent Spine starting stacks.

With the except of the stats (i.e. `hp`, `atk`, etc...), all other fields not starting with a `+` are mandatory

## Enemy

Enemy example:

`target lvl=88 pyro=0.1 dendro=0.1 hydro=0.1 electro=0.1 geo=0.1 anemo=0.1 physical=.1 cryo=.1;`

There must be at least one enemy in the config file. You can have multiple enemies to simulate multi target situation. Each enemy does not have to have the same resistance etc...

## Rotation

See [Action List](https://github.com/genshinsim/gsim/wiki/Action-List)

## Active char

There must be a line in the configuration that defines the active character. Otherwise sim will not run. Example:

`active xiangling;`

## Simulating taking damage

```
hurt once interval=300 amount=100,200 ele=pyro #once at frame 300 (or nearest)
hurt every interval=300,600 amount=100,200 ele=physical #randomly 100 to 200 dmg every 300 to 600 frames
```

Sim can deal random amount of damage (uniformly distributed) to the active char randomly either once at a set time, or every so often at a set interval (picked randomly between this interval, uniformly distributed)

## Simulating energy

```
energy once interval=300 amount=1; #once at frame 300, drop 1 small particle
energy every interval=200,300 amount=1;
```

Energy behaves similar to taking damage
