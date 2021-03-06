---
type: landing
directory: developer-docs/singlesignon
title: Tokens
page_title: Tokens
description: Tokens for single sign on process
published: true
allowSearch: true
---


Token is aone of the basic component of any surce code. Tokens are used to describe the characters in a code. For single sign process in Sunbird, JSON (JWT) web token is used. JWT (pronounced "jot") is used in the protocol to generate signed tokens which can be verified by the Receiving Party (RP). A JWT is a signed token containing claims from the sender to the recipient. Because the token is signed by the sender, the recipient can be sure that the token has not been tampered. For a more detailed overview of JWTs see: [https://jwt.io/introduction/](https://jwt.io/introduction/)

To authenticate with Sunbird via SSO (Single Sign-on), a JWT provided to the auto-login end point must contain the following fields (also known as claims) in its payload: 

* jti: a unique id of the token, can be any string generated by the sender which is unique

* iss: the issuer of the JWT, the id of the registered client 

* sub: the subject of the token, the user id of the person who will log in on Sunbird

* aud: the consumer of the token, for now this is [https://www.ntp.in](https://www.ntp.in)

* nbf: not before, the earliest time when the token can be used (expressed as the number of seconds since epoch in GMT). The nbf time cannot be in the future

* exp: expires, the timestamp at which the token expires (expressed as the number of seconds since epoch in GMT). The exp time cannot be more than 600 seconds after the nbf time

* name: the name of the person whose user id is in sub

* email: the email of the person whose user id is in sub

* email_verified: whether the email id has been verified. Only Verified emails are accepted on Sunbird 

* phone_number: 10-digit phone number of the person whose user id is in sub. This field is optional

* phone_number_verified: whether the phone number has been verified. Only Verified phone numbers are accepted on Sunbird. This field is optional

* redirect_uri: the url of the page where the user should be directed after login

### Base Url

The base url for Sunbird staging will be https://staging.opensunbird.net.in

### Signature

The payload described must be signed before sending it the authentication endpoint. The JWT specification permits signing in via HMAC, RSA or ECDSA algorithms. For this authentication end-point, the only permitted algorithm will be RSA signing via a private key. The corresponding public key will be provided during registration of the client. 

To read further on creating a RSA-signed JWT in Java see: [https://connect2id.com/products/nimbus-jose-jwt/examples/jwt-with-rsa-signature](https://connect2id.com/products/nimbus-jose-jwt/examples/jwt-with-rsa-signature))
