# Architecture Principles

[Use Design Patterns that solve your problem or improve re-usability](#use-design-patterns-that-solve-your-problem-or-improve-re-usability)
[Keep Domain logic re-usable in Service Classes](#keep-domain-logic-re-usable-in-service-classes)
[Send requests to databases via a Data Layer by using repositories or Gateways](#send-requests-to-databases-via-a-data-layer-by-using-repositories-or-gateways)
[Use dependency injection to maximise efficiency and testability](#use-dependency-injection-to-maximise-efficiency-and-testability)
[Keep Controllers or Actions free from Domain logic and extremely thin](#keep-controllers-or-actions-free-from-domain-logic-and-extremely-thin)
[Create interfaces to optimize the testability of your code](#create-interfaces-to-optimize-the-testability-of-your-code)
[Avoid using all in one solutions and their helper libraries](#avoid-using-all-in-one-solutions-and-their-helper-libraries)
[Pioritise Unit Tests over Integration Tests](#pioritise-unit-tests-over-integration-tests)
[Keep code simple](#keep-code-simple)
[Dont re-invent the wheel](#dont-re-invent-the-wheel)

## Use Design Patterns that solve your problem or improve re-usability

Design patterns should be used when appropriate and they should solve a problem or make your code more re-usable.
Common design patterns and methodologies that are recommended to employ for web development are as follows

- DDD (Domain Driven Design)
- ADR (Action Domain Response)
- TDD (Test Driven Tesign)
- Factory Pattern
- Adapter Pattern
- Strategy Pattern
- Decorator Pattern
- Singleton Pattern
- Observer Pattern

## Keep Domain logic re-usable in Service Classes

Any domain logic (business logic) which is specific to the application should be seperated into services.
This allows for the service domain logic to be reusable from other parts of your application and makes maintanence easier.

## Send requests to databases via a Data Layer by using repositories or Gateways

Any queries to a database should be held in the data layer of your application by using repositories or gateways. This enables your data layers repositories to make use of entities with an ORM or even simple raw queries and your application is not aware of how the data is retrieved, all it needs to know is what method to call on which repository and it should expect a consistant response. This frees you up to maintain and change your communication with the database without affecting the applications domain logic.

## Use dependency injection to maximise efficiency and testability

Classes you depend on should be injected via the classes constructor to allow them to be easily mocked when testing.

## Keep Controllers or Actions free from Domain logic and extremely thin

Controllers (in mvc) or Actions (in ADR) should never contain more logic than needed to recieve any data from the request required for processing, and to hand off to services which in turn should repspond.

To assure correct decoupling of responsabilities your services should not generate the response itself but only the data for the response, the response class should be built by the action or controller with the data from the service.

## Create interfaces to optimize the testability of your code

Most if not all classes should impliment some form of interface to allow them to be easily mocked in testing and swapped out for alternative implimentations as your code base scales and changes with the business.

## Avoid using all in one solutions and their helper libraries

You should avoid all in one solutions like laravel which are great for new comers to coding but encourage bad architechture and usage of lots of static methods. This code is not testable. 

If in a situation where an all in one solution must be used then avoid using as much of their implimentations and helpers as possible because its ideal to work towards a more agnostic approach, and using less of their propietory functionality means that extracting into a more abstract agnostic and scalable solution in the future would be easier.

## Pioritise Unit Tests over Integration Tests

Unit tests should generally be prioritised over integration tests as if ever unit of functionality is tested indipendantly then the entegration can be assumed to be successful anyway. Remember that unit tests should test 1 isolated piece of functionality and not test by sending requests to the application (that is the responsability of the integration tests).

## Keep code simple

Often the most effective solution is the simplest solution, Nuff Said!

## Dont re-invent the wheel

If you are working on a feature always check with your team if similar implimentations have been done before if not exactly the same thing. You can re-use the code, or maybe even use the time you were going to use re-inventing the wheel to abstract that code to a seperate library and then you have 2 applications working on some abstract code.

Always think about if there is any helper libraries made already within your team that can be of use to you before diving in. Often libraries and wrappers exist already in teams which you can utalise.