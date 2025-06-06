---
layout: default
title: Pragmatic Programmer 
parent: Software Development Methodologies
nav_order: 3
---

# [TitleThe Pragmatic Programmer: Your Journey To Mastery](https://www.amazon.com/Pragmatic-Programmer-journey-mastery-Anniversary/dp/0135957052)
{: .no_toc }

![The Pragmatic Programmer: Your Journey To Mastery cover](https://m.media-amazon.com/images/I/71f743sOPoL._SL1500_.jpg "The Pragmatic Programmer: Your Journey To Mastery cover")

## Details
- Author: Andrew Hunt, David Thomas
- Rented to: No

## Key takeaways
- What makes a *Pragmatic Programmer*:
  - **Early adopter/fast adopter**: Love trying out new things. New things are grasped
  quickly and integrated with the rest of your knowledge. Your confidence is born
  of experience.
  - **Inquisitive**: Tend to ask questions, you want to know the little facts that may
  affect some decision years from now.
  - **Critical thinker**: Don't think about things without the facts first. You smell
  trouble when someone gives empty promises.
  - **Realistic**: Want to understand the underlying nature of a problem
  - **Jack of all trades**: Broaden knowledge alongside specialization.
  - **Care about your craft**: Nurture your craft.
  - **Think about your work**: Do not run on autopilot, think always.
- If you take [responsibility](#12-cat-ate-my-source-code) you only than you are accountable.
- When handling [technical dept](#13-software-entropy), tell yourself: "No broken windows".
- When you know what needs to be done and how to do it, use [the stones](#14-stone-soup-and-boiled-frogs)
- Use the system requirements to know [when to stop](#15-good-enough-software)

## Quotes

> *"I'm not in this world to live up to your expectations and*
> *you're not in this world to live up to mine"* -- Bruce Lee

> *"Striving to better, oft we mar what's well." -- Shakespeare King Lear 1.4*

## Summary

## 1 A Pragmatic Philosophy


Being a pragmatic programmer is displaying an attitude, a style, a philosophy of
approaching problems and their solution. Thinking about a problem placing it
in the grander context of things, the big picture. Without the bit picture
informed decisions and intelligent compromises can not be made.

Another separation is that pragmatic programmers take responsibility for
everything they do, they will not stand by and watch a project fall apart.

Understanding the big picture helps understanding how good the software must be,
to look for trade-offs when perfections is unattainable. This of course requires
broad knowledge.

### 1.1 Your life

It is your life so you are in charge and you have control. You have agency in
software engineering profession most likely more than anywhere else, use it.
If your job is boring, try to fix it but not forever, as Martin Fowler says:
"... you can change your organization or change your organization". If you
are not learning things, don't wait for your employer to find time use our
own, it is your life in the end, you are responsible.

### 1.2 Cat ate my source code

In the software engineering profession one of the cornerstones of pragmatism is
to take responsibility for yourself, your actions in terms of career advancements,
your learning and education, your project, and your day-to-day work.

Trust from your team is the other tremendously important aspect. The team needs
to trust you and be able to rely on you and vice versa. Where there's trust, there
is honesty and loyalty.

Responsibility is a commitment that somethings is done right, even if you are
not directly controlling it. You must analyze the situation for the risks that
are out of your control. You have the right not to take responsibility for an
impossible situation, or one in which the risk is to grate, or the ethical
implications to sketchy. If you do accept than you are accountable for the
outcome. If you do make a mistake do not blame others, admit it review it
and offer solutions.

### 1.3 Software Entropy

In Physics *Entropy* refers to the amount of "disorder", and unfortunately the
laws of thermodynamics guarantee that the entropy tends to a maximum. Although
software is not govern by physic entropy is software is real. In software it is
also referred to as *"software rot"* or *"technical debt"*.

We as pragmatic programmers can not let the entropy spread. From many contributors
to software rot the most notable is routed in project psychology, or culture at work
on a project. The project psychology, even in team-of-one is a delicate thing and
even amongst well crafter processes and well behaved engineers a project can still
face ruin and decay in its lifetime. What makes the difference, according to the
[researches in the field of crime and urban decay](https://www.theatlantic.com/magazine/archive/1982/03/broken-windows/304465/),
a broken window. A broken window if not fixed in a certain period of time causes
a sense of abandonment in people, a sense if not dealt with causes neglect
where one broken window leads to two, littering, graffiti, etc. And soon
the building really is abandoned.

Why does that make a difference, scientists have done
[studies](https://pubmed.ncbi.nlm.nih.gov/7932064/) that show haplessness can be
contagious. So the conclusion is do not leave broken windows in code (bad design,
wrong decision, bugs, etc.). Even if it can not be fix because of time, patch
it up and leave a comment for refactor.

The most important thing is: do no harm. Anecdote where fireman went to
extinguish a fire in a immaculate house. After getting to the house and
assessing the situation, they put a carpet from the entrance to the fire
to not mess up the floor and existing carpet. Moral of the story don't
cause more harm than there is. Do not degrade existing code while trying
to fix something urgently (for a showcase, deadline, release date)
respect the current excellent state. The urgency is not worth degrading
a good code.

When handling urgent situations and software rot tell
yourself: "No broken windows".

### 1.4 Stone soup and boiled frogs

Story about soldiers coming to a war affected village, and start preparing a soup
from three stones. The villagers gather round and were amazed. They asked if that's
all that goes in the soup. The soldiers stated that additional ingredients would make
it better. After hearing that a missing ingredient the soup would be better a villager
ran to his house and brought the missing ingredient from his personal hoarded stash.
One by one villager asked the same question and the soldiers replied with a new
ingredient. Before you know it they had a soup with loads of ingredients. When the soup
was done the soldiers removed the stones.

The moral of the story is that although the soldiers tricked the villagers in the end
it was for everybody's benefit. Some times you need to be as the soldiers a catalyst.

In a situation you may know what needs to be done but asking permission to tackle the
whole thing you'll be met with delays and blank stares. Everybody will guard their
resources (boards will form, approval comities, etc.). Time for the stones. Work out
what you can reasonably ask for, develop it and present it. Make the people admire it.
Than plant the seed: "it would be better if ...". Pretend it is not important.
Be a catalyst for change.

From the villagers perspective the story is about gradual and gentle deception. We all
fall for it. The tightly focused point, and the rest of the world gets forgotten. In
software development it happens constantly, projects slowly and inexorably get totally
out of hand. Systems drift from their specifications feature by feature, while patch
after patch gets added until there is nothing left from the original. It is the
accumulation of small things that break morale and teams.
Always remember the big picture.

This is proved by the frog and boiling water experiment. If you put a live frog into
boiling water it will immediately jump out, because it is to hot all of a sudden.
On the other hand if you put a frog into cold water and start heating the pot, the
frog won't notice the gradual temperature increase and will boil to death.

### 1.5 Good enough software

There is an anecdote regarding a company that placed an odrer for 100,000 ICs. As the
parot of the specification the defect rate was defined: one chip in 10,000. A few weeks
later two boxes arrived, one large containing thousands of ICs and a small box containing
just ten. Attached to the small box was a note: "These are the faulty ones".

If only we could control the quality in such a way, but in the real world we can not.
However not all hope is lost. In the article [IEEE Software, When good-enough software is best](https://www.computer.org/csdl/magazine/so/1995/03/s3079/13rRUzpQPLU)
by Ed Yourdon. You can discipline yourself to write software that is good-enough --
good enough for your users, future maintainers, for your peace of mind. This leads
to more productive personal work, happier users and better programs. But what does it
mean "good enough" software. If definitely does not mean sloppy or poorly produced code.
All systems must meed their requirements, basic performance, privacy and security
standards. We simply want to include the user in the process of deciding when the
program is good-enough for their needs.

Sometimes there will be no options and the requirements will be strict and with
little to no deviations (pacemakers, an autopilot, low-level library). However
when working on something brand-new and the restrictions are going to be few.
But we have other limitations in those circumstances: marketing promises,
delivery schedule, cash-flow constraints. We will need to find compromises
with delivery speed and quality. Make quality a part of system requirements
during scope and quality discussions.

It is better to have a unpolished software today than a perfect software
tomorrow. This is an art to restrain yourself to stop when needed. As painters
would say: *"If you add to much details and layers, the painting becomes lost in the paint"*.

### 1.6 Your knowledge portfolio

### 1.7 Communicate
