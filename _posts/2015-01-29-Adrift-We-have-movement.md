---
layout: post
title: Adrift - We have movement
date: 2015-01-29
---

A floating, rotating island is very pretty. But, we need more than that for a game. Namely, we need a way to navigate over, around and through said island.

Before movement, we also need input. I don’t really need to say much about this, as LibGDX makes input super simple (at least where keyboard and mouse are concerned). It even provides methods to test if a key is held or just tapped, where the mouse is and how far it has moved since we last asked. This has saved me plenty of donkey work writing boring input handling stuff.

The first, easiest kind of movement to implement was actually flying rather than walking. Rotate the player using the mouse, and press forward to move. Walking and jumping were not much more difficult, just adding acceleration due to gravity and removing the y-axis component from the “flying” direction.

Once we have input and movement, the next task is to keep the player _on_ the ground, rather than _in_ the ground.

![The island as it stands](/assets/20150129/island.png)

Keeping the player outside of the terrain is actually very easy. Collisions in adrift are managed with simple AABBs, checked once per frame. I had read up on integrating the movement over several time steps, or using swept collisions with oriented bounding boxes, and several other sophisticated ways of dealing with person / ground intersection, but these turned out to be unnecessary.  The system as it stands hangs together very nicely, even at pretty high speeds.

The final challenge was less of a technical one, and more a problem in need of a creative solution. Flying can get you anywhere, but makes the game too easy. Walking is much closer to what I want for the game, but could be too limited. The random terrain generator makes islands that have all sorts of unpredictable features. There are steep hills, deep caves and tiny holes to spelunk into. I don’t really want to tone down the possibilities, but I also don’t want navigation around the island to be a chore or, worse, cause the player to get completely stuck.

The solution, for now, is the simplest one that I could think of.  To prevent the player from not being able to get into a cave with a tiny entrance, I just made them smaller than the smallest possible terrain feature (one block in our blocky minecraft-esque world). And to prevent the possibility of an intrepid adventurer falling down into a cave that they cannot get out of, there is a limited flying ability: pumping the jump key repeatedly causes the player to gradually gain altitude. This might have to be toned down in the future, it does make it exceptionally easy to just fly around the island quickly rather than having to actually explore it.

But for now, we have movement.