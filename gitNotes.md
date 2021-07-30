## Git Notes

## Download all branches from Github repository

Download all branches/Move changes to new branch
https://stackoverflow.com/a/42172410/2771704
https://stackoverflow.com/a/13575102/2771704
https://stackoverflow.com/questions/1394797/move-existing-uncommitted-work-to-a-new-branch-in-git

GIT alias
clone-All = !git clone --bare $1 .git && !git config --unset core.bare && !git reset --hard
  clal = "!f(){ mkdir \"${1##*/}\" && cd \"${1##*/}\" &&  git clone --mirror \"$1\" .git && git config --unset core.bare && git reset --hard; };f"