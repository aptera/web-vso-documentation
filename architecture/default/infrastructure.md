# Infrastructure View

## To The Cloud
Deploying to an all-Azure environment helps to offload the following typical infrastructural concerns as much as possible.
- Maintenance
- Scaling
- Uptime/connectivity
- Disaster recovery

### Web Application 
The web application will be deployed as an [Azure App Service](https://azure.microsoft.com/en-us/services/app-service/?b=16.52).

### Database 
#### Transactional data
The application database will be hosted using the SQL Azure Database service.

#### Session data
Temporary session data will be held in the database (or Redis), to enable horizontal scaling at the web server layer.