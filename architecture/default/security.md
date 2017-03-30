# Security View

Here is some detail on the implementation of authentication and authorization in the app, and some of the processes around managing user accounts.

## Authentication
### Web
Since the web application is a SPA, the secured application exists entirely in a single ASP.NET MVC view. The login/signup area of the application will be delivered using a separate MVC area. 

### API/Mobile
Ensure that the registration and login functionality is entirely available via the Web API, so that these operations may be reused by clients other than the web application for the same purposes.

## Authorization
Permissions-based authorization using ASP.NET Identity's Claim mechanism.

## Role/Permission Association
The association between role and claims will be configured in code. There is no need to store this in a configuration file or in the database, because these associations only define a template set of permissions to be given to a new user when the login is created, based on their role in the system. This does not need to change at runtime; each time a new permission is added, it is a safe assumption that there are already related code changes occurring.

## Non-standard configurations
In order to meet modern web security standards, the following modifications are made to a standard ASP.NET app configuration.

1. Redirect from HTTP to HTTPS ([like this](http://stackoverflow.com/questions/9823010/how-to-force-https-using-a-web-config-file))
1. Remove standard ASP.NET HTTP Headers ([like this](https://azure.microsoft.com/en-us/blog/removing-standard-server-headers-on-windows-azure-web-sites/))
1. A CSP header to whitelist domains the app's client code can interact with
1. Prevent Clickjacking using an `X-Frame-Options` header
1. Use HttpOnly cookies (`<httpCookies httpOnlyCookies="true"/>`)

## Processes