# Distributed Teams

The problem with software development is that good developers are sparse.
It can be extremely difficult to collect a team together into a single location.
Traditional office hours, commuting, meetings, 
and many traditional business structures do not appeal to young talent.

## Overview

We attempt to solve these problems by making use of distributed teams,
and an asynchronous communication model.

## Kanban 

We use agile development, but with continuous feature development instead of sprints.
The work-pipeline introduced by Kanban is a means of controlling pacing and work in progress.

![Kanban Board](https://github.com/jacobgroundwater/My-Blog/raw/master/kanban_board.png)

The team should aim to achieve a steady pace for moving features across the board.
Team roles are divided according to traditional Scrum roles, but this is not scrum.
There are no meetings, communication is moved to asynchronous chat rooms, email,
and pull-requests.

Every team has a single **product owner**, 
all stakeholders must coordinate their needs through the single owner.
The owner is responsible for the overall vision and direction of the product.

A team of **developers** work together in a self-organized group to move feature requests across the board according to the Kanban methodology.

A scrum master oversees the entire process, 
making sure everyone involved knows what their responsibilities.

## Rules of Engagement ##

Rules of Engagement (RoE) are a key component of distributed efficiency.
A RoE grants permission to do something automatically.
There is no need to wait for permission, or a meeting.
RoEs are designed to bypass the latency of internal communications and let everyone get working.

### Product Owner ###

The product owner may:

1. add, re-order, or remove features to the backlog at any time
2. remove a feature marked Done from the board
3. inspect the in-progress features at any time
4. notify the team master of problems or concerns

The product owner has no direct control over the development team.

### Developer ###

Any developer may:

1. pull the top **Todo** feature into **In Progress** if there is an available slot
2. open a pull request for any reason
3. provide feedback on another pull request
4. pull more information about a feature from the product owner

### Team Master ###

There are no rules of engagement for the team master. 
All actions taken by the master involve other team members, 
thus there really is no solo action that can be taken.

## Team Guidelines ##

Guidelines are different from rules of engagement. 
An RoE specifies what a team member may do without direct approval because 
those actions have been pre-approved as part of the overall process.

### Developers ###

A developer is free to work wherever, however, and whenever they like. 
Their only responsibility is to support the team. 
The team as a whole is responsible for moving features through the pipeline.

In order to support the team, developers must communication. 
The asynchronous chat system is notification driven. 
Any time a developer is stuck, bored, blocked, or confused, they should notify their team. 
If possible mention key people in the notification with @mentions.

The duty of a developer is the keep his or her team updated.

Use pull-requests for any and all work. Work in progress is judged by how often code is pushed. 
If a developer has not pushed code in 3 days, 
from the teams perspective they have not done any work in the last 3 days.
Aside from vacation or sick days, this should not occur.
It doesn't matter how much code is being pushed, one line can be as good as one thousand.

Working code is the ultimate measure of success, 
and working code means passing tests.

### Master ###

The masters job is to give feedback to the entire team. 
Thus all work done by the master involves directly communicating with team members. 
The master should trust but verify as many parts of the project as possible.

1. has code been reviewed before merging
2. are developers pushing their changes often enough
3. are features in the pipeline bottlenecking or backing up
4. has the product owner submitted a proper feature request

The master should keep the wheels greased and find and optimize hot-spots.

### Product Owner ###

Despite the owner bearing sole responsibility for feature decisions, 
they are allowed and encouraged to seek team feedback while writing user stories and feature requests.

They owner may inspect the same code repository as the developers use to push their daily work, 
but the owner feedback will be limited to correcting misunderstandings. 
The master may choose to weigh in as to whether their comments can be incorporated right away, 
or will have to be placed in a new feature request.

The owner may place emergency features in an expedite lane. 
The expedite lane preempts all work, even features currently in progress. 
The entire team works to push expedited features through as fast as possible. 
Developers are not expected to work on other features during expedited work.

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


## Testing ##

Test coverage must be high enough that any developer, 
at any time, can refactor any part of the code they wish over a new pull request. 
If all tests pass, the code can be merged into main.

Refactored code should still be reviewed by the team.

## Distributed Revision Control ##

All projects may reside in a single git repository.

If you contribute to a feature, push often, at least daily. 
This allows integrations to be done fast and often.


