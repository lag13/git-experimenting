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
