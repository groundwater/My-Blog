# Git #

We recommend using Git for all development.
See [Introduction to Git](http://learn.github.com/p/intro.html) for an introduction,
or [Git-Scm](http://git-scm.com/about) for more information.

Git lets developers focus on small tasks, rather than the entire project.
Developers should focus on each commit,
in isolation, as an independent, incremental, and atomic update.
No single change is perfect,
but if every commit advances the functionality of the code,
the project as a whole moves towards completion.

## Commits ##

Each commit should take the code from one working state to another.
There are reasonable exceptions to this,
but incremental working states are a good baseline.

It is quite reasonable to commit ever minute,
but it may also be every half hour.
Experience, practice and peer feedback are the best ways to determine what's appropriate.

### Designing Commits ###

Good code starts with good commits, and good commits tell a story.
There are no hard rules, a commit may touch a single file, or hundreds.

For example, refactoring a class name might affect most of the source in the repository.
Since every instance of the name must be changed,
it makes sense to include every effected file in the commit.

Git never commits code that you have not explicitly staged.
Not only can individual files be staged, but individual lines in a file.
Use `git add -p` to interactively add chunks of changes.
You can see exactly what has been staged with `git diff --cached`.
Use `git add -i` to fine-tune commits by adding or removing chunks interactively.

Once a commit has been designed,
there will be staged and unstaged code left in the working directory.
It is good practice to test the code with _only_ the staged changes.
Use `git stash --keep-index` to temporarily remove all unstaged changes.
This will leave your working copy exactly as it would appear after the next commit.
After you test and verify the commit, use `git stash pop` to re-apply the unstaged changes.

### Commit Message ###

All commits require messages, and how you write a message is important.

A commit message should explain _why_ you did something.
The message should have a short title,
but may include a body of text as long as you require.
Use the commit message to reference any sources that inspired the change,
such as an issue number,
links to discussions, etc.

## Branching ##

Branching is cheap in git, so cheap that _all_ changes should be done on a branch.
You should _never_ work from main — Main is for merging!

Since branching is so easy,
developers are free to explore and share wild ideas without impacting the main code base.
Developers are free to create as many branches as they like.
Branches are pushed individually and explicitly to a shared or remote repository.

## Merging ##

A branch is useless unless it can be merged with another branch.
Practically, branches can merge with any other branch,
it is good practice to get used to frequent branching and merging.

There are two ways to bring branches together, with a **merge** or **rebase**.
Each method combines two branches together, merging code changes along the way.
The difference between each method is how they appear in the commit history.

A rebase produces a sequential history, a merge produces a parallel history.

If your code has not been shared (i.e. `git push`) use rebase.
Using rebase locally makes your commit history cleaner.
If your code has already been shared, you **must** use merge.
Rebasing shared code is the git equivalent of an oil spill,
it creates a mess that requires a lot of time and effort to clean up.

**Never Rebase Shared Branches!**

## Sharing ##

The true power of git comes from sharing.
Developers should push their changes daily.
_Do not share everything you do._
It is not necessary to share every experimental branch.
Use lots of branches locally to craft a set of commits worth sharing.

![Git Sharing Model](//github.com/jacobgroundwater/My-Blog/raw/master/DistributedTeams/git-sharing.png)

By sharing daily, other developers can give early feedback,
and changes can be merged early.
Merging early creates small frequent conflicts,
rather than a few large conflicts.

If by the end of the day you're not confident about sharing anything,
just pick a branch and push it.
Uncertainty means you need feedback,
the only way to get feedback is to share.
Use a pull request to tell others why you are stuck and that you need feedback.

### Pull Requests ###

Although not actually a feature of git,
pull requests are an indispensable part of the git work flow.
A pull request is an online space to discuss a particular branch of code.
Other developers can comment on the code directly,
or make general comments related to the branch.

Pull requests (PR) form a permanent archive of the intended change,
regardless if the pull request is accepted or denied.
It is okay to open an PR with no intention of ever merging it.
PRs can be used as a place to share experimental code,
or other wild ideas.

Almost all shared branches should have open pull requests attached to them.
Since developers are supposed to push their changes daily,
most PRs should be updated every day.

## References

- [A successful Git branching model](http://nvie.com/posts/a-successful-git-branching-model/) by Vincent Driessen
- [A (simpler) Successful Git Branching Model](http://drewfradette.ca/a-simpler-successful-git-branching-model/) by Drew Fradette
