---
toc: True
comments: True
layout: post
title: Hard Resetting
cover-img: /images/swordplaylink.gif
description: My (messy) process of trying to restore my work.
courses: {'csp': {'week': 2}}
type: hacks
---

### 03.14.2024: Hard Resetting or Hardly Resetting?  

Today, I had a pretty tough time trying and failing to integrate the code from the Mario game, so I ended up on a difficult journey trying to get back to where I was.  

I tried to get the game by dragging folders and files from the teacher portfolio into mine, but it ended up making drastic changes to my blog. My navbar disappeared and the font color became grey instead of the standard white. The categories I had at the top of my page disappeared as well, so I could no longer access my blog posts. When I opened Game x2, the screen would remain frozen with Mario, Mr. Lopez, and and a Monkey sprite at the home, but I couldn't move them. The Settings and Leaderboards also appeared in the basic HTML font and color.  

To start on my resetting journey, I ran git revert to a blog update I made yesterday.


```python
git revert bf01702
```

However, this ended up not working and it ended with a lot of failed actions filling up my inbox, so I decided to try reverting to a previous one because I realized that this one already had changes I didn't want.


```python
git revert 35ea7c4
```

Still didn't work! At this point, I was getting a bit scared, so I decided to try something a little more serious.


```python
git rebase -i 35ea7c4
```

I learned that rebasing would, hopefully, help me identify and apply the correct commits to where I wanted them to be. However, this didn't work, so I finally went all out.


```python
git reset --hard 35ea7c4
```

This one finally ended up working, but now it wasn't letting me commit anything (probably a good idea, considering all of this had happened because I committed unnecessary changes anyway). Because of this, I accidentally ran the following in an attempt to get it to work:


```python
git pull origin main
```

...aaaaand I was back to where I started. Luckily, I was able to hard reset it again and unstage all of the incoming changes from main, effectively deleting them. My blog is now back to normal, and I can update it again!

<div style="text-align: center; margin-top: 20px; margin-bottom: 20px;">
  <img src="{{site.baseurl}}/images/letsgogozelink.gif" alt="Link, The Legend of Zelda: Tears of the Kingdom" />
</div>  

So, what did I learn?  
- ONLY COMMIT CHANGES IF YOU'RE SURE THAT THEY WORK!  
- Do NOT run "git pull origin main" if said "origin main" has changes you don't want.  
- "Hard reset" may be your best friend, but you should never find yourself in a situation where it's your *only* friend.
