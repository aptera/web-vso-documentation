# Deployment View

## How is the app deployed?
- The web application is deployed using [Web Deploy](http://www.iis.net/downloads/microsoft/web-deploy), as part of a continuous integration process triggered by commits to master.
- Database changes for the application [dbo] schema are managed via Entity Framework [Code First Migrations](https://msdn.microsoft.com/en-us/data/jj591621.aspx). Migrations are executed on ASP.NET app startup.
- Configuration changes should be implemented via Slot Settings under Application Settings in the App Service.

### Environments
#### Production
The Production environment consists of an Azure Website, and a SQL Azure database.

#### Test
The Test environment mimics the Production environment identically, managed using Azure Deployment Slots.

### Continuous Integration
- A commit to master will trigger an automated build, test, and deploy to the Test environment.
- Once validated, the changes in Test can be deployed to Production by issuing a Deployment Slot Swap.
- Production deployment is a frequent, anticlimactic event. We promote everything *at least* at the end of every sprint.  

### Feature Flags
- New features that take longer to implement and test should be concealed behind a temporary feature flag. 
- This practice helps to avoid a complicated branching strategy and to keep code changes flowing in small batches into Production.