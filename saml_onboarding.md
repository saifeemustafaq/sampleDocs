# Onboarding Guide for SAML Flow in Harness Platform

## Introduction

Harness is a powerful platform designed to streamline continuous delivery processes, enabling teams to deploy applications efficiently and reliably. Security and seamless user authentication are critical components of any enterprise application, and Harness supports Single Sign-On (SSO) through the Security Assertion Markup Language (SAML). This guide provides a comprehensive onboarding tutorial for setting up and configuring SAML authentication in the Harness Platform.

## Table of Contents

1. **Overview of SAML**
    - What is SAML?
    - Benefits of SAML Authentication
2. **Pre-requisites**
    - Required Information and Tools
3. **Configuring SAML in Harness**
    - Step-by-Step Configuration Guide
4. **Identity Provider (IdP) Configuration**
    - Setting Up IdP for SAML
5. **Testing and Troubleshooting**
    - Common Issues and Solutions
6. **Advanced Configuration**
    - Custom Attributes and Mappings
7. **Best Practices and Security Considerations**
8. **Conclusion**

## 1. Overview of SAML

### What is SAML?

Security Assertion Markup Language (SAML) is an open standard for exchanging authentication and authorization data between parties, specifically between an identity provider (IdP) and a service provider (SP). It enables Single Sign-On (SSO), allowing users to log in once and gain access to multiple applications.

### Benefits of SAML Authentication

- **Improved User Experience**: Users can log in once and access multiple applications without needing to re-enter credentials.
- **Enhanced Security**: Centralized authentication mechanisms and reduced password fatigue for users.
- **Ease of Management**: Simplified user account management and improved compliance with security policies.

## 2. Pre-requisites

### Required Information and Tools

Before configuring SAML authentication in Harness, ensure you have the following:

- An active Harness account with administrative privileges.
- Access to your organization's Identity Provider (IdP) (e.g., Okta, Azure AD, OneLogin).
- The following information from your IdP:
  - **IdP Entity ID**
  - **IdP SSO URL**
  - **IdP Certificate** (X.509)
- Basic understanding of SAML and SSO concepts.

## 3. Configuring SAML in Harness

### Step-by-Step Configuration Guide

1. **Log in to Harness**:
   - Navigate to your Harness account and log in using your administrative credentials.

2. **Access Authentication Settings**:
   - In the Harness dashboard, go to `Account Settings` -> `Authentication`.

3. **Enable SAML Authentication**:
   - Locate the `SAML Authentication` option and toggle it to enable.

4. **Configure SAML Settings**:
   - Enter the following details obtained from your IdP:
     - **IdP Entity ID**: This is the unique identifier for your IdP.
     - **IdP SSO URL**: This is the URL endpoint where the SAML requests will be sent.
     - **IdP Certificate**: Upload the X.509 certificate provided by your IdP.

5. **Service Provider (SP) Configuration**:
   - Harness will generate the following details that need to be configured in your IdP:
     - **SP Entity ID**: Unique identifier for Harness.
     - **ACS URL (Assertion Consumer Service URL)**: The URL where SAML assertions are sent after authentication.
     - **RelayState**: Optional parameter to maintain state across requests.

6. **Save and Test Configuration**:
   - Save the configuration and proceed to test the SAML authentication setup.

## 4. Identity Provider (IdP) Configuration

### Setting Up IdP for SAML

Each IdP has its own interface and process for configuring SAML applications. Below, we outline the general steps and provide specific instructions for popular IdPs like Okta, Azure AD, and OneLogin.

### Okta Configuration

1. **Log in to Okta**:
   - Access the Okta admin console with your administrative credentials.

2. **Create a New SAML Application**:
   - Navigate to `Applications` -> `Add Application`.
   - Choose `Create New App` and select `SAML 2.0`.

3. **Configure General Settings**:
   - Enter the application name and optional logo.
   - Click `Next`.

4. **Configure SAML Settings**:
   - Enter the `SP Entity ID` and `ACS URL` from Harness.
   - Set the `Name ID format` to `EmailAddress`.
   - Map attributes as needed (e.g., `email`, `firstName`, `lastName`).

5. **Configure Feedback**:
   - Select `I'm an Okta customer adding an internal app`.
   - Click `Finish`.

6. **Download IdP Metadata**:
   - Download the IdP metadata file or note down the `IdP Entity ID`, `IdP SSO URL`, and `IdP Certificate`.

### Azure AD Configuration

1. **Log in to Azure Portal**:
   - Access the Azure portal and log in with your administrative credentials.

2. **Create a New Enterprise Application**:
   - Navigate to `Azure Active Directory` -> `Enterprise applications`.
   - Click `New application` and select `Non-gallery application`.
   - Enter the application name and create the app.

3. **Configure Single Sign-On**:
   - Under the `Single sign-on` section, select `SAML`.

4. **Basic SAML Configuration**:
   - Enter the `Identifier (Entity ID)` and `Reply URL (ACS URL)` from Harness.
   - Set the `Sign on URL` to your Harness instance URL.

5. **User Attributes & Claims**:
   - Configure necessary attributes (e.g., `user.email`, `user.givenname`, `user.surname`).

6. **Download IdP Metadata**:
   - Download the IdP metadata file or note down the `IdP Entity ID`, `IdP SSO URL`, and `IdP Certificate`.

### OneLogin Configuration

1. **Log in to OneLogin**:
   - Access the OneLogin admin console with your administrative credentials.

2. **Create a New SAML Application**:
   - Navigate to `Applications` -> `Add App`.
   - Search for `SAML Test Connector (IdP w/attr)` and select it.

3. **Configure SAML Settings**:
   - Enter the `SP Entity ID` and `ACS URL` from Harness.
   - Map the required attributes (e.g., `NameID`, `email`, `firstname`, `lastname`).

4. **Download IdP Metadata**:
   - Download the IdP metadata file or note down the `IdP Entity ID`, `IdP SSO URL`, and `IdP Certificate`.

## 5. Testing and Troubleshooting

### Common Issues and Solutions

1. **Invalid Certificate**:
   - Ensure the certificate uploaded in Harness matches the one provided by the IdP.
   - Check for any extra spaces or line breaks in the certificate file.

2. **Mismatched Entity ID**:
   - Verify that the `IdP Entity ID` in Harness matches the value configured in your IdP.

3. **SSO URL Errors**:
   - Ensure the `IdP SSO URL` is correctly entered and accessible.
   - Check network connectivity and firewall settings.

4. **Attribute Mapping Issues**:
   - Confirm that the attribute names and values are correctly mapped in your IdP configuration.
   - Ensure mandatory attributes like `email` are included.

### Testing SAML Authentication

- Use an incognito or private browsing window to test the SAML authentication flow.
- Attempt to log in to Harness using SSO and verify that you are redirected to your IdP for authentication.
- Upon successful authentication, ensure you are redirected back to Harness and logged in.

## 6. Advanced Configuration

### Custom Attributes and Mappings

Harness supports custom attribute mappings, allowing you to pass additional user information from the IdP to Harness. This can be useful for roles, department information, and other custom data.

1. **Define Custom Attributes in IdP**:
   - Add custom attributes in your IdP configuration (e.g., `department`, `role`).

2. **Map Custom Attributes in Harness**:
   - Go to `Account Settings` -> `Authentication` in Harness.
   - Under the `SAML Configuration` section, map the custom attributes to their corresponding values from the IdP.

### Multiple IdP Support

Harness allows configuration of multiple IdPs to support diverse user bases and scenarios.

1. **Add Additional IdPs**:
   - Repeat the configuration steps for each additional IdP.
   - Ensure each IdP has unique identifiers and settings to avoid conflicts.

2. **IdP Discovery**:
   - Configure IdP discovery mechanisms to route users to the appropriate IdP based on email domain or other criteria.

## 7. Best Practices and Security Considerations

### Strong Encryption

- Ensure the SAML assertions are encrypted to prevent tampering and interception.
- Use strong, up-to-date encryption algorithms for SAML responses.

### Regular Certificate Rotation

- Regularly update and rotate your IdP certificates to maintain security.
- Schedule periodic reviews and updates of your SAML configuration.

### Audit and Monitoring

- Enable logging and monitoring for SAML authentication events in both Harness and your IdP.
- Regularly review audit logs for suspicious activity and unauthorized access attempts.

### User Education

- Educate users on the SAML SSO process and the importance of using their organizational credentials.
- Provide clear instructions on how to access support for authentication issues.

## 8. Conclusion

Configuring SAML authentication in Harness enhances security and user experience by enabling seamless Single Sign-On capabilities. By following this comprehensive onboarding guide, you can ensure a smooth and secure setup process. Regular maintenance
