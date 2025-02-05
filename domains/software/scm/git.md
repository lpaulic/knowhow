# Git

## Learning Git
Materials that serve as good starting point to:
- [Learn Git branching](https://learngitbranching.js.org/)
- [Oh S**t Git](https://ohshitgit.com/)
- [Git Exercises](https://gitexercises.fracz.com/)

## Rebasing feature branches
- count all commits from branching point to now
```
git rev-list --count start..end
```

- rebase command
```
git rebase -i HEAD~n
```

- combined commands
```
git rebase -i HEAD~$(git rev-list --count start..end)
```

- reverting intent to add
```
git diff --name-only --diff-filter=A -z | xargs -r0 git reset -q --
```

## Fixing up a commit
Useful when you want to add necessary changes to an original commit 
that is not proper but is related to the same thing. Steps for 'fixing'
a commit:
1. Add changes: `git add <changed-file-1> ...`
2. Commit as a fix to the commit with `<commit-hash>`: `git commit --fixup <commit-hash>`
3. Rebase the commit fix: `git rebase -i --autosquash <commit-hash>~1`
