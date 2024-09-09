# Multi-Factor Authentication

Multi-factor authentication (MFA) is a security process that requires users to provide two or more verification factors to gain access to a system, application, or account. This adds an extra layer of protection beyond just using a password.

By requiring more than one verification method, MFA helps reduce the risk of unauthorized access, even if someone has obtained your password. It’s highly recommended for securing sensitive information stored in your notes.

Warning! OpenID and TOTP cannot be both used at the same time!

## Log in with your Google Account with OpenID!

OpenID is a standardized way to let you log into websites using an account from another service, like Google, to verify your identity.

## Why Time-based One Time Passwords?

TOTP (Time-Based One-Time Password) is a security feature that generates a unique, temporary code on your device, like a smartphone, which changes every 30 seconds. You use this code, along with your password, to log into your account, making it much harder for anyone else to access them.

## Setup

### TOTP

1. Start Trilium Notes normally.
1. Go to "Menu" -> "Options" -> "MFA"
1. Click the "Generate TOTP Secret" button
1. Copy the generated secret to your authentication app/extension
1. Set an environment variable "TOTP_SECRET" as the generated secret. Environment variables can be set with a .env file in the root directory, by defining them in the command line, or with a docker container.
    ```SH
    # .env in the project root directory
    TOTP_ENABLED="true"
    TOTP_SECRET="secret"
    ```
    ```SH
    # Terminal/CLI
    export TOTP_ENABLED="true"
    export TOTP_SECRET="secret"
    ```
    ```SH
    # Docker
    docker run -p 8080:8080 -v ~/trilium-data:/home/node/trilium-data -e TOTP_ENABLED="true" -e TOTP_SECRET="secret" triliumnext/notes:[VERSION]
    ```
1. Restart Trilium
1. Go to "Options" -> "MFA"
1. Click the "Generate Recovery Codes" button
1. Save the recovery codes. Recovery codes can be used once in place of the TOTP if you loose access to your authenticator. After a rerecovery code is used, it will show the unix timestamp when it was used in the MFA options tab.
1. Load the secret into an authentication app like google authenticator


### OpenID
_Currently only compatible with Google. Other services like Authentik and Auth0 are planned on being added._

In order to setup OpenID, you will need to setup a authentication provider. This requires a bit of extra setup. Follow [these instructions](https://developers.google.com/identity/openid-connect/openid-connect) to setup an OpenID service through google.

Set an environment variable "SSO_ENABLED" to true and add the client ID and secret you obtained from google. Environment variables can be set with a .env file in the root directory, by defining them in the command line, or with a docker container.

#### .env File
```sh
# .env in the project root directory
SSO_ENABLED="true"
BASE_URL="http://localhost:8080"
CLIENT_ID=<client ID from google>
SECRET=<client secret from google>
```

#### Environment variable (linux)
```sh
export SSO_ENABLED="true"
export BASE_URL="http://localhost:8080"
export CLIENT_ID=<client ID from google>
export SECRET=<client secret from google>
```
#### Docker
```sh
docker run -d -p 8080:8080 -v ~/trilium-data:/home/node/trilium-data -e SSO_ENABLED="true" -e BASE_URL="http://localhost:8080" -e CLIENT_ID=<client ID from google> -e SECRET=<client secret from google> triliumnext/notes:[VERSION]
```
After you restart Trilium Notes, you will be redirected to Google's account selection page. Login to an account and Trilium Next will bind to that account, allowing you to login with it. 

You can now login using your google account. 

