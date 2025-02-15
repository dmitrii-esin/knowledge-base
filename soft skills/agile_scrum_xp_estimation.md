## Code quality

### Main

What is code quality \- level of human-readable, easy to understand and making changes, well-structered and organized code.

### Markers of clean code

* We can run through clean code rules from top level to the bottom obvious file-structure  
* well-structured classes, modules and functions  
* uniform code style and following the established rules (naming, \- formatting, etc.)  
* using tools for track and improve code quality

### Markers of code smells

* not obvious file structure or structure of modules  
* nested if..else statements  
* magic numbers  
* callback hell  
* not obvious naming  
* code formatting  
* and so on.

### Tools to track code quality

* TS and flow  
* test libs  
* linters  
* sonar cube  
* sentry (error tracking)  
* etc.

### Measures to improve code quality

* create code styles and code conv in documents  
* follow the rules  
* code review process (using checklists and docs)  
* tests, linters \=\> autoformatting  
* tech debt fixing and then refactoring (we have to del with tech debt when adding new features became very expensive by time and resourcses) (creating tasks for following tech sprint, TechDebt quadrant By Martin Fowler)  
* ciintegration of them and integration of code style rules with linters  
* Common measures of quality of unit tests provided by testing tools, for example it is a table of test properties like code coverage lines for a functions or lines.

## Testing

Types of testing strategies: \- TDD \- BDD \- smoke tests \- manual tests \- classic pyramid \- white box testing \- black box testin \- and so on.  
This pyramid describes what tests can be and what they affect, but this pyramid don’t talk about how many tests needs to be written. \*we should test own logic and we shouldn’t test third-party libs logic

### Classic pyramid:

E2E test  
Integration tests  
Unit tests  
![image][image1]  
image

### Additionally we have a lot of implementations of this idea, like:

by UI  
by Service  
by Unit  
by Feature

### First principles of testing stand for

Fast  
Isolated/Independent  
Repeatable  
Self-validating  
Thorough

### 3 A’s of testing

Arrange, Act, Assert  
But from my point of view we should guided by wisdom and separate our tests per feature or per domain instead of separating per tech role.  
We should write unit tests for the crucial libraries and components of our system and don’t forget to test main functionalities of features by e2e or integration tests.

### TDD

I’m familiar TDD approach where we start writing code from writing tests based on business task and implement feature in parallel with evaluating this test.  
When: I use this approach for helpersfunctions with complex data transformation or huge business logic with deterministic cases, that approach don’t waste the time it’s about time saving.  
Connected with discipline and DI (dependency inversion technic)

### BDD

GivenWhenThen \- styles with tests representing, like “specificationByExample”  
What that means \- break down the test scenario by 3 sections \- given, when, then.  
Not familiar with in practice and with tools (maybe Cucumber, etc.), maybe uses some DSL.

### Structure of test

Simple naming with “GivenWhenThen” advice from Martin Fowler AAA pattern for structure and steps for hight readability Separated

### Tools

* Jest, Testing-library or Enzyme (unit, integration)  
* Cucumber (bdd)  
* Cypress (e2e)

## SDLC \- software development life cycle

What for: provided well-structured phases for organising creating high-quality software.

### Steps:

* Requirement analysis  
* Planning  
* Software design such as architectural design  
* Software development  
* Testing  
* Deployment

### Pros:

* well-structured and transparent process for all participants all knows what and why do  
* identified problems, goals and solutions to solve these problems

### Cons:

* Resources  
* Wrong meaning \- methodology is not a law and not a religion

### Models:

most familiar:

* waterfall model (oldest, sequential model, one step finishing then start next step \- collect requirements, design, implement, test, maintenance, we can use when we have strict plan and stable env and clear requirements, problem \- result can be not suitable)  
* agile model (many repeatable life cycles, features is very small, mvm, problem \- need communication between team mates \- customers, devs, designers, ops, etc.)

less familiar:

* spiral model  
* big bang model  
* iterative model

### Agile manifest

Individuals and interactions over processes and tools  
Working software over comprehensive documentation  
Customer collaboration over contract negotiation  
Responding to change over following a plan

### Twelve principles

### Agile development life cycle:

1. Products backlog  
2. Sprint backlog (grooming \- breaking down the tasks into smaller parts, decomposition)  
3. Sprint (Planning, Design, Testing, Delivering, Release)  
4. Final product

### SRUM framework

* Longer sprints  
* Self-organised teams  
* Roles, ceremonies, artefacts, sprint

### Extreme programming framework (XP)

* Iteration-based  
* Defined roles  
* Focus on technical practices

#### Extreme programming is a part of Agile methodology and includes some tech and process practices and values:

* TDD  
* Pair programming  
* SPIKE  
* planning game  
* CI  
* coding standards  
* communication  
* simplicity  
* incremental  
* quality  
* feedback

#### Stages:

1. planning (iterations, release plan, stories, small releases, incremental design, focus on faster ttm)  
2. design  
3. coding  
4. testing  
5. listening (communication and feedback)

### TDD (writing test before writing code, as a result \- good qulity of code and minimisation of bugs)

### Pair programming (two developers solve problem together, as a result \- improving skills and doing the task faster)

### Kanban practise (useful for maintenance step or testing or QA)

* Continuous workflow  
* Focus on visualisation  
* No predefined roles

### DOR and DOD

Concepts uses in SCRUM framework  
Definitions of done \- checklist for done, as developers we have to strictly clarify and don’t be paralysed  
Definitions of ready \- checklist of what needs to be done to a product backlog item before the team can start implementing it in the next sprint (it’s like DOD for customer)

## Estimation

### Main

Estimation processes: \- planning meeting \- planning poker \- estimation in story points \- creating tech tasks (business tasks or research tasks)

### Goof for start form T-Shirt to Story Points

When \- money  
Points: relative points \- track work complexity  
fixed points \- track time  
We need to clarify all requirements before estimation and change estimation when requirements was changed.  
I like to use WBS (work breakdown structure) technick for the estimation of big tasks and consulting with more experienced developers or Competency Center).  
Accuracy of estimation depends on details.  
During working on project we will receive additional info and knowledge and our estimations will be more accuracy.  
Capacity Velocity

### Types of estimation

* Start from T-shirt then move to Story points and other technics.  
* Top-down  
* Bottom-up  
* Analogous Estimation (similar)  
* Parametric Estimation (like analogous but within variables)  
* Three Point Estimation (based on average of three scenarios: best case scenario, worst case scenario and most likely scenario)

### More productive advices

* Involve in estimation process particular team  
* Use more then one type of estimation  
* Provide ranges (range of time more accurate instead of particular specific time)  
* Re-estimate

### Particular estimation tools and methods

* Breaking down the project to small parts  
* WBS  
* Excel  
* AWS cost explorer  
* etc.

### Risks

* external risk 🎩 – the result of the client’s influence  
* internal risk 🔧 – the result of the software development process itself  
* personal risk 👥 – the result of the efforts, quality and \- commitment of individual team members in the project  
* bus factor (illness)  
* overloaded (or underloaded) sprints  
* changes to the schedule  
* incomplete or extended sprints  
* sudden need of adding more people to the team  
* miscommunications

### Estimation mistakes

* Underestimate  
* Overestimate  
* How to estimate  
* Compare old work with new  
* Identify work of similar complexity  
* Use the actual time it took as estimate for new work

### Dealing with unclear requirements

* Go to agile  
* RND (spike)  
* Communicate with stakeholders

## Story points

### What is:

This is a measure to express the required amount of resources and efforts to implement the piece of work.  
This type of estimation help us to classify and track the complexity of the same pieces of work and use them in the following estimations processes.  
During working on the project our estimates will improved because our knowledge of project parts are improved.  
As a result, the estimations process became more accurate on the latest project stages.  
This is a measure to track the complexity of task.  
Why we don’t use estimation in absolute units? In some cases we don’t familiar with team members work capacity and we can track the progress by this way, because over time we can receive the velocity of team members.

### What to include:

* Personal factors  
* Risk

### Additionally:

The most important advice for more accurate estimation \- spend time to receive requirement, additional info, risk factors, complexity of system, necessarily to communicate with another people, etc. by creating strict DOD.  
WBS, RND tasks and other technics.  
Update estimation with the new knowledge about task and requirements

[image1]: <data:image/png;base64,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>