# Starting out internal teams

## Communicate

### Merges can't fix a lack of communication

Major refactorings, major renaming, overlapping changes. All of these can lead to massive merge conflicts that will be difficult to resolve. Communication must come first, even the best SCM system can't fix a lack of communication.

**Why?** we should align our strategies independent of SCM

## Branching

### Don't get crazy with branches, keep it simple

- Stick with master for development work
- At most, consider release branches to help track releases, but definitely not necessary

**Why?** branches tend to become islands, they are rarely integrated with main lines of development, thus leading to merge conflicts

### Avoid [feature branches](http://martinfowler.com/bliki/FeatureBranch.html)

[Feature toggles](http://martinfowler.com/bliki/FeatureToggle.html) are a much better alternative and allow continuous integration in the same development branch.

**Why?** decreases risk of merge conflicts

### If you do use feature branches, merge from the source frequently

If you do develop a new feature in a branch, if master is the main line of development, make sure you merge master INTO the FEATURE branch daily or at some frequency that matches the pace of your development. This way when you go back to merge the feature branch INTO MASTER there will be less chance of a merge conflict. You will only have conflicts from changes in the feature branch since the last merge from master.

**Why?** decrease risk of merge conflicts

## Work-flows

### Stick with a central repository and have each contributor work in it

- Git provides for crazy complexity in repository work-flows, stay away from these initially and probably for most internal development purposes
- Have one central repository everyone pulls from and pushes to.  
- Public projects with many contributors and perhaps a team of maintainers often need more than a central repository. This is where GitHub pull requests come into play.
- Some teams setup advanced work-flows for approval processes, in my opinion this is best handled outside version control
	- Deployment processes can control who performs them
	- Preventing mistakes in the central repository from new contributors is better left as an education opportunity, a chance to enhance team collaboration instead of adding overhead to approve every change ever.
	 
**Why?** this central model provides for most needs of a small development team, advanced work-flows add significant overhead.

### Integrate frequently 

- At a minimum, try to pull in the morning and push in the evening.
	- If you can't push, at least pull daily.
- Even if you aren't working full time on a project, integrating is a great way to make sure you don't lose commits, plus if you push when you do these changes you are much more likely to leave your work in a completed state since you will likely care more about what you push versus what you commit only locally.

**Why?** the less frequent you integrate, the more likely you will have merge conflicts

### If it's been a while since you worked on a project, integrate first

If you put a project down for a few months and others are working on it, make sure you pull (fetch + merge) first. This is really about forming a habit because you'll never intentionally forget this one :).

**Why?** You'll hate the surprises if you make changes and then go to pull afterwards :)

## Tools

### Use a good GUI, learn the concepts with it

Many concepts in SCM just have to be visualized, especially branching, diffs, merge conflict resolution, and viewing history. Don't fall into the trap that the "cool kids" only use the CLI, a good GUI is always going to be complementary to the CLI.

**Why?** the concepts are more important than the tool, use a GUI when it helps

### Don't be afraid to use the command line interface

There are some advanced things that may be hard to do with a particular GUI. Don't be afraid to use the CLI in these cases, it's not as bad as it may seem. Use `git help` to learn but also look at my resources as the `git help` documentation is often very hard to follow.

**Why?** with git CLI, anything is possible :)

## Commits

Most of these come from my post [Things I've noticed with DVCS](http://devblog.wesmcclure.com/posts/things-ive-noticed-with-dvcs), read it to double re-enforce these ideas :)

### Commit frequently, locally

Your local environment is yours, commit when you are confident a set of changes are complete, even if it's only partial to the full commit. You can always amend the commit as you build up more of the commit. I mention committing around business value, but locally you can do whatever you want as you can repackage those commits before you push them remotely.

Commit many times locally, per day.

**Why?** If anything goes wrong you can abandon the last 15 minutes of work instead of the last day! Do more exploratory changes without worrying about what to "undo".

### Use the outstanding changes as a guide

Build up confidence in the work you are doing by reviewing the outstanding changes to see where you left off. If you get interrupted with a meeting or phone call, study the outstanding changes before you get back into your work. Use it as a crutch! This is especially effective with frequent local commits.

**Why?** Have more confidence in where you left off.

### Check build/test after merges

Merges can break things (there may be no conflict in merging the text, but the code may not compile!), run the build after a merge, before you push!

**Why?** don't break the build :), a merge commit is your commit too!

### Don't blind commit

Make sure you review your changes before you commit. Find the things you didn't intend to commit, or the things that aren't quite done.

**Why?** reduces cruft that builds from committing unnecessary code, good chance to review and see if you are done, sometimes something will stand out and you can fix it

### Adopt what you like from my Commit Review post

[Commit Review Questions](http://devblog.wesmcclure.com/posts/commit-review-questions)

### Leave meaningful commit messages

- Blank and or "asdf" just don't help anyone! 
- Try to make the first sentence a synopsis of the change. 
- The first sentence is what will show in most log views. 
- Then, add any pertinent information as necessary to explain the impetus for the commit. 
- If you use a project management system to track features, you could include a feature id, story id etc, however if this isn't consistently done, it's probably not going to be very valuable.

**Why?** The commit message is the first thing someone looks at when understanding a commit. Plus, you can search these, even locally!

### Try to commit around business value - not tasks

I've seen a tendency to commit html changes, then a separate commit of the css changes, then a separate commit of the javascript changes, etc. Instead, bundle these changes around the business value (behavior) that you are changing, not the type of the file. It will be much easier to see what was impacted by a particular new feature if the changes are bundled together.

**Why?** History will be much more meaningful.

### Integrate when you complete a new unit of business value

Share it with everyone as soon as you are done. Even share partially complete versions of it if possible. Get your completed changes to everyone to get feedback faster. However, this doesn't mean push broken code or code that will cause problems, nor is it about rushing work.

**Why?** you can't get feedback if you don't share your changes.

### Careful with renames and significant changes, if it matters 

Renames are detected based on similarity from deleted/added files in a commit. If you are renaming a file and changing it's content, the similarity may not detect the rename. If you want the rename for historical purposes, then do the rename separate of the changes. Yes I just violated my suggestion about committing around business value :), there are some commits that are about maintaining the code, such as a rename, so in these few cases bundle them separately if you have something to gain like preserving history.

**Why?** if preserving the history of a rename is important, rename independent of making significant changes

### Do significant code reformatting (style) in separate commits

Sometimes code doesn't match a project's coding style. If you do major cleanup of the style (such as using an automatic styling tool), it's best not to change the code behavior in the same commit. If the reformatting is small, don't worry about it, but if you reformat an entire file, I'd do that as a separate commit.

**Why?** can be hard to see what the behavioral change was versus the stylistic changes. 

### Try not to commit binary formats

Git really can't version these very well, they aren't as big of a problem if they don't change very often. If they change often though, repository sizes can grow very large. An example would be build artifacts, try not to commit these. A good continuous integration server will verify the build process and provide artifacts for deployment.

Another example, don't commit a test database, yes it's been done before!

**Why?** repository size can grow quickly. Also, build artifacts are duplicates of the code itself, why have two copies?

### Only change commit history locally

Don't try to rewrite commit history that you have already pushed to a remote repository. In the very rare (like once every 5 years case you need to), talk to everyone that might be affected. Make sure everyone is in agreement.

**Why?** commits in the remote repository can be lost, also it will increase the chances of merge conflicts for everyone else who now has to merge the new central repository back into theirs, it can get very messy.

### Don't force push

**Why?** commits can be lost, changes what other people think is in the central repository

### Use rebase unless the merge has significance

In my opinion the use cases for a merge are
- You have a release branch (say production) and you are merging a fix back into the development branch (master)
- You have a long running feature branch and you are merging it back into the primary development branch

If you are just working locally and you want to integrate with the central master branch, use a rebase.

**Why?** merge commits can have changes and often people will over look them (assuming they were automatic), also they add overhead to reading the log.
