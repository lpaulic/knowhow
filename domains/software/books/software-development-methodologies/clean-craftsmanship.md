---
layout: default
title: Clean Craftsmanship 
parent: Software Development Methodologies
nav_order: 2
---

# [Clean Craftsmanship: Disciplines, Standards, and Ethics](https://www.amazon.com/Clean-Craftsmanship-Disciplines-Standards-Ethics/dp/013691571X)
{: .no_toc }

![Clean Craftsmanship: Disciplines, Standards, and Ethics cover](https://m.media-amazon.com/images/I/61Pk6qD6stL._SL1360_.jpg "Clean Craftsmanship: Disciplines, Standards, and Ethics cover")

## Details
- Author: Robert C. Martin
- Rented to: No

## Key takeaways
- Craftsmanship is split in three main groups:
    - Disciplines → *TDD*, *Refactoring*, *Simple design*, *Pair programming*
    - Standards → *Productivity*, *Quality, Courage*
    - Ethics → *Damage*, *Integrity*, *Teamwork*
- Discipline is set of rules that are based on two parts: core part and optional part.
The core part gives discipline the meaning of its existence whereas the optional
part gives discipline its shape and content.
- TDD is difficult and complex, but it is worth it.
- [Three laws](#21-tdd-laws) of TDD
- Whenever you take a look at someones code refactor it as an act of kindness, even if there are
 no unit test add them
- Refactoring is a continuous effort, it doesn’t change the behavior only the structure, and it
should never be planned or scheduled. Never ask for permission you do it always
- **Incorrect responsibility** -- error in design where the function name depicts an operation
that it does not do. The operation is done elsewhere.
- TDD heuristic rules:
  01. Write a test which will make you write production code you already want to write
  02. Let if fail. Let it pass. Fix it.
  03. Do not go immediately for the gold.
  04. Write the simplest, most specific and most degraded test that fails.
  05. Generalize where possible
  06. When it seems that the code (test or production) is wrong, fix the design before continuing.
  07. Use current simpler test case before moving to the next, more complex, case.
  08. If to much production code is needed to make the test pass, delete the test
  and write a simpler test that is easier to pass.
  09. Follow a deliberate and gradual pattern that covers the test cases.
  10. Do not add unnecessary things to tests.
  11. Do not use production data in tests.
  12. Separate the structure of test code from the production code.
  13. As the tests become specific, the code becomes generic.
  14. If transformation leads to an suboptimal solution tryout a different one.
  15. Avoid the use of the debugger.
- Push code to SVC whenever you have a new passing test that is refactored. If you stop working,
commit whatever you have, with an appropriate message.
- TDD is a generic technique to incrementally construct an algorithm
- [AAA and BDD](#31-arrange-act-assert----aaa) are two of the famous test patterns
- BDD and TDD are synonyms
- [test doubles](#32-test-doubles) are patterns to write test with dependencies
- TDD uncertainty principle: *If we demand certainty from our test we will sacrifice flexibility.*
*If we demand flexibility from our test we will sacrifice certainty.*
- London school and Chicago school to tackle the TDD uncertainty
- Rules of [database testing](#41-database-testing):
  - Do not test the database
  - Separate the database from business rules
- Guide lines for [testing GUI](#42-testing-gui)
- Intro to [test patterns](#43-test-patterns)
- How to [designing tets](#44-test-design)
- Following good [test design](#44-test-design) we want to accomplish that changes to
production code demand minimum changes in test code
- A unit in unit test, should relate to functionality and not structure specific
(i.e. function, module, etc.)
- [Transformations](#45-conditions-for-priority-transformations) used when practicing TDD
- Rule of thumb for [refactoring](#5-refactoring): *Small changes so I don't need to fix errors.*
- Actions to use when refactoring are mentioned in the section: [Refactoring](#5-refactoring)
- When you refactor always start after you commit working code so you can revert
back if things go to a dead end
- Remove knowledge duplications not code duplications, because two parts that are
not handling the same thing can have same code.
- Standards that should be followed are categorized by:
  - [Productivity standards](#9-productivity)
  - [Quality standards](#10-quality)
  - [Courage standards](#11-courage)
- Intro to ethics from Uncle Bobs perspective starts from page 280.
- The programmers oath that is further discussed in sections [Damage](#12-damage),
[Integrity](#13-integrity) and [Teamwork](#14-teamwork):
  01. I will not produce harmful code.
  02. The code I produce will always be my best work. I will not purposefully allow
  accumulation of code that has defects in functionality and structure.
  03. In every version I will create a fast, safe and reproducible proof that every
  element of code works as expected.
  04. I will create periodic and small versions that will not interrupt the work of others.
  05. I will rigorously and fearlessly improve my creations in every opportunity. I will
  never degrade them.
  06. I will do everything I can that my productivity and the productivity of others is as
  high as possible. I will never do anything that will decrease productivity.
  07. I will always make sure that others can replace me and that I can replace others.
  08. I will create estimates that are honest by size and accuracy. I will not make promises
  in which I am not certain.
  09. I will respect my colleagues because of their ethics, standards, disciplines and skills.
  No other characteristic or attribute will be a factor in my relation towards my software engineering
  colleagues.
  10. I will never stop learning and perfecting my craft.

## Quotes
> *“Leave code cleaner than you found it.”* -- Uncle Bob

> *“First make it work, than make it right.”* -- Uncle Bob

> *"As the test get more specific, the code becomes more generic"* -- Uncle Bob

> *"In BDD examples are used to describe haw an application behaves... and these examples are then discussed"* -- Liz Keogh

> *Small refactor changes so I don't need to fix errors.* -- Uncle Bob

> *"Find a good mentor  and become an even better one."*  -- Luka Paulic

## Summary
## 1 Craftsmanship

The history of software development is quite similar to the history of aviation. It was decades of attempts,
mistakes, disasters until commercial flight became a reality. Similarly in software engineering from Countess
Ada, Alan Turing, Edsger Dijkstra to modern companies in their humble beginnings such as Apple, IBM and Microsoft
Both are filled with gradual enrichment in technology and knowledge through hastiness and failure. The question
that arises is have we prepared captains Sullenberger in our software engineering world. Software engineers
that navigate their profession in the same manner pilots do in theirs?

Craftsmanship is knowing how to do something the right way and it a result of great mentoring and decades long
experience. Most of today’s programmers have not learned the necessary disciplines, standards and ethics that
define the software engineering craft. Most programmers look at software engineering as gateway to management.

## 2 Test Drive Development

Main discipline is software engineering, without it other disciplines are meaningless or impossible. Test Driven
Development, or TDD for short, governs ow programmers work from second to second. You either do it or you don’t.

The core of TDD are small cycles and tests come first. They are written first and they are cleaned up first.
The cycles are measured in seconds, not minutes and progress is measured in characters not lines of code.
The feedback loop created is very short and gives us result instantaneously.

The purpose of TDD is to provide a group of tests that we trust and provide us we the courage refactor, make good
estimations and good decisions. TDD is a loot like double bookkeeping in accounting.

### 2.1 TDD Laws

TDD ensures the following:

1. Creates a suit of tests that enable *refactoring* and which we trust in such a way that if the tests pass
the software can be deployed.
2. Creates production code that is decoupled enough that it can be *tested* and *refactored.*
3. Creates a short feedback loop that maintains the code writing process stable and productive.
4. Creates tests and production code that are decoupled enough so both can be maintained, without
multiplying the changes between them

There are three laws:

1. Do not write production code before you write a test that fails because the production code is missing
2. Do not write more test code than it is necessary for the test to fail or not compile.
Solve the error by writing some production code.
3. Do note write more production code than it is necessary for solving the current failing test.
When the test passes, write more test code.
4. *Unwritten rule: **Refactor***

These three laws, if followed correctly, provide us with the following benefits. The first benefit is
that we spend lest time debugging. Contrary to popular belief not being a debugger guru is a good thing,
because you focus more on writing code that works instead of fixing code that doesn’t work.
TDD won’t eliminate debugging, but it will significantly decrease it.

The second benefit is that the written test act as documentation. Test written using TDD provide us
with *usage examples* of our code. These test explain the details of how our package system works,
i.e. how to call an API, what arguments are expected by the API and what errors are generated and
in which conditions. It is important to point out test are great low level documentation,
they fail to provide the big picture of the system and why are things done in a specific way.

The third benefit is that we don’t have wholes in the design. This phenomenon is noticeable in the
traditional approach where we write code and then we write tests. Then when test are written for the
code that we test manually and “know” that it works we write test because we have to. Quickly we ran
into a situation where a test is hard to write because the production code is hard to test, than we
have to change the production code to be able to test it. That is an issues because it takes a lot
of time and it can break stuff and we don’t have anything to check if the tings we change are working.
This is the point where we give up and stop with the tests and leave a hole in the test suit.
Holes in the test suit prevent us from making decisions about deploying because we don’t know if it works.

The fourth benefit is courage. Test suits give us the foundation for refactoring and deploying to production.
When the tests pass we can be highly certain that the software works and can be deployed to production.

Refactoring is the fourth rule of TDD. It is necessary that in the cycle of writing test and working production
code that we clean it up following good software development standards so we prevent the code from degrading
over time. The TDD is extended: write a test that fails, write production code that makes the test pass,
clean up the production code.

![Refactoring cycle](assets/202.1.0002/2-1-refactoring-cycle.png)

1. **Red**: Write a failing test.
2. **Green**: Write as much production code as needed to pass the test.
3. **Refactor**: Clean up that code without breaking any tests.

### 2.2 TDD Basics

The primary goal of every software designer is to big and complex systems to small and simple problems.
The TDD heuristic rules are extracted in the [Key takeaways](#key-takeaways).

The first step in developing with TDD is to write a test that does nothing, cleverly named `nothing()`.
It passes so we can continue. Now we are faced with the problem of what to test when there is nothing
to test. The answer is simple: *write the test code for the production code you want to write*.
This is described with the first heuristic
rule *1. Write a test which will make you write production code you already want to write*. For example
you would need and structure, or a function that does something, etc. Now that you know what production
code you want to write, before writing it add a test. Rewrite the test that does nothing so it creates a
structure that you want, or calls the function that you want. Than you add the structure or the function.
After the test passes see if you can refactor something before continuing adding new test. It is important
to note that **some test will be removed, or they will be renamed but that**
**is normal life cycle in TDD, because they will be replaced with different test that are more suitable**
**for the production code that is changing**.

The second heuristic rule *2. Let if fail. Let it pass. Fix it.* ensures that changes are done continuously
until you get to the functionally that is required. This intervals between writing test, writing code and
then refactoring are small. Initially starting from ~10s increasing as the more and more functionality is
added but is still measured in ~10 mins.

The heuristic rule *3. Do not go immediately for the gold.* is an important one. Because if we start with
the implementation of the core functionality, we will skip a lot of the incremental step in TDD. That is
why we should start it the less important parts because they will enable us to add small bits of production
code and progress steadily. The concrete guidelines on doing the small steps and the order of doing them
is explained in detail in [2.3 Advance TDD](#23-advance-tdd).

The heuristic rule *4. Write the simplest, most specific and most degraded test that fails.* leads us to
start by writing small, simple, basic tests which enable us to test the edge cases, by adding small parts
of production code. When the production code grow we always have this test that need to pass to ensure
that the behavior did not change when the production code had structural and behavioral changes.

Writing the simple, most specific and degraded test implies that the test code is going to have a lot of
constants. The next steps would be to replace them with variables. This gets us to the next heuristic
rule *5. Generalize where possible*. The generalization doesn't only focus on constants and variables but
also on extracting code to functions, changing if to while, etc.

After we start generalizing the code one of next challenges is to detect issues with the design in both
test code and production code. This skill is something that comes with experience and knowledge.
This skill enables us to recognize that some part of the code is working in such a way that make other
things difficult, i.e.: writing new tests, implicit changes, etc. One most notable error in design is the
responsibility issue -- the name of a function suggests that the function does something that in reality
it does not or vice versa. This challenge is depicted with the rule
*6. When it seems that the code (test or production) is wrong, fix the design before continuing*.
This is accomplished by refactoring. Refactoring is the process of changing the code structure without
affecting its behavior.

Now we covered the basic of TDD. Starting with an empty test, expending it with test code that test
production code what we want to write, than writing that production code. Test code start of simple,
testing not the main functionality but the side parts and production code implements those simple cases.
The product code, based from test, start of simple as well by using constants, code duplications,
to later, using refactoring, grow to well structured and functioning production and test code.
The constants and duplications have been replaced and the main functionality implemented.

## 3 Advance TDD

The advanced TDD concepts start by expanding the heuristic rules for writing more complete test cases.
The rule *7. Use current simpler test case before* *moving to the next, more complex, case* guides us
to start with a simple test case and exhaust it until moving to the next test case. For example if we
test a integer sum function, this rule would mean to cover all relevant possible scenarios with
summarizing 2 numbers before moving to summarizing 3 numbers. That would mean to summarize with zero,
one negative number, two negative numbers, two positive number, number that causes extra digit in the
result.

This rules ties great with the next rule *8. If to much production code is needed to make the test pass,*
*delete the test and write a simpler test that is easier to pass*, which is the main problem for TDD
newcomers. As soon as you get lost or stuck adding production code to pass a test or you've added a lot
of production code. Turn back to the test and see if it can be simplified in a sense if there is a different
test pattern that will simplify the production code increments. If you get to a point were you have to
add a bunch of production code in one iteration to make a test pass, remove one or more test and replace
them with a simpler test(s). This is backed by also the ninth heuristic rule
*9. Follow a deliberate and gradual pattern that covers the test cases*. Where we achieve these simple test
by following a natural pattern that arises from the requirements.

### 3.1 Arrange, Act, Assert -- AAA

First to discover the pattern for writing test was Bill Wake. He called it 3A, or Arrange, Act, Assert.
The pattern states that the first thing you should do is edit the test data. This is usually done in a
`Setup` function or at the beginning of a test function. The purpose is to get the system in a desired
state before starting the test.

After the test is setup next we execute something. This is done when the function that wants to be tested
is called from the test function. Then the last step is it verify the result from the execution. This is
done by comparing the return from the execution with an expected value to verify if the system is in
the desired state.

To the same conclusion came Dan North, together with Chris Stevens, Chris Matz but they used different
semantic, they called it Given-When-Then (GWT). First it was tough that GWT was a better pattern than AAA,
but in essence they are the same, with addition that GWT has a better dictionary to include in testing
frameworks. Even though tests specified with GWT are in natural language, because of the form it is
relatively easy to parse it and execute a test programmatically. Some frameworks that use BDD and TDD are
JBehave and RSpec. It is important to note that BDD and TDD are synonyms.

Overtime GWT served more as a language to specify requirements and behavior than a way to write tests.
It is hard to entirely separate GWT and AAA, this is depicted with:
- Given data that is Arranged
- When the test case is Acted on
- Then the desired result is Asserted

There is one more pattern that is related to GWT and AAA and is used in software and that is FSM, or also
known as Finite State Machine. FSM is depicted with states, in which a system can be, transitions, by which
the system changes its states, and triggers that cause the systemd to change state using a specific transition.
Because of tis FSM is equal to GWT and that is why every test that is written goes to a specific sets of
states describing the systems behavior and reaches the desired (end) state.

So tests that are written using TDD and behaviors that are described using BDD are transitions through states
that we write. So the test suite is a FSM. Affiliates of BDD ironically reached the conclusion that the best
way to describe system behavior is through FSM.

### 3.2 Test doubles

Everything looks fine and dandy for TDD for now, right? But we still haven't reached the crucial part and
that is the real word problems. Usually the systems are not so simple and we have dependencies, that most
likely are provided by a standard source or a 3rd party. One of those examples are driver/library for
IO devices, communication with databases, network communication over sockets, etc. We can not force those
parts to always act as we want them, if we can it is usually tedious. The smart programmers came to the idea
to use fake objects to replace the real IO devices and databases, so that test are simplified and controllable.
The fake objects are sometimes, especially in the early days, referred to as *mocks*, but than Gerard Meszaros
came along and in his book *xUnit Test Patterns: Refactoring Test Code*, and introduced a new language to
refer to those objects: *test doubles*.

![Test doubles](assets/202.1.0002/3-2-test-doubles.png)

There are multiple types of test doubles:
- **Dummy**: Dummy test double requires and abstract interface. This interface is used so we have an
abstraction layer in our code which hides implementation details. This enables us to have multiple
implementations of the same interface, one of which is the dummy test double. Test double is the
abstraction implementation that does nothing. It only implements the interface and if there are
interface functions that return a value that value is close to `null` or `0` depending on the language.
Use case is when a function takes an object as a parameter but that object is not needed to test
the function.
- **Stub**: Stub test double is a Dummy, the abstraction function does nothing, but instead of returning
`null` or `0`, Stub functions return values that enable the function to take branches in code which the
test wants to test. We can create as much stub implementation of the abstraction as there are possible
execution paths for a functionality.
- **Spy**: Spy test double is a Stub, it returns values specific for the test case so desired path of
the system functionality is tested, but Spy test double remembers what has happened and allows the test
code to ask about it. Spy objects can vary in complexity, from a simple boolean value to a complex
structure, because of that it is useful to check if the code is behaving as expected, but is also
dangerous because it tightly couples the test code with the production code.
- **Mock**: Mock test double is a Spy, returns values specific for the test so the test case goes through
desired path of the system functionality and remembers what happened, but also knows what to expect and
based on that can pass or fail on a test. A mock test double can be viewed as an extension of the Spy.
The extended part is that the Mock test double can hold the expected values, and expose a validate
function to check if the status of the Mock is correct after the functionality was tested. One big issue
with Mock test doubles is that the test code is embedded in the mock and that hides part of the test
implementation and makes test code unclear.
- **Fake**: Fake is not a Dummy, or a Stub, or a Spy, or a Mock. Fakes are test doubles that implement
business rules in a way that the test code can select how the fake will act based usually on the value
passed. For example a fake authenticator can return `false` for a password if it is by some rules bad,
or `true` if it is good. The bad part of Fake test doubles is that the fakes grow as the application
grows so it has to be constantly maintained.

Test doubles align with the heuristic rules *10. Do not add unnecessary things to tests*,
*11. Do not use production data in tests*.

### 3.3 TDD uncertainty principle

The TDD uncertainty principle is the problematic of when to say that test for certain functionality are
enough to state that the functionality works. It maybe looks silly based on the simple examples shown in
the Clean Craftsmanship up to this chapter. But those functions had the format where low amount of test
inputs proved that the production code works. Adding more examples would not made a difference in the
validity of the test. On the other hand there is set of problems for which it is not that clear when
the test give certainty that the production code works. One of those examples shown by the book is
implementation of the sinus trigonometry function. Inputs to the sinus are degrees in radians as decimal
numbers and gives decimal numbers as return. The problem is that no amount of tests give you a sense that
the code is tested enough to say that the production code is working as expected. The problem is that
inputs are rational numbers that have a lot of possible values that also depends on the selected
precision. The other problem is that comparing rational number on computers is only possible by
having an tolerance of error.

There aren't that many functions that leave you in this state of worry if there is an special input that
could invalidate your test that you didn't try. So TDD is not doomed yet. This types of problems are
still possible to solve and it is not by trying all possible values of the input parameter type.
The solution is not that simple tough and it depends on the problem. The solution is to find ways to test
the results not by testing them directly but to test identities that are related to the problem.
This is best explained by the trigonometry problem from the beginning. It is not feasible, to completely
validate that the sinus function returns the correct result for a given angle but we can check if the value
is in the range [-1, 1]. We can also check if the Pythagoras theorem is valid for the sinus and cosines of
the same angle. Also this test will depend on the implementation and for the example Taylor series was used
with the order of 20 elements. The order of 20 was selected because on the system it was tested in the book
that number was needed for the trigonometry identities to be validated successfully.

This all boils down to this fact: *If we demand certainty form our tests, we will inevitably connect the*
*test code with the production code and that will make the test brittle.*

This principle only set some limitations on the usefulness of our test. We need to find a compromise between
certainty and flexibility. There are two streams of taught regarding this issue London school and Chicago
school. They try to tackle the problems of brittle tests and test certainty.

*Brittle test* occur when tests are not properly designed. This leeds to situations where small changes in
production code, even just refactoring, cause majority of tests to fail and force the developer to refactor
them as well. The more the test code is coupled with the production code more brittle the test code becomes.
Test doublers Spy and Mock rely on the production code implementation and make the test code brittle.
Tools for simulation more often than none require the use of Spy and Mock. Experience suggests to avoid
simulation tools.

*Test certainty* if test double Spy is avoided only options are testing values and properties. Testing values
means to pair input values with output values, as we have seen works good for majority of test but not for all
(trigonometry example). Property testing are test that go through multiple input values and test invariants.
These tests are good but they can leva you in doubt after they are ran, but on the other hand they are maximally
decoupled from the production code implementation, change of the implementation does not affect the tests.

The London school (Steve Freeman, Nat Pryce) values certainty more than flexibility, that's why they use more Spy
and Mock test doubles. This doesn't mean they do not care for flexibility they absolutely do but they are ready
to sacrifice flexibility to ensure certainty which will provide them with more safety. They value how the results
are calculated more than they value the results themselves, the algorithms to them are more valuable then results.
That is why they approach a problem using the outside-in method. The outside-in method of designing software
starts from the UI and moves towards business rules one use case at a time. They use Spy and Mock test doublers on
avery architecture boundary to prove that an algorithm for the internal communication works. At the end when they
reach the business rules they connect them with databases after which they follow the reverse path to UI and test it.
This approach is cyclic going from outside in one use case at a time. This is a highly disciplined and clean
approach that, if done well, leads to great results.

The Chicago school (ThoughtWorks) values flexibility more that certainty. They understand the value of certainty and
safety by they sacrifice it for flexibility where possible. They focus more on results than on algorithms. This leads
to completely different philosophy of software design than the London school. Chicago school starts from the business
rules and go towards UI, this is referred to as inside-out software design method. Although also disciplined, this
approach does not got through one use case at a time but they use value and property test to verify business rule
implementations before moving to UI. Layers between UI and business rules are implemented as needed. The integration
of business rules with databases are also going to  be done last. Instead of following one use case from start to end
and duplication implementation along the way, this approach searches for patterns and duplications and add abstraction
and generalization. This approach is less tidy then the London school approach but it shows the big picture better.

So which one to go with. The short answer is: depends. One school is not more correct than the other its just a matter
of preference. Followers of one school don't only use the one school but use both with more inclination to one.
The compromise is best depicted in the [Clean Architecture](202.1.0005-clean-architecture.md). Short story when writing
test for low lever parts of the architecture, test doubles will be used for the components outside the architecture
boundary, in other words when testing a component that has dependencies those dependent components are replaced with
test doubles. So London school when test need to go pass the architectural boundary. When tests are only inside the
component that we are Chicago school and test values and property.

## 4 Designing Tests

Proper test design is one of many layers of TDD, which takes years to master. The principles for test design that
are covered by this section include database testing, GUI testing, principles of good test design, test patterns
and interesting and influential theoretical possibilities.

### 4.1 Database testing

First rule of database testing is: *Do not test databases*. It is a safe assumption that databases work.
The real thing you want to test are the queries, or to better phrase it the thing to test is the formant
of the commands that are sent to the database. For example if SQL is used directly you will test if the
SQL query does what is planned. One important thing to note is that non of the test need business data to
test you just need the queries. This brings us to the Second rule of database testing:
V*Separate the database from business rules.*

The way to separate the database from the business rules, suggested by Uncle Bob, is to add an interface
that is an abstraction which will hold methods for each manipulation on the database. This interface then
allows us to simply implement whichever database we are using, i.e. SQL, NoSQL, ORM, etc. No database
implementation details are now below the abstract interface that is placed on the architectural boundary.
The interface implementation constructs business objects from the database so nothing regarding the
database is known pass this interface.

This approach makes testing the database simple, we can create a simple database for testing purposes on
which we call the interface methods to ensure that method calls have the desired effect on the database.
We make sure that business object returned from the interface method calls are just as we expect the to
be depending on the method. Do not use the production database it is not needed, because we only need
data in the database that will enable us to test the interface. One important thing is to always setup
the database with initial data for every test, so each test is called upon the same data. When testing
business rules that utilize the database use the Stub and Spy test doubles to replace the actual interface
implementation. This is important because the use a real database because this will prolonge execution time
and can be error prone because ghost in the machine type of bugs.

### 4.2 Testing GUI

Rules for testing GUI are the following:
1. Do not test the GUI
2. Test everything but the GUI
3. GUI is smaller than you think

The GUI is actually a small portion of the software that is only tasked with displaying information
on the screen. For Web based applications GUI is the part of the software that creates the HTML,
for desktop applications the GUI is the software that calls the API for graphical control.
It is the software designer to make the GUI software part as small as possible. The simplest example
is data formatting, the GUI should not know how to format the data, the GUI only needs the character data.

The module that formats the data for GUI is called the **Presenter**. The **Presenter** deals with all the
logic for formatting the data so that GUI can be as small as possible. The **Presenter**, for example,
determines the state of each button and each menu. It determines the names and should the elements be available.
If the button name changes because of the window state, the **Presenter** is the one who know about that
state and changes the name. If on the screen should display a grid of numbers, the **Presenter** creates a
table of strings correctly formatted and distributed, also if special fields need to be different colors or
fonts the **Presenter** adjust that as well.

The **Presenter** creates simple data structure of strings and boolean flags that GUI know how to use to
create commands that are sent to the screen. The data structure that the **Presenter** creates is called
**ViewModel**. An **Interactor** communicates with the **Presenter**, by exchanging data structures via
**Presenter** interface. The **Presenter** interface prevents the **Interactor** to know the implementation
details of the **Presenter**. The **Presenter** than constructs the **ViewModel** structures that will be
sent to the GUI which will transform the **ViewModel** into commands to control the screen.
The **Interactor** can be tested by using Spy test doubler for the **Presenter** and the **Presenter** can
be tested by sending the commands over the **Presenter** interface calls and validating the **ViewModel**.
The only thing that can not be tested with automated unit tests is the GUI, that is why it is made as small
as possible. Never the less the GUI is still tested, by using testers eyes. This turns out to be simple
because the **ViewModel** for each GUI can be prepared and than sent to the GUI to render. The verification
can be done by an engineer to see if the display is correct. There are tools for automating GUI testing
but writing those tests are impractical because the GUI tends to change a lot so the automated GUI tests
would also need to be changed a lot.

Testing the GUI inputs follows the same rules: we try to make the GUI part as small as possible.
A **GUI framework** that is located on the architectural boundary that can be whatever framework available
for the technology in use (i.e.: web container, [Swing](https://en.wikipedia.org/wiki/Swing_(Java)),
[Processing](https://processing.org/)). The **GUI framework** communicates with a **Controller** using
a **EventHandler** interface. The purpose of the **EventHandler** interface is to ensure that
the **Controller** doesn't depend on the **GUI framework**. The **Controller** collects the necessary events
from the **GUI framework** in a clean data structure conveniently called **RequestModel**. When the
**RequestModel** has been created, the **Controller** sends it to the **InputBoundary** interface.
The **Interactor** implements the **InputBoundary** interface. Testing the **Interactor** is easily, simply
create the **RequestModel** data structure filed with data to be tested and send to **Interactor**.
The **Controller** is easy to test as well, we call the **EventHandler** interface functions and check
if the correct **RequestModel** is created.

### 4.3 Test patterns

Not all test patterns are going to be covered here, only the ones most useful as per Uncle Bob will
are mentioned. The more complete list of test patterns are covered by dedicated books:
[*xUnit Test Patterns*](202.1.0010-xunit-test-patterns.md),
[*Junit Recipes*](https://www.manning.com/books/junit-recipes).

#### 4.3.1 Test subclass

This pattern is primarily used for safety reasons. For example if you want to test the method *align* of
class *XRay*. But the method *align* calls the method *turnOn*. You don't want the XRay to start whenever
you run test. So the solution is to create an test subclass for testing the *XRay* class. This test subclass
overrides the *turOn* method so it does nothing. The test code would create the test subclass instance, in
this example *SafeXRay*, and calls *align* method without worrying that the XRay would really turn on.
This is shown by Uncle Bobs picture below:

![Test subclass](assets/202.1.0002/4-3-1-test-subclass.png)

It is useful to make test subclass a Spy test doubler so it can track if what methods have been called
and how many times. In case *SafeXRay* was a spy the *turnOn* method would track its calls and the
**XRayTest** can verify the call count. Sometimes the test subclass pattern is used for convenience
and execution speed.

#### 4.3.2 Self-Shunt pattern

A slightly modified version of the Test subclass pattern is the pattern for self-start Self-Shunt pattern.
The class for testing becomes a test subclass. Example is shown with Uncle Bob's picture.

![Self-Shunt test pattern](assets/202.1.0002/4-3-2-self-shunt.png)

Good for cases where we need a simple Spy test double or simple safety. Downside is that test code and the
object that is part of a pattern and code can be hard to read. Use of this pattern depends on the language
used and the development environment.

#### 4.3.3 Humble object

It would be great if every part of the system production code can be tested using the three laws of TDD,
but that is not always the case. The parts of code that communicate over the hardware boundary are very
hard to test. Example for this are: testing what is displayed on the screen, testing what is sent over
network, testing what is sent over parallel or serial I/O. Without specialized hardware that can interact
with test this is impossible. Specialized hardware could be created but it can introduce separate issues
and they can slow down the testing.

The Humble object is a compromise solution. This pattern verifies that a code exists that can be
practically tested. The purpose of the Humble object is to degrade the problematic code to the point that
is to simple to test. Part of this approach was shown in GUI input testing in [Testing GUI](#42-testing-gui)
section. The general strategy is shown by Uncle Bob picture.

![Humble object general strategy](assets/202.1.0002/4-3-3-humble-object.png)

The point is that the Humble object should work with the **Presentation** data structure, which should be
as simple as possible, and use it to do the necessary operations using the interface from across the
hardware boundary. For the detailed example reference the book at page 157.

### 4.4 Test design
Designing test code is as important as designing production code. There are several problems that can arise
because of neglecting test code design.

The issue is the already familiar problem: brittle tests. This a common headache for TDD newcomers.
A test is brittle if a smaller change in production code causes leads to errors in many tests.
The problem is bigger when a small change in production code leads to more tests to fail.
Brittleness is a common disease in software design, if a small change in one module cause change in
other modules that means we have a problem with design.

The first practice that causes bad test code design is creating and maintaining the ono-to-one mapping
between test module and production module. TDD apprentices make a mistake to think that every class,
structure or module need to have a corresponding test class or test module. This coupling unfortunately
creates a structural tie between test code and production code. This leads to brittle tests. The heuristic
ule *12. Separate the structure of test code from the production code* teaches us to make this decoupling.

To decouple this dependency between test code and production code the test module design needs to be
approached the same way as we approach module design in production code. This is done, you guessed it,
by using interfaces. If we have multiple modules that module **A** depends on than all of the implementation
details are hidden behind module **A**. Module **A** serves as an interface to the family od dependencies.
A **ATest** test module interacts only with the module **A**, without knowing any of the module
**A** dependencies. We effectively test only the functionalities exposed in the interface. If it is important
it should be in the interface and it will be tested, if it is not it should not be and it will not be tested.

Example of test design in the book is a Move store implementation starting from page 164.

A word regarding specifics and generic. As mentioned by the heuristic rule *13. As the tests become specific,*
*the code becomes generic*. As the production code grows, the test code will grow as well. But their growth
happens in different directions, production code grows to be generic and tests code grows to be specific.
This happens because of TDD and refactoring. We add test code that we enable to pass by adding small and
simple production code, after the test passes we refactor. As we add more test the test code becomes specific
and the production code, after refactoring, gets more generic.

Important thing to note is that the dependency between test code and production code will always exist.
There will always be changes to production code that will cause changes in test code. The point of good design
is to minimize those changes.

### 4.5 Conditions for priority transformations

As it was mentioned before the test code becomes specific and the production code becomes more generic through
TDD and refactoring. What transformation should be done in the refactoring step and in which order is a different
problem. These transformations are small changes in production code that that change the code and make it more generic.
These transformations are:
- **{} -> Null**: The first transformation that is utilized in the beginning of TDD. We start without code `{}`,
and we write the most degraded test that we can thing of. Than, to enable this test to compile and fail, we make
the function return `Null` (or whatever is the most degraded form in working language) in production code.
We turn nothing into something that returns nothing. This rarely makes the test pass, so we continue.
- **Null -> Constant**: The `Null` is replaced with a constant, it can be a primitive or any data type creation
without assignment.
- **Constant -> Variable**: Previously added `Constant` is replaced with a variable with good name.
- **Unconditional -> Choice**: This transformation adds `if` or equivalent operator. The programmer needs to
make sure that the predicate in the choice command is not specific for the current failing test.
- **Value -> List**: This transformation changes a variable that holds one value to a variable that holds
an collection.
- **Statement -> Recursion**: This transformation changes a statement to a recursion statement instead of
iteration statement. This is applicable only in languages that support recursion but also keep in mind the
limitations of your system.
- **Choice -> Iteration**: We made the observation that `if` is a degraded for of `while`. So this
transformation generalizes choice in iteration where needed.
- **Value -> Value change**: This transformation changes the value of a variable.

The transformations are listed in the order of priority Uncle Bob believes is correct. The order and priority is not
set in stone but is a good guide line, if we believe we can combine multiple transformations in one for one test this
could mean we should split the test intu multiple tets.

Examples of this transformation are shown additionally from page 191. Where we extract the second last heuristic rule
from using transformations and it is: *14. If transformation leads to an suboptimal solution tryout a different one*.

## 5 Refactoring

*Refactoring* is the practice of improving the structure of the code without changing its behavior.
This behavior is defined by the test cases, which must still pass after the code has been refactored.

The practice of Refactoring is strongly coupled to the practice of TDD. A good test suite is
required so that the code can be refactored fearlessly. The third rule of TDD states that one
must not write more production code than needed in order to pass the test. Improving that
very code, however, is allowed—and strongly encouraged.

The refactoring could lead us to the debugger but if we do it in the short cycles, even if we end up
needing the debugger it won't be so awful because the issues was introduced with few lines of code but
still *15. Avoid the use of the debugger*. There probably will be a need for bigger refactors,
the architectural design will need updating, etc. Never plan refactors, never stop adding functionalities
and fixing bugs. Simply give more effort to do the necessary refactor when doing the normally development
activities.

Good set of refactoring tools (actions) that are a great starter and should be used always,
these are most likely supported by your IDE:
- **Rename**: Naming is hard, and finding the right name might take several iterations but don't be
afraid to change the name. Try to do it in the beginning of the project
because as the project matures it is harder to change some names.
*Domain-Driven Design: Tackling Complexity in the Heart of Software* is mentioning how to pick
good names.
- **Extract Method**: Might be the most important refactoring step. This step has two goals,
first goal is that every function has to do one task, and the second goal is that the function
should be easily read like a good novel. Don't let the idea of numerous small functions worries
you, it shouldn't because this will make your code easy to read and clear. Also rule of thumb
for naming functions is that the length of function name is reverse proportional to scope that
uses the function. Public functions should be short, and private functions should be long.
- **Extract Variables**: Sidekick to the extract method refactoring step. It is often required
to extract variables before extracting methods. The most noticeable purpose is to create clear
intent of what is happening.
- **Extract Field**: This refactoring step is not used often but when it is it substantially
improves the code. It is used when extract method doesn't fit the job. We extract local
variables to the class attributes so methods can have one task and simple parameter list.

Disciplines to follow to enable safe and easy refactoring:
- **Tests**: Without tests we can not safely and confidently refactor code
- **Fast Tests**: Not only that we need tests they also have to be fast. The speed
requirement is necessary because refactoring should go smoothly because is a integral
part of adding features or fixing bugs. So if tests take more than seconds to execute
it will prolonge the development.
- **Intercept the one-to-one dependency**: To be able to execute the test fast and to
execute a subset of tests we need to remove the one-to-one dependency between test code
and production code. The other reason why one-to-one dependencies are dangerous is that
they lead to brittle tests.
- **Continuous refactoring**: Never wait for a time to do the refactoring, refactor
always as you go. When you cook you should clean the dishes in parallel, you will
be finished quicker in the end.
- **Ruthless refactoring**: Inspired by Kent Beck. Never be afraid to try out thing
while refactoring for the benefit of reaching good architecture.
- **Let the tests pass**: There will be a time when you will need to change the
production code structure because of new feature or because of new insights on
how to structure the code better. Never stray from the refactoring attempt but
never let the test fail more than the refactoring cycle requires it.
If the refactoring requires days, decompose it to smaller steps so the test
pass while you do it.


## 6 Simple Design

The practice of *Simple Design* aims to write only the code required, and its structure being as
simple, small, and expressive as possible. Kent Beck has four rules to achieve this goal:

1. **Pass all the tests**. The code must work as intended, of course.
2. **Reveal the intent**. The code must be expressive, i.e. easy to read and self-descriptive. Split-
ting up code into smaller units and applying cosmetic refactoring helps in this respect.
3. **Remove duplication**. The code should not say the same thing more than once. Grouping
common code into new functions and calling them from that code’s original place is a
simple way to do this. Other situations require more sophisticated solutions, such as the
Strategy or the Decorator design patterns.
4. **Decrease elements**. The code must be freed from any superfluous structural elements like
classes, functions, variables, etc.

Complex design puts the programmer under high cognitive load—the *Design Weight*. A system with a
high Design Weight takes more effort to understand and to manipulate. Likewise,
requirements with high complexity make it harder to understand and manipulate the system.

However, a more elaborate design can help to handle more complex requirements, so a tradeoff
between complexity in requirements and appropriate design must be found in order to achieve
the goal of simple design.

Extreme programming adopted the idea of YAGNI (You Ain't Gonna Need It). Before the 90s the
process of building the software tended to be slow. It took hours to build the source code.
So developers learned to put hooks for future changes to make the easier to do. After the
leap in technology this became redundant in the sense that building the code and testing it
was fast. So the YAGNI principle was if the cost of ont placing the hook was bearable, you
probably should not put the hook. If the cost of placing the hoot in the design, after years
were high but the chances of that hook being used were small, don't place it. The idea of YAGNI
was not to eliminate the efforts to think of the future and that we shouldn't care but that we
the cases where we should put hooks and prepare for future are reduced.

The other problem we face is the code coverage. The asymptomatic goal is to have 100% coverage,
because what else number actually makes sense. Now this should not be approach as if it is not
100% it is not good, but that we should strive to have it in the 90s range. Simple design helps
us with this because making the code simpler indirectly makes it easier to reach high coverage as well.

On the subject of duplicates, not all duplications are bad. There is such a thing as
*coincidental duplication*. This is when there are two parts of code that are similar, but they change
for different reasons. Those kind of duplications should not be removed because the knowledge is
not duplicated only the code is.

## 7 Pair Programming

The practice of *Pair Programming* or *Pairing* is the act of two programmers working together
on a single programming problem by sharing their keyboard and screen — physically by sitting
at the same desk, or virtually using screen sharing software.

Pairing is optional and intermittent: Some of the time you pair, then you program alone again.
Whether or not to pair is an individual and team decision — not the manager’s!

The two programmers can take on different roles when pairing: one is the driver with keyboard
and mouse, following the directions of the navigator, giving recommendations and hints. The
technique Ping-Pong consists of one programmer writing a test, and the other programmer
making it pass. Those roles can be switched frequently.

Pairing is neither mandated nor scheduled, but done spontaneously. Pairs are short-lived and
dissolve after a session of 30 minutes up to a full working day.

The ultimate goal of pairing is sharing knowledge. This is achieved especially if seniors pair up
with juniors. At first glance, pairing looks inefficient and costly: certainly, two programmers
behind a single screen and keyboard cannot write as much code as if they’d have their own
workstation. However, pairing not only distributes knowledge, it also reduces errors, improves
the design, and strengthens collaboration within the team. In general, managers like to see their
people collaborating and sharing knowledge, and won’t complain about pairing.

Pairing is not only useful for writing new, but also for reviewing existing code. It’s also not
strictly limited to two programmers, but called “mob programming” when done by three or
more individuals.

As with testing, refactoring, and designing, do not ask for permission to pair. This is the
programmer’s domain, and the programmer is the expert.

To sum up:

The technical practices introduced in the chapter are at the very core of Agile. With
Agile, it’s possible to make a big mess in a hurry, if you ignore these technical practices.

## 8 Acceptance Tests

Software engineers have don't have as much impact on acceptance tests, because business needs
to be involved. Acceptance tets should provide the answer if the software is ready for deployment.
The QA testing disciplines recognize that test that the QA team do are the definition of the system
behavior regardless what is written in the software documentation.

The acceptance tests should be written by the BA (business analysts) and QA (quality assurance) teams,
one functionality at a time, before the functionality is implemented. QA and BA teams are not responsible
for the execution of the acceptance tests, that part is on the software engineers, who will most likely
automate those tasks.

Since the BA and QA teams write the tests, software engineers need to show to those teams that the tests
are automatically executed. So the language in which the tests are automated needs to be in the language
BA and QA teams understand, mending BA and QA should be able to write the tests in the language used for
automatization. It is recommended that the format of acceptance tests can be in either AAA or GWT format.
There are few languages designed to help this problem:[FitNesse](https://fitnesse.org/),
[JBehave](https://jbehave.org/), [SpecFlow](https://specflow.org/), [Cucumber](https://cucumber.io/), etc.

The writing of acceptance test should be approached with the discipline that the happy path is written by
the BA team, whereas the QA team focuses on exploring countless of ways the system can fail. The acceptance
test are written in the same time or prior to writing the implementation for the functionality. In agile
development approach this tests are written in the beginning of the iteration.

Acceptance test become the *definition of done* for software engineers. The functionality is not complete
until all acceptance tets successfully pass.

When the acceptance tests are properly written and the implementation passes them they are incorporated
int the suit of tests executed during *Continuous build*. This process starts every time a programmer
wants to integrate changes they made to the main repository. The *Continuous build* than builds the source
code and runs unit tests, and acceptance test automatically. If everything finishes successfully the
changes made by the programmer are eligible for integration with the main repository.

## 9 Productivity

This section covers the expectations a great technical director would have for his employees in the
aspect of productivity. The expectations are:

- **We will never deliver s\*\*t**: Our priority will always be on good design, complete tests,
refactoring, etc. We will not be pushed to deliver software that is not ready to be delivered.
We will setup processes so we have testability handled in the fastest and best possible way.
- **Cheap adaptability**: Software should be the malleable part of technology. We need to use the
disciplines learned in this book to get the software in a state that changes are chap to make.
It is expected that the software engineering team will be able to respond to change with a strategy
whose cost will be proportional to the scope of the change.
- **We will always be ready**: It is expected that software will be ready depending on the development
methodology used. Using agile that would mean that every iteration the software will be technically ready
for release. Technically ready for release doesn't mean that business will want to release it but that
it is able to release it.
- **Stable productivity**: The development teams productivity will not fluctuate over longer period of
time. This is dependent on the software disciplines that were utilized. If we follow TDD and refactor,
automate builds and releases, share knowledge our productivity will not greatly fluctuate.

## 10 Quality

This section covers the expectations a great technical director would have for his employees in the
aspect of quality. The expectations are:

- **Continuous improvement**: It is expected that over time design and architecture of our systems
will improve. Every week our software should be cleaner and more flexible, the cost of change should
decrease, quality will improve.
- **Undeterred competence**: We will not allow our system to degrade and leave the development team
helpless and controlled by the system. Instead we will be disciplined in the art of software development
and keep the system under control.
- **Exceptional quality**: It is expected that we give our all to eliminate bugs in our system.
- That we follow the disciplines to the maximum and don't allow our self to accept that errors are
- inevitable and a part of software. This is not only related to functionality but also to structure.
- **We won't overload QA**: We will not allow to give software to QA without giving our all to test
everything. The goal of software engineering team must be to do everything possible to remove all bugs
and give a bug-less software to QA. We should not accept that the success in QA team is in the bugs that find.
- **QA will not find anything**: This speaks for it self. Software engineering team will do what
QA would do to ensure they will not find bugs.
- **Automated tests**: As soon as the test are working when run by hand and are validated that
they are valid tests we automate them.
- **Automated tests and GUI testing**: Automated test do not test business rules in GUI.
It was stated that we must design software so GUI is so basic that it is not tested at all.

## 11 Courage

This section covers the expectations a great technical director would have for his employees in the
aspect of courage. The expectations are:

- **Mutual support**: We must share knowledge so we in case of emergency we can stand up for teammates
that have to handle some unexpected events. Just as the marines handle the work on boat. It is every
developers responsibility to make sure that someone can replace him if needed. We must make sure that
we are replaceable. The best way to do this is pair programming, wise approach would be to do it with
more team members.
- **You have to be able to say NO**: Most important rule that when you did you research that you say no
when the request will cause the company more damage than do more good. Never be disrespectful but stand
your ground. They will often threaten or say that you must give more, don't fall for that. You must give
your all before talking to the manager so he has no leverage. Prepare facts for all possible cases and
never ever scarify quality.
- **Continuous aggressive learning**: Learn as much as you can, but take notes because the knowledge will
fail. So don't waist your time by just reading because you will forget.
- **Mentorship**: Make sure to find a good mentor. If you can't learn to learn from everybody. Take feedback
separate the who and the how and only focus on what. Take notes for your profession because it is mandatory
for being a good mentor.

## 12 Damage

The parts of the programmer's oath that prevents damage:

01.  **I will not produce harmful code.**: Do not allow your work to harm your users, employers, colleagues,
environment. You must not harm the functionality of your code, you must know what your code does and
if it is clean. You must not harm the structure of your code. More about that from Uncle Bob from page 296.
02.  **The code I produce will always be my best work. I will not purposefully allow**
**accumulation of code that has defects in functionality and structure.**: Leave behind you code that works,
is clean and maintainable, has test. Remember: first make it work, than make it right. Developer job is not
than when the code works, it does not it never ends and you need to make sure it not only works but is clean
and testable. Nurture both values of software: functionality and structure. Follow the good practices of simple
design. When faced with urgent tasks, never sacrifice quality and always follow
the [Eisenhower Matrix](https://corporatefinanceinstitute.com/resources/management/eisenhower-matrix/). One key
aspect to think about is that developers are stakeholders in your system development they have use of the system as well.
Because of the mentioned things above, programmers are stakeholders and structure is more important than functionality,
you need to stand for that in front of management who do not, and don't have to, understand the engineering practices,
that is your job.
03.  **In every version I will create a fast, safe and reproducible proof that every**
**element of code works as expected.**: Although Dijkstra's vision to have mathematical proof that a program works
might not be pragmatic today, the closest thing we have to that are tests. The TDD and refactoring cycle is a
functional decomposition. Dijkstra did say that we can not prove that the program works we can only that the
program doesn't work. Dijkstra tried to view at software as a for of mathematics, while we should look at it
as a for of separate science. So we will have tests that we can execute fast and multiple times to provide
evidence that the software works on that scope of tests.

## 13 Integrity

The parts of the programmer's oath that ensures integrity:

04. **I will create periodic and small versions that will not interrupt the work of others.**:
As the technologies grew the process and period between changes in software was shortened drastically,
for the history of source control see the book from page 328. As the CVS systems came to existence
the cycles between getting the software module, making a change and integrating it back to the main
repository. In order to push code to main repository we have two approaches, create toggles in code or
create branches for unfinished code. The branch approach means you will have a separate branch that will
last until the feature is done. You can run test on the branch and incorporate the changes on main to
your branch so integration to main goes smoothly. This is ok in todays age because git offers
methods to make it non-disturbing to others. The other approach is to make a implementation that will not
be finished and it will be deactivated with toggles and pushed to main branch as soon as possible.
The implementation is then worked on step by step and the dummy code is replaced by real code. The feature
is turned on only when all dummy code is replaced with working functionality.
This needs to be tied with continuous integration that will incorporate the changes,
validated by running tests, into the main repository. This is necessary to the other can work
undisturbed with the newest possible code. It needs to be short so the integration is simple.
Continuous integration is tied with continuous build and continuous deployment.
05. **I will rigorously and fearlessly improve my creations in every opportunity. I will**
**never degrade them.**: We should strive to continuously improve and refactor production code.
We should measure the coverage and use that information to improve the production code, it should
not be used as a report for the management. Also we should improve our test both in structure
and validity. One approach of verifying our tests is to use *Test mutation*. Test mutation is a
method of verifying the test by changing the production code and checking if the test will fail.
If it doesn't that means the test has a bug and needs fixing.
06. **I will do everything I can that my productivity and the productivity of others is as**
**high as possible. I will never do anything that will decrease productivity.**:
We should improve the workflow to be effective, decrease our distractions and manage our time efficiently.
When talking about workflow improvement it is tied to the software build, testing, debugging and deploy procedure.
The build should be optimized, so it doesn't take half an hour to build for a five minutes of editing. We should not
look for excuses why this is like that but find solutions to speed it up. Test should also not slow down our build.
We should do necessary steps to make tests execute faster. This should be achieved by modifying the design of test
so we don't automatically test GUI or use real databases, network connections in tests. IF we follow the disciplines
we learned in this book debugging is most likely minimized. Deployment must be automated even if hardware is involved.
Do not deploy manually. Regarding distractions (meetings, music, bad mood, ultra focus) try to avoid them or solve
them and don't be one. As for managing time look into [Pomodore technique](https://en.wikipedia.org/wiki/Pomodoro_Technique)

## 14 Teamwork

The parts of the programmer's oath that promotes integrity:

07. **I will always make sure that others can replace me and that I can replace others.**:
Never keep knowledge in silos, distribute it as much as possible. Spread knowledge by working in pairs or in a group.
An additional factor is the social factor, the development team should interact with each other. If the remote work is
a thing than organizing virtual offices with long lasting calls with remote workers or other tools.
08. **I will create estimates that are honest by size and accuracy. I will not make promises**
**in which I am not certain.**: The only honest correct estimate in software development is: **"I don't know"**. This
now needs to be modified to remain true but be usable. That is why you never give dates but give estimations, i.e. Trivariate
estimation.
09. **I will respect my colleagues because of their ethics, standards, disciplines and skills.**:
**No other characteristic or attribute will be a factor in my relation towards my software engineering**
**colleagues.**: Self explanatory, nothing matters.
10. **I will never stop learning and perfecting my craft.**: Always learn, and don't rely on anyone to provide the means for you
to lear, not even from your employer. If the company provides educations use it definitely.
