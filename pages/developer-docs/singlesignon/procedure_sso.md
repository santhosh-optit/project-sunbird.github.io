---
type: landing
directory: developer-docs/singlesignon
title: Procedure
page_title: Procedure to Onboard Organizations
description: FIve step procedure to onboard organizations on Sunbird
published: true
allowSearch: true
---

## Procedure to Onboard Organizations

1. Generate RSA private and public key pair

2. Get public key registered in production

3. Create tenant organization

4. Create organizations, and users, and register

5. Single-Sign-On with Sunbird

### Generating RSA Private and Public Key Pair

To create a new pair of public/private keys, run the following command:

$ openssl genrsa -out private.pem 2048

This private key must be kept secret. To generate a public key corresponding to the private key, execute:

$ openssl rsa -in private.pem -outform PEM -pubout -out public.pem

If you run these commands, the public key will be written in public.pem, while the private key will be written in private.pem

### Accessing the APIs Using Token

The token generated should be sent in Authorization header of the request with value bearer <token>. Example curl request

curl -H "Authorization: Bearer <token>" https://staging.ntp.net.in/api/echo/hello

### Onboarding New Tenant Organization on Sunbird

Sunbird allows creation and configuration of multiple tenant organizations in a single instance:

* Every tenant organization has a unique channel, i.e. all the activities by users belonging to that tenant organization are tagged by the tenant's channel id (activities include content creation, content consumption, etc)

* Tenant organizations have the option to setup a custom home page and configure the logo to be displayed for users who belong to the tenant

* Tenant organizations can create multiple sub organizations and add users to those organizations

Example: Each state is a tenant on Sunbird and all schools/institutes in that state are created as sub-organizations under that tenant organization.

### Custom Homepage & Logo for Tenants

Sunbird supports over-riding of default home page and configuring a custom home page and logo for each on-boarded tenant. The tenant organization should provide package containing the following files for customising the home page and logo:

* The home page html file should be named index.html. All the dependent files (like js, css and images) used by the home page should be within the package and referred using relative paths from the "index.html".

* Logo of the tenant which should be with the name "logo.png"

* Optionally, tenants can also configure the following:

    * an icon (to be displayed as browser favicon) which should be named as "favicon.ico"

    * a poster image (to be used as flash screen in the mobile app) which should be named as "poster.png"

All the files should be placed in a folder. The folder name should be the same as the channel value of the tenant organization.

### Sign In link from Custom Home Page

Following link needs to be added at an appropriate place in the custom home page to invoke Sunbird portal login:
<a href="/private/index" title="Sign In"><span>Sign In</span></a>


