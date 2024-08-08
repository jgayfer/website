---
author: James Gayfer
title: My intro to game (engine) dev
description: How I discovered the joy of game development, despite staunchly avoiding it for years.
featured: false
postSlug: intro-to-game-dev
pubDatetime: 2024-08-07T12:00:00.000Z
tags:
  - personal
  - gamedev
---

I wrote my first line of code in January of 2013. I wasn’t pursuing a career
in software at the time, but I enjoyed writing code enough to give it a
serious try. Unlike many young aspiring programmers, learning how to make
games was not a priority for me. In fact I actively avoided it throughout
my education and early career.

At the time game development didn’t appeal to me. I was concerned about
turning a hobby into a career (and killing the enjoyment). I was told that
game development could involve long hours and lower salaries. But if I’m
being honest, the main reason I shied away from game development was imposter
syndrome. Bearing fresh scars from first year calculus, I didn’t think I
had what it took to succeed in game development. My peers spoke of the math
required in their graphics classes. It spooked me. My strategy in university
was to avoid hard things, and graphics certainly seemed hard. I was afraid
of failure.

I successfully avoided game development for the next 11 years. Then one day
this spring, I decided to try making a game. These days I have a different
mindset around trying new things. I love exposing myself to new things, and
I embrace failure. I find deep satisfaction in learning, especially when it
comes to mastering a craft.

The two game engines I played around with were
[Godot](https://godotengine.org/) and [Bevy](https://bevyengine.org/). I
initially tried Bevy, but became fatigued with how much mechanical work
was needed for basic things (it’s not a feature complete engine yet). I
switched over to Godot, but very quickly tired of doing everything in a
GUI. I realized I wanted to understand what was happening under the hood. I
didn’t want to make a game; I wanted to learn how games were made.

Bevy didn’t (and still doesn’t) have first party support for 2d lighting. I
was mostly interested in 2d games, specifically top down games like Zelda,
which in my mind need some basic lighting. I didn’t want to go back to
Godot, so I decided it was time to roll up my sleeves and tackle 18 year
old me’s greatest fear: rendering.

The amount of learning was astronomical. It was intoxicating. Render pipelines,
shaders, light maps, signed distance fields, shadows. I loved the learning
process. I even started reviewing some Bevy rendering PRs to further my
understanding. Many of my evenings were spent writing down my learnings,
soaking up as much as I could. Applying my years of programming knowledge
to a completely new paradigm was liberating.

After a few weeks of hacking away, I had a working 2d lighting
implementation. It was basic, offering only point lights and ambient
light, but the final API wasn’t bad. I released it on crates.io under
the name [`bevy_light_2d`](https://crates.io/crates/bevy_light_2d),
and was pleased to see a few people start using it. I’ve
continued to tinker on the library, with the most recent addition
being light occlusion and dynamic shadows. You can find a demo on
[Mastodon](https://fosstodon.org/@jgayfer/112913186285363067). I’d like
to thank [Miguel Albernaz](https://github.com/malbernaz) for helping with
the implementation.

My fervour for game development has come down to a simmer, but the highs
of my initial learning will not be forgotten. I plan to continue working on
[`bevy_light_2d`](https://github.com/jgayfer/bevy_light_2d), but I’d also
like to make a proper game in the near future.

Despite years of avoiding it, learning the ins and outs of graphics and
rendering has been some of the most fun I've had with programming since I
first learned to code.
