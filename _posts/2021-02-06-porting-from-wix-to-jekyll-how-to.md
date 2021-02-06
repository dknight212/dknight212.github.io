---
layout: post
title:  Porting from Wix to Jekyll - how-to
---

I've moved my blog posts from a paid Wix site to Github, using Github Pages and the [Jekyll](https://jekyllrb.com/) website/blog engine. This enables me to write posts in [Markdown](https://www.ultraedit.com/company/blog/community/what-is-markdown-why-use-it.html) and integrate with my [Obsidian](https://obsidian.md/) vault (I'll write about that another day).

There were several reasons why I moved this blog:
  - cost - why pay for Wix when Github Pages are free?
  - annoyance with Wix 1 - I don't like organisations that repeatedly email with (the same) "time-limited" offers
  - annoyance with Wix 2 - it was really overkill for what I wanted
  - annoyance with Wix 3 - I didn't want to get locked into a proprietary system
  - ease of workflow - drafting posts on the Wix website just doesn't fit with the way I want to work
  - challenge - I like changing things around from time to time and to learn new stuff along the way
  
  The Markdown format is widely used (in several dialects) and has the great advantage that it's plain text so easy to copy from one system to another. Having control over the files on my own system (and backing them up!) adds to the feeling I've got a much more portable system.
  
  There really wasn't much challenge involved in this change, partly because I wanted the blog to be very straightforward. I'm using the default theme and no tags but may reconsider this approach.
  
## Basic set up
In order to do this you need some basic knowledge of Git/Github, a very small amount of HTML and Markdown (but this is really very simple).

I find it easiest to use the Github desktop application in Windows but cloning and pushing files to the site can also be done at the command line.

It's useful but not essential to have your own domain name.

There are various websites that take you through the process in more depth, in particular:

- [Getting started with GitHub Pages - GitHub Docs](https://docs.github.com/en/github/working-with-github-pages/getting-started-with-github-pages)

The following sites are limited on Medium but if you don't have a Medium account then you can save them to Pocket:

- [Building a Beautiful Static Webpage Using GitHub | by Cody Glickman | Towards Data Science](https://towardsdatascience.com/building-a-beautiful-static-webpage-using-github-f0f92c6e1f02)
- [Launch a Website for Free in 5 simple steps with GitHub Pages | by Emile Gill | Towards Data Science](https://towardsdatascience.com/launch-a-website-for-free-in-5-simple-steps-with-github-pages-e9680bcd94aa)

You can read more about Git and Github at

- [Getting started with GitHub - GitHub Docs](https://docs.github.com/en/github/getting-started-with-github)
- [What Exactly Is GitHub Anyway? | TechCrunch](https://techcrunch.com/2012/07/14/what-exactly-is-github-anyway/)
- [Getting started with Git and GitHub: the complete beginner’s guide | by Anne Bonner | Towards Data Science](https://towardsdatascience.com/getting-started-with-git-and-github-6fcd0f2d4ac6)

A quick run-through of what you need to do to set-up:

- create an account at Github if you don't already have one
- fork the Jekyll Now repository (link)
- rename the cloned repository to *yourusername*.github.io
- using the Github desktop application, clone the repository to your local system
- add a profile picture to the images folder
- create a new assets folder
- customise the \_config.yml file
	- this contains the basic details that is shown on the home page, this is a template so it's just a case of filling in the blanks, no coding needed
- customise the about.md file
	- this is the text of the About page, again this is a simple template
- customise the \_highlights.scss file
	- renamed the `highlight` block to `pre-highlight` to get rid of annoying double-boxes around code (as explained at [Stackoverflow](https://stackoverflow.com/questions/55308142/why-do-i-get-a-double-frame-around-markdown-code-block-on-jekyll-site))
- customise the index.html file
	- I changed the post list to include the date and to truncate the post excerpt like so:
```
---
layout: default
---

<div class="posts">
  {% for post in site.posts %}
    <article class="post">

      <h2><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }} - {{ post.date | date: "%-d %B %Y" }}</a></h2>

      <div class="entry">
		{{ post.excerpt | strip_html | truncatewords:75 }}
      </div>

      <a href="{{ site.baseurl }}{{ post.url }}" class="read-more">Read More</a>
    </article>
  {% endfor %}
</div>
```

- add posts to the \_posts folder and images to the assets folder
- commit and push the changes from your system

This whole set up took me about 30 minutes, and I'm sure it can be done a lot quicker.  New posts are added just with the last two steps, everything else is a one-off.

[Jekyll site - how to write posts](https://jekyllrb.com/docs/posts/) is a good site to start with in terms of writing posts but it's really easy.

## Porting from Wix
By far the most time I spent on this whole process was copying the posts and images from Wix to the new site. Some issues I faced:

- I did not use a good file naming system for the screenshots and I found it tedious to match up the actual files with the posts. I've improved this by renaming image files to include the date of the related post.
- copying the text from Wix introduced backslash quoting of code and file references, particularly to underscores. These were hard to track down.
- some of the Power BI M code included double curly braces. Unfortunately these are used by the underlying [Liquid](https://jekyllrb.com/docs/liquid/) templating language. I had to surround such code with [raw](https://shopify.github.io/liquid/tags/raw/) tags.

I used Notepad++ at times to reformat codes since its search and replace features are so powerful. Yes, I used to use Vi(m).

## My new process
Now that Obsidian is now very much part of my daily routine, being in it for much of the day, and being able to see my notes from other sources and my page of ideas, makes the whole writing experience so much better. I found it distracting moving from one tool to another.

I can now draft posts in Obsidian in a separate drafts folder, keeping track of ideas in another file. When they're cooked, I can transfer posts to the final folder. In the meantime, everything is separately backed up (also to Github).

Links to images are fine since the draft and final blog post folders are in the same path relative to the assets folder as they are on Github. So the markdown:

```
![Figure 1](../assets/yyyy-mm-dd-fig1.png)
```

will work in both. It's really helpful when drafting to see the images.

Links from post to post don't work but that's easily checkable.

I use a short [Powershell](https://docs.microsoft.com/en-us/powershell/scripting/overview) script with [RoboCopy](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/robocopy) to copy posts from the final posts and assets folders in my Obsidian vault to the cloned Jekyll Now repository in a separate folder structure. Together with my latest toy, [Keypirinha](https://keypirinha.com/), I can copy the files in a few keystrokes. I'm sure if I were still using Linux, I'd have similar bash scripts for this (and committing/pushing changes).

I can then use the Github desktop application to commit and push the changes. After a minute or so the changes have been processed and are live on the website.