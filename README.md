# SC-500 Lab Runbook: Secure an Enterprise Application with Microsoft Entra ID

---

# Lab Information

| Item | Details |
|------|---------|
| *Lab* | SC-500 Lab 02 |
| *Title* | Secure an Enterprise Application with Microsoft Entra ID |
| *Technology* | Microsoft Entra ID, ASP.NET Core, Microsoft Identity Platform, Visual Studio Code |
| *Objective* | Configure an ASP.NET Core web application to authenticate users through Microsoft Entra ID using modern authentication and centralized identity management. |

---

# Business Scenario

An organisation intends to deploy an internal web application that will be accessed by employees across different departments. Rather than creating and managing separate usernames and passwords within the application, the organisation wants users to authenticate using their existing Microsoft Entra ID accounts.

By integrating the application with Microsoft Entra ID, authentication is centralized, allowing administrators to manage user identities, enforce security policies such as Multi-Factor Authentication (MFA) and Conditional Access, and provide a seamless Single Sign-On (SSO) experience across enterprise applications.

---

# Prerequisites

- Microsoft Entra ID tenant
- Global Administrator or Application Administrator role
- Registered ASP.NET Core web application
- Visual Studio Code
- .NET SDK installed
- Internet connectivity
- Microsoft.Identity.Web package

---

# Runbook

---

# Step 1: Register the Enterprise Application

## Definition

An *Application Registration* creates a trusted identity for an application within Microsoft Entra ID. This registration enables Microsoft Entra ID to recognise the application whenever users attempt to authenticate.

Without registering the application, Microsoft Entra ID cannot establish trust or issue authentication tokens.

## Procedure

1. Sign in to the Microsoft Entra admin center.
2. Navigate to:


Identity
   └── Applications
        └── App registrations


3. Select *New registration*.
4. Enter the application name.
5. Choose the appropriate supported account type.
6. Complete the registration.

## Expected Result

The application is successfully registered and receives:

- Application (Client) ID
- Directory (Tenant) ID
- Object ID

These identifiers uniquely represent the application within Microsoft Entra ID.

*Screenshot*

![Application Registration](images/ENTRA-APP-Registration-Created.png)

---

# Step 2: Configure the Redirect URI

## Definition

A *Redirect URI* specifies the destination to which Microsoft Entra ID returns users after successful authentication. Only registered Redirect URIs are trusted, preventing authentication responses from being sent to unauthorized locations.

## Procedure

1. Open the registered application.
2. Select *Authentication*.
3. Click *Add a platform*.
4. Select *Web*.
5. Configure the Redirect URI:


https://localhost/signin-oidc


6. Save the configuration.

## Expected Result

The Redirect URI is successfully configured and associated with the application.

*Screenshot*
![Redirect URI Configuration](images/
ENTRA-Authentication-RedirectURI-Configured.png)

---

# Step 3: Create a Client Secret

## Definition

A *Client Secret* is a confidential credential used by an application to authenticate itself with Microsoft Entra ID. It functions similarly to an application password and is required when requesting authentication tokens.

## Procedure

1. Navigate to:


Certificates & secrets


2. Select *New client secret*.
3. Provide a description.
4. Select an expiration period.
5. Create the secret.
6. Copy the *Value* immediately and store it securely.

> *Security Note:* The Client Secret value is displayed only once. It should never be committed to source control or shared publicly.

## Expected Result

A Client Secret is successfully created and ready to be used by the application.

*Screenshot*
![Client Secret Created](images/
ENTRA-Client-Secret-Created.png)

---

# Step 4: Configure the ASP.NET Core Application

## Definition

The ASP.NET Core application must be configured to trust Microsoft Entra ID as its identity provider. This enables the application to redirect users for authentication and validate identity tokens returned after successful sign-in.

## Procedure

1. Open the project in Visual Studio Code.
2. Configure the *appsettings.json* file by adding:
   - Tenant ID
   - Client ID
   - Client Secret
   - Callback Path
3. Update *Program.cs* to:
   - Configure Microsoft Identity Web.
   - Enable OpenID Connect authentication.
   - Register authentication and authorization services.

## Expected Result

The application is successfully configured to authenticate users through Microsoft Entra ID.

*Screenshot*

![Program.cs Configuration](images/
VSCODE-ProgramCS-EntraID-Authentication-Configured.png)

---

# Step 5: Build and Launch the Application

## Definition

Building the application compiles the source code, restores dependencies, and verifies that the Microsoft Entra ID configuration has been correctly integrated.

## Procedure

Open the integrated terminal and execute:

bash
dotnet run


Verify that the terminal displays:


Now listening on:
http://localhost:5182


## Expected Result

The application builds successfully and starts listening for incoming requests.

*Screenshot*

![Application Build Success](images/
VSCODE-WebApp-Build-Success.png)

---

# Step 6: Validate the Deployment

## Definition

Validation confirms that the application is operational after integrating Microsoft Entra ID and is ready for authentication testing.

## Procedure

1. Open a web browser.
2. Navigate to:


http://localhost:5182


3. Verify that the ASP.NET Core application loads successfully.

## Expected Result

The web application opens successfully without errors, confirming that the deployment is functioning correctly.

*Screenshot*

![Application Running](images/
VSCODE-WebApp-Running-Browser.png)

---

# Validation Checklist

- ✅ Enterprise application successfully registered.
- ✅ Redirect URI configured correctly.
- ✅ Client Secret generated successfully.
- ✅ ASP.NET Core application configured for Microsoft Entra ID.
- ✅ Authentication services configured successfully.
- ✅ Application built without errors.
- ✅ Web application launched successfully.
- ✅ Deployment validated through browser testing.

---

# Knowledge Gained

Upon completing this lab, the following knowledge and skills were developed:

- Understood the purpose of Application Registration in Microsoft Entra ID.
- Learned how Redirect URIs support secure OpenID Connect authentication.
- Created and securely managed a Client Secret for application authentication.
- Configured an ASP.NET Core application to use Microsoft Entra ID.
- Integrated Microsoft Identity Web for centralized authentication.
- Successfully built, launched, and validated an enterprise application secured by Microsoft Entra ID.

---

# Business Benefits

Integrating enterprise applications with Microsoft Entra ID provides organisations with a centralized and secure identity platform that simplifies authentication while strengthening access control.

By completing this implementation, an organisation can:

- Centralize authentication using Microsoft Entra ID.
- Provide Single Sign-On (SSO) across enterprise applications.
- Enforce Multi-Factor Authentication (MFA) and Conditional Access policies.
- Reduce the risks associated with locally managed application credentials.
- Simplify user provisioning and deprovisioning through centralized identity management.
- Improve auditing, monitoring, and compliance with organisational security policies.
- Deliver a consistent and secure authentication experience for users across cloud-based applications.

---

# Conclusion

This lab successfully demonstrated how to secure an ASP.NET Core web application using Microsoft Entra ID. The application was registered, configured for OpenID Connect authentication, integrated with Microsoft Identity Web, and validated through successful deployment. This implementation illustrates how organisations can modernize application authentication by adopting centralized identity management, improving both security and operational efficiency.
