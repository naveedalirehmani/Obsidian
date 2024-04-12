
#### creating and deleting branches

- git branch : to create a branch
- Git branch -d “branch-name” : to delete a branch
- Git branch -D “branch-name” : to delete a branch that has unmarked commits.

#### Adding files to stage and committing.

- Git add . : to add all unstaged files to stage.
- Git add index.html : moving a specific file to stage.
- Git commit -m “commit-name” : to commit stage files
- Git commit -am “commit-name” : to add and commit files.

#### Creating branches with switch ( alternative to checkout ).

- Git switch -c “branch-name” : to create and switch to a branch. (newer).
- Git switch “branch-name” : to switch branches.

#### Creating branches with checkout.

- Git checkout -b “branch-name” : to create and switch to a branch.
#### Moving back in history with checkout.

- Git checkout “commit-hash” : to go back to a specific commit. Head is deatched here.
- Git switch - : to move head back to its last position, basically undoing above command.
- Git checkout HEAD~1 : alternative to git checkout “commit-hash”. ~1 here means move checkout 1 commit.

#### Working with stash.

- Git stash : to move unstaged files to clipboard.
- Git stash list : to list all stashes.
- Git stash pop : to reproduce stashed files ( the most recent stash will pop)
- Git stash apply : same as above but will not remove stash file for stash list.
- Git stash pop/apply stash@{stash-index-here} : to pop or apply a specific stash.

#### Logging commit history.

- Git log : to log all commits
- Git log —oneline : to log all commits in oneline (less information)
- Git log —oneline —graph —all : to log all commits with their graph.

#### Merging branches.

- Git merge “branch-name” : merge branch-name into current branch

#### Discarding with checkout.

- Git checkout HEAD index.html : to discard a specific file content by moving back to HEAD.

#### Discarding with restore (alternative to checkout).

- Git restore “file-name-here” : to discard a specific file content by moving back to HEAD. Same as above

#### Moving back with restore.

- Git restore --source HEAD~1 index.html : this will change the content of a specific file back to where it was 1 commits prior. You will lose any unstaged files. This will not move back commit history. Just the content and the new content of index.html will appear as unstaged file.
- After git restore —source HEAD~1 index.html you can either do git restore index.html to again go back to HEAD. Basically undoing the “git restore —source HEAD~1 index.html” command or create a new commit from here.

#### Unstaging files with restore ( alternative to reset ).

- Git restore --staged “file-name-here” : will unstage a specific file.g
#### Unstaging files with reset.

- Git reset “file-name” : same as above
- Git reset : will onstage all file ( this is not possible with restore )

#### Moving back in history with reset.

- Git reset “commit-hash” : delete all commit history back to a specific commit. Will keep all deleted changes in working directory.
- Git reset “commit-hash” --hard : same as above but will not keep changes in working directory.

#### Moving back with revert.

- Git revert “commit-hash” : this will move content back to how it was in a specific commit but will not delete commit history rather will create a new commit for that. Same as doing git restore —source HEAD~2 index.html and then committing it.

#### Working with local and remote branches

- Git remote -v : to list remote variables
- Git remote remove “name-of-remote-origin” : will delete a remote variable
- Git switch apples : normally when we do this and we don’t have a branch called apples we get error, but if we clone a repo and that has a remote branch called apples we can just switch and git will automatically create a local branch called apple and connect it to remote branch origin/apple.
- Git fetch origin “branch-name” : this will update our origin/branch-name with the remote branch. If a developer has contributed new commits to a specific branch and our local remote/branch does not know about this we can use this command and it will update remote/branch. This will not merge only fetch new commits.
- Git fetch : will fetch new remote/branches.
- Git pull origin ‘branch-name’ : this will fetch latest changes on remote/branch and also merge them into our local branch and local remote/branch. Merge conflicts can arise if we have also made commits in our local branch and remote tries to merge new

