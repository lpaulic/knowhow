# [Clean Architecture: A Craftsman's Guide to Softwar Structure and Design](https://www.amazon.com/Clean-Architecture-Craftsmans-Software-Structure/dp/0134494164)

![Clean Architecture: A Craftsman's Guide to Softwar Structure and Design](https://m.media-amazon.com/images/I/71stxGw9JgL._SL1500_.jpg "Clean Architecture: A Craftsman's Guide to Softwar Structure and Design")

## Details
- Author: Robert C. Martin
- Rented to: No

## Quotes

> *"Only way to go fast, is to go well."* -- Uncle Bob

## Key takeaways

In aspect of software develpoment architecture and design are the same thing.
Usually there is a sense that architecture deals with high-level, and that 
design deals with more detailed level. But in reality a good architect 
defines both high level all the way to the detials.

Goal of software architecture is: **minimize human resoruces necessary to 
make and maintain the desired system**

The unit of the quality of the software design is: **effort needed to 
satisfy needs of the customer**

If the effort remains low and consistantly low through time (more 
and more requests) the system has good design.

A way to measure for a companyt:
- graph that shows Year/Software Engineers
- graph that shows Year/Product size (KLOC), where LOC is lines of code
- graph that shows Year/Product cost (LOC), where LOC is lines of code
- graph that shows Version/Productivity, where producitvity are features
- graph that shows Year/Monthly pay, that will get through to management

Biggest lie in programmers life: **Bad code helps us get quicker to the
market**. Where in reality in the long run makes you slower and less 
reliable.

Be wary of the approach from starting from scratch, it can lead similar
mess from where you started.

## Two values in software engineering

Behaviour (functionality) and strucutre (architecture) are the main two values 
of a system. The software engineer is required to fulfill both.

Behaviour is the thing that software must do that the user 
of the system wants it to do. It needs to be done well and reliable.

The other value, often neglected, is structure. The basis of software 
is that is 'soft', meaning easy to change. It needs to be easlity
addapted to the everchaning needs.

What is more valuable: Behaviour or Structure? Depends who you ask, most would
argue that behaviour is more important, but that is short term thinking.
If you do an extreme test:
- If a program that is working but it can't be changed, when required 
behaviour changes the program will not be able to change and you end up 
with a usless program.
- If you give me a program that doesn't work but it can be changed, that 
it can be changed to work, and addapted when behaviour requirements change.

When we talk about impossible to change, we mean that the cost of change is 
to high to make it worth it.
So structure appears to be more important.

Most important: No manager will let you focus on structure more than behaviour
but down' the line you will be crisified if that system can not be changed. 
So it is a programmers duty to make sure that structure is ensured.

D.D. Eisenhower matrix perfectly describes the relation of behaviour and function.
Eisenhower matrix: *Two types of problems, urgent and important. 
Urgent are not important, and important are never urgent.*

Behavior => urgent : always but never actually important.
Structure => important : but never urgent.

So the matrix, and the priority order is:
1. Urgent and important
2. Not urgent, but important
3. Urgent, but not important 
4. Not urgent and not important

## Programming paradigms

Paradigm in programming is a way of programming not tied to a specific 
programming language. Paradigms in programming:
- Structural programming
- Objective oriented programming
- Functional programming

All of the paradigms are order in such a way that it shows how each paradigm
puts additional enforcements and removes something, but they
never give something more.

### Structural programming
Widely used, but not the first one inveted. Proposed by Edsger Wybe Dijkstra
in 1968. Dijkstra pointed out that wide use of `goto` is harmfull for the 
prgram structure, so he proposed to use alternatives such as: `if/then/else`,
or `do/while/until`

**Structural programming enforces a constraint to direct transfer of control.**

### OOP
Discovered in 1966, two years prior to structural paradigm. Inveted by 
Ole Johan Dahl and Christan Nygaard. They noticed that in ALGOL language 
te stack frame could be transfered on the heap, enabeling local changes inside 
te funcion to persist after the funciton exits. As a result a function became 
class constructor, local changes became instance changes, and nested functions 
became methods.

**OOP enforces a constraint to indirect tranfer of control.**

### Functional programming
Discovered first, predates the invention of a program. It is an result of 
the works of Alonzo Church, who fount the lambda expression in 1936. working 
on the same mathematical problem. The lambda expression is the root of 
the LISP programming language. The basic concept is that the lambda expression 
is not changeable, there is no assignment.

**Functional programming enforces a contraint on assignemnt.**

## Principles of design

Good desing principles are based on [SOLID](https://en.wikipedia.org/wiki/SOLID):
- S: SRP (Single Responsibility Principle)
- O: OCP (Open-Closed Principle)
- L: LSP (Lisk Substitution Principle)
- I: ISP (Inteface Segregation Principle)
- D: DIP (Dependency Inversion Principle)

SOLID principles define how to combine functions and data structures 
in "classes" and how to combine those "classes" with eachother. The 
term "class" doesn't necessary meand the OOP class, it simply refers 
to something that is used to group functions and data structures.
Other terms: modules (structural programming).

The goal of SOLID principles is to crate software strucutres of mid level that:
- tolerate change,
- easy to understand,
- baseis for components that can be used in other software systems.

SOLID is not enough to ensure a good system, it will ensure that 
the building bloks are good but not what is done with those building blocks.
For that other principles on higher level need to be used. ?????


### SRP

Dos NOT mean that a module should only do (be responsible for) one thing.
The better definition is:
` Modul should be repsonsible to one and only one actor.`

Actors can be one or a group o people or interested parites that want the same 
change. This doesn't meand that every module shold be directly linked 
to and outside actor, but the actor can be another module that is part 
of the system.

SRP goal of a module is:
If multiple modules use a module, any change to that module should still make 
sense and be relevant to all of them—because they rely on the same 
responsibility.

Deals with functions and "classes" but comes in defferent forms on two other 
levels:
- CCP (Common-Closure Principle) - komponent level
- Axis of change - architecture level 

### OCP

`Softer artifact has to be open for extension, but closed for modification`

In human terms, a component should be extended with new behavior without 
modifying the current behaviour. Can be applied on class and module level 
but is most important on component level.

All component relations should be in one direction on a component diagram

The "closed" means that the other funcions, modules, classes are NOT aware 
that the change happened and should not be changed, retested. It also 
means the the existing code should not be modified to add new functionality.

### LSP

`If for every object O1 of type S, there is an object O2 of type T, such 
that for every program P defined in terms of T, the behaviour of P stays the 
same if O1 is replaced by O2, than S is a subtyp of T`

On architecture level it is important in terms to define the interfaces
correctly based on the classes and what wants to be acheived. It ties to the 
OCP and SRP.

### ISP 

Goald of this principle is to add interfaces that only have dependecies used 
by a module, the implementor of the interface might have other functionalities.
The goal is that the user of the interface is not affected if the implementor
changes things that the user is not using. Not using ISP might lead to 
unnecessary depenencies.

### DIP

Enables a system to be flexible by ensuring that the dependecies are made 
on abstractions and not on concrete implementations. Goes along with the ISP. 

Some things can not be abstracted, standard types in a probramming language,
but even they can be hidden begind policies. Most important is to avoid 
dependencies on variable elements of the system, modules that are activly 
developed on and prone to change.

Interfaces are less prone to change than implementations.

It is imposible to not violate the DIP principle but the goal is to localse
it and isolate from the rest. The usual approach is to have glue code 
(tipicall main or something similar) that instatiates tha concrete 
implementation and assigns it to a variable with the abstracted interface type.

## Organizing components

SOLID -> how to build walls for rooms
Organzing components -> how to arrange rooms in a building

Components are units of arrangement. The smallest entitites that can be 
applied as part of the system. In compile languages they are binaries
: .jar, .dll.

Good designed components retain the possibility to be independently 
arranged and developed independently.

This originates from the days where programs where loaded on 
a fixed location. In that time compiling took much longer, so engineers 
separeted the functions and applications to separate locations. 
This wasn't scaleable becasue the compiler generated fix address locations 
so if the functions or applications grew the compiler had to be 
instructed to split application to different locations.

To solve that issues loaders were introduced, they enabled that the compiler 
genereates code with relative addresses so it can be loaded anywhere, 
and the loader would than put it on exact location.
Than compilers where updated to enable assiging names to the addresses.
As programs grew loaders became to slow to connect the function names 
to exact memories and than load them. That is why they were split 
into loaders and linkers. The slow part, linking, was separated so 
the output was a binary where the functions were linked to the 
relative addresses and the loader than had to just load it into memory.

### Principles

Principles when organizing components RCC:
- R: REP (Reuse/Release Equivalence Principle)
- C: CCP (Common Closure Principle)
- C: CRP (Common Reuse Principle)

REP defines that the unit of reuse is the unit of version. This goes in 
todays age with the SCM tools, like git or svn. The goal is that the 
component has classes and modules that are work together and are 
related to eachother by some criteria, often the purpose of the 
whole component. It is hard to point the rules to enforce this 
but it is easy to see when it is violated. Some parts of the 
componente never change or want to change unrelated to the rest.
This rule is enforect by CCP anr CRP.

CCP defines that the component should hold the classes that change for the 
same reasons and in the same time. Separate other components in that change 
for different reasons in different times. Important in development becase 
the change is localized on one component only, other components will not change 
so validation is not necessary for other comonents but the ones tha truly
need to change. This principle is tight to SRP and OCP principle on class level.
Full closuer is imposible, so we focus on strategic closure, we design classes 
to be closed for most common reasons to change that we expect or experienced.
Group classes that are closed to the same rason for change in the same compoent.

CRP defines that users of a component should not be forced to depend on things 
that they don't need to use. This principle guides us to see what classes or 
modules need to be in the same component. Classes that work with other clases 
should be in the same module. When we depend on a component we have to 
depend on all (close to all) classes of that component. Classes in a component 
have to be inseparable, othervise we need to split the component further. The 
CRP is linked to ISP on class level. ISP states that no dependecy should 
be crated on a class whose methods are not used, CRP states that no component 
should be dependent on if there are unused classes.

[Cohesion principle tension graph](https://medium.com/@mammimia/clean-architecture-part-iv-component-principles-89d3cb58c195)

### Making connections between components

There are three principles to follow when connection components ASS:
- A: ADP (Acyclic Dependency Principle) 
- S: SDP (Stable Dependency Principle)
- S: SAP (Stable Abstraction Principle)

Violating the ADP causes the "Morning After" syndrome. You go home after a good 
days work where everything is work, only to return the day after and nothing is
working because someone else modified something that your code depends on.
A good test to see if ADP is violated is to go throug the component graph, if 
you can not get to the starting component by trafersing the depenencies and 
that is true for each component than ADP is satisfied.
A dependency cycle can always be broken:
1. Use the DIP principle.
2. Create a new component that the compoentns that crated the cycle depend on,
pull calls(es) in that component that are dependencies on the compenents that 
crated a cycle.

Other approach is known as the "Jitter", where the changin requirements will 
affect the depenencies so there is a need for constant checks.

Important the components DO NOT have to represent system functionailities directly.
The purpose is to ensure good structure not behaviour. Creating components comes 
AFTER creating classes and modules. Why, because if we start with components 
most definitely we will do a bad job, because we don't know what should be grouped,
we don't konw what can be reused and most likely we will create cyclic dependencies.
