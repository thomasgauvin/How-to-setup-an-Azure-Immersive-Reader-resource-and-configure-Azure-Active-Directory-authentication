# How to setup an Azure Immersive Reader resource and configure Azure Active Directory authentication
This repository documents the manual creation of an Azure Immersive Reader resource in the Azure portal and configure Azure Active Directory authentication. 

![](./images/2022-03-08-13-31-00.png)

## Introduction

The Azure Immersive Reader is a helpful resource that allows you to embed an accessible text reader with features like reading aloud, translating languages, focusing attention through highlighting, etc. More documentation can be found [here](https://docs.microsoft.com/en-us/azure/applied-ai-services/immersive-reader/).

## How to create the resources

Creating the Azure Immersive Reader requires the configuration of Azure Active Directory permissions. This is because the Immersive Reader only works with Azure AD permissions (it does not support authentication with connection strings, managed identities, or access tokens).

The steps to create the Immersive Reader resource and configure the Azure AD authentication are documented [on the Microsoft Docs](https://docs.microsoft.com/en-us/azure/applied-ai-services/immersive-reader/how-to-create-immersive-reader). However, I encountered issues when running the PowerShell script due to breaking changes in the APIs. Therefore, I researched how to create the Immersive Reader resources manually through the Azure Portal and am documenting it here to help make it easier to create the resources.  

## Prerequisites

* An Azure account with the necessary permissions as documented here https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal
* A resource group in which you will create the resources

## Getting Started

1. In the Azure Portal, create a `Immersive Reader` resource by searching for Immersive Reader.     
    ![](./images/2022-03-08-13-44-29.png)

2. Navigate to `Azure Active Directory` by searching for `Azure Active Directory`. 
    ![](./images/2022-03-08-13-52-11.png)

3. Navigate to `App Registrations`
    ![](./images/2022-03-08-13-56-05.png)

4. Create new registration
    ![](./images/2022-03-08-13-54-02.png)

5. Take note of the **Application (client) ID** and the **Directory (tenant) ID** (hidden here for security purposes)
![](./images/2022-03-08-14-14-02.png)

6. Navigate to `Certificates & secrets` witin the app registration
    ![](./images/2022-03-08-14-10-35.png)

7. Create new client secret
    ![](./images/2022-03-08-14-11-19.png)

8. Note the **secret value** (you can only copy it upon creation, so store it well)
    ![](./images/2022-03-08-14-12-23.png)

9. Return to the Immersive Reader resource and note the **subdomain of your endpoint**
    ![](./images/2022-03-08-14-15-20.png) 

10. Go to the `Access control (IAM)` of the Immersive Reader resource
    ![](./images/2022-03-08-14-17-07.png)

11. Add role assignment
    ![](./images/2022-03-08-14-16-43.png)

12. Select `Cognitive Services Immersive Reader User`
    ![](./images/2022-03-08-14-18-12.png)

13. Assign access to the Azure AD app registration you created previously
    ![](./images/2022-03-08-14-19-12.png)

14. Review & assign

15. You may now use the Immersive Reader resources as documented in the [quickstart guides](https://docs.microsoft.com/en-us/azure/applied-ai-services/immersive-reader/quickstarts/client-libraries?pivots=programming-language-nodejs). You have taken note of the tenant id (in step 5), the client id (in step 5), the client secret (in step 8), the subdomain (in step 9). You will need these to use the Immersive Reader SDK.
