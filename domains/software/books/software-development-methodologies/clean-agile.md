---
layout: default
title: Clean Agile 
parent: Software Development Methodologies
nav_order: 1
---

# [Clean Agile: Back To Basics](https://www.amazon.com/Clean-Agile-Basics-Robert-Martin/dp/0135781868)
{: .no_toc }

![Clean Agile: Back To Basics cover](https://m.media-amazon.com/images/I/61q+XwMbDIL._SY466_.jpg "Clean Agile: Back To Basics cover")

## Details
- Author: Robert C. Martin
- Rented to: No

## Key takeaways
- Ward Cunningham [wiki](http://c2.com/), original wiki page on the Internet
- Agile values
    - **Individuals and interactions** over processes and tools
    - **Working software** over comprehensive documentation
    - **Customer collaboration** over contract negotiation
    - **Responding to change** over following a plan
    - values on the left are valued more then those on the right
- What does Agile actually do for us?
    - It provides us with **data**
    - The agile team produces data every iteration that is crucial for the manager to make good decisions
    - agile development is govern by feedback
    - the purpose for tracking the data is to have a quick way to determine the project status
- The first and most rigid information that we now on the start of the project is the **end date**
    - It should be picked because of the best business interest of the company, which makes it hard to renegotiate
- Setup user stories, compilation, deployment and test automation in the Zero iteration
- Agile iteration as usually 1 or 2 weeks, 1 week preferred because of quicker response
- Software is not a reliably estimated process
- Estimations should be as accurate as possible, but only accurate enough so that the costs of estimation are low
- **Estimations are not commitments**
- [Program evaluation and review technique](https://en.wikipedia.org/wiki/Program_evaluation_and_review_technique)
- Trivariate estimation
    - worst case → longest duration, but most accurate 95 %
    - nominal case → medium duration, 50 % accurate
    - best case → shortest duration, but least accurate 5%
- IPM length = Iteration length / 20
- Have additional metric for the value of a user story should affect priority
    - High, medium, low
- Stories should satisfy the [INVEST principle](#313-invest-stories)
- User stories should not have details in them, acceptance tests are used for that later on
- User story should be small in a way it can be implemented by 1 to 2 developers in one iteration
- Number of stories should be roughly the same as the number of developers on the team
- Agile team size should not be greater than 10. Factors that affect this decision are project complexity, cross-team factor, budget, etc.
- Simpler story estimations schemes are better
    - Poker cards and Fibonacci series
        - 0 → To trivial to estimate
        - Infinity → To large, should be broken down
        - ? → We know to little, need to investigate to be able to estimate
    - Flying fingers, 1 to 5
        - Thumb down == Infinity
        - Little finger up == 0
        - Index finger up == ?
- Velocity is a measurement not a goal, **do not put pressure on things you measure.**
- The only unsuccessful iteration is the one that doesn’t generate data
- “Customer” in agile refers to a person or group who understand the user needs
- Overtime work is not a sign of devotion or loyalty to your employer it is a sign of a employee susceptible to manipulation employee, who can’t say no and lack of planing, overtime should be exceptions (when there is no other way, a spike)
- [Standup meetings](#45-standup-meetings) in Agile should only be concerned on providing answering on 3 questions from each team member
- Through mastery, the tool becomes transparent. Without mastery, tools can become an impediment and even do harm to our project
- Follow the [following](#65-agile-tools-by-tim-ottinger-and-jeff-langr) rules when picking the right tool for the job

## Quotes
> *“The only way to go fast, is to go well.”* -- Uncle Bob

> *“There is no such thing as quick and dirty, only dirty and slow.”* -- Uncle Bob

> *“Adding manpower to a late software project makes it later."* -- F.P. Brook

> *“The race is not fast…”* -- Preacher 9,11

> *“… who endures until the end, will be saved.” -- Mathew 24,13


## Summary

## 1 Introduction to Agile

The [Agile Manifesto](https://agilemanifesto.org/) originated from the gathering of 17 software experts in early 2001 as a re-
action to heavy-weight processes like [Waterfall](https://en.wikipedia.org/wiki/Waterfall_model), or [Rational Unified Process](https://en.wikipedia.org/wiki/Rational_unified_process). Since then, Agile was adopted widely and has
been extended in various ways — unfortunately, not always in the spirit of the original idea.

### 1.1 History of Agile

The basic idea of Agile—working with small, intermediate goals and measuring the progress—
might be as old as civilization. Agile practices might also have been used in the early days
of software development. However, the idea of Scientific Management, which is based on Taylorism, with its top-down approach and heavy planning, was prevalent in many industries at
that time, conflicting with the Pre-Agile practice then prevalent in software development.
Scientific Management was suitable for projects with a high cost of change, a well-defined
problem definition, and extremely specific goals. Pre-Agile practices, on the other hand, were
a good fit for projects with a low cost of change, an only partially defined problem, and goals
only being informally specified.
Unfortunately, there was no discussion at that time on which approach was the better fit for
software projects. Instead, the Waterfall model—initially used as a straw man to be proven
unsuitable by Winston Royce in his 1970 paper Managing the Development of Large Software
Systems—was widely adopted in the industry. And Waterfall, with its emphasize on analysis, planning, and closely sticking to a plan, was a descendant of Scientific Management, not of
Pre-Agile practices.

![Waterfall model](assets/202.1.0001/1-1-waterfall-model.png)

Waterfall dominated the industry since the 1970s for almost 30 years. Its subsequent phases of
analysis, design, and implementation looked promising to developers working in endless “code
and fix” cycles, lacking even the discipline of Pre-Agile.

What looked good on paper—and produced promising looking results in the analysis and design phases—often terribly failed in the implementation phase. Those problems, however, have
been attributed to bad execution, and the Waterfall approach itself wasn’t criticized. Instead, it
became so dominant that new developments in the software industry like structured or object-oriented programming were soon followed by the disciplines of structured and object-oriented
analysis and design—perfectly fitting the Waterfall mindset.

Some proponents of those ideas, however, started to challenge the Waterfall model in the mid-
1990s, for example Grady Booch with his method of object-oriented design (OOD), the Design
Pattern movement, and the authors of the Scrum paper. Kent Beck’s Extreme Programming
(XP) and Test-Driven Development (TDD) approaches of the late 1990s clearly moved away
from Waterfall towards an Agile approach. Martin Fowler’s take on Refactoring, emphasizing
continuous improvement, certainly is a bad fit for Waterfall.

### 1.2 The Agile Manifesto

17 proponents of various agile ideas—Kent Beck, Robert C. Martin, Ward Cunningham (XP),
Ken Schwaber, Mike Beedle, Jeff Sutherland (Scrum), Andrew Hunt, David Thomas (“Pragmatic Programmers”), among others—met in Snowbird, Utah in early 2001 to come up with a
manifesto capturing the common essence of all those lightweight ideas. After two days, broad
consensus was reached:

> We are uncovering better ways of developing software by doing it and helping others do it.
>   - Individuals and interactions over processes and tools
>   - Working software over comprehensive documentation
>   - Customer collaboration over contract negotiation
>   - Responding to change over following a plan
>
> That is, while there is value in the items on the right, we value the items on the left more.

This Agile Manifesto was published after the gathering on [Agile manifesto webpage](http://agilemanifesto.org/), where it still
can be signed. The [12 Principles](https://agilemanifesto.org/principles.html) were written as a collaborative effort within the two weeks
that followed the conference. This document explains and directs the four values stated in the
manifesto; it shows, that those values have

### 1.3 Agile Overview

Many software projects are managed using approaches based on faith and motivational techniques. As a result, such projects are chronically late, despite developers working overtime.
All projects are constrained by a trade-off called the Iron Cross of Project Management: good,
fast, cheap, done — pick three! Good project managers understand this trade-off and strive for
results that are done good enough within an acceptable time frame and budget, which provide
the crucial features.

Agile produces data that helps managers taking good decisions. The velocity shows the amount
of points a development team finishes within an iteration. A burn-down chart shows the points
remaining until the next milestone. The latter not necessarily shrinks at the rate of the velocity,
because requirements and their estimations can change. Still, the burn-down chart’s slope can
be used to predict a likely date when the milestone is going to be reached.

Agile is a feedback-driven approach. Even though the Agile Manifesto doesn’t mention velocity
or burn-down charts, collecting such data and taking decisions based on it is crucial. Make that
data public, transparent, and obvious.

A project’s end date is usually given and not negotiable, often for good business reasons. The
requirements, however, often change, because customers only have a rough goal, but don’t
know the detailed steps how to reach it.

### 1.4 A Waterfall Project

In the Waterfall days, a project was often split up into three phases of equal length: analysis,
design, and implementation. In the analysis phase, requirements are gathered and planning is
done. In the design phase, a solution is sketched and the planning is refined. Neither phase
has hard and tangible goals; they are done when the end date of the phase is reached.

The implementation phase, however, needs to produce working software—a goal that is hard
and tangible, and whose attainment is easy to judge. Schedule slips are only detected in this
phase, and stakeholders only become aware of such issues when the project should be almost
finished.

Such projects often end in a Death March: a hardly working solution is produced after a lot of
overtime work, despite deadlines being moved forward repeatedly. The “solution” for the next
project usually is to do even more analysis and design—more of what didn’t work in the first
place (Runaway Process Inflation).

### 1.5 The Agile Way

Like Waterfall, an Agile project starts with analysis—but analysis never ends. The time is divided in iterations or sprints of typically one or two weeks. Iteration Zero is used to write the
initial stories, to estimate them, to set up the development environment, to draft a tentative
design, and to come up with a rough plan. Analysis, design, and implementation take place in
every iteration.

After the first iteration is completed, usually fewer stories have been finished than originally
estimated. This is not a failure, but provides a first measurement that can be used to adjust
the original plan. After a couple of iterations, a realistic average velocity and an estimation of
the project’s release date can be calculated. This might be disappointing, but realistic. Hope is
replaced by real data early in the process.

Project management dealing with the Iron Cross—good, fast, cheap, done: pick three!—can
now do the following adjustments:

- **Schedule:** The end date is usually not negotiable, and if it is, delays usually cost the
business significantly. But if the date is not crucial to the business it could be wise to negotiate with the stakeholders that it should be changed of other elements can not.
- **Staff** : [Brooke’s Law](https://en.wikipedia.org/wiki/Brooks%27s_law) states that if more staff is added to a project, productivity first plummets, and only increases over time. Staff can be added in the long run, if one can afford it.
- **Quality**: Lowering the quality might give the impression of going faster in the short run,
but slows down the project in the long run, because more defects are introduced. Lowering the quality is never an option, we can only increase it.
- **Scope**: If there’s no other way, stakeholders can often be convinced to limit their demands
to features that are absolutely needed. If development team has the data, and it should, it will win in any rational organization.

![Iron cross](assets/202.1.0001/1-5-iron-cross.png)

Reducing the scope is often the only sensible choice. Make sure at the beginning of every
iteration to only implement features that are really needed by the stakeholders. You might waste
precious time on “nice to have” features otherwise.

### 1.6 Circle of Life

Extreme Programming (XP), as described in Kent Beck’s Extreme Programming Explained, captures the essence of Agile. The practices of XP are organized in the Circle of Life, which consists of three rings.

![Circle of life](assets/202.1.0001/1-6-circle-of-life.png)

The outer ring contains the business-facing practices, which are quite similar to the Scrum
process:

- **Planning Game**: breaking down a project into features, stories, and tasks
- **Small Releases**: delivering small, but regular increments
- **Acceptance Tests**: providing unambiguous completion criteria (definition of “done”)
- **Whole Team**: working together in different functions (programmers, testers, management)

The middle ring contains the team-facing practices:

- **Sustainable Pace**: making progress while preventing burnout of the developing team
- **Collective Ownership**: sharing knowledge on the project to prevent silos
- **Continuous Integration**: closing the feedback loop frequently and keeping the team’s
focus
- **Metaphor**: working with a common vocabulary and language, domain language (ubiquitous language)

The inner ring contains *technical* practices:

- **Pair Programming/Pairing**: sharing knowledge, reviewing, collaborating
- **Simple Design**: preventing wasted efforts
- **Refactoring**: refining and improving all work products continuously
- **Test-Driven Development**: maintaining quality when going quickly

These practices closely match the values of the Agile Manifesto:

- Individuals and interactions over processes and tools
    - Whole Team (business-facing)
    - Metaphor (team-facing)
    - Collective Ownership (team-facing)
    - Pairing (technical)
- Working software over comprehensive documentation
    - Acceptance Tests (business-facing)
    - Test-Driven Development (technical)
    - Simple Design (technical)
    - Refactoring (technical)
    - Continuous Integration (technical)
- Customer collaboration over contract negotiation
    - Planning Game (business-facing)
    - Small Releases (business-facing)
    - Acceptance Tests (business-facing)
    - Metaphor (team-facing)
- Responding to change over following a plan
    - Planning Game (business-facing)
    - Small Releases (business-facing)
    - Acceptance Tests (business-facing)
    - Sustainable Pace (team-facing)
    - Refactoring (technical)
    - Test-Driven Development (technical)

To sum up:

Agile is a small discipline that helps small software teams manage small projects.
Big projects are made from small projects.

## 2 The Reasons for Agile

Many developers adopting Agile for the promise of speed and quality end up disappointed as
these results do not show up immediately. However, the more important reasons for adopting
Agile are *professionalism* and *reasonable customer expectations*.

### 2.1 Professionalism

In Agile, high commitment to discipline is more important than ceremony. Disciplined, professional behavior becomes more important as software itself becomes more important. Computers are almost everywhere nowadays, and so is software. Little gets accomplished without software.

Software is written by programmers—and bad software can kill people. Therefore, programmers will be blamed as people are getting killed due to erroneous software. The disciplines of
Agile development are a first step towards professionalism—which might save people’s life in
the long run.

We are responsible to give the best possible solution and to be aware of what is requested and what we are doing.

### 2.2 Reasonable Customer Expectations

Managers, customers, and users have reasonable expectations of software and its programmers.
The goal of Agile development is to meet those expectations, which is not an easy task:

- **Do not ship bad software**: A system should not require from a user to think like a programmer. People spend good money on software—and should get high quality with few defects in return.
- **Continuous technical readiness**: Programmers often fail to ship useful software in time,
because they work on too many features at the same time, instead of working only on
the most important features first. Agile demands that a system must be technically deployable at the end of every iteration. The code is clean, and the tests all pass. Deploying or not—this is no longer a technical but a business decision.
- **Stable Productivity**: Progress usually is fast at the beginning of a project, but slows
down as messy code accumulates. Adding people to a project only helps in the long
run — but not at all if those new programmers are trained by those programmers that
created the mess in the first place. As this downward spiral continues, progress comes
to a halt. Developers demand to start again from scratch. A new code base is built — with
the old, messy code base as the sole reliable source for requirements. The old system
is maintained and further developed by one half of the team, and the other half lacks
behind working on the new system; trying to hit a moving target. Big redesigns often
fail, few are ever deployed to customers.
- **Inexpensive Adaptability**: Software (“soft”), as opposed to hardware (“hard”) is supposed to be easy to change. Often seen as a nuisance by some developers, changing
requirements are the reason why the discipline of software engineering exists. (If nothing ever changed, hardware could be developed instead.) A good software system is easy to change.
- Continuous Improvement: Software should become better as time goes. Design, architecture, code structure, efficiency, and throughput of a system should improve and not deteriorate over time.
- **Fearless Competence**: Developers are often afraid of modifying bad code, and therefore, bad code isn’t improved. (“You touch it, you break it. You break it, you own it.”)
Test-Driven Development is helpful to overcome this fear by allowing for an automated
quality assessment after every change to the code.
- **No QA Findings**: Bugs should not be discovered by QA, but avoided or eliminated by
the development team in the first place. If the QA finds bugs, the developers must not
only fix those, but also improve their process.
- **Test Automation**: Manual tests are expensive and, thus, will be reduced or skipped if
the project’s budget is cut. If development is late, QA has too little time to test. Parts
of the system remain untested. Machines are better at performing repetitive tasks like
testing than humans (except for exploratory testing). It is a waste of time and money to
let humans perform manual tests; it’s also immoral.
- **Cover for each other**: Developers must help each other; they must act as a team. If
somebody fails or gets sick, the other team members must help out. Every developer
must ensure that others can cover for him or her by documenting the code, sharing
knowledge, and helping others reciprocally.
- **Honest Estimates**: Developers must be honest with their estimates based on their level
of knowledge. Under uncertainty, ranges (“5 to 15 days”) rather than exact estimates
(“10 days”) should be provided. Tasks can’t always be estimated exactly, but in relation
to other tasks (“this takes twice as long as that”).
- **Saying “No”**: If no feasible solution for a problem can be found, the developer must say
so. This can be inconvenient, but could also save bigger trouble down the road.
- **Continuous Learning**: Developers must keep up with an ever and fast changing industry
by learning all the time. It’s great if a company provides training, but the responsibility
for learning remains with the developer.
- **Mentoring**: Existing team members must teach new team members. Both sides learn in
the process, because teaching is a great way of learning.

### 2.3 The Bill of Rights

Agile is supposed to heal the divide between business and development. Both sides — customers
and developers — have complementary rights.

Customers have the right to …

- … an overall plan: what can be accomplished when at what cost?
- … get the most out of every iteration.
- … see progress in terms of passing tests they define.
- … change their minds and priorities.
- … be informed on schedule and estimate changes.
- … cancel at any time and remain with a working system nonetheless.

Developers have the right to …

- … know what is needed, and what the priorities are.
- … produce high-quality work.
- … ask for and receive help.
- … update their estimates.
- … accept responsibilities rather than having them assigned.

Agile is not a process, it is a set of rights, expectations, and disciplines that form the basis for an
ethical profession.

## 3 Business Practices

Development must follow the business-facing practices of Planning, Small Releases, Acceptance Tests, and Whole Team in order to succeed.

### 3.1 Planning

A project can be planned by breaking it up into its pieces recursively and estimating those
pieces. The more those pieces are broken up—down to individual lines of code in the extreme
case—the more accurate and precise the estimate becomes, but the more time it takes to come
up with this estimation. An estimate should be as accurate as possible, but only as precise as
necessary.

By giving a range of time (e.g. 5-15 days) instead of an exact duration (e.g. 10 days), an estimate
can be imprecise, but still accurate. A trivariate estimation gives a best-case, a nominal-case,
and a worst-case for a task to be finished with a probability of 5%, 50%, or 95%, respectively.
For example, a task estimated to take 8 (best-case), 12 (nominal-case), and 16 (worst-case) days
has a 5% chance of finishing within 8 days, a 50% chance of finishing within 12 days, and a
chance of 95% to finish within 16 days. To put it differently: Given 100 similar tasks, 5 will
be completed within the best-case, 50 within the nominal-case, and 95 within the worst-case
estimate.

### 3.1.1 User stories and story points

Trivariant technique works well for long-term planning, but is too imprecise for day-to-day planning
within a project. For this purpose, a technique based on an iteratively calibrating feedback loop
is used: *Story Points*.

A *user story* is written from the user’s perspective and describes a feature of the system to be
developed, for example: “As a user, I want to be asked if I want to save my document when I
close the application without saving.” The details are left out at first and will be clarified as the
developers are taking the story up for development.

Despite modern technology, writing those stories on index cards lets you physically *handle*
those stories in meetings, which can be highly valuable. Index cards impose a certain discipline
of keeping the stories vague, so that the planning process isn’t bogged down by too much detail.
The cards also must not become too valuable for being discarded.

The story cards written in Iteration Zero are estimated in an informal meeting, which takes
place regularly, usually at the beginning of every iteration. Writing and estimating stories is an
ongoing process. Estimation starts by picking a story of average size, to which an average
number of story points is assigned, say, 3 story points when working with a range of 1-5 story
points.

Other stories are compared in size against this *Golden Story* and assigned story points accordingly. The story points estimated are written on the story’s index card. Those points do not map
to units of time! Different developers would spend a different amount of time for implementing the same story. Fortunately, those differences even out as a lot of stories are implemented
over the course of many iterations thanks to the *Law of Large Numbers.*

### 3.1.2 Iteration planning

An iteration starts with the *Iteration Planning Meeting* (IPM), which should not take up more
time than one twentieth of the total iteration, i.e. at most half a day for a two week iteration. The
whole team—stakeholders, programmers, testers, business analysts, project managers—attend
the IPM.

The programmers estimate their velocity for the upcoming iteration, i.e. how many story points
they think they can complete. This is a rough guess and probably way too high for the first
iteration. The stakeholders choose the stories to fit in within the velocity estimated by the
programmers. This estimate is *not* a commitment!

The stakeholders play the *Four-Quadrant Game* to pick the right stories, i.e. those with the
highest return on invest (ROI). Along the two axes of cost and value, each story can be put in
one of four quadrants:

![Four quadrant game](assets/202.1.0001/3-1-2-four-quadrant-game.png)

1. **Valuable, but cheap**: those stories should be done right away.
2. **Valuable, but expensive**: those stories should be done later on.
3. **Not valuable, but expensive**: don’t do this stories, discard them.
4. **Not valuable, but cheap**: consider doing those stories (much) later.

At the midpoint of the iteration, half of the story points should be done. If less are done, which is
to expect from the first iteration, the iteration is *not* a failure, because it generates valuable data.
The first half of the iteration is a good prediction for its second half in terms of velocity, like
today’s weather is the best predictor for tomorrow’s weather. Likewise, the current iteration’s
velocity is also a good predictor for next iterations’s velocity.

Iterations empty the “stack” of ROI and continuous user story investigation fills the ROI “stack”. The project ends when investigation does not produce no stories and there are no more current stories in the ROI “stack” worth implementing. As long as the ROI stack is filled more than it is emptied the project continues.

### 3.1.3 INVEST Stories

User stories do not describe features in detail, they are rather a reminder of features. The
acronym INVEST stands for simple guidelines to be followed when writing stories:

- **I: Independent**. User stories don’t have to be implemented in a particular order, because
they are independent of each other. Even though dependencies cannot be avoided sometimes, they should be kept at a minimum, so that stories can be implemented in the order
of their business value.
- **N: Negotiable**. User stories should leave space for negotiations between business and
development. Those negotiations can help to keep the cost low by agreeing on simple
features and easy implementations.
- **V: Valuable**. User stories must create clear and quantifiable value to the business. Soft
quantification like high/medium/low are fine, as long as stories can be compared in
terms of their business value. Such stories usually cut through all layers: from frontend
over backend to the database and middleware. Architecture, refactoring, and cleanup
tasks are not user stories!
- **E: Estimable**. User stories must be concrete enough in order to be estimated by the developers. However, stories must still be negotiable, so aim for the sweet spot between
specificity and vagueness by being precise about the business value while leaving out implementation details.
- **S: Small**. User stories should be small enough so that they can be implemented by one
or two developers within a single iteration. A good rule of thumb is to pick roughly the
same number of stories for an iteration as there are developers on the team.
- **T: Testable**. User stories should be accompanied by tests specified by the business. A story
is complete when all of its tests pass. Tests are usually written by QA and automated by
the developers. Specifying the tests can happen later than the actual story is written

### 3.1.4 Story Estimation

There are different ways to estimate user stories. *Flying Fingers* is the simplest: After reading
and discussing a story, developers hold up the amount of fingers corresponding to their estimation of story points. They do so behind their backs, and all hands are shown on the count of three.

*Planning Poker* is a similar approach based on numbered cards denoting story points. Some
decks use a Fibonacci series (1, 2, 3, 5, 8), sometimes with additional indications: infinity (∞)
for stories too big for estimation, a question mark (?) if there’s not enough information available
to estimate a story, and zero (0) if the story is too trivial for estimation.

As fingers or cards are revealed, there might be a consensus, in which case the common number
is written on the index card. If there is a big deviation, those differences are being discussed,
followed by another round of estimation, until a consensus can be reached.

Stories too trivial for estimation (0) can be combined by stapling those index cards together.
Here, multiple zeros can indeed add up to something more than zero. Stories too big (∞) can
be split up as long they comply to the INVEST guidelines.

Stories too unclear for estimation (?) often require additional research. A meta-story — a so-called *spike*, cutting a very thin slice through the system — is created and referred to as a dependency of the original, unclear story.

### 3.1.5 Iteration and Release

An iteration produces data by getting stories done. The focus should be on finishing entire
stories rather than tasks within stories: better 80% of stories completely done than 80% of the
tasks for each story done. Stories are not assigned to programmers, but picked individually
or by negotiating within the developer team. Experienced programmers should guide rookies
away from picking up too many or too heavy stories.

QA should start writing the acceptance tests right after the IPM, so that they are finished up to
the midpoint of the iteration. Developers can help in the process, but not the same developer
should be responsible for implementing a story and writing the acceptance tests for it. However,
QA and developers should work closely together on the acceptance tests. A story is done when
all of its acceptance tests pass.

At the end of every iteration, a demo is given to the stakeholders. The newly added features
and passing acceptance tests—both old and new—should be shown. After the demo, velocity
and burn-down charts are updated. Noisy at the beginning, the velocity will average out after
a few iterations.

A rising velocity can hint to story point inflation: as pressure is put on the development team
to get more done, developers start assigning more points to their stories. Velocity is a measurement and not an objective; don’t put pressure on something you measure!

A falling velocity likely points to bad code quality, dragging further development down. If too
few unit tests are written, developers become hesitant refactoring the code. As pressure builds
up, developers will be tempted to inflate story points. Keep in mind the *Golden Story* of the
initial iteration and use it as comparison when estimating other user stories to counter the story point inflation.

Release as often as possible. The goal of continuous delivery is to release to production after
every change. Historically, those cycles were long because of long technical turnover times
(testing, checking out code). With modern source code management systems, working with
optimistic locks, checkout time approaches zero, and Continuous Delivery becomes possible.
Old organizations must adjust their processes accordingly to overcome their inertia, which
requires cultural change.

### 3.2 Acceptance Tests

*Acceptance Tests* are based on the idea that requirements should be specified by the business.
The word “specify” has different meanings, depending on who’s using it: business wants to
keep the specification somewhat vague in natural language, whereas programmers prefer a
specification as precise as needed for a machine to execute it.

The solution to this conflict is that business specifies a test in a natural language, but using
a formal structure like *Given, When, Then* (as used in *Behavior-Driven Development, BDD*).
Developers then implement those tests using their programming language. Those tests become
the “Definition of Done” for the user story.

- A story is not specified until its acceptance tests are written.
- A story is not completed until its acceptance tests pass.

Business people usually define the “happy path”, which shows that the system produces the
intended value. QA extends those tests with the “unhappy paths”, because they are good at
finding corner cases and ways a user might break the system.

QA no longer is the bottleneck at the end of the iteration, but deeply involved from the beginning. Finding lots of bugs at the end of the iteration is no longer considered proof of QA doing
its job properly. Instead, QA supplies test specifications to development, and development
makes sure that those tests all pass. This process of running the tests should be automated, of
course.

### 3.3 Whole Team

The Whole Team practice used to be called On-Site Customer. It is based on the idea that reducing physical distance improves communication. “Customer” is meant in a broad sense: it can describe a stakeholder of a project or a Scrum Product Owner.

Having the whole project team sitting in the same room not only makes communication more
efficient, it also creates serendipity: People in different roles will get together by mere chance
(water cooler, coffee machine). Hopefully, those unplanned interactions create synergy within
the team.

The advantages of co-location—better communication, serendipity—fall off in outsourcing set-
tings. As the distance—physical, cultural, in terms of language, and time zone—becomes bigger,
communication tends to get worse. Technology has improved, however, and working remotely
works quite well nowadays, especially if there’s only a gap in space, but none in terms of culture, language, and time zone. Serendipitous conversation and nonverbal communication,
however, are significantly reduced in a remote setting.

## 4 Team practices

Agile’s Team Practices are all about the relationships of the individual team members to one
another and with the product they are building. Those are *Metaphor*, *Sustainable Pace*, *Collective
Ownership*, and *Continuous Integration*.

### 4.1 Metaphor

Effective communication within a team requires a common language, including a well-defined
vocabulary of terms and concepts. Using metaphors, e.g. comparing a multi-step process with
an assembly line, can improve communication both within the team and with the customer.
Silly and bad metaphors, on the other side, can be embarrassing or even insulting towards the
stakeholders.

The term *Ubiquitous Language*, coined by Eric Evans in his book *Domain-Driven Design*, very
well defines what a team needs: a model of the problem domain, described by a commonly
accepted vocabulary, i.e. by programmers, QA, managers, customers, users—everyone involved
with the project.

### 4.2 Sustainable pace

Working long hours can make programmers feel proud of themselves. They are valuable and
needed, after all, and sometimes a project is saved by working overtime. Unfortunately, this
well intended dedication can lead to burnout, with long-term negative effects for both programmer and employer.

Judgement is often impeded when working late at night after a full working day; often grave
mistakes are made and bad decisions are taken at that point.

A software project is more like a marathon than a sprint or a series of sprints, and therefore
must be approached at a sustainable pace. If there’s spare energy just before the finish line, it’s
ok to sprint for this last stretch.

Developers must not comply when asked by the management to go faster. Working a lot of
overtime is not a demonstration of dedication to the employer, but a consequence of bad planning, and often the result of manipulable developers being coerced into agreeing on unrealistic
deadlines.

Programmers should figure out how many hours of sleep they need, and make it a priority to
consistently get that amount of sleep.

### 4.3 Collective Ownership

In an Agile project, code is not owned by individuals, but collectively, i.e. by the team as a
whole. Even though specialization is allowed and becomes a necessity as the system grows,
the ability to work outside of one’s speciality must be maintained.

The need for generalization in a system grows with its code base. But generalization can only
be achieved by developers seeing the big picture. With Collective Ownership, knowledge is
distributed across the team, which then becomes better at communicating and making decisions.

Teams practicing individual code ownership with strong barriers to modifying or even reading other’s code often become dysfunctional. Finger pointing and miscommunication become
rampant in such teams. Code solving the same problem is written multiple times rather than
shared.

### 4.4 Continuous Integration

The practice of *Continuous Integration* initially consisted of checking in source code and merging it with the main line every couple of hours. Feature toggles are used to hide changes that
were already deployed, but should not be active yet. Later, the introduction of *Continuous
Build* tools, which run all the tests automatically as code is check in, shortened this cycle to
minutes.

Programmers should run all the tests locally before checking in code, so that the continuous
build never breaks. If the build breaks nonetheless, it’s the highest priority for the entire team
to get it running and the tests passing again. Once discipline slips and the build is left in a
broken state, the team very unlikely will make the effort to “catch up later”. As a consequence,
broken systems will be deployed sooner or later.

### 4.5 Standup Meetings

The Standup Meeting or Daily Scrum is optional. It can be held less often than daily, at whatever
schedule it fits the team best. The meeting should take roughly ten minutes, no matter how big
the team is.
The team members stand in a circle and answer the following questions:

1. What did I do since the last meeting?
2. What will I do until the next meeting?
3. What is in my way?

No discussions are held, no explanations are given, no complaints are made. Every developer
gets half a minute. If people other than developers take part, they either should only listen or
talk according to the same rules as the developers.

The *Chicken and the Pig* is a fable that demonstrates why non-developers—the chickens, making
a small sacrifice to provide eggs—and developers—the pigs, sacrificing their life to provide
meat—should not have the same weight in making decisions about the (menu) plan.

## 5 Technical Practices

The technical practices of Agile reach deep into the programmer’s behavior when writing
code, by adding a set of rituals considered absurd by many programmers. Those practices
at the very core of Agile are: *Test-Driven Development*, *Refactoring*, *Simple Design*, and *Pair
Programming*.

For details for this section take a look at sections 2 to 5 in [Clean Craftsmanship](202.1.0002-clean-craftsmanship.md).

## 6 Becoming Agile

Even though becoming Agile looks easy—it’s just a couple of disciplines and practices, after
all—many organizations fail at it. The reason for this could be that those organizations trying
to adopt Agile have misconceptions about what becoming Agile actually means.

### 6.1 Agile Values

Kent Beck named the following four values that are at the very core of Agile:

1. **Courage**: Agile teams don’t sacrifice quality and opportunity in exchange for political
safety. It takes courage to maintain high code quality and to stay disciplined. However,
deploying code without confidence in its quality and design is reckless, which is not the
same as being courageous.
2. **Communication**: Agile teams value communication—not only within their team, but also
with stakeholders on the outside. Informal communication is especially useful, for it
helps teams to grow together and strengthens the relationship to the stakeholders.
3. **Feedback**: The Agile practices and disciplines have one common benefit: they provide
rapid feedback. This helps to detect when things go wrong early on, so that there’s still
space for corrections. This feedback also confronts the team with the consequences of
decisions made earlier.
4. **Simplicity**: Being simple is being direct. Software problems are often solved by introducing additional layers of indirection. Agile values reduce the amount of problems to be
solved, so less indirection is needed. Indirection in communication—passive aggression
or grudgingly acceding to unreasonable demands instead of openly opposing them—just
postpones conflicts to a later date. Reduce indirection in the code to a sustainable level,
but eliminate indirection in personal communication completely.

When adopting Agile, don’t spend a lot of time evaluating different frameworks like XP or
Scrum. At the end, you’ll tweak the framework in a way best fitting your organization’s
needs.

Adopt the Circle of Life, especially the technical practices in the innermost circle. Without
those, the code will degrade, and the Agile practices in the two outer rings will make a mess
of everything very quickly.

### 6.2 Transformation

The values of large organizations—safety, consistency, command-and-control, plan execution—
are diametrically opposed to the values of Agile. Therefore, a transition to Agile is a transition
in values.

Such change is usually opposed the most by the middle-management layer, which is trained
to avoid risks and direct communication. Middle management is a layer of indirection, after
all—exactly what is to be avoided in Agile. Executives, on the other side, are risk takers that
constantly seek out new opportunities, and therefore tend to be supportive of Agile transformations.

Employees in special roles, such as tech leads, architects, or project managers, also tend to
oppose Agile transformations, for they see their roles diminished in an Agile team. Actually,
their skills and experience are especially needed in Agile teams.

It is also possible for a development team to internally make the transition to Agile while still
conforming to the process imposed by middle management towards the outside. Instead of
arguing against writing analysis and design documents, those artifacts are just created during
the first couple of sprints as a by-product of the code that already has been written. Analysis
and design are done for every story, after all, especially in early stories.

Even though this “faking it” can be considered dishonest, nobody will complain if it yields good
results. The team just acts for the greater good of the company, as opposed to just complying
to the demands of middle management.

If the transition to Agile values only happens for a few individuals within a team, those employees tend to leave the team or the organization sooner or later, seeking out new opportunities better in alignment to their freshly acquired mindset. Large organizations usually don’t adopt Agile as a whole entity, but create new, smaller organizations based on Agile values. Eventually, those new companies become bigger and grow out of the parent company, as the former thrives with Agile and the latter stagnates with its old ways.

### 6.3 Coaching

An *Agile Trainer* conducts the initial training with the team and inculcates Agile values. Agile
trainers are usually hired from the outside for a short tenure, i.e. for a couple of weeks.

The role of an *Agile Coach*, on the other hand, should be filled from someone within the team,
even though an Agile trainer from the outside could initially take that role during a short
transition period.

The coach makes sure that the team sticks to the Agile way, acting as the team’s conscience. The role of the coach can be re-assigned to other team-members frequently, as long as it is taken seriously.

The coach is not a manager and also not responsible for planning and budget. Neither do
customers nor managers need to know who the coach is, for that role is strictly internal to the
team.

In Scrum, such a coach is called a *Scrum Master*. Since many project managers have taken the
training and certification to become a Scrum Master, that role is often conflated with the role
of the project manager.

Even though the trainings that lead to such certificates are useful, the certificate itself proofs
next to nothing, i.e. only that the certification fee has been paid. If formal training is given, not
only a single person should receive it, but the entire team.

### 6.3.1 Coaching—An Alternative View (by Damon Poole)

A big part of coaching is to ask questions. Agile training needs to take the learner’s unique
circumstances into account. Embracing Agile requires a shift in thinking. To overcome that
hurdle, one needs to be shown “what’s in for me”. Coaching is not so much offering expertise,
but rather pointing out how Agile can help to overcome challenges and solve problems.

Coaching is not prescribing a solution, but to discover blind spots and to bring the underlying
beliefs that stand in the way to the surface.
An Agile transformation should be conducted in an Agile way, and not as a project with a clear
goal, executed in a top-down manner.

### 6.4 Agile in the Large

Agile was intended for small teams of 4 to 12 developers, not for big ones. However, it was
soon tried to adopt Agile for multiple teams and large organizations. First using a technique
called Scrum of Scrums, later with frameworks like *SAFe* (Scaled Agile Framework) and *LeSS*
(Large Scale Scrum).

The problem of managing big teams is as old as civilization and has been solved already rather
well. (If this weren’t the case, no pyramids would have been built.) The problem of organizing
small teams that develop software, however, is rather new. Software is unique and requires a
special set of disciplines. Agile was brought up to solve that particular problem of software
development. It therefore isn’t suitable for managing other endeavors, such as construction
or hardware manufacturing.

The problem of managing big software teams is just a matter of organizing them into smaller
teams. The former is a standard management technique, i.e. a problem solved, the latter is
done using Agile. Software organizations have very diverse teams, such as development, QA,
marketing, research, etc. But even the problem of organizing very diverse teams has been
solved long ago by many civilizations time and again, just think of organizing a big army.

### 6.5 Agile Tools (by Time Ottinger and Jeff Langr)

Carpenters first learn to master hand tools—hammer, measure, saw—before they move on to
power tools—drill, nail gun, CAD. However, they never abandon their hand tools entirely, but
always pick the appropriate tool for every job: simple task, simple tool.

Mastery of every item in the toolbox allows us to focus on the problem at hand, as opposed to
the tool that is in our hand: Through mastery, the tool becomes transparent. Without mastery,
tools can become an impediment and even do harm to our project.

Software developers use a lot of different tools (editors, compilers, version control, etc.), so it
is unfeasible to master each and every tool. Therefore, only the tools should be picked that offer
the most value for the least learning effort.

Tools for the same purpose (e.g. version control) are replaced by better ones now and then, like
CVS was replaced by Git in recent years. If you learn a tool like Git well enough—the 80/20
rule applies (20% of the effort gives you 80% of the benefit), such a tool becomes transparent,
so that you can focus on the task instead of the tool.

Better tools can influence and improve the way we’re working. Git, for example, with its
support for fast and cheap branching, allows for new workflows, such as *test && commit ||
revert*: the tool is exapted, i.e. used in a way the creator of the tool hadn’t intended.

Great tools do the following:

- Help people accomplish their objectives
- Can be learned “well enough” quickly
- Become transparent to users
- Allow adaptation and exaptation
- Are affordable

For co-located Agile teams, simple physical tools like sticky notes, tape and a whiteboard often
do the job. However, they fail for remote teams and don’t automatically retain a history of the
project.

In IT, the temptation to use powerful software tools is always there. Before adopting such
powerful tools, make sure that you really can handle the process. The tool you introduce must
support your specific process. Shape the tools to your needs, not the other way around.

Complicated tools for Agile Lifecycle Management (ALM) require constant attention and upfront training. They usually can only be changed in the ways their vendors intended—if at all.
ALM tools usually are expensive and require maintenance and administration. Such tools never
become transparent, and thereforee don’t help the developers doing their work. Instead, those
tools offer powerful performance charts and statistics, which can be used as a weapon against
programmers to shame them into working harder, because the tool suggests so. ALM tools
should not replace or even stand in the way of personal, informal interactions. When in doubt,
start with a simple tool, and consider switching to a more powerful one later if needed.

## 7 Craftsmanship

Covered in detail in the notes for [Clean Craftsmanship](202.1.0002-clean-craftsmanship.md)
