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


## Git lfs

Super easy to use are my first impressions! I really don't have to do any
extra stuff. Everything "just works". On the github repository, none of these
pointer files appear, instead the actual picture is there. The only indication
that it is hosted in a different place is that when you click to view it it
will say "hosted with git lfs" at the top. Wow.
