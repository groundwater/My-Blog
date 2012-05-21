Kanban w/ Lean

Backlog -> In Progress -> Done -> Validated

Introduce the idea of validating each feature as part of the work process. Use split testing for example to show a correlation between new features and growth.

The validation becomes part of development. The developers are involved in validating feature decisions. Because developers are involved in validation, code can be designed from the start of the feature request to support validations.

## Rules of Engagement ##

These rules of engagement are the clearly defined, explicit duties of each person on the team. Violating a RoE, done with purpose, is probably okay but not advised. A RoE is more about pre-allocating work, so team members can act without needing to verify things in lengthly meetings.

### Product Owner ###

The product owner may:

	1. add, re-order, or remove features to the backlog at any time
	2. mark a validated feature as done, and remove it from the board

### Developer ###

Any developer may:
	
	1. pull the top feature from the backlog and work on it
	2. work on any in-progress feature
	3. open a pull request for any reason

### Team Master ###

There are no rules of engagement for the team master. All actions taken by the master involve other team members, thus there really is no solo action that can be taken.

## Team Guidlines ##

Guidelines are different from rules of engagement. An RoE specifies what a team member may do without direct approval because those actions have been pre-approved as part of the overall process.

### Developers ###

A developer is free to work wherever, however, and whenever they like. Their only responsibility is to support the team. The team as a whole is responsible for moving features through the pipeline.

In order to support the team, developers must communication. The asynchronous chat system is notification driven. Any time a developer is stuck, bored, blocked, or confused, they should notify their team. If possible mention key people in the notifiaction with @mentions.

The duty of a developer is the keep his or her team updated.

Use pull-requests for any and all work. Work in progress is judged by how often code is pushed. If a developer has not pushed code in 3 days, from the teams perspective they have not done any work in the last 3 days. If a developer really has not done any work, that is fine. We are guarding against solo-developers who go it alone.

The team also values working code over chat and discussions. There are certainly days that will involve a lot more chat than coding, but the team only judges progress by working code. The team however does not use lines of code as a sub-measure. These guards are just about keeping the team moving, not micro-managing progress on a day-to-day basis.

### Master ###

The masters job is to give feedback to the entire team. Thus all work done by the master involves directly communicating with team members. The master should trust but veryify as many parts of the project as possible.

	1. has code been reviewd before merging
	2. are developers pushing their changes often enough
	3. are features in the pipeline bottlenecking or backing up
	4. has the product owner submitted a proper feature request

The master should keep the wheels greesed and find and optmize hotspots.

### Product Owner ###

Despite the owner bearing sole responsibility for feature decisions, they are allowed and encouraged to seek team feedback while writing user stories and feature requests.

They owner may inspect the same code repository as the developers use to push their daily work, but the owner feedback will be limited to correcting misunderstandings. The master may choose to weigh in as to whether their comments can be incorporiated right away, or will have to be placed in a new feature request.

The owner may place emergency features in an expidite lane. The expidite lane pre-empts all work, even features currently in progress. The entire team works to push expidited features through as fast as possible. Developers are not expected to work on other features during expidited work.


## Pull Requests ##

At the very least, open a pull request for each feature. Put all relevant discussion in the pull request, including how to design, how to test, and how to meausre the feature. What split test to be used should be specified in the feature story.

If a feature fails validation, close the pull request without integrating. It is acceptable to submit another feature based off an old pull request.

A pull request is a shoot-first ask questions later design. If you want to work on something, do it. No need to wait for a meeting since there are no meetings. Any work that follows the "Rules of Engagement" is allocated.


## Testing ##

Test coverage must be high enough that any developer, at any time, can refactor any part of the code they wish over a new pull request. If all tests pass, the code can be merged into main.


## Distributed Revision Control ##

All projects may reside in a single git repository.

If you contribute to a feature, push often, at least daily. This allows integrations to be done fast and often.


