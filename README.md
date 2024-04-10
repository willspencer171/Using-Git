# Using-Git

It's about time I thoroughly learned how to use Git, so here's me messing about with it all to see what happens

Straight off the bat, I used `git clone` to clone this repository from the Github page to my directory. This sets it up as a remote repository since I didn't do `git init` on the local system.

Since updating this README, I'm going to commit it using `git add README.md`, then `git commit`.

`git commit` takes some options. Without any options, it'll open a file that allows you to write a commit message. You can also shortcut this using the `-m` option: `git commit -m <message>`

## Tracking changes in the command line

### [`git status`](https://git-scm.com/docs/git-status)

- This shows you which files in the directory are untracked, staged for commit, modified, deleted, etc.
- Very useful for a quick overview of your directory structure as it appears in your local directory, without having to use an IDE like VS Code (like I'm using)

### [`git log`](https://git-scm.com/docs/git-log)

- Shows the entire *commit* history of your repository (not the working directory)
- Useful for seeing the names of different commits and their commit messages, in case you need to revert some changes.
- When using this, you'll be given an interface to work with. Press h to open the help menu, and q to exit.

### [`git diff`](https://git-scm.com/docs/git-diff)

- Show unstaged changes between the working directory and the repository
- Good for finding things that you had forgotten about, or maybe some files need committing before others.
- When using this, you'll be given an interface to work with. Press h to open the help menu, and q to exit.

## Undoing Changes

One of the main purposes of tracking your directory is to be able to hit the big ol' control-Z. You want to undo things up to a certain point. Commit numbers are your way through this.

### [`git revert`](https://git-scm.com/docs/git-revert)

Once you've used `git log`, you can use the commit numbers in `git revert` to undo the commit you've chosen. This undoes the commit, rather than reverting *to* the commit.

- Reverts the repository branch back to the point before the given commit.
- Undoes the last commit

### [`git reset`](https://git-scm.com/docs/git-reset)

This is used to remove any staged files from the stage without modifying the working directory.

- Reset the stage, not the repository
- You can choose a file to reset or unstage if you specify it
- You can also use the `--hard` option to reset to the last commit *and* modify the working directory to reflect this. This cna be done in conjunction with the `<commit>` option to specify a commit to revert *to*

### [`git clean`](https://git-scm.com/docs/git-clean)

This removes untracked files from the working directory.

- Use the `-i` option for more information on how to use this
- Use the `-n` option to just show which files would be removed
- Use the `-f` option to force removal at the same time

## Rewriting History

Sometimes you also want to look at a commit and you think "I actually don't like this, let's change it". You can, in fact, rewrite history.

### `git commit --amend`

This is the simple amendment command - it replaces the last commit with the currently staged files

- If there are no files staged for commit, you can change the commit message.

### [`git rebase <base>`](https://git-scm.com/docs/git-rebase)

Move the head of the current branch to `<base>`. The base may be a branch name, commit ID, or relative reference to HEAD.

- Can use the -i option to open an interactive rebasing interface. makes it easier apparently

### [`git reflog`](https://git-scm.com/docs/git-reflog)

I think this is ref-log rather than re-flog. Shows a log of all changes to the local repository's HEAD

## Branching Out

When you're working collaboratively, or you're making new progress and aren't sure you won't need to revert to a particular point, you can branch off from the main repository.

### [`git branch`](https://git-scm.com/docs/git-branch)

This lists all of the branches in your current repository. Currently, this will list `* master` for me.

- If you pass a name as an argument, it'll create a branch with that name.

### [`git checkout`](https://git-scm.com/docs/git-checkout)

This will set your working branch to whichever branch you pass to the function. This moves the HEAD to the branch you specify.

'Checking out' also actually locks the branch such that, if the branch is checked out in a different working directory, you cannot reset it from a different worktree.

- If no parameter passed, this will just show you the tracking information for the current branch, in an expensive manner. Don't bother
- If you pass `-b` as an option, it will create a branch of name `<branch>`, then immediately set the HEAD to that branch.

### [`git merge`](https://git-scm.com/docs/git-merge)

This is a really important one when you're working with multiple branches. If you have two branches, say `master` and `test`, and you've committed a few changes on both so your repo history looks like this:

> &emsp;&emsp;&ensp;A---B---C test\
> &emsp;&emsp;/\
> D---E---F---G master

If you do `git merge test`, you'll apply the three commits that got you to point C to create a new commit on branch `master` at H:

> &emsp;&emsp;&ensp;A---B---C test\
> &emsp;&emsp;/&emsp;&emsp;&emsp;&emsp;&ensp;\ \
> D---E---F---G---H master

## Worldwide Access

Since Git is a repository management system that is open-source, it is helpful to know that you can host your repository online, remotely. Places like GitHub and GitLab are great for this. This is a remote repository hosted on GitHub

### [`git remote`](https://git-scm.com/docs/git-remote)

A vastly useful and optionable function used to manage remote repositories and your access to them. Running without a subcommand will list the remote repositories that are being tracked locally, but you can pass a whole load of other subcommands like:

- `add`
  - Add a remote called `<name>` for the `<URL>` passed
  - This allows you to use `git fetch` to keep your local directory up to date with the remote
- `rename`
  - change the name of the remote connection. Does not change the name of the repository, just the name of our local interface with the repo.
- `remove`
  - Remove the remote interface that you are tracking the repository with. All remote branches and configurations are removed

### [`git fetch`](https://git-scm.com/docs/git-fetch)

Download a copy of the repository (or the branch you specify) to the local working directory.

- V simple, does what it says on the tin.
- Many options for specifying which repository or branch, and how much of them gets copied

### [`git pull`](https://git-scm.com/docs/git-pull)

Similar to the fetch, but this immediately merges the download into the current working directory.

- More like `git merge` but the remote version of it. Merge the remote repository into the local.

### [`git push`](https://git-scm.com/docs/git-push)

This will push the named branch into the remote repository. Typically, I'll use the `-u` option to set the upstream location of the push.

- Again, lots of options here, and remote repos can actually be a little confusing in the specifics.
- `git push` on its own will work, but requires that the upstream push location is set. Will default to `origin`, the repository that your work came from.
- Typical commands will be `git push -u origin <branch>` or `git push origin HEAD` or `git push origin <branch>`.
  - `-u` will set the upstream to `origin` if not already set as default.
  - `HEAD` is an easy way of making sure the current branch goes back to the branch it came from
  - `<branch>` is good for if your branch does not exist on the remote yet, and you'd like to add it

### More on Working Remotely

Sometimes, when you're working remotely, you won't have been granted access to whatever repository you'd like to work on. This happens when you'd like to download some source code, but aren't allowed to directly edit the repository.

In this circumstance, you can 'fork' the repository. This will create a copy of the repo in your local directory for you to work on that is entirely in your namespace and is technically yours, even if you reupload it and give it another name (shifty).

This is where working collaboratively really gets its engines going. You can fork things, blame people and raise issues. Not sure what blaming is entirely.

## Extensions

There are a number of useful extensions in VS Code for Git management. The first you'll want is Git Graph - this one makes it easy to see a timeline of your Git repository, and includes even remote branches. You can do most of the main Git commands directly from the graph as well.
