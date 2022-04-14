# Backend Standards

Development Teams should ideally all be on the same page and adhere to an agreed upon list of standards that benefit both the
development team and the business. These rules should not just blindly follow PSR rules however also integrate
styles that the development team like to adopt.

![Backend Standards](backend.gif "Backend Standards")

# Table of Contents
- [PSR-12 Should always be followed where possible](#psr-12-should-always-be-followed-where-possible)
- [Comment only what the code cannot say](#comment-only-what-the-code-cannot-say)
- [Scope should be restrictive where possible](#scope-should-be-restrictive-where-possible)
- [Whitespace and dead code](#whitespace-and-dead-code)
- [Input should always be validated](#input-should-always-be-validated)
- [Dont use FQCNs](#dont-use-fqcns)
- [Line Length should not exceed 120 chars](#line-length-should-not-exceed-120-chars)
- [Be strict](#be-strict)
- [Method Readability](#method-readability)
- [Naming Conventions](#naming-conventions)
- [Managing Internal Dependencies](#managing-internal-dependencies)
- [Composer](#composer)


## PSR-12 Should always be followed where possible

It is not always possible to follow PSR rules, especially when dealing with frameworks and extending their classes.
For that reason you should be required to adhere to PSR-12 in all cases unless there is a specific reason it cannot
be done, or there is a rule the team as a whole has chosen to ignore.

https://www.php-fig.org/psr/psr-12/

## Comment only what the code cannot say

Pre PHP 7.4 you really needed certain parts of your classes to have doc-blocks and comments, but as of PHP 7.4
Comments and doc-blocks have no need in existing unless used for parsing in the same way Doctrine does.
With type hinting for all parameters on methods and classes including return type hinting most information we need to
know is in the code. The only exception I have come across for this is `@throws`. This rule insinuates that you name
variables well

## Scope should be restrictive where possible

Sometimes it is not always possible to choose the scope of methods or variables if you are extending a class from a
3rd party or framework, however in most cases you can define the scope. When defining scope all class variables should
be private and have getters and setters added. Any methods not intended to be used outside the class should be
private, unless the intent is for the class to be extended and those methods to be used from the child.

## Whitespace and dead code

There should always be 1 blank line at the bottom of every file. Not all IDEs may enforce this so make sure to check
your IDE is configured correctly. You can also set this up in `.editorconfig`. Within methods there should not be any
stray linebreaks that do not increase readability. For example line breaks should exist to separate sections of control
logic.

There should not be any methods that exist with an empty body, or a body with just a comment.
Any code that is no longer needed should not be commented out and committed, it should be deleted and git will maintain
that history.

## Input should always be validated

All user input to the application should be validated. Not just for validity but also for silly mistakes that the user
might make such as leaving white space on the end of a discount code (this should be trimmed).

## Dont use FQCNs

In modern PHP no class should ever be referred to with an FQCN (Fully Qualified Class Name). All namespaces should go in the use statements at the top of a class.

## Line Length should not exceed 120 chars

Lines should not exceed 120 chars long to avoid the need to scroll sideways. This can be a pain when people don't
have a mouse that allows sideways scrolling.

## Be strict

Your control logic should always be written strict to avoid ambiguity and introduction of bugs. As a developer
you should always know exactly what your logic is comparing against and never should allow the code to guess.
By that I mean DON'T do the following things:

```php
if ($val) {
    //do logic
}
```

Doing this allows your logic to run if the value is truthy which can be a boolean true or any string or any object or
any array. Pretty much most things that aren't boolean false or null. The reason this is bad is that if something
goes wrong elsewhere in the application and the `$val` gets set to something you don't expect your logic still runs
either making it seem like nothing is wrong or causing a fatal further down the line.

The same applies to the following

```php
if (!$val) {
    //do logic
}
```

Notice the difference is the exclamation mark. This reverses the logic to check for false-ish values, so as said before
the same problems exist as above with the added problem of the exclamation mark is very! easy to miss when a developer
is scanning it and can cause errors in additional logic added to the same class or control logic where the developer
didn't realise the logic was that way round.

The fix is to always! be strict with your checks, for example like this:

```php
if ($val === true) {
    //do logic
}
if ($val === 'a string') {
    //do logic
}
```

The advantage of doing this is when an error occurs you will be taken to the correct location when debugging and no doubt
will find it easier to work out how to fix this logic. It is also much more verbose as to what is going on in your control
logic.

## Method Readability

A method should be able to be read predominantly by scanning down, and marginally left to right. Increasing scanning
from left to right decreases readability.

When method parameters exceed 1 they should be seperated onto multiple lines to increase readability and decrease the
possibility of sideways scrolling. For example:

```php
public function foo(int $bar, string $diddly, array $squat) :void
{
    //Some Logic
}
```

would become:

```php
public function foo(
    int $bar,
    string $diddly,
    array $squat
) :void {
    //Some Logic
}
```

In this case it is far easier to spot the method parameter types and to see if any parameter are missing type hints.

## Naming Conventions

Methods and variables should always be named using camel case and not be ambiguous. When choosing a descriptive method
name you must do so with care thinking of the future developer looking at your code. For example:

```php
getCat(); //This makes sense to you, to another developer there's more than one meaning
private string $cat; //This makes sense to you, to another developer there's more than one meaning
```

```php
getCategory(); //This is better and less ambiguous
private string $category; //This is better and less ambiguous
```

99% of the time most methods will be prefixed with either get, set, or is, based on its operation. Get should be used
for methods that return data, set for methods that change data, and is for methods that tell you the status of existing
data. For example:

```php
getName();
setName();
isLive();
```

Often you come across methods which the domain logic inside them doesn't point towards a getter or a setter. Instead,
they point more towards something like `calculateFoo()` or `processFoo()`. These situations often cannot be avoided,
however it's good to think about if the method `processPriceFromInput()` for instance could actually just be named
`getPrice()`.

All boolean variables should ideally be prefixed with is. For example:

```php
private bool $isActive;
private bool $isTest;
```

In some cases you may find the necessity to prefix them with `should` or `has` or `can`, dependent on the situation.
Often this would be the naming convention for a method that may combine the result of checking multiple boolean values. 

## Managing Internal Dependencies

Managing internal dependencies can be tricky depending on your companies current workflow. Even using modern tools it still can be a bit of a bottleneck on workflow and can be difficult to manage between the development team and the business.

### Composer

Ideally composer should be used to manage internal PHP dependencies. All dependencies should be listed in your composer.json file against a tag release of the relevant dependency.

dev-xxxxxx should be avoided being used unless you are working on a branch that is in active development and not yet merged into develop and/or into a deployed branch.

Before being merged into develop and/or a deployed branch, the branch in use on composer for an internal package should be tagged and released.

This means for branches that have multiple internal packages that they depend on, it can cause a large slow down in QA because you end up with PRs having to be merged and released in a linear chain a bit like a chain in the housing market. It is what it is though.
