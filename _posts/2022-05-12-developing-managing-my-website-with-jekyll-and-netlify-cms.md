---
layout: post
category: blog
title: Developing my Website with Jekyll and Netlify CMS
date: 2022-05-12T21:55:51.917Z
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

*I wanted more!* After going through some of the code and how things work, I started feeling like tweaking and changing things, making it my own version of the template (the source code can be found on [my Github page](https://github.com/RicardoEPRodrigues/ricardoeprodrigues.github.io/)). My designer veins decided to add an accent color (the text selection color is also changed), then some "cool" backgrounds, and I made it so the theme changes depending on system preference (now it syncs with the dark theme, \*\*groovy\*\*). Just add some values to your config file and there you go!

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

If you want to use [my template](https://github.com/RicardoEPRodrigues/ricardoeprodrigues.github.io/) and add them to your posts and pages you can use this code snippet:

```html
<div class="buttons-container">
    <a class="button" href="https://ricardoeprodrigues.github.io/" target="_blank" rel="noopener noreferrer">Visit Ricardo's Website!</a>
    <a class="button" href="https://quenestil.itch.io/" target="_blank" rel="noopener noreferrer">He also makes Games!</a>
</div>
```

Finally, I have a website that is my own! With the tweaks and stuff and all! ([See the source on my Github page](https://github.com/RicardoEPRodrigues/ricardoeprodrigues.github.io/)).

## CMS

You may ask *"What about the content? Do you still add it by hand? Writing `.md` files every time you want to add new content?"* To that, I say "Of course not you dummy! 😎😎😎 I use [Netlify CMS](https://www.netlifycms.org/)."

Dealing with the Markdown files isn't so bad, so if you are OK with it, great, less work for you! Yet, this won't really be a full website without a way to edit posts easily, without downloading the project and editing everything directly. This is where [Netlify CMS](https://www.netlifycms.org/) comes in, it is an "open source content management for your Git workflow. Use Netlify CMS with any static site generator for a faster and more flexible web project." The magic is in the last sentence, you can use this Netlify CMS with any static site generator (in our case, Jekyll). In essence, we use Netlify CMS to generate `.md` files, that will be compiled by Jekyll in static HTML files, and then displayed in Github Pages!

Unlike the other sections, I think this one deserves a bit more details, as I didn't see a lot of good tutorials discussing this topic of connecting Netlify CMS with Github, although a mix of multiple gave me the answers ([Link 1](https://www.netlifycms.org/docs/github-backend/), [Link 2](https://cnly.github.io/2018/04/14/just-3-steps-adding-netlify-cms-to-existing-github-pages-site-within-10-minutes.html), [Link 3](https://github.com/netlify/netlify-cms/issues/770#issuecomment-482293908)). I'll steal some bits from one tutorial and another, so here it goes.

### Creating a GitHub OAuth App

*Originally from [Link 2](https://cnly.github.io/2018/04/14/just-3-steps-adding-netlify-cms-to-existing-github-pages-site-within-10-minutes.html)*.

First, go to [GitHub Dev Settings](https://github.com/settings/developers) (<https://github.com/settings/developers>) and click **New OAuth App**.

Enter whatever you like for the **Application name** and **Homepage URL** (I used "Personal Website CMS" and "<https://ricardoeprodrigues.github.io/>", respectively).

In the **Authorization callback URL**, enter: `https://api.netlify.com/auth/done`.

Once finished, leave the page in the background. You will need the **Client ID** and **Client Secret** on this page later.

### Creating a Netlify Site

*Taken from [Link 2](https://cnly.github.io/2018/04/14/just-3-steps-adding-netlify-cms-to-existing-github-pages-site-within-10-minutes.html)*.

Go to [Netlify](https://app.netlify.com/account/sites) and create a new site from… *any* repo. We are not really using Netlify to host that, anyway. (I used the Github Pages repo, but it doesn't really matter.)

After that, go to **Settings**, and copy your **Site name**. It should be something like `octopus-cat-123456`.

From the sidebar go to **Domain Management** and add your GitHub Pages domain (`you.github.io`) as a custom domain. Choose **Yes** when asked if you are `github.io`'s owner.

From the sidebar go to **Access control**, scroll down to **OAuth** and click **Install provider**.

Choose **GitHub** as a provider, and enter the **Client ID** and **Client Secret** from the GitHub OAuth app page mentioned above.

Then you can close the Netlify and GitHub webpages.

### Back to basics

Now we can create our CMS instance. This CMS depends on a `admin` folder with a `HTML` file for the interface and a `config.yml` that defines its behavior (more details are on the [official documentation](https://www.netlifycms.org/docs/add-to-your-site/)). While avoiding too much detail, let me show you the important bits.

Create the `admin/index.html` based on this template that grabs scripts from a public CDN:

```html
<!--As seen in https://www.netlifycms.org/docs/add-to-your-site/ -->
<!doctype html>
<html>
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Content Manager</title>
</head>
<body>
  <!-- Include the script that builds the page and powers Netlify CMS -->
  <script src="https://unpkg.com/netlify-cms@^2.0.0/dist/netlify-cms.js"></script>
</body>
</html>
```

Now we create our `admin/config.yml` (some elements were simplified - the current implementation can be found on [the Github page](https://github.com/RicardoEPRodrigues/ricardoeprodrigues.github.io/blob/gh-pages/admin/config.yml) -, for more information visit [the official documentation](https://www.netlifycms.org/docs/add-to-your-site/)):

```yaml
# This variable determines what connection the CMS will use to update the website.
# See more here https://www.netlifycms.org/docs/backends-overview/
backend:
  # we want to use the github backend
  name: github
  # our repo
  repo: RicardoEPRodrigues/ricardoeprodrigues.github.io
  # the branch to push to
  branch: gh-pages
  # IMPORTANT: this determines the domain and allows for the redirects to work. 
  # Without this Login in to the CMS is not possible.
  site_domain: ricardoeprodrigues.github.io


media_folder: "assets/uploads" # Media files will be stored in the repo under images/uploads

collections:
  # Some collections (pages and projects) were ommited for this example.
  - name: "blog" # Used in routes, e.g., /admin/collections/blog
    label: "Blog" # Used in the UI
    folder: "_posts" # The path to the folder where the documents are stored
    create: true # Allow users to create new documents in this collection
    slug: "{{year}}-{{month}}-{{day}}-{{slug}}" # Filename template, e.g., YYYY-MM-DD-title.md
    editor:
      preview: false # This avoids ill-rendered pages in the editor for Jekyll.
    fields: # The fields for each document, usually in front matter
      - {label: "Layout", name: "layout", widget: "hidden", default: "post"}
      - {label: "Category", name: "category", widget: "hidden", default: "blog"}
      - {label: "Title", name: "title", widget: "string"}
      - {label: "Publish Date", name: "date", widget: "datetime"}
      - {label: "Description", name: "description", widget: "string"}
      - {label: "Show Header Image", name: "headerImage", widget: "boolean", required: false}
      - {label: "Header Image", name: "image", widget: "image", required: false}
      - {label: "Tags", name: "tag", widget: "list", required: false}
      - {label: "Author", name: "author", widget: "string", default: "ricardorodrigues"}
      - {label: "External Link", name: "externalLink", widget: "string", required: false}
      - {label: "Body", name: "body", widget: "markdown"}
```

Now if we commit and wait a few minutes a new page on our website will be available under `https://you.github.io/admin`. It is over!

## It's ALIVE!

Finally, we have the complete website! It includes a theme you selected and edited. Not only that, but it is also dynamic, in which you are able to open a CMS and create/modify/delete your content from your website!

If we want to summarize into steps, you need to:

1. Set up a [Github Pages](https://pages.github.com/) repo.[](https://pages.github.com/)
2. Select and configure a Jekyll template.
3. Configure your Netlify CMS instance.
4. ???
5. Profit!

I hope you find this post useful and feel free to [fork my repo](https://github.com/RicardoEPRodrigues/ricardoeprodrigues.github.io) to make your own pages!