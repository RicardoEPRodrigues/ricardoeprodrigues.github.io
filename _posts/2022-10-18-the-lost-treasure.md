---
layout: post
category: blog
title: The Lost Treasure
date: 2022-10-19T23:00:00.000Z
description: An exploration on how to creating sensations in a 3D environment.
headerImage: true
image: /assets/uploads/losttreasure11.png
tag:
  - game
  - ue4
author: ricardorodrigues
hidden: false
published: true
---
During my Master's degree, in 2015, I took a course on 3D Programming. Although I do not remember much of the course, the final project was one of the most exciting challenges in the degree.

The students would propose concepts of sensations to be implemented in a real-time cinematic in a game engine. My group (of three students) decided to tackle the feeling of claustrophobia, mystery, and awe. I was responsible for the sensation of mystery. We decided to design a cinematic where the viewer would start at the entrance of a cave, start moving into it, pass through a claustrophobic corridor almost entirely submerged, and then be led to an old temple with a skylight, where they would find and open an old chest filled with treasures. Here is the report where we describe the whole process (it is written in Portuguese):

<object data="{{ site.url }}/assets/uploads/the-lost-treasure-report.pdf" width="800" height="500"></object>

I remember exploring a way of painting moss on bricks by using a custom shader and vertex color to define areas where you would want to paint the moss. If the color was black no moss would appear, red color would paint moss in the crevices, while green would scatter moss over the brick (mixing the two colors, resulting in yellow, would present both).

![Moss painting on brick depending on Vertex color](/assets/uploads/moss-vertex-paint.png "Moss painting on brick depending on Vertex color")

Check out the final result of the project in the video below:

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/CyGn7-4ckyw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>