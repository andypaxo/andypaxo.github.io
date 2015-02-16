---
layout: post
title: Adrift - Building an island
date: 2015-02-14
---

The basic building blocks of Adrift are, well, blocks! The piles of blocks which make up the island are generated using Perlin noise which is a technique that has been discussed and explained many, many times ([Here, for example is one nice tutorial](http://libnoise.sourceforge.net/tutorials/tutorial3.html "Libnoise tutorial")). However, as the technique is so integral to Adrift, I'll give a quick rundown here.

The pedant in me wishes to interject right now that Adrift actually uses simplex noise, rather than Perlin, but the method is identical.

The question in generating terrain is how to make something which is fairly random (so each island is unique) without being *completely* random (the terrain should still consist of recognizable objects, such as hills and lakes). There are a great many ways of doing this, but the simplest for a quick start is to use a noise algorithm. Here's a rundown in 2D of how this works, imagining the same process in 3D is left as an exercise for the reader.

On the left, what complete randomness looks like. On the right, what we want to achieve:

<img alt='step 1' src='/assets/20150214/terrain-gen-1.jpg' style='max-width:600px' />

First of all, we simply get a smooth noise algorithm, such as [simplex noise](http://webstaff.itn.liu.se/~stegu/simplexnoise/simplexnoise.pdf "Simplex noise demystified") and we run it. This produces a nice curve, like this:

<img alt='step 2' src='/assets/20150214/terrain-gen-2.jpg' style='max-width:600px' />

Nice, but a little dull. We can then add "octaves" of lower amplitude but higher frequency noise to give the terrain some roughness:

<img alt='step 3' src='/assets/20150214/terrain-gen-3.jpg' style='max-width:600px' />

That's looking like a nice slice of terrain, but what we want is  an island, so we can't have it so tall at the edges. We can multiply all the heights on that line with the kind of shape that we want to see in order to scale our terrain into the right shape.

<img alt='step 4' src='/assets/20150214/terrain-gen-4.jpg' style='max-width:600px' />

Part of the "interesting-ness" of the islands in Adrift are the caves that we can go explore. Let's add those now. This is where we get our one dimensional line, and combine it with two dimensional noise, which looks like this:

<img alt='step 5' src='/assets/20150214/terrain-gen-5.jpg' style='max-width:600px' />

Okay, that's shaping up to look like the right kind of, well, shape. The islands of Adrift are made out of big blocky cubes, so we need to transform that continuous contour into squares. (As an aside for the more technical reader, the simplex noise algorithm really gives us a density map, so our contour is actually the threshold of where the density value crosses a specific point). Our finished product comes out like this:

<img alt='step 6' src='/assets/20150214/terrain-gen-6.jpg' style='max-width:600px' />

Each colour (in this case white and green) corresponds to an integer values. The resulting multitude of integers are simply stored in an array, which is then used for lighting, collisions and, of course, making the 3D model of the island that you see in the game.