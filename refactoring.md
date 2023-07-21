# Refactoring Code: An Incremental and Purpose Driven Approach

Speaker: Venkat Subramaniam

- [Refactoring Code: An Incremental and Purpose Driven Approach](#refactoring-code-an-incremental-and-purpose-driven-approach)
  - [What is Refactoring?](#what-is-refactoring)
  - [When Should We Refactor?](#when-should-we-refactor)
  - [When Should We Rewrite?](#when-should-we-rewrite)
  - [Code Smells](#code-smells)
  - [How To Refactor](#how-to-refactor)
    - [Steps](#steps)
  - [Refactoring Patterns](#refactoring-patterns)
  - [Code Quality](#code-quality)
  - [General Advice](#general-advice)
  - [Other Resources](#other-resources)
    - [Books](#books)
    - [Libraries](#libraries)

## What is Refactoring?

> "Make it work; make it better real soon"

- A genuine desire to the improve the quality and design of code
- It is the art of improving the internal design of existing code without changing it's external behavior
  - When we refactor, the code is not going to do anything different but it is going to do it differently
- It is really about the economic impact of the code
  - You want to reduce the cost, time, and effort to modify the code as we move forward
  - Try to convince yourself not to do it, and only do it if it will actually benefit you and your team
- It's not rewriting a codebase
  - Better to refactor in small pieces where possible
- It's not a stop the world approach
  - Shouldn't need a code freeze
- Impossible to make it right on the first write
  - Red-Green-Refactor

## When Should We Refactor?

- It's about discipline
- Before you fix a bug, after you fix a bug, but not in the middle of fixing it
- Before you make an enhancement, after you make an enhancement, but not in the middle of making it

## When Should We Rewrite?

> "Rewrite your own code, refactor other people's code"

- Risky and requires a large investment
- If it's a small part, rewrite
- If it's a large part, refactor

## Code Smells

> "Code smell is like body odor, you almost always sense that of others but not your own"

- Much like real smell, you get use to code smells after seeing them for a while
  - Code smell today, looks like a pattern tomorrow
- Dealing with existing code smells
  1. Don't propagate the smell
  2. Prototype another approach to determine if it is better
  3. Write new code in the better way
  4. Refactor old code over time when it makes the most sense
- Also need to think about design smells

## How To Refactor

> "The key is to have feedback loops, as fast as they can be"

- Refactoring should be very incremental
  - Commit as soon as a small refactoring step is completed with a passing test
  - Should be releasable between steps
  - Refactoring should be in a different commit than a bug fix or enhancement
- Do not confuse your inability with impossibility
  - Ask advice from others
  - Rubber ducking
- Have automated tests as a safety net before refactoring
  - Automated unit tests > automated integration tests > manual integration tests
  - Use/write the best you can
  - Make sure tests fail when you intentionally break the code

### Steps

1. Identify a smell
2. Analyze to see if that is useful ro refactor (don't assume)
3. If it is a candidate for refactoring, check if test exists
4. Write tests if there are none
5. Refactor in small steps
   1. Verify tests pass
   2. Commit the code
6. Repeat until refactoring is complete

## Refactoring Patterns

- Compose Method
  - Single Level of Abstraction Principle
    - Instructions in a function should all be at one level of detail or abstraction and delegate to other functions any details or abstractions at a lower level
  - Compose methods at one single level of abstraction
- Remove duplication
- Replace algorithm loop
  - Add redundant new code alongside old code to not break tests and code at the same time
- Remove redundancy

## Code Quality

> "The quality of code is inversely proportional to the time it takes to understand"

- Better quality leads to higher agility and lower development time
- Make technical debt visible and prioritize from most to least damaging
- Schedule time to pay and reduce technical debt
- Minimize risk by fixing technical debt sooner rather than later
  - People leave, products stay
  - People with context should be around to resolve technical debt
- Favor high cohesion and low, loose coupling
- Remove coupling or move it where possible
  - Knock it out before you mock it out
- Program to reveal intention
  - Good naming
  - Use constants instead of literals
- Prefer clear code over clever code
  - Simplicity
  - Clarity
  - Brevity
  - Humanity
- Comment the why not the what
  - Comments shouldn't be used to cover up bad code
  - Don't use comments when you can use better naming or extract descriptive methods
- Avoid long functions
- Use SLAP (Single Level of Abstraction Principle)
- Avoid single letter variable except for a few cases
- Make names domain specific
- Do continuous code reviews
  - Review tests first
  - Say what to do and why, as opposed to calling out what not to do
  - Give kudos
- Use automated tooling to gauge code health
- High code coverage (with a grain of salt)
  - Code with poor coverage indicates a design flaw or code smell
  - Don't increase coverage just to increase coverage, figure out why the coverage is low

## General Advice

- Whenever a test passes, however small the change, commit
  - Frequent commit lowers the cost of undo and increases the agility to innovate
- At any time either the code needs to change or the test need to change, but never both
  - With each change, ask how do you break the code or the tests but not both
- Make private constructors and write static factory methods
- If you want feedback, get frequent reviews; if you want a blessing, get infrequent reviews

## Other Resources

### Books

- [Refactoring Databases](http://www.amazon.com/gp/product/0321774515/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0321774515&linkCode=as2&tag=passionaboutd-20)
- [On Writing Well](https://www.amazon.com/Writing-Well-Classic-Guide-Nonfiction/dp/0060891548)

### Libraries

- [Radon: Python tool that computes code health](https://pypi.org/project/radon/)
