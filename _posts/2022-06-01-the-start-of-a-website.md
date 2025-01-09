---
title: The start of a website
date: 2022-06-01
categories: [Homelab, Website]
tags: [homelab,website,github,self-hosted,jekyll]     # TAG names should always be lowercase
media_subpath: /assets/img/the_start_of_a_website
image:
  path: the_start_of_a_website.png
  width: 100%
  height: 100%
  alt:
---

# The start of a website
A long time ago I had the Idea to start a website where I could make posts about my new experiences with any kind of IT related tech. 
I tried allot of software to build a website as I felt that a simple HTML would be to much of a pain to watch to and which had less functionality. Wordpress or Joomla… not my kind of flavor to use. 
Although I have been using Wordpress for quite some time I felt that I had to search it somewhere else and put more effort into the purpose of running my own website. It had to be easy to use, minimal effort in maintenance and have some basic functionality. 
That’s where I found Jekyll!

## Jekyll
Jekyll is a website generator which uses plain-text to create the most amazing websites. Because Jekyll generates static websites with the use of Markdown templates, Nginx and best of all. No Database required! This changes the use for dependencies like MySQL, MariaDB or other database options. Of course you can use other options for the use of templates or how the website will be served. 

### Template rendering
-	Markdown
-	Textile
-	Liquid

### Webpage can be served by

-	Apache
-	Nginx

Jekyll has no complex configuration and is easily setup with the included YAML file. In this file we will configure a few options to make sure settings are configured and the website gets generated as intended. The documentation on this is pretty straight forward and not too hard to complete.
Another cool feature that you can use is the option to attache your website to Github. That way we can push new version updates like new pages, features or some changes to your website.

## Install Jekyll

So to start out there are a few different ways to achief this. I for myself played around and my way is usually not the best or most efficient way, but! It works.


If you are using windows to work with lets first install a Ruby devkit. You can download it [Here](https://rubyinstaller.org/)

Once you have installed Ruby and are able to start it we can continue. 

- Open up a Ruby instance
- Create a folder where you would like to build your website
- In the Ruby instance, go to the directory where your website will be

Within the ruby instance, do the following to get your new website running. 

Install the bundler
```shell
gem install jekyll bundler
```
Create your website and giving it a name
```shell
jekyll new nameofyourwebsite
```
To have a look at your website serve it. Once you are in the right directory and serving the page, it will be available localy to edit. It will also refresh itself so its easyer for your to edit new pages. Dont forget to give it a hard refresh by rerunning the local hosting. 
```shell
jekyll serve
```
---

## Build
Once you have the basics setup you can continue working on your website. You can also add theme's or fork it from other editors. The example I have been following is the [Chirpy Theme](https://github.com/cotes2020/jekyll-theme-chirpy)

You can fork a copy for yourself and edit the pages with Markdown. Every change you make can then be build with jekyll by using the next line.

```shell
jekyll build
```
This will create a new folder with all the raw website content. This is usefull if you run it in your homelab or uploading it to your external host. 

I have been running Chirpy for quite some time now and I am really happy with the outcome! Consider a donation to the maker of this theme [Cotes2020](https://github.com/cotes2020/jekyll-theme-chirpy)



