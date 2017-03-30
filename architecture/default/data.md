# Data View

This page details how this application's data will be persisted.

- OLTP using SQL Azure Database
- Application Insights for telemetry
- Archiving/partitioning policy for old/inactive data?
- Storage requirements?
- Will we need Analysis Services?
- Will we need to import/sync data from a legacy system?

## Caching
[EFCache](https://github.com/moozzyk/EFCache) will be used for in-memory caching.

## Resiliency
The [SQL Azure Execution strategy](https://msdn.microsoft.com/en-us/library/dn456835.aspx) will be configured. This will make the app retry on exceptions that are known to be possibly transient when working with SqlAzure.