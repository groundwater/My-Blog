## Agile

The team is agile at its core; the [agile manifesto](http://agilemanifesto.org/) reads:

1. Individuals and interactions over processes and tools
2. Working software over comprehensive documentation
3. Customer collaboration over contract negotiation
4. Responding to change over following a plan

Agile development breaks products into a collection of prioritized features 
that are implemented in managable increments.
Features are the core unit of measurement to an Agile team.

## Scrum

Agile has a number of implementations, one of which is scrum.
We are not a scrum team, but we do cherry-pick the team roles developed by scrum.

Every team has a single **product owner**, 
all stakeholders must coordinate their needs through the single owner.
The owner is responsible for the overall vision and direction of the product.

A team of **developers** work together in a self-organized group to move feature requests across the board according to the Kanban methodology.

A **team master** oversees the entire process, 
making sure everyone involved knows their responsibilities.


## Kanban 

Kanban is another agile methodology for continuous feature development.
A Kanban board displays all current and upcoming feature development in a single place.
The Kanban board must be available to the entire team at any time.
The team works together to pull features across the board, implementing them in the process.

Kanban is a continuous process, features are not divided into sprints like traditional scrum.

![Kanban Board](https://github.com/jacobgroundwater/My-Blog/raw/master/kanban_board.png)

The team should aim to achieve a steady pace for moving features across the board.
Work in progress is limited, so existing tasks must be completed before new tasks are started.
There are no meetings, communication is moved to asynchronous chat rooms, email,
and pull-requests.


## Continuous Validation

Introduce the idea of validating each feature as part of the work process. 
Use split testing for example to show a correlation between new features and growth.

The validation becomes part of development. 
The developers are involved in validating feature decisions. 
Because developers are involved in validation, 
code can be designed from the start of the feature request to support validations.

Developers are very much involved in the validation of features.
Often validating an idea will mean deploying it to a subset of the product users and collecting data.
The feature is not completed and removed from the board until it is validated and fully deployed.
Validated features will be merged to main, 
failed features will be closed but kept as inactive branches in case they're needed again.

## Pull Requests ##

At the very least, open a pull request for each feature. 
Put all relevant discussion in the pull request, 
including how to design, how to test, and how to measure the feature. 
What split test to be used should be specified in the feature story.

If a feature fails validation, close the pull request without integrating. 
It is acceptable to submit another feature based off an old pull request.

A pull request is a shoot-first ask questions later design. 
If you want to work on something, do it. 
No need to wait for a meeting since there are no meetings. 
Any work that follows the "Rules of Engagement" is allocated.

### Code Reviews ###

Pull requests can be created by anyone, but are closed as a team.
Before code is merged into main, the updated code should be reviewed by other team members.
Pull requests have no expected lifetime, some will be bug fixes that are merged immediately, 
others may never be merged.
Any developer may review code at any time, the commits should be commentable line-by-line.


## Test Driven Development ##

Exactly what Test Driven Development (TDD) means is a debated topic.
We have a practical, yet abstract definition of TDD.
Test coverage must be high enough such that,
any developer, at any time, may refactor the code base in a new branch.
Should all the tests pass, the code may be merged into main.

Practically a developer should branch, refactor, then open a pull request.
It is good practice to have another developer review all commits.
Then if all the tests pass, the branch can be merged into main.

## Distributed Revision Control ##

All projects may reside in a single git repository.

If you contribute to a feature, push often, at least daily. 
This allows integrations to be done fast and often.
