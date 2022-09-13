# Modernize EWS Apps

Modernize your Exchange Web Services apps with Microsoft Graph. The idea is to upgrade existing (legacy) applications using Exchange Web Services (EWS) with either using OAuth instead of Basic authentication, or to develop new applications or services using Microsoft Graph.

## Modernize your Exchange Web Services apps with Microsoft Graph

This repository includes information for the session "Modernize your Exchange Web Services apps with Microsoft Graph" held together with [@magrom](http://twitter.com/magrom) at [Microsoft Exchange Community Airlift](https://mecairlift.event.microsoft.com/ ) in September 2022.

## What is EWS

- is a cross-platform API that sends SOAP-based XML messages
- supports EXO, and on-premises versions >= Exchange Server 2007
- enables applications to access mailbox items such as email messages, meetings, and contacts from Exchange Online
- Communicate with EWS by using the EWS Managed API
- https://docs.microsoft.com/en-us/exchange/client-developer/exchange-web-services/how-to-communicate-with-ews-by-using-the-ews-managed-api

## Status of EWS

- This API is in sustaining mode (since July 2018)
- It´s Open Source: https://github.com/officedev/ews-managed-api 
- The end of Basic authentication in EXO for EWS is near (or already here, latest Oct. 2022)
- Continue using EWS: Authenticate by using OAuth
- Use Microsoft Graph as the logical successor

## Identity usage of EWS in code

If you can identify code like the following, the app is using EWS.

~~~~C#
ExchangeService service = new ExchangeService(ExchangeVersion.Exchange2013_SP1);
service.Credentials = new WebCredentials("svc@domain.com", "password");
service.AutodiscoverUrl("svc@domain.com",RedirectionUrlValidationCallback);

// Define one callback function for the AutodiscoveryUrl function:
private static bool RedirectionUrlValidationCallback(string redirectionUrl)
{
    // The default for the validation callback is to reject the URL.
    bool result = false;
    Uri redirectionUri = new Uri(redirectionUrl);
    // Validate the contents of the redirection URL. 
    // In this sample callback we consider valid if it´s HTTPS
    if (redirectionUri.Scheme == "https")
        { result = true; }
    return result;
}
~~~~

## Use EWS OAuth

- Authenticate an EWS application by using OAuth https://docs.microsoft.com/en-us/exchange/client-developer/exchange-web-services/how-to-authenticate-an-ews-application-by-using-oauth
- OAuth authentication for EWS is only available in Exchange Online as part of Microsoft 365
- EWS applications that use OAuth must be registered with Azure Active Directory

## Microsoft Graph

- a unified programmability model with a single endpoint https://graph.microsoft.com 
- access the tremendous amount of data in Microsoft 365, Windows, and Enterprise Mobility + Security
- Security
- PowerShell module & SDK´s
- **Start at https://aka.ms/graph**
- Microsoft identity platform and OAuth 2.0 authorization code flow https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-oauth2-auth-code-flow

## Use Microsoft Graph sample

- Microsoft Graph quick start
- Build a sample app that connects to Microsoft 365 and calls the Microsoft Graph API.
- https://developer.microsoft.com/en-us/graph/quick-start 

Generate this sample and adapt it as needed.
