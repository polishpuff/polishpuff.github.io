---
layout: post
title:  "Did I break my blog..."
date:   2017-06-16 21:11:12 -0400
---


...is a question I'm wondering. 

I decided I wanted to change the look of the blog. No harm there, right?

I attended a Flatiron event a few weeks ago and one of the engineers walked me through which files I should and shouldn't touch in my GitHub repo. Then I forgot which ones they were! 

The other night I finished the CSS section of the curriculum so I thought, *"well now is the time to jump in and see what I retained."* 

I did some research on Jekyll and decided to start with changing the header pics and the font color. NO HARM THERE RIGHT?

------

I wrote this original post as a test but it still works to post! For some reason, it no longer works to update my settings from learn.co. But that's OK, I can do it from the code. 

Woo! Can't wait to dig into the Jekyll code a little more this weekend!

-----

**June 17 post-script**

*Some context: I decided pretty early on into the Flatiron course that I wanted to change the way the blog template they provide looked. I wanted to have one that was unique from the others but also unique to me; something that contained a bit of myself. I searched in the FAQ section of learn.co, where I read that it was possible to play around with the CSS but explicitly forbade making changes to certain files.*

*Just as I was finishing up the CSS portion of the curriculum I attended a Flatiron event with the specific intent to ask someone there about making these changes. I met an engineer there who told me a little bit about Jekyll, the template that Flatiron uses to generate students' blogs, as well as about which files were most likely safe to make edits to in my repo.*


Since I just finished up CSS, I decided to tackle making some small changes. I figured making a small change might be less impactful than any major ones. I went ahead and found two royalty-free images to use for the headers: one on the home page and one on the about page. 

**img**

The images were pretty straightforward. "About" has its own .html page so I added a picture of the BK Bridge to the img directory and changed the code on the img element a little bit:

```
---
layout: page
title: About
header-img: "img/brooklyn-bridge.png"
---
```

Pretty simple. For some reason I couldn't get a .jpg to work (the blog would only show a gray background instead of the image) - only a .png displayed correctly. I checked and it seems like there should be no obstacles to using a .jpg with Jekyll so either 1) there's something in the code preventing .jpg files from being used or 2) the connection between the repo and learn.co is slow, which I do suspect is the case anyway, + I'm impatient.

The element for the image on the home page and the individual blog posts was on the config.yml page. Also an easy change: 

```
# Site settings
title: i bet i could do that
header-img: img/triangles.png
```

But this is one of the files the [FAQ was pretty clear about not modifying](http://help.learn.co/blogging/blog-settings/can-i-edit-the-css-of-my-blog). After I finished with all of my commits last night, I tried to make changes to my blog title via learn.co and was told I couldn't. Luckily I can still edit anything I need from the code and push it up to my repo. That's when I created this test post to confirm that connection to Learn was still active. No problems there, which is great.

**font color**

This piece was a challenge because I couldn't decide which font color I wanted to use and because the Learn-GitHub connection is not instant. I didn't realize that until the end; I kept going back to the code and trying to figure out where I might have needed to add additional color elements.

The [Jekyll directory structure](http://jekyllrb.com/docs/structure/) is pretty straight-forward. In the page.html and post.html files, two header classes are referred to: 

"site-heading" and "subheading"
```
<div class="container">
   <div class="row">
      <div class="col-lg-8 col-lg-offset-2 col-md-10 col-md-offset-1">
         <div class="site-heading">
            <h1>{% if page.title %}{{ page.title }}{% else %}{{ site.title }}{% endif %}</h1>
            <hr class="small">
            <span class="subheading">{% if page.title != "About" %}{{ site.description }}{% endif %}</span>
         </div>
      </div>
   </div>
</div>
```

For awhile, I was playing around with the font on the "site-heading" selector but then I thought probably "subheading" was more correct, once I settled down and read the code a bit more closely. 

I cheated a bit by cmd-f'ing through the code at points to try to find all the selectors for these two classes within the two CSS files: bootstrap.css and clean-blog.css. Next time I make changes, most likely to the font style, I'll take a bit of a better look at where the bootstrap CSS diverges from the custom CSS in the clean-blog file. 

-------

Changes to make in the weeks ahead: font-style and ensuring links open in new tabs. I'll keep updating with changes I want to add as I think of them.
		
