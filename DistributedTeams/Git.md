# Git #

We recommend using Git for all development.
See [Git-Scm](http://git-scm.com/about) for an introduction.
Git lets developers focus on quality incremental updates.

## Commits ##

Commits should be atomic.
Each commit should take the code from one working state to another.
There are reasonable exceptions to this,
but incremental working states are a good general measure.

It is quite reasonable to commit ever minute,
but it may also be every half hour.
Experience, practice and peer feedback are the best ways to improve committing behaviour.

### Desinging Commits ###

Good code starts with good commits.
Git never commits code that you have not explicitly placed into the next commit.
Before code is committed, it must be placed into a staging area called the index.

Not only can individial files be staged, but individual lines in a file.
Use `git add -p` to interactively add chunks of changes.
You can see exactly what has been staged with `git diff --cached`.
Use `git add -i` to fine-tune commits by adding or removing chunks interactively.

Once a commit has been designed,
there will be staged and unstaged code left in the working directory.
It is good practice to test the code with _only_ the staged changes.
Use `git stash --keep-index` to temporarily remove all unstaged changes.
This will leave your working copy exactly as it would appear after the next commit.
After you test and verify the commit, use `git stash pop` to re-apply the unstaged changes.

These commands should be used together to produce better commits,
it might be worth aliasing them.

### Commit Message ###

All commits require messages, and how you write a message is important.

The first line is the commit title:

1. Use Title Case
2. Single Line
3. Use Simple Present Tense
  (i.e. "Fix Type", "Create New Messenger Class")

If necessary, leave a blank line and write a message explaining _why_ you made the change. 
Write it either as an internal monologue, 
or as a justification to the rest of the team. It should contain your reasoning, not the execution. 
The code will self-document what functionality has changed,
commit messages are about explaining why the change was made.
Include references to tickets, communications, and messages that inspired the change.

## Branching ##

Branching is cheap in git, so cheap that _all_ changes should be done on a branch.
You should _never_ work from main — Main is for merging!

Create and checkout a new branch with 

    git checkout -b MyNewFeature

Since branching is so easy,
developers are free to explore and share wild ideas without impacting the main code base.
Developers are free to create as many branches as they like;
branches remain local until explicitly pushed.
While it is better to share early, it is not a requirement to share immediately.

## Merging ##

Brances are re-combined in one of two ways:

1. Merge
2. Rebase

Each method combines two branches together, merging code changes along the way.
The difference between each method is how they appear in the commit history.

A rebase produces a sequential history, a merge produces a parallel history.

If your code has not been shared (i.e. `git push`) use rebase.
Rebase looks cleaner, and resolves conflicts better than merge.
If your code has already been shared, you **must** use merge.
Rebasing shared code is the git equivalent of an oil spill,
it is creates a mess that requires a lot of time and effort to clean up.

> Never Rebase Shared Branches

## Sharing ##

The true power of git comes from sharing.
Developers should push their changes daily.
Do not share everything you do,
it is not necessary to share every experimental branch.
Use lots of branches to craft a set of commits worth sharing.

![Git Sharing Model](//github.com/jacobgroundwater/My-Blog/raw/master/DistributedTeams/git-sharing.png)

By sharing daily, other developers can give early feedback,
and changes can be merged early.
Merging early creates small frequent conflicts,
rather than a few large conflicts.

