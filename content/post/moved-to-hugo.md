+++
date = "2015-09-13T19:03:00+03:00"
draft = false
title = "Github Pages + Hugo = Love"
tags = ["Golang", "Hugo"]
+++

I was aware of [Jekyll](http://jekyllrb.com) and [Github Pages](https://pages.github.com) long time ago, but I didn't want to have Ruby environment to generate my blog, so I've ended up with [Ghost](https://ghost.org) blog on [DigitalOcean](https://www.digitalocean.com).

Few months ago when I was on vacation I started to learn Golang:

<blockquote class="twitter-tweet" lang="en"><p lang="en" dir="ltr">Let the vacation begin! <a href="https://twitter.com/hashtag/golang?src=hash">#golang</a> <a href="https://twitter.com/golang">@golang</a> <a href="http://t.co/LqAXc3g5ot">pic.twitter.com/LqAXc3g5ot</a></p>&mdash; Dmitri Logvinenko (@VorT3x) <a href="https://twitter.com/VorT3x/status/612938326140715008">June 22, 2015</a></blockquote> <script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

And of course I found [Hugo](http://gohugo.io). But I was busy and had no time for my blog until now.

So, what's Hugo? Per [gohugo.io](http://gohugo.io):

>Hugo is a general-purpose website framework. Technically speaking, Hugo is a static site generator. This means that, unlike systems like WordPress, Ghost and Drupal, which run on your web server expensively building a page every time a visitor requests one, Hugo does the building when you create your content. Since websites are viewed far more often than they are edited, Hugo is optimized for website viewing while providing a great writing experience.

And since it's static site you can host it on Github Pages (**for free!**). And the most important is that you don't need to maintain server/web application yourself, any change to your blog is just a commit to repository using Git. But previously I had to update Ghost theme, Ghost version manually using FTP.

It took me one evening to migrate from Ghost to Hugo, the main problem for me was to choose theme or create my own :) Current theme I use called [Cactus](https://github.com/digitalcraftsman/hugo-cactus-theme) and it's open source.

But now It's a matter of a commit to change/add anything on the blog. I use this script to deploy my changes:

```bash
#!/bin/bash
cd vort3x-blog-hugo

# Build the project.
hugo

cd public

git add -A

# Commit changes.
msg="rebuilding site `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi
git commit -m "$msg"

# Push source and build repos.
git push origin master
```

I want to thank Steve Francia ([spf13](http://spf13.com)), the creator of Hugo and all [contributors on Github](https://github.com/spf13/hugo/graphs/contributors) (208+ at the time of this writing)! Great job!

Feel free to ask me any questions in the comments below.
