# Procedures & Best Practises

There are a number of procedures and best practises that apply to both frontend and backend, which can help 
improve your code quality and how you develop as a team, here are some of the best the team has picked up over 
the years.

## Boy Scouting

The boy scouting rule states that `you should always leave the campground cleaner than you found it`. This should be
adopted by all developers to help make sure that technical debt doesn't become a huge problem.

This means that all classes you make changes to when writing new features, should have a conscious effort made to
clean up any existing code and fix any technical debt within reason and scope of those classes. This includes changes
to the code to make it meet company standards not previously set and stamping out bugs.

All this ensures that whenever a new feature is worked on improvements to existing code always comes along with it and
technical debt does not mount up.

## Code SOLID

I wont explain solid here but the gist of it can generally be summed up by saying `be aware of seperation of concerns`,
read more about it here - https://en.wikipedia.org/wiki/SOLID

## Code DRY

Coding DRY means `Dont Reapeat Yourself`, which sometimes is harder said than done. This though can be accomplished
with the boy scouting practise which allows you to clean up code after it's done incrementally. So here you should be
abstracting and DRY'ing up code either as you go along and/or part of doing boy scouting.

## Throw Exceptions

Make sure that as you are writing code you are thinking about all possible edge cases that could happen which may not
be something that your code should handle and make sure to throw exceptions for it. By doing so these exceptions can be
caught at a later point and transformed into something more friendly for the user where if the application is an API for
example, this leaves the consumer of the API in a position where they are to handle it and avoid hitting that exception.
Effectively pushing that problem onto them and not you.

The more exceptions you throw on edge cases can also help in debugging too.

## Catch & Log

Particularly when making external requests consuming APIs or running jobs, make sure you are dropping in logs if an
exception is thrown. Should the company you work for have a plan wth a log management service such as Rollbar you will
be able to easily see these errors and be alerted of problems. This will make debugging much easier.

## Commit only working code

The git tree should be traversable back in time without the codebase running into fatal exceptions due to broken
features. When committing code, think about how you break up the commits, sometimes committing file by file or even chuck
by chunk to create a git tree that flows nicely. Should you need to commit broken code to allow a fellow developer to
help debug with you, prefix the commit with `WIP:`, `[WIP]`, or `WIP -` and once solved, swiftly commit again the solution
to that issue alone in a single commit. A WIP commit should only exist for a short period of time while the issue is solved.

## Aiming for high Code Coverage by testing all edge cases

All code created should have tests added where coverage is valuable. When creating an API, you will need integration tests for each
endpoint, including unit tests for the individual sections of code. When consuming APIs you will need to either stub
the API endpoints you're using or get hold of a sand boxing environment for that API which you can use in local.

You should be hitting as many edge cases in testing as possible both happy and unhappy paths. Your tests should be
structured in that 1 feature or unit is tested per file with multiple scenarios in the file as separate test methods.

For example, it is not recommended to have an `OrderTest` file which has multiple test scenarios that create, add, edit.
You should in fact have a `CreateOrderTest` which has multiple scenarios for creating a test correctly and incorrectly.

## Automate proceedures with CLI commands

When developing a new feature it is a good idea to add certain aspects of that feature as CLI commands. Sometimes you
may receive requests from the business to perform these tasks once the application is live, and you'll be pleased
you made those commands then.

## Pair coding

Pair coding is not or everyone and doesn't work in all teams. It can sometimes require a strong bond and similar
working style between 2 developers. When this rare situation is found it should be encouraged for solving complex
issues and debugging difficult mystical problems. The power of 2 minds working together can be far better than 1 mind
going round and round in circles.

## Plan your design and architecture

A well planned architecture for an application is much better than unplanned. There is no shame in spending the
first few days of developing a new feature or application, thinking through ideas, architecture and prototyping.
Jumping straight into creating a new feature or application will inevitably have you coding yourself into a corner and
you will need to spend time refactoring aspects as you move further into the feature/s. Planning it all out to start with
avoids that, even if this means getting a pen to paper and drawing some ERD's.

Use the right tool for the right job, do not use tools just because it is new and on trend as that can lead to
technical debt and/or security issues in the future. Make sure to use design patterns when they are needed to solve a
problem, and don't use the business you work for as a testing ground for new un-proven design patterns that may not
solve your problem.

## Use new features of your coding language where possible

If your infrastructure has access to the latest version of your coding language, don't be scared to use the new 
features it provides. Some features that are available in current versions can be great and can make your code
cleaner and easier to work with. So if you can, don't stay using the old methods when new ones are there for you.
