# Using-Git

It's about time I thoroughly learned how to use Git, so here's me messing about with it all to see what happens

Straight off the bat, I used `git clone` to clone this repository from the Github page to my directory. This sets it up as a remote repository since I didn't do `git init` on the local system.

Since updating this README, I'm going to commit it using `git add README.md`, then `git commit`.

`git commit` takes some options. Without any options, it'll open a file that allows you to write a commit message. You can also shortcut this using the `-m` option: `git commit -m <message>`

## Tracking changes in the command line

### `git status`

- This shows you which files in the directory are untracked, staged for commit, modified, deleted, etc.
- Very useful for a quick overview of your directory structure as it appears in your local directory, without having to use an IDE like VS Code (like I'm using)

### `git log`

- Shows the entire *commit* history of your repository (not the working directory)
- Useful for seeing the names of different commits and their commit messages, in case you need to revert some changes.
- When using this, you'll be given an interface to work with. Press h to open the help menu, and q to exit.

### `git diff`

- Show unstaged changes between the working directory and the repository
- Good for finding things that you had forgotten about, or maybe some files need committing before others.
- When using this, you'll be given an interface to work with. Press h to open the help menu, and q to exit.

## Undoing Changes

One of the main purposes of tracking your directory is to be able to hit the big ol' control-Z. You want to undo things up to a certain point. Commit numbers are your way through this.

### `git revert`

Once you've used `git log`, you can use the commit numbers in `git revert` to undo the commit you've chosen. This undoes the commit, rather than reverting *to* the commit.

- Reverts the repository branch back to the point before the given commit.
- Undoes the last commit

### `git reset`

This is used to remove any staged files from the stage without modifying the working directory.

- Reset the stage, not the repository
- You can choose a file to reset or unstage if you specify it
- You can also use the `--hard` option to reset to the last commit *and* modify the working directory to reflect this. This cna be done in conjunction with the `<commit>` option to specify a commit to revert *to*

### `git clean`

This removes untracked files from the working directory.

- Use the `-i` option for more information on how to use this
- Use the `-n` option to just show which files would be removed
- Use the `-f` option to force removal at the same time

## Rewriting History

Sometimes you also want to look at a commit and you think "I actually don't like this, let's change it". You can, in fact, rewrite history.

### `git commit --amend`

This is the simple amendment command - it replaces the last commit with the currently staged files

- If there are no files staged for commit, you can change the commit message.
