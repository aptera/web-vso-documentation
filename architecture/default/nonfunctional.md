# Nonfunctional View

Here are some overall characteristics of the system, and the implementations that will enable them.

## Usability
#### Performance and Responsiveness
Pages must load quickly and smoothly. At most, a page should load and be responsive to user interaction within 10 seconds. As a general metric, though, **performance should not be a noticable part of the user experience**.

There may, of course, be exceptions to this for certain operations. These should be handled by increasing the responsiveness of the application, allowing the user to interact while the operation runs, or at the very least communicating a message that the operation will be taking its time, and maybe the user should go have a sandwich.

A loading indicator will be displayed during all Web API operations. 

#### Simplicity and Discoverability
The application must be simple to use.  Users must be able to quickly understand how to get the information they need or perform the task they need to get done.

#### Validation
The software must indicate to the user the data that is required for successful entry prior to page submission, and also prompt the user to save changes if they navigate away before doing so. It must also stop the user from entering invalid input as early as possible in the data entry process, and give quick usable feedback.

#### Default Values
If the system can make a reasonable guess at a default value for a field, it should prefill the field and not make the user enter that data.

### Implementation
#### Single Page Application
The main web application will be built using Single-Page architecture. Users of modern web applications have come to expect a rich, desktop-like experience from web applications, and the [app] experience should be no exception.

#### Notifications
The application will communicate in a responsive, friendly, and fun way with the user via a few different kinds of notifications.

#### Application Notifications
These notifications will be presented across the bottom of the screen, in a color appropriate to the content of the message (blue for info, red for error, etc.). The notification can be quickly dismissed if the user clicks or taps on it. 

A notification can be just a string of text, but can also be composed using HTML, if a relevant action or input is required.

#### Push Notifications
If required by a user story, push notifications can be sent from the server. For web application users, a push notification will appear on the notifications page. A count of new notifications is shown in red near the user's avatar. 

For mobile application users, notifications will appear according to the conventions of the platform.

#### Email Notifications
The app will send email notifications in the following scenarios:
- New user sign-up
- Successful payment processing
- Failed payment processing
- Password reset
- User encounters an unhandled exception in the application (for admin/support)

#### Default Selections
In general, a user's default input selections will be pre-populated by querying recent relevant data. How these queries are designed varies by scenario, and should be balanced against a responsive user experience.

## Reliability
#### Availability
The service must always be available, with 99% uptime. 

#### Recoverability
It must be redundant so that service is not interrupted in the event of failure or disaster.  

#### Scalability
It must be scalable to meet demand and maintain the specified level of performance.

#### Integrity
Data stored in the system should always be valid according to the business rules that govern it, and should never be stored in an inconsistent state. 

Look up values including projects should not actually be deleted from the database, but hidden from use when entering new data. Invoice and Time Entry data will be the only items actually deleted when a marked as deleted by the user.

### Implementation
#### Azure
All of the reliability requirements, with the exception of integrity, are met by hosting the service entirely in Azure environments.

#### Unit of Work
All data changes in the system will be done as part of a Unit of Work, a pattern implemented by the Entity Framework. When a unit of work's changes are saved, the transaction is atomic; if one action fails, the entire set of changes fails. This will ensure that the data stored in the database is always in a consistent state.

#### Soft Deletes
Entities in the data model that tend to drive dropdowns or otherwise link to temporal project or invoice data will all bear a boolean IsActive column. When one of these items is removed in the settings section, this bit will be set to false, and the item will no longer appear as an option when entering new data. The record will remain, however, for historical data integrity.

## Security
- No one may access the application or its data without a valid user account. 
- A user will not have access to the application or its data if their account is locked, cancelled or expired.
- A user may only read or change data to which they have access to according to their permissions granted in the application.
	
### Implementation
#### ASP.NET Authentication and Authorization
User authentication and authorization will be implemented using the standard ASP.NET Identity membership provider and data store. The Roles assigned to each user using this mechanism will actually be permissions, access to certain application features. Details can be found in the Security section.

## Sustainability
The application should be easy for developers to understand, develop, and maintain. It should be resilient when changes are needed. It should be obvious to determine when a change to the application has broken working functionality.

### Implementation
The [Practices](practices.md) page outlines the methods by which we will keep the code clean, readable, tested, and maintainable.

## Supportability
The system needs to track any error incurred by user, with the ability to have it email the error details to support staff. Application support staff must also be able to determine who added, modified or deleted information in a client's account.

### Implementation
#### Instrumentation
- Azure Application Insights for monitoring and notification
- .NET Tracing where custom logging is necessary
- Trace listeners configured as needed
	
### Auditing
Changes to the data of certain entities will be logged as events in App Insights. This will be implemented by handling the SavingChanges event on the Entity Framework context. An audit entry will contain the following data:
- The user name
- The UTC timestamp
- The name of the API event
- A description of the record(s) affected (implemented by overriding the ToString method for the entity in question).

## Interoperability
If external systems need to consume or work with the information and functions of this system, they should be able to do so in using a standard method of communication. Modification to this system should not be required to accomplish this.

### Implementation
#### Web API
All system data and logic will be presented to client apps via a versioned HTTP API. This ensures that both the client applications and the server components can evolve peacefully and independently for a long time, making for a sound investment in the lifespan of the system.

