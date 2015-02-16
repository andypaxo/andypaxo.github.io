---
layout: post
title: Adrift - Throwing Shapes
date: 2015-02-16
---

Another post with a technical / pedagogical bent!

In the last blog post, we built an island as an array of numbers. That's great, but a video game player is probably going to want to see more than just a huge grid of digits (unless said player is into Dwarf Fortress, but that's a different story). What we really want is a 3D view. We do that by making a big array of vertices to pass to OpenGL.

The process for doing this is very simple. Just go through the entire array of terrain data, every x, y and z of it, and if there is solid ground there, spit out a cube. I won't go into the details of simple creating polygons here, [other people have done that in much more depth](http://arcsynthesis.org/gltut/ "arcsynthesis OpenGL tutorial").

Which is exactly what Adrift does, aside from one caveat. Doing things that way would create far too many polygons, so we only actually create the faces of the cube which are visible (in other words, ones which are touching air). This means that most solid blocks, which are buried underground, don't get any polygon data.

![Step 1](/assets/20150216/shapes-1.jpg)

To see it, we add some crude lighting (courtesy of LibGDX's default shader and a directional light), and some very basic shadows, which I'll cover in a later post... and we get this: 

![End result](/assets/20150216/shapes-2.jpg)