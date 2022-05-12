---
layout: post
category: blog
title: Developing/Managing my Website with Jekyll and Netlify CMS
date: 2022-05-19T17:00:12.668Z
description: How I made the website you are on by using a Jekyll template and Netlify CMS.
tag:
  - webdev
  - tutorial
author: ricardorodrigues
---
Perhaps you are interested in making your own website, but you are poor just like me! After looking at the most common choices to make a website, like CMS (e.g. WordPress, Joomla, Drupal) or Website Builders (e.g. Wix, SquareSpace, Weebly), you come to the conclusion that **(1)** you don't want to pay for hosting a web server, **(2)** you don't want to pay for someone to make it. So what can you do?

## Hosting

Regarding a place to put your website, I found [Github Pages](https://pages.github.com/) a good solution and while there may be other platforms that might offer the same behavior, I use this one. I followed the instructions in the link above and create a public repo name `ricardoeprodrigues.github.io`. I invite you to play around with it and learn the ropes.

## Jekyll Template

Now that we have free and (mostly) easy-to-use hosting, we can focus on building our own page. First off, Github Pages uses [Jekyll](https://jekyllrb.com/), "a simple, blog-aware, static site generator perfect for personal, project, or organization sites", so that's exactly what we'll use (hey it is free, so why not?). Now, being the lazy guy I am, I don't want to build a website from scratch, so I looked into website templates. The internet is an amazing place filled with wonderful (and free!) things, so I ... **\*[yoink](https://www.youtube.com/watch?v=MJq8IxTxkLQ) this*** [Indigo Minimalist Jekyll Template from Sergio](https://github.com/sergiokopplin/indigo), and started hacking (note that my page no longer has the default version present on the template, more on that later). 

![Indigo Minimalist Jekyll Template](https://raw.githubusercontent.com/sergiokopplin/indigo/gh-pages/assets/screen-shot.png "This is what the Indigo Minimalist Jekyll Template looks like.")

Following the website setup, I got everything going and finally had my own website online and free! (I hope this joke doesn't get old too fast.) If you want a minimalist website without a hassle and don't mind editing some [Markdown](https://www.markdownguide.org/) files with your content, then this is for you! The template offers Blog posts, Projects, an About page, and even a way of showing your Curriculum Vitae! Edit away and you can stop reading here.

## My Jekyll Template

*I wanted more!* After going through some of the code and how things work, I started feeling like tweaking and changing things, making it my own version of the template. My designer veins decided to add an accent color (the text selection color is also changed), then some "cool" backgrounds, and I made it so the theme changes depending on system preference (now it syncs with the dark theme, \*\*groovy\*\*). Just add some values to your config file and there you go!

```yaml
# These are the definitions I use on the website.
# site color theme, true for dark theme, false to light theme, auto to switch with system.
dark-theme: auto
accent-color: "#308941"
accent-color-dark: "#41A700"
background: "linear-gradient(315deg, white 0%, white 60%, #D9FFE0 100%)"
background-dark: "linear-gradient(315deg, black 0%, black 60%, #143300 100%)"
```

But it wasn't enough! So my programmer's veins kicked in and I added more social media links, moved the Projects to be a separate Content-Type (or collection in Jekyll), although that creates some issues, and added ***buttons!*** like these:

<div class="buttons-container">
    <a class="button">A Button</a>
    <a class="button">Another Button</a>
</div>

If you want to use my template and add them to your posts and pages you can use this code snippet:

```html
<div class="buttons-container">
    <a class="button" href="https://ricardoeprodrigues.github.io/" target="_blank" rel="noopener noreferrer">Visit Ricardo's Website!</a>
    <a class="button" href="https://quenestil.itch.io/" target="_blank" rel="noopener noreferrer">He also makes Games!</a>
</div>
```

Finally, I have a website that is my own! With the tweaks and stuff and all!

## CMS

You may ask *"What about the content? Do you still add it by hand? Writing `.md` files every time you want to add new content?"* To that, I say "Of course not you dummy! 😎😎😎 I use [Netlify CMS](https://www.netlifycms.org/)."

Dealing with the Markdown files isn't so bad, so if you are OK with it, great, less work for you! Yet, this won't really be a full website without a way to edit posts easily, without downloading the project and editing everything directly. This is where [Netlify CMS](https://www.netlifycms.org/) comes in, it is an "open source content management for your Git workflow. Use Netlify CMS with any static site generator for a faster and more flexible web project." The magic is in the last sentence, you can use this Netlify CMS with any static site generator (in our case, Jekyll). In essence, we use Netlify CMS to generate `.md` files, that will be compiled by Jekyll in static HTML files, and then displayed in Github Pages!

Unlike the other sections, I think this one deserves a bit more details, as I didn't see a lot of good tutorials discussing this topic of connecting Netlify CMS with Github, although a mix of multiple gave me the answers ([Link 1](https://www.netlifycms.org/docs/github-backend/), [Link 2](https://cnly.github.io/2018/04/14/just-3-steps-adding-netlify-cms-to-existing-github-pages-site-within-10-minutes.html), [Link 3](https://github.com/netlify/netlify-cms/issues/770#issuecomment-482293908)).

(WIP)