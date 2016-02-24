---
layout: post
title: Migrating my blog from Wordpress to Jekyll and GitHub Pages
comments: True
summary: Jekyll, how could I live without you? Die hard blogging with markdown in vim :) Also note that my site loads much faster now than when it was using Wordpress, impressive to say the least.
categories: [Projects]
tags: [Jekyll, blogging, tools, markdown, vim, ruby, wordpress, github]
image: blog-jekyll-github.png
---

[Jekyll](http://jekyllrb.com) is a static site generator, an open-source tool for creating simple yet powerful websites of all shapes and sizes. From the [readme](https://github.com/jekyll/jekyll/blob/master/README.markdown):

> Jekyll is a simple, blog aware, static site generator. It takes a template directory [...] and spits out a complete, static website suitable for serving with Apache or your favorite web server. This is also the engine behind GitHub Pages, which you can use to host your project’s page or blog right here from GitHub.

## Hello, Jekyll

Here are some links and notes from the migration I am doing from Wordpress to Jekyll: 

1. get started: very [good post](http://joshualande.com/jekyll-github-pages-poole/) which starts with the poole base theme.

2. you need to install some dependencies and I needed to changes to _config.yml to get it running locally, see [here](https://github.com/poole/lanyon/issues/124)

3. import posts from WP, see [here](http://import.jekyllrb.com/docs/wordpressdotcom/) and [Stackoverflow](http://stackoverflow.com/questions/31216857/import-wordpress-posts-in-jekyll) - how awesome:

        $ ruby -rubygems -e 'require "jekyll-import"; \
          JekyllImport::Importers::WordpressDotCom.run({ \ 
          "source" => "bobbelderbos.wordpress.2016-01-27.xml" } )'
        Downloading images for Chrome for web development
          http://bobbelderbos.com/wp-content/uploads/2010/03/...
            OK!
        ..
        ..
        Downloading images for How to programatically get a youtube movie trailer
        ..
            OK!
        Imported 151 posts

4. permalinks: easily configurable [here](http://jekyllrb.com/docs/permalinks/)
5. considering changing the Poole them to the nice two-column [Hyde theme](http://hyde.getpoole.com/)
6. write posts in markdown? [Not a problem](https://daringfireball.net/projects/markdown/)
7. I will update after having used Jekyll for some time ...

---

### Update 15.02.2016

I am using the awesome [dbyll theme](https://github.com/dbtek/dbyll) now with [Mr Robot (Sega) font](https://www.reddit.com/r/MrRobot/comments/3h3l31/mr_robot_font_to_download/). It took a bit of debugging / tweaking but I am very happy with the looks plus having full control of my blog from the command line! Besides no more heavy CMS (Wordpress), database dependency and (!) (buggy) plugins that affect performance. The site loads superfast!

![Jekyll loads way faster]({{ site.baseurl }}/assets/load_time_jekyll.png)



