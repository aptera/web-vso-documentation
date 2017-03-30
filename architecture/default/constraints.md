# Constraints View

Here are some technical constraints that informed some of these architectural decisions.

- Application data should be stored in a SQL Server database. 
- If required, SSIS and SSAS should be used for ETL and BI support.
- The system will be hosted on Azure.
- This document contains most tribal knowledge needed to work with the code, in case the original team is not available for support.

`// TODO: Add constraints specific to this project. For example:`

    Time, budget and resources.
    Approved technology lists and technology constraints.
    Target deployment platform.
    Existing systems and integration standards.
    Local standards (e.g. development, coding, etc).
    Public standards (e.g. HTTP, SOAP, XML, XML Schema, WSDL, etc).
    Standard protocols.
    Standard message formats.
    Size of the software development team.
    Skill profile of the software development team.
    Nature of the software being built (e.g. tactical or strategic).
    Political constraints.
    Use of internal intellectual property.

Client apps for multiple mobile platforms will need access to most of the same functionality that the desktop web application will provide. 

