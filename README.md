SUMMARY
The repository contains sample projects that can be used to make Acumatica ERP business entities like Sales Orders or Invoices 
available in Salesforce.com organization.
The sample provides a custom field in Acumatice ERP with an URL to an instance, and a couple of inquires exposed via OData. 
The inquires exposed by OData are used in Salesforce.com to query Acumatice ERP for data (e.g. invoices or sales orders) related
to accounts in real time.

LICENSING
The repository contents are licensed under MIT license.
See License for more details.

CONTENTS
Acumatica Customization -- contains a sample customization package for Acumatica ERP.
Acumatica ERP Objects -- contains a sample project with Salesforce.com objects.

REQUIREMENTS
Acumatica ERP administration or development skills are required to deploy the customizaiton package to Acumatica ERP instance.
Salesforce.com administration or development skills are required to deploy the objects to Salesforce.com organization.
For the sample to work, Salesforce.com sync module of Acumatica ERP must be enabled and configured.

INSTALLATION
Installation steps are listed below.
1. In Acumatica ERP instance:
- Import and publish SFDC.zip from Acumatica Customization folder into Acumatica ERP instance as a customization package. 

2. In Salesforce.com organization:
- Create custom "Acumatica ERP URL" field for Accounts.

3. In Acumatica ERP instance:
- Add "Acumatica ERP URL" to integration scenario and map it to new Acumatica ERP URL field just created in SFDC
- Configure URL to be used in Notifications in SM204001 screen -- it should be an Acumatica ERP instance URL
- Push the changes from Acumatica to SFDC, either by record update, or export / import via Data Loader to make the newly 
added "Acumatica ERP URL" data available in Salesforce.com organization.

4. In Salesforce.com organization:
- Configure External Data Source in SFDC
    ○ External Data Source: Acumatica ERP
    Note: the name is important as it is used for reference in SFDC package. If you change it you will need to update external 
    data source name in SFDC package later.
    ○ Type: OData 2.0
    ○ URL: <url for odata endpoint for your company>
    ○ Request Page Count: uncheck
    ○ Enable Search: uncheck
    ○ Identity Type: Per User
    ○ Authentication Protocol: Password Authentication
- Grant admin profile permissions for "Acumatica ERP" external data source
    ○ Go to profiles and select you administrator profile (e.g. System Administrator)
    ○ Edit Enabled External Data Source Access
    ○ Add Acumatica ERP to the list of enabled data sources and Save
- Sync external objects schema:
    ○ Go to "Acumatica ERP" external data source
    ○ Press Validate and Sync
    ○ Check SF-SalesOrders and SF-Invoices
    ○ Press Sync
- Add Acumatica ERP credentials for admin user
    ○ Go to My Settings / Personal / Authentication Settings for External Systems
    ○ Click New
    ○ Provide credentials for Acumatica ERP and Save
- Deploy SFDC package from Acumatica ERP Objects folder of this repository to SFDC (e.g. via sandbox or Force.com IDE)
    ○ During deployment overwrite the external objects and layouts created during previous steps
    ○ Optionally add the related external Acumatice ERP objects to Account layout manually
- Assign users that should have access to Acumatica ERP data in SFDC to Acumatica ERP permission set:
    ○ Open Acumatica ERP permission set
    ○ Click Manage Assignments button
    ○ Click Add Assignments button
    ○ Select desired users and click Assign button
- Review and re-configure if needed Acumatica ERP permission set for Acumatica ERP objects

    
