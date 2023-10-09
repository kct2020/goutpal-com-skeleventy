# GoutPal.com Admin Area
![GoutPal Logo](https://goutpal.com//images/friendly-help-for-gout-620.webp "GoutPal's Friendly Help For Gout")

Gout sufferers can ignore this and go straight to [GoutPal's Gout Forum](https://links.goutpal.com/p/goutpal-links-gout-discussions?a=888958067). Where you can chat with fellow gout sufferers. Also, seek personal help about any GoutPal page.

For anyone who wants to contribute as a programmer/technician/author, you can start by helping me improve this page. Or get involved with resolving Issues.

## 220329 Tech Note
Because I don't want to lose this URL replace tip, I'm noting it here so I don't lose it:
`git grep -l 'https://keith-taylor.pages.dev' | xargs sed -i 's|https://keith-taylor.pages.dev|https://shrewdies.net|g'`
Props https://blog.jasonmeridth.com/posts/use-git-grep-to-replace-strings-in-files-in-your-git-repository/ and https://gist.github.com/msamendinger/c2da6f5fafc43e72ef576a0cc7ad0165?permalink_comment_id=3820228#gistcomment-3820228

## 220524 Project Note
I need to update the social media tags in Skeleventy. Because the Open Graph image is set to a Skeleventy logo. Which makes all social postings, and Google Search Engine results, use a Skeleventy banner instead of my featured image. At the same time, I noticed other issues, so here are the changes that I need to apply to all my Skeleventy templates:
- site/includes/components/social-meta.njk
 - twitter length from 140 to 280
 - og length from 140 to 300
 - og:image from {{ site.images.og }} to {{ page.post_image }}
 - twitter:image:src from {{ site.images.twitter }} to {{ page.post_image }}
- site/includes/layouts/post.njk
 - added             "url": "{{ site.author.url }}"
 - publisher.logo.url from /images/meta/article-schema.png to /images/meta/apple-touch-icon.png
- site/globals/site.json
 - added         "url": "https://shrewdies.net",


## 220207 Project Note
This README needs rewriting to describe how to contribute to GoutPal. Most importantly, all regular contributors need to focus on is Issues and Discussions. Eventually, I can include a link for people who wish to make technical contributions to this template.

Also, I will add notes here about technical issues. Though they should become part of the template documentation. In short, I need a workflow for maintaining template changes.

Workflow for maintaining content also needs to refine how Gitpod is deployed. Because my earlier test of recompiling within Gitpod isn't quite working for me. In particular, I need to address 2 specific workflows for content-only changes and for template layout changes.

Today I have deleted gitpod.yml:
`tasks:
  - init: npm install
    command: npm run dev`

But later I need to refine how and when running npm in gitpod is better than running it on deployment to Cloudflare Pages.

## Original README
This template can be used to create a new website. Also, that new website can optionally include WordPress Transmigration.

Intention is to deploy this using Cloudflare Pages. But it should also work fine on Netlify and similar platforms. Deployment is usually done:

1. Trial Deployment after committing 1st Config Changes (minimal changes to make sure deployment works).
2. Import WP or Add Admin (gets content). Note, for WP Transmigration, there are steps needed to prepare the zip file for import. E.g., remove Cloudflare apps, check footer, create Simply Static file.
3. Complete config changes. Aim is for all these to be in `site/globals/site.json`. But otherwise search for `UpdateThis`.
4. Create pre-launch content.

## 1. 1st Config Files
- This readme project note
- site/globals/site.json

## 2. Optional Import WP
- Upload wp-static.zip to wp folder
In Terminal:
- cd wp
- unzip wp-static.zip
- rm wp-static.zip
In Gitpod explorer
- rename wp/index.html 

If you're not importing WordPress, you can optionally remove the config instruction:
- eleventy.config.js config.addPassthroughCopy({ "wp/": "/" })

## 3. Look and Feel
These are current working notes. Eventually, this is about setting colors, background-image (if any), header images.

- resources/scss/04-layout/_site.scss: change background to image to a different color. Not sure if this needs changing in main.css and/or main.min.css *
- site/includes/components/nav.njk: Change link to WP version of About Page or to appropriate blog post. 

Should be simplified to search for UpdateThis (including About Page link above). Except that should be split to UpdateSetting and UpdateContent to change 1st Config or Start Blog - meaning that look and feel is a simple part of installing in most cases. But might consider 2nd Config once content has been added to change text/background and other layout settings for a different look.

- site/index.md: rewrite.
- site/includes/components/footer.njk: Change footer links. But these need updating as new admin pages are created. Should also include a feedback link direct to issues.
- site/includes/components/footer.njk: Change disclaimer
- Change favicon.icon (root) & images/meta/apple-touch-icon.png. 

* I got confused by the way css works in this setup and I hacked the background image 
in css/main.css and css/main.min.css which seem identical. Need to learn the 'right' way to edit css in this template! Which is probly something to do with this note in the original readme...

CHANGE these notes to reflect how the process actually works. Also, resources/scss/04-layout/_site.scss and related files only need changing if text/background colors change from template settings. Because primary/secondary are set in 1sr config.

### The build pipeline

[Laravel Mix](https://laravel-mix.com/docs/5.0/basic-example) gives us a nice API layer on top of Webpack. Skeleventy uses a simplistic set up, but you _can_ take advantage of extending Mix with custom Webpack configurations, code splitting and plugins such as PostCSS, if you so wish.

You'll find the site's uncompiled SCSS and JS within `resources/` where Mix will be watching these directories for any changes. **Tip:** _it's best to always restart the server when creating any new partials or folders_

#### SCSS

- `scss/` is structured into opinionated sub folders
- The `_config.scss` file is where you can change the site's colours and the utility classes generated by Gorko

## 4. Start Blog

Amend or replace examples. Note, this will eventually include all admin pages as blog posts with 'using' tag.

