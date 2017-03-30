# Design View

Here are some implementation/interaction patterns we will be using during development that everyone on the team should understand.

## Layer interaction
### Web client side
- User interface semantics defined in HTML
- UI elements bound to js view models.
- Common presentation logic is defined in service modules.
- View models depend on service modules when needed.
- View models and services will be developed entirely using TDD

### iOS client side
- User interface semantics defined in storyboards and xib files.
- Presentation logic is contained in ViewControllers and Coordinator classes.
- ViewControllers and Coordinators reside in a separate Presentation framework, consumed by the app project.
- ViewControllers and Coordinators are test-driven.
- Swagger codegen is used for API interaction.

### Server side
- Web API controllers should only contain the barest plumbing code
- Data is passed between client and server using message models. In most cases, these will be mapped back and forth with their Data Model counterparts using AutoMapper. More complex mappings will be performed by a (tested) Adapter service class.
- Logic is defined in [Domain Service](http://lostechies.com/jimmybogard/2008/08/21/services-in-domain-driven-design/) classes
- Dependencies (EF context, HttpContext, etc.) must be injected in the controller and passed in to the Domain Service(s) used.
- Commit operations (i.e., SaveChanges for EF) may only be called by controller code, not by Domain Service code
- Domain Services will be developed entirely using TDD
- No business logic will be housed at the database layer (in Stored Procedures, Functions, etc.). Database-layer code will only be used in exceptional cases, to achieve performance or other such architectural requirement for a feature.

## Developing a new page
The web application uses AngularJS to handle SPA concerns such as routing and loading.  

- The folder structure of the app is determined by subject, not technology.
    - For example, an order view/model would be found in `html` and `js` files together under an `orders` folder, as opposed to a `views` folder containing `html` files and a `models` folder containing `js` files.

1. Once the design is discussed and decided, begin by test-driving the view model.
1. Any dependencies will be mocked and designed as needed, to ensure the correct shape and data required by the feature.
1. Once the model is test-driven into place, implement the mocked dependencies until the feature can be tested manually.
