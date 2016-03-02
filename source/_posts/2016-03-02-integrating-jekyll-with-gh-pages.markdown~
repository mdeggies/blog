---
layout: post
title: "Integrating Jekyll with gh-pages"
author: Michele Degges
date: 2016-03-02 00:29:36 -0800
comments: true
categories: [jekyll, octopress, gh-pages]
---

Integrating Jekyll with gh-pages shouldn't take more than 15 minutes. The idea is simple: you already have a personal website hosted on yourusername.github.io. The goal is to create a blog and host it on yourusername.github.io/blog. Sounds easy, right?!

Well, not so fast.. Jekyll and gh-pages are not the stellar, easy-going couple that they claim to be. Integrating the two- especially when you already have a static site at yourusername.github.io- is not such an easy task.

In comes Octopress! Octopress is a static blogging framework built on top of Jekyll. It's supposed to allow for easy integration and deployment. I was so excited when I found out it existed.. but then I started reading through it's documentation and my excitement fizzled out pretty quick.

# The goal

We know the goal- to get a blog up and running on gh-pages- specifically, gh project pages- since we already have a site at yourusername.github.io

# The steps

First, create a new repo on github.com called blog. This is where our octopress site will live. Copy the location (https://github.com/yourusername/blog.git).

In your terminal, navigate to the directory you want to create and edit your blog project in. In that directory, perform these commands:  

- git clone git://github.com/imathis/octopress.git blog
- cd blog
- git init
- git add .
- git remote add origin https://github.com/yourusername/blog.git
- git commit -m "initializing octopress"
- git push origin master

You've just initialized your blog project with Octopress! Now let's set everything up:

- gem install bundler
- bundle install
- rake setup_github_pages

At this point, you'll be asked to give a repository url. Use the same url you copied from github (https://github.com/yourusername/blog.git)

- git	config branch.master.remote origin
- rake install
- rake generate
- rake deploy
- rake preview

Rake install will install the default Octopress theme on your site. Generate and deploy will get it running, and preview will allow you to preview your site locally at localhost:4000

# HOLD UP!!

There's one last step you need to follow to get your blog up and running! Navigate to the _config.yml file in the root of your blog project. In addition to changing the default info in 'Main Configs' to your info (url will be https://yourusername.github.io/blog - title will be whatever you want - author will be your name - etc) you must do one more thing!

Navigate to the 'Jekyll & Plugins' section. Change the option 
##### root: / 
to  
##### root: /blog 

This will point the root url of your site to the correct page. Don't forget to do this step, or none of your styling will be visible (as you will be doing GET requests to the wrong urls!) 

After adding, committing, and pushing your changes to github, you'll be able to view your blog at yourusername.github.io/blog

# Optionally install a new theme

To install a new theme, such as ioveracker's MNML, follow these steps:

- git clone git://github.com/ioveracker/mnml.git .themes/mnml
- rake install['mnml']
- rake generate
- rake deploy
- rake preview


# And that's how it's done

As always, don't forget to git add .&& git commit -m "updating site.." && git push -u origin master to save your changes and make them visible at yourusername.github.io/blog

If you have any questions, feel free to hit me up at mdeggies@gmail.com, or message me on twitter. 
