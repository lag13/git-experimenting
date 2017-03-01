# git-experimenting

Repository for experimenting with git features

## .git Size History

- 92K (original)
- 684K (after committing to master a 572K jpg)
- 984K (after committing+pushing a 304K jpg to a seperate branch). Similar
  size when cloning that repository.
- 984K (after deleting that separate branch). But 660K after cloning the
  repository after the branch was deleted from github. Does this mean that git
  clone will not include any history from deleted branches? It seems that your
  local git will remember everything you've ever done (even deleting branches)
  and allow you to recover (unless you REALLY mess something up) but when you
  pull something from another git repository it only gives the things which
  are not deleted.
- 1016K before adding a png file (which I've told git lfs to track).
- 1.0M after adding png file. I probably should have had `du` use a more
  accurate number and/or used a bigger png file. Will do that now.
- 5.6M after adding png file. And 5.3M on a fresh clone (also, I got an error
  when I tried to pull instead of clone, unsure why this happened). I'm a
  little confused here. I thought the .git folder wouldn't get touched in
  terms of these files being tracked by git lfs.
- After rotating the 4.6M png file, it somehow became a 15M png file. I'm not
  sure what Preview is doing under the hood here. Either way when I pull now
  the .git directory is 16M so lfs worked! It only downloaded the image that
  we needed instead of the entire history for that image. When I switched to
  the older commit where I added the image, that older image had to be
  downloaded and the size grew to 21M so things seem to be working as
  expected!
- After adding the 1.3M image .git was 22M.
- After rotating that image it becamse 1.4 and after committing+pushing .git
  was 23M which makes sense (after a fresh clone it's only 19M because that
  23M came from switching to older versions of lfs tracked images). So we see
  that on each commit of the image not tracked by lfs the git repository grows
  roughly by the size of the image.


## Git lfs

Super easy to use are my first impressions! I really don't have to do any
extra stuff. Everything "just works". On the github repository, none of these
pointer files appear, instead the actual picture is there. The only indication
that it is hosted in a different place is that when you click to view it it
will say "hosted with git lfs" at the top. Wow.

I am having some trouble with it though. I've gotten a couple errors now from
either pushing or pulling things. Pushing:

```
lls-lgroenendaa:git-experimenting lgroenendaal$ git push origin master
Git LFS: (0 of 1 files) 15.48 MB / 15.48 MB
Fatal error: Server error: https://lfs.github.com/lag13/git-experimenting/objects/6e888e2cca08a92018700eaa8e9ea97052b450e3fd8132341988440215052f22/verify

Errors logged to /Users/lgroenendaal/gocode/src/github.com/lag13/git-experimenting/.git/lfs/objects/logs/20170301T091622.811671581.log
Use `git lfs logs last` to view the log.
error: failed to push some refs to 'git@github.com:lag13/git-experimenting.git'
```
Pulling:

```
lls-lgroenendaa:somsom lgroenendaal$ git pull
remote: Counting objects: 4, done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 4 (delta 1), reused 4 (delta 1), pack-reused 0
Unpacking objects: 100% (4/4), done.
From github.com:lag13/git-experimenting
   64c33cd..33d14fb  master     -> origin/master
Updating 64c33cd..33d14fb
Downloading largepng1.png (4.59 MB)
Error downloading object: largepng1.png (b3dded50f818121d864da7a971cb1916708f1fc2c2c524f3d189bf55eebf7fa3)

Errors logged to /Users/lgroenendaal/gocode/src/github.com/lag13/somsom/.git/lfs/objects/logs/20170301T090501.986401855.log
Use `git lfs logs last` to view the log.
error: external filter git-lfs smudge -- %f failed 2
error: external filter git-lfs smudge -- %f failed
fatal: largepng1.png: smudge filter lfs failed
```

So is git lfs still not stable? Or am I doing something wrong?

Another thing, when I had the failed push I just retried and things worked.
But even after they did, github still displayed the non-rotated image for
quite a while. So cache invalidation seems slow?

### How Does it Work in circleci?

Or more specifically, does circleci use git with the lfs extension?
