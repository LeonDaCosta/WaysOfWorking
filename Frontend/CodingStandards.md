# Frontend Standards

Is it essential that development teams reach and maintain consensus regarding the conventions and practices that must be followed throughout development. There should however be a level of flexibility regarding any possible overrides of such proposed standards when and where the team see fit to adopt and thus adapt to satisfy new requirements.

![Frontend Standards](frontend.jpg "Frontend Standards")


# Table of Contents
- [1️⃣ Utilise Lint Automation Tooling](#1️⃣-utilise-lint-automation-tooling)
    - [🔹 ESLint](#eslint)
    - [🔹 StyleLint](#stylelint)
    - [🔹 Prettier](#prettier)
- [2️⃣ General Development Practices](#2️⃣-general-development-practices)
- [3️⃣ Atomic Design & Development](#3️⃣-atomic-design-and-development)
- [4️⃣ AirBnb Coding Standards](#4️⃣-airbnb-coding-standards)

---

## 1️⃣ Utilise Lint Automation Tooling
When it comes to modern frontend development, we have a vast array of tooling at our disposal, and that includes tooling...for linting. When these packages are installed into a project, configured correctly, and enabled in your IDE, they can keep you aligned with Airbnb (or any other regarded) coding standard specification as you code, just by hitting save.

Here at PrecisionProco we utilise 3 main linting libraries for our frontend: ESLint, StyleLint, and Prettier.

### ESLint
ESLint is a very configurable linting library for identifying and reporting on patterns in JavaScript, allowing for easy and effective code maintenance.

```yaml
Website:
    https://eslint.org/

Benefits include:
    ➡️ Toggling individual rules instead of imposing strict or opinionated standards on you
    ➡️ Assigning configuration levels to rules for better lint granularity
    ➡️ Plugins created by the community; battle-tested, transparent, updated actively
    ➡️ Support for custom rules and parsers
    ➡️ Very good, thorough documentation
    ➡️ Lints your code on save for automated code adjustments
    ➡️ Easy to plug and play a set of rules from one project into another, good for team sharing
    ➡️ There is a very useful community plugin that auto-sorts file imports (eslint-plugin-simple-import-sort)
```

### StyleLint
StyleLint can be seen almost as the ESLint counterpart for stylesheets. This can be used to automate code adjustments also on save, for your CSS / SASS / Less (etc) files.

```yaml
Website:
    https://stylelint.io/

Benefits include:
    ➡️ Support for the latest CSS syntax, including CSS-like syntax such as SCSS and Less
    ➡️ Automatically fixes some styles of errors
    ➡️ Has over 170 built-in rules to catch errors and enforce stylistic conventions
    ➡️ Easy to plug and play a set of rules from one project into another, good for team sharing
    ➡️ Decent documentation
    ➡️ It is opinionated, providing the capability to enable only the rules you want to use and configure them to suit your preferences
    ➡️ There is a very useful community plugin that alphabetises styles (stylelint-order)
```

### Prettier
Prettier, like StyleLint, is an opinionated linting library, which actually works very well alongside ESLint to aid your linting quest.

```yaml
Website:
    https://prettier.io/

Benefits include:
    ➡️ Building and enforcing the style guide of suitability
    ➡️ Helping newcomers with the project's linting formalities
    ➡️ Easy to adopt, minimal overhead
    ➡️ Effectively clean up an existing codebase with speed
    ➡️ Easy to plug and play a set of rules from one project into another, good for team sharing
    ➡️ Works very well alongside ESLint
    ➡️ Can help lint stylesheets too
```

---

## 2️⃣ General Development Practices
As times goes on, this list is bound to refinement, but as it stands, we dutifully follow these practices when writing code to ensure order, code reuse, and other vital conventions are adhered to throughout the lifecycle of the project:

```yaml
Practices:
    ➡️ Always try to reuse code the best you can
    ➡️ Extract helper functions into `helpers/utils` directory
    ➡️ Extract constants into `helpers/constants` directory
    ➡️ Extract custom hooks into `helpers/hooks` directory
    ➡️ Strictly no `!important` directives in stylesheets as it badly affects specificity, which causes issues for the future you and other developers
    ➡️ Do not use classes, use functional components
    ➡️ Do not use id props in React components, only classes (using className)
    ➡️ Do not interact with the DOM in React (using document.querySelector() etc), only interact with Virtual DOM
    ➡️ Try to use Redux/Persist over state in components
    ➡️ Make sure to use linters on `.ts`, `.tsx`, and `.scss` files to preserve code cleanness
    ➡️ Use the Atomic UI design principles, by creating components which can be categories as either `Atoms`, `Molecules`, `Organisms`, `Pages`, or `Widgets`
    ➡️ With Next.js (which we may be later migrating to), any new pages you make must be added to the `/pages` directory, where the file name will be the route name, e.g. `checkout` will become `localhost:8080/checkout`
    ➡️ Make sure to use `Sass Modules` format instead of regular Sass, as Next.js does not support that
    ➡️ Make sure components are responsive on every form factor, including `iPhone 5/SE`
    ➡️ Any global styles should be included in `src/styles/globals.scss` directory
    ➡️ Make sure to commit and push code on feature branches regularly, and do PRs to merge into dev, to acquire feedback, and to prevent data loss
    ➡️ Next's dynamic routing (pages go into /pages directory) instead of React Router
    ➡️ Next's dynamic Head component for SEO instead of React Helmet
    ➡️ `TypeScript` (`.tsx` for components / `.ts` for constants/helper functions)
    ➡️ `Sass Modules` (not CSS, or SASS [due to lack of support in modern Next versions])
    ➡️ `Jest` / `Enzyme` for unit/integration testing
    ➡️ `Cypress` for end-to-end (E2E) testing
    ➡️ `Redux / Persist / Sagas` over state in components when and where possible
    ➡️ No global styles abuse; global styles are strictly reserved for pure tag reform (changing styles for general `div`, `p`, etc, not for editing e.g. `WidgetWrapper` component etc.)
    ➡️ Atoms/Molecules/Organisms/Templates/Widgets/Pages format over random file creation/positioning
```

## 3️⃣ Atomic Design and Development
Atomic design/development allows us to better modularise our code into different sized components, abstracting out irrelevant logic. We can then use these components to build bigger ones, creating an app which is easily readable, decoupled, and properly testable.

Brad Frost has a great guide to Atomic Design/Development here: http://atomicdesign.bradfrost.com/table-of-contents/


Components are categorised into five main categories:

```yaml
Categories:
    ➡️ Atoms: smallest level components, e.g. search bar, divider
    ➡️ Molecules: comprised of 2+ atoms, e.g. list component
    ➡️ Organisms: comprised of 2+ molecules, e.g a complex datepicker
    ➡️ Templates: comprised of 2+ organisms, e.g. a navbar, header, footer
    ➡️ Pages: comprised of a template and other features (Next.js handles these with their own 'pages' directory due to dynamic routing)
```

---

## 4️⃣ AirBnb Coding Standards

It is not always possible to follow AirBnb standards, especially when dealing with frameworks and extending their classes.
For that reason you should be required to adhere to AirBnb coding standards in all cases unless there is a specific reason it cannot
be done, or there is a rule the team as a whole has chosen to ignore, in which case such rules can be overridden.

ESLint has been configured to lint the code in line with these coding standards, with some team-preferred overrides in place. You can read more about these standards here: https://airbnb.io/javascript/

Here is a breakdown of practices used for each part of code, of which may change over time as and when the team's convention/linting requirements change:

```yaml
References:
    ➡️ Use const for all of your references; avoid using var
    ➡️ If you must reassign references, use let instead of var
    ➡️ Note that both let and const are block-scoped

Objects:
    ➡️ Use the literal syntax for object creation
    ➡️ Use computed property names when creating objects with dynamic property names
    ➡️ Use object method shorthand
    ➡️ Use property value shorthand
    ➡️ Group your shorthand properties at the beginning of your object declaration
    ➡️ Only quote properties that are invalid identifiers
    ➡️ Do not call Object.prototype methods directly, such as `hasOwnProperty`, `propertyIsEnumerable`, and `isPrototypeOf`
    ➡️ Prefer the object spread operator over Object.assign to shallow-copy objects. Use the object rest operator to get a new object with certain properties omitted

Arrays:
    ➡️ Use the literal syntax for array creation
    ➡️ Use Array#push instead of direct assignment to add items to an array
    ➡️ Use array spreads ... to copy arrays
    ➡️ To convert an array-like object to an array, use spreads ... instead of Array.from
    ➡️ Use Array.from instead of spread ... for mapping over iterables, because it avoids creating an intermediate array
    ➡️ Use return statements in array method callbacks. It’s ok to omit the return if the function body consists of a single statement returning an expression without side effects
    ➡️ Use line breaks after open and before close array brackets if an array has multiple lines

Destructuring:
    ➡️ Use object destructuring when accessing and using multiple properties of an object
    ➡️ Use array destructuring
    ➡️ Use object destructuring for multiple return values, not array destructuring

Strings:
    ➡️ Use single quotes '' for strings
    ➡️ Strings that cause the line to go over 100 characters should not be written across multiple lines using string concatenation
    ➡️ When programmatically building up strings, use template strings instead of concatenation
    ➡️ Never use eval() on a string, it opens too many vulnerabilities
    ➡️ Do not unnecessarily escape characters in strings

Functions:
    ➡️ Use named function expressions instead of function declarations
    ➡️ Wrap immediately invoked function expressions in parentheses
    ➡️ Never declare a function in a non-function block (if, while, etc). Assign the function to a variable instead. Browsers will allow you to do it, but they all interpret it differently, which is bad news bears
    ➡️ ECMA-262 defines a block as a list of statements. A function declaration is not a statement
    ➡️ Never name a parameter arguments. This will take precedence over the arguments object that is given to every function scope
    ➡️ Never use `arguments`, opt to use rest syntax ... instead
    ➡️ Use default parameter syntax rather than mutating function arguments
    ➡️ Avoid side effects with default parameters
    ➡️ Always put default parameters last
    ➡️ Never use the Function constructor to create a new function
    ➡️ Spacing in a function signature
    ➡️ Never mutate parameters
    ➡️ Never reassign parameters
    ➡️ Prefer the use of the spread operator ... to call variadic functions
    ➡️ Functions with multiline signatures, or invocations, should be indented just like every other multiline list in this guide; with each item on a line by itself, with a trailing comma on the last item

Arrow Functions:
    ➡️ When you must use an anonymous function (as when passing an inline callback), use arrow function notation
    ➡️ If the function body consists of a single statement returning an expression without side effects, omit the braces and use the implicit return. Otherwise, keep the braces and use a return statement
    ➡️ In case the expression spans over multiple lines, wrap it in parentheses for better readability
    ➡️ If your function takes a single argument and doesn’t use braces, omit the parentheses. Otherwise, always include parentheses around arguments for clarity and consistency
    ➡️ Avoid confusing arrow function syntax (=>) with comparison operators (<=, >=)

Classes & Constructors:
    ➡️ Always use class. Avoid manipulating prototype directly
    ➡️ Use extends for inheritance
    ➡️ Methods can return this to help with method chaining
    ➡️ It’s okay to write a custom toString() method, just make sure it works successfully and causes no side effects
    ➡️ Classes have a default constructor if one is not specified. An empty constructor function or one that just delegates to a parent class is unnecessary
    ➡️ Avoid duplicate class members

Modules:
    ➡️ Always use modules (import/export) over a non-standard module system. You can always transpile to your preferred module system
    ➡️ Do not use wildcard imports
    ➡️ And do not export directly from an import
    ➡️ Only import from a path in one place
    ➡️ Do not export mutable bindings
    ➡️ In modules with a single export, prefer default export over named export
    ➡️ Put all imports above non-import statements
    ➡️ Multiline imports should be indented just like multiline array and object literals
    ➡️ Disallow Webpack loader syntax in module import statements
    ➡️ Imports should be structured in categories in this order -
    ➡️ import "./setup" - Side effect imports. (These are not sorted internally)
    ➡️ import react from "react" - Packages (npm packages and Node.js builtins)
    ➡️ import a from "/a" - Absolute imports and other imports such as Vue-style @/foo
    ➡️ import a from "./a" - Relative imports

Iterators and Generators:
    ➡️ Don’t use iterators. Prefer JavaScript’s higher-order functions instead of loops like for-in or for-of
    ➡️ Don’t use generators for now (as they do not transpile well to ES5)
    ➡️ If you must use generators, make sure their function signature is spaced properly

Properties:
    ➡️ Use dot notation when accessing properties
    ➡️ Use bracket notation [] when accessing properties with a variable
    ➡️ Use exponentiation operator ** when calculating exponentiations

Variables:
    ➡️ Always use const or let to declare variables. Not doing so will result in global variables. We want to avoid polluting the global namespace
    ➡️ Use one const or let declaration per variable
    ➡️ Group all your `consts` and then group all your `lets`
    ➡️ Assign variables where you need them, but place them in a reasonable place
    ➡️ Don’t chain variable assignments
    ➡️ Avoid using unary increments and decrements (++, –)
    ➡️ Avoid linebreaks before or after = in an assignment. If your assignment violates max-len, surround the value in parens

Hoisting:
    ➡️ var declarations get hoisted to the top of their closest enclosing function scope, their assignment does not. const and let declarations are blessed with a new concept called Temporal Dead Zones (TDZ). It’s important to know why typeof is no longer safe
    ➡️ Anonymous function expressions hoist their variable name, but not the function assignment
    ➡️ Named function expressions hoist the variable name, not the function name or the function body
    ➡️ Function declarations hoist their name and the function body

Comparison Operators & Equality:
    ➡️ Use === and !== over == and !=
    ➡️ Conditional statements such as the if statement evaluate their expression using coercion with the ToBoolean abstract method and always follow these simple rules -
    ➡️ Objects evaluate to true
    ➡️ Undefined evaluates to false
    ➡️ Null evaluates to false
    ➡️ Booleans evaluate to the value of the boolean
    ➡️ Numbers evaluate to false if +0, -0, or NaN, otherwise true
    ➡️ Strings evaluate to false if an empty string '', otherwise true
    ➡️ Use shortcuts for booleans, but explicit comparisons for strings and numbers
    ➡️ Use braces to create blocks in case and default clauses that contain lexical declarations (e.g. let, const, function, and class)
    ➡️ Ternaries should not be nested and generally be single line expressions
    ➡️ Avoid unneeded ternary statements
    ➡️ When mixing operators, enclose them in parentheses. The only exception is the standard arithmetic operators (+, -, *, & /) since their precedence is broadly understood

Blocks:
    ➡️ Use braces with all multi-line blocks
    ➡️ If you’re using multi-line blocks with if and else, put else on the same line as your if block’s closing brace
    ➡️ If an if block always executes a return statement, the subsequent else block is unnecessary. A return in an else if block following an if block that contains a return can be separated into multiple if blocks

Control Statements:
    ➡️ In case your control statement (if, while etc.) gets too long or exceeds the maximum line length, each (grouped) condition could be put into a new line. The logical operator should begin the line
    ➡️ Don’t use selection operators in place of control statements

Comments:
    ➡️ Use /** ... */ for multi-line comments
    ➡️ Use // for single line comments. Place single line comments on a newline above the subject of the comment. Put an empty line before the comment unless it’s on the first line of a block
    ➡️ Start all comments with a space to make it easier to read
    ➡️ Prefixing your comments with FIXME or TODO helps other developers quickly understand if you’re pointing out a problem that needs to be revisited, or if you’re suggesting a solution to the problem that needs to be implemented. These are different than regular comments because they are actionable. The actions are FIXME -- need to figure this out or TODO -- need to implement
    ➡️ Use // FIXME - to annotate problems
    ➡️ Use // TODO - to annotate solutions to problems

Whitespace:
    ➡️ Use soft tabs (space character) set to 2 spaces
    ➡️ Place 1 space before the leading brace
    ➡️ Place 1 space before the opening parenthesis in control statements (if, while etc.). Place no space between the argument list and the function name in function calls and declarations
    ➡️ Set off operators with spaces
    ➡️ End files with a single newline character
    ➡️ Use indentation when making long method chains (more than 2 method chains). Use a leading dot, which emphasizes that the line is a method call, not a new statement
    ➡️ Leave a blank line after blocks and before the next statement
    ➡️ Do not pad your blocks with blank lines
    ➡️ Do not add spaces inside parentheses
    ➡️ Do not add spaces inside brackets
    ➡️ Add spaces inside curly braces
    ➡️ Avoid having lines of code that are longer than 100 characters (including whitespace). Note - per above, long strings are exempt from this rule, and should not be broken up

Commas:
    ➡️ Say no to leading commas
    ➡️ Say yes to trailing commas

Semicolons:
    ➡️ Say yes to these too

Naming Conventions:
    ➡️ Avoid single letter names. Be descriptive with your naming
    ➡️ Use camelCase when naming objects, functions, and instances
    ➡️ Use PascalCase only when naming constructors or classes
    ➡️ Do not use trailing or leading underscores
    ➡️ Don’t save references to this. Use arrow functions or Function#bind
    ➡️ A base filename should exactly match the name of its default export
    ➡️ Use camelCase when you export-default a function. Your filename should be identical to your function’s name
    ➡️ Use PascalCase when you export a constructor / class / singleton / function library / bare object
    ➡️ Acronyms and initialisms should always be all capitalized, or all lowercased
    ➡️ You may optionally uppercase a constant only if it (1) is exported, (2) is a const (it can not be reassigned), and (3) the programmer can trust it (and its nested properties) to never change

Accessors:
    ➡️ Accessor functions for properties are not required
    ➡️ Do not use JavaScript getters/setters as they cause unexpected side effects and are harder to test, maintain, and reason about. Instead, if you do make accessor functions, use getVal() and setVal(‘hello’)
    ➡️ If the property/method is a boolean, use isVal() or hasVal()
    ➡️ It’s okay to create get() and set() functions, but be consistent

TypeScript-specific:
    ➡️ Interfaces  should be prefixed with an  I
    ➡️ Types       should be prefixed with a   T
```
