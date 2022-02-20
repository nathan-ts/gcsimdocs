---
sidebar_position: 4
title: Advanced KQM Standards and Alignment to Sheet Calcs
---

# Simming for Team DPS Calculations per KQM Standards

## Getting Optimal Substats
The sim now supports a currently experimental substat optimizer, which is available on the desktop mode only. Please see [this page](../reference/modes/substat_optimizer.md) for further details.

Alternatively, you may manually calculate optimal substats and enter them into each character’s artifact substats. Below are a few general guidelines/tips for doing this manually in the UI.
- For nearly all teams/characters, the optimal is going to involve first putting enough substats into ER to meet your ER requirements, then dumping all possible substats into CR/CD. 
- If there are any substats remaining (e.g., if a character has no ER requirements then usually they will have 2 substats leftover, then you can just put them in the next most desirable DPS substat (e.g., ATK% for most characters, HP% for Hu Tao, etc.).
- The only tricky characters are those who have some type of stat sharing mechanic that works off of their own stats, such as Sucrose EM share, Kazuha Dmg% share, etc. Currently, basically all of the characters that have such a mechanic in game want to max out on the substat that contributes to their sharing mechanic since it is also their best damage substat.
- For any character where this is not true, you will likely have to just manually fiddle with the substats (preferably in increments of 5 to make sure it has a measurable impact) while running the sim to see if DPS changes significantly. If not, then it’s probably sufficient to leave it.

For my own purposes I’ve put together a calculator [here](https://docs.google.com/spreadsheets/d/1rGa-Fe5OtA68sA7rYoMtWXjjt8aBRwfgqWd-6xspLvE/edit?usp=sharing) that you can use if you want.

## Alignment to Sheet Calculations Using the KQM Standard
In general, sheet calculations should align somewhat closely to sim results, but not perfectly. In general, you should expect results that are within 5% of each other, but there are a few caveats to take note of:
- In general, sheet calculations are only done over 1 rotation, and the ER requirements are obtained using Zakharov’s ER Calculator. To align with that, you will want to limit the simulation so that it only runs over 1 rotation, as results will not align closely at all if you simulate over multiple rotations due to variance of particle generation. For example, it’s actually very possible for Fischl to rarely generate 0 elemental particles if you’re very unlucky with the RNG. In sheets this possibility is discarded, but it is a possibility in the simulation.
  - An alternative to doing this is by setting the number of HP particles to some absurd number to ensure that ER is never a problem.
- Sheet calculations may sometimes assume that random procs will always happen. For example, some sheet calculations will assume that Sacrificial weapons always proc, whereas this will not be the case in the sim. Unfortunately there is no easy way to align to such simplified calculations using the sim. In general for these situations the simulation is likely the “more correct” view since it properly takes these random events into account, so you should expect a higher divergence from sheet results in these situations.
