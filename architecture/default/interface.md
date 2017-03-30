# Interface View

This page describes the details of interfaces between major app components.

## [Application]
### Client Applications
- HTTPS protocol
- JSON data format
- AJAX functions in Web implementation
- Asynchronous
- Consuming scripts and API will live in the same Web Application/Domain, to eliminate CORS issues

### Server API
- ASP.NET Web API
- [Swagger](http://swagger.io/) UI and metadata generated using [Swashbuckle](https://github.com/domaindrivendev/Swashbuckle)
- Idempotent (stateless and repeatable)
- Versioned using [namespaces](http://blogs.msdn.com/b/webdev/archive/2013/03/08/using-namespaces-to-version-web-apis.aspx)
- URIs should be [hackable](http://www.nngroup.com/articles/url-as-ui/), and they should reveal intent
- Liberal with regard to requests, conservative with regard to responses

## External Systems
### Email with SendGrid

### Payments with Stripe
- Consumed only by server code  
- Call syntax wrapped by Stripe.NET library
- [PCI Compliant](https://stripe.com/us/help/faq#pci-compliance)
