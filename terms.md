These are just some analogies I relate to, by no means should anyone take these as absolutely definitive definitions of these terms in git.

- commit - think of a commit as a snapshot of the entire code base at a point in time, the entire repository, as if you had a folder with the code base and you made a copy of it and locked it forever, that would be a commit. commits hold relationships to the commits (snapshots) that came before them, as well as meta data about the commit (message, author, date etc)
- index - pre commit, another type of commit really, changes from the working tree can be staged into the index as they are "approved for committing"
- working tree - where we make changes, before committing/staging
- HEAD - alias to last commit that we are checked out from, usually a reference to the current branch
- detached HEAD - when you checkout without a branch
- branch - just a reference/alias to a commit, if commits were just folder snapshots we kept on our computer, a branch would be a shortcut to a specific folder.
- merging - it's about consolidating commits, if you had two versions of code in separate folders and you dropped one folder on top of the other, that would be like a merge, naturally you would have to resolve any conflicts
- rebasing - it's like merging each commit in another branch (line of work) onto another commit, as if the changes were made after that commit, naturally any conflicts in each commit you rebase will be resolved during the rebase, so this is still a merge at the end of the day, it's just a merge of one commit at a time, instead of creating a merge commit to commit the differences of all commits in the other branch at once.