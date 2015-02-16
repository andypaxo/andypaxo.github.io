---
layout: post
title: Adrift - On abstraction, and levels thereof
date: 2015-01-17
---

I'm starting to carve out the code for "adrift", as it is called for now. And, as at the very beginning of any software project, technologies must be chosen. (I think it's good practice to defer as many technology decisions as possible as late as possible, but you have to begin somewhere).

The biggest decision right now is how low level and nitty gritty to go. There's a trade-off between wanting fine grained control of everything, and having the convinience of letting someone else take care of decisions and just focusing on the game. I considered three different levels of this control / convenience trade-off:

1. Direct to graphics driver (via Java or C# bindings, I'm not interested in coding OpenGL or DirectX in C)
2. A game library, such as XNA or JMonkeyEngine
3. A graphical game building tool, such as Unity

I started out with learning how option 1 (using OpenGL via LWJGL) would go. I went down that route for a couple of reasons. Firstly because I love learning and making, secondly because I've run into trouble with game libraries before by simply not knowing what they are doing "under the hood". After a week or so of following tutorials it became evident that I was making progress too slowly to reach the milestones I've set for myself.

So, about a week ago, I switched to a higher level game library. Namely LibGDX. I'm making much smoother progress now. LibGDX has a learning curve of its own, but not quite as steep as learning to make your own world to camera space transform matrices.Also, I have tried out using LibGDX before. It makes much more sense now with a little more knowledge OpenGL, so the first week was not in vain!

I'm not really considering the third option terribly seriously. I'm too much of a control freak to have a big black box like the Unity engine at the heart of this project.

So, LibGDX it is!