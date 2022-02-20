---
sidebar_position: 3
title: Action Priority Mode Guide
---

# Basics
Action Priority Mode action lists work as a priority queue, so what happens is that whenever it is possible to run a new action, the sim will scan through the action list that you provided from top to bottom, and will pick the first possible one to run. The benefit of this approach is that you are not beholden to a purely fixed rotation, which allows you to run a single action list across a wide variety of situations. For example, a single action list can easily account for situations where Sacrificial Sword procs vs. situations where it does not proc with a few conditionals. Furthermore, Priority Mode action lists allow for on the fly adjustments related to other sources of RNG such as elemental particle production, which can alter rotations.

This mode will result in much more flexible action lists that tend to provide a more accurate view of overall team DPS if it is based on many random elements with high variance (sac procs, fav procs, etc.), and also allows for simming desync/quickswap style teams.

# Creating a New Action Priority Mode Action List
The exact way that you think about this may vary, but one way to build these is to start from a video source, put in the basic blocks that are in that video, and then refine as necessary by moving blocks around and adding conditionals as needed.

So for example, let's say that you are interested in building an action list for a Raiden-Beidou-Bennett-Xiangling desync team. In that case, your basic blocks would look like the below, which I've annotated with comments.

```
# Always want to do a full Raiden attack chain in burst
raiden attack:4,dash,
       attack:4,dash,
       attack:4,dash,
       attack:2,charge
       +if=.status.raidenburst>0;

# Refresh Raiden skill
raiden skill
       +if=.status.raidenskill<240;

# Bennett should burst whenever he can
bennett burst;

# Xiangling and Raiden needs Bennett snapshot
xiangling burst,skill
          +if=.status.btburst>0;

raiden burst
       +if=.status.btburst>0 && .status.beidouburst<120;

# Beidou needs to snapshot Bennett buff
beidou_swap:beidou swap;
beidou_bt:wait_for mods value=.beidou.bennett-field==1 max=100;
beidou_bt_burst:beidou skill,burst,attack;
chain beidou_swap,beidou_bt,beidou_bt_burst
       +if=.status.btburst>0;

# Beidou needs to wait to catch her own particles
beidou_particle:wait_for particles value=beidou max=200;
beidou_skill:beidou skill[counter=2],attack;
chain beidou_skill,beidou_particle
      +if=.energy.beidou<70;

# Funnelling Xiangling
bennett attack,skill
        +if=.status.beidouburst>240&&.energy.xiangling<70 && .status.btburst == 0
        +swap_to=xiangling;

# Gap fill
bennett skill;
xiangling attack +is_onfield;
bennett attack +is_onfield;
```

Most of the conditionals above use frame counts aside from the obvious energy conditionals, but otherwise they are the key to ensuring that your action priority mode list works as intended. After assembling the basic blocks, you can then move them around to ensure that their ordering matches the ordering of how you would perform them at any given moment in game.

For example, the reason why the Raiden 3N4DN2C block is up top is because I would always want to finish that regardless of if Xiangling burst came off of cooldown during that combo. Similarly, funnelling Xiangling is down close to the bottom since that's really the last thing that I would want to be doing, as making sure that I'm bursting off of cooldown appropriately is far more important.

# Syntax Details
Action priority mode has a lot more in depth syntax than calc mode. For more details, see the [Action List Reference](../reference/configuration/action-list.md).
