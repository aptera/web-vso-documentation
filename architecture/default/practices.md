# Practices

This page details some of the practices that the team will follow, in an effort to produce a valuable system and keep the development process predictable and engaging for everyone involved.

## Quality
### Behavior Driven Development
No **view model**, **persentation service**, or **domain service** code will be written without a failing test having been written first. 

- Each test, by its naming, describes a behavior of the tested component. 
- For example, the `loginViewModel` should be tested by a suite described as "The login view model", and will contain a test described as "validates that a username and password have been entered". The test runner will then display this test as "The login view model validates that a username and password have been entered".

### Pair Programming
Pair programming will be used on tasks with a noticeable "unknown factor", at least until unknowns are resolved and the task becomes more straightforward. 

### Tools
- [FakeItEasy](https://fakeiteasy.github.io/)
- [NUnit](https://www.nunit.org/)
- [tSQLt](http://tsqlt.org/)
- [Jasmine](https://jasmine.github.io/)
- [Chutzpah](https://github.com/mmanela/chutzpah)

For detailed explanation and demonstration of these techniques, see Clean Coders episode 6 pt. 2, [here](\\apterasoftware.com\jfazzaro\lunch\clean-coders). 

## Sustainability
### What Kent Beck Said
1. Make it work
2. Make it right
3. Make it fast

Apply this pattern to [the development of each feature](http://code.jon.fazzaro.com/2012/11/29/kent-becks-mother-doesnt-work-here-and-neither-does-yours/). There will be no great refactoring phase in which all of our sins are washed away. We clean the code as we go, because [the only way to go fast is to go well](http://blog.8thlight.com/uncle-bob/2013/03/05/TheStartUpTrap.html).

### Naming and the Single Responsibility Principle
- Each method should do only one thing, and it should be named for exactly what it does.
- Public methods should have short, concise names. Private methods, which do more specific tasks, should have longer, more detailed names.
- Don't rely on comments to explain your code. Instead, aim for the usage of your code to read like sentence in English. If a method's functional purpose changes, so should its name.
- Methods should not be more than about 5 lines long. If you find this too restrictive, look closer. There are lines in there that are doing something discrete that can be extracted into their own method.
- This approach keeps the code clean, readable, and resilient to change. The extra time taken to do this as we go will be repaid exponentially as the codebase grows and changes.

For detailed explanation and demonstration of these techniques, see Clean Coders episodes 1, 2, and 3, [here](file:///\\apterasoftware.com\jfazzaro\lunch\clean-coders).

### Dependency Inversion / Constructor Injection
- [AutoFac](https://autofac.org/) is used for [Dependency Injection](http://en.wikipedia.org/wiki/Dependency_injection).
- A service locator and IoC container may be used conservatively to allow for DI in extension methods. Please limit this, since [the service locator is an anti-pattern](http://blog.ploeh.dk/2010/02/03/ServiceLocatorisanAnti-Pattern/).
- Here is a common example of this pattern that will occur in the application. This pattern is also described [here](http://blog.apterainc.com/bid/323676/Extension-Cords-Tea-Kettle-Whistling-and-the-Contractor-s-Wrap-for-Your-Code).
	- An object that operates on the application's data (referred to as a "domain service") will receive an instance of the data context interface (implemented elsewhere using Entity Framework) in its constructor. 
	- Nowhere in any method of this object should the context's SaveChanges method be called.
	- This class will be instantiated and used by code in the API of the application. For each API call, use the following pattern.
		- A data context is listed as an argument in the constructor of the API Controller. Ninject will then provide an instance of this context.
		- Domain service instances are created for the operation(s) that compose the call's functionality. The context is passed in to each via its constructor.
		- If applicable, the API method calls the context's SaveChanges method.
		- This is also a good place to log events to Application Insights.
	
#### Fluid Query Extensions
Most LINQ expressions in an application are likely to show up more than once. They should be factored out into discrete extension methods. This approach is described in detail [here](http://code.jon.fazzaro.com/2012/01/27/get-your-legos-right-with-fluent-query-extensions/).

## Source Control
We will implement a feature-branching strategy with continuous integration.

- Branches will be created for major feature development, especially if two or more developers are working on the same feature. 
- When the feature's development is complete (with passing tests), the branch is merged back into master and destroyed.
- master will always be functional and deployable.
- Bugs will be repaired in master.

