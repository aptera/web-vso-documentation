# Operational View

This page elaborates on the support process for the app.

## Instrumentation
API Events and unhandled exceptions are logged using Application Insights.

## Support Workflow
In the event of an unexpected application issue or error, administrators and support users can follow these general steps to pinpoint the problem.

1. Log in to the application and reproduce the issue as yourself. If the issue cannot be reproduced, sign in as the user who reported the issue, and try again.
2. Once the issue has been reproduced, check the JavaScript console and/or App Insights for related error messages. 
5. Problem API calls can be recorded and replayed using an HTTP client such as [Fiddler](http://fiddler2.com/), [Postman](https://chrome.google.com/webstore/detail/postman-rest-client/fdmmgilgnpjigdojojpjoooidkmcomcm?hl=en), or [Swagger](http://swagger.io/) to boost debugging efficiency.
