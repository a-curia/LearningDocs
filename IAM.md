# IAM - Identity and Access Management #


Authentication(**AuthN**)

- determines **who** the user **is**
- via OIDC, SAML, Docker Auth, Kerberos
- Internal & Federated User Storage - Kerberos, LDAP, Custom(internal user store or federated user store)


Authorization(**AuthZ**)

- determines **what** the user **is allowed** to do
- hierarchical Role-based Access Control (HRBAC)
- Authorization Services
	- Flexible Access Control Management
	- More Variants like ABAC(Attribute Based Access Control), UBAC(User Based Access Control), CBAC(Context Based Access Control) supported - dinamically determine which permissions the user has to do what it has to do



SSO - Single Sign-on and Single Sign-out


- SSO -> Login once to access all applications
- standardized Protocols
	- Open ID Connect 1.0 (OIDC)
	- Security Assertion Markup Language 2.0 (SAML)
- Browser based **"Web SSO"**
- works for Web, Mobile and Desktop Apps
- support for Single Sign-out
	- Logouts can be propagated to clients
	- Clients can opt-in(app client can decide to react to that or not)


SSO Protocols 

- OIDC 1.0
	- protocol based on Oauth 2.0
	- uses OAuth 2.0 tokens + IDtoken to encode Identity
	- Tokens are encoded as JSON Web Tokens (JWT)
	- Requires secure channel HTTPS/TLS
	

- SAML 2.0 Security Assertion Markup Language
	- very mature standard & common in enterprise environments
	- XML based protocol
	- uses XML signature and encryption -> no secure channel required; relies on XML security and encryption standards



***Web SSO with OIDS: Unauthenticated User***

![sso-oidc-unauthenticated-user](https://i.imgur.com/DJyG9wg.png)

App can verify those tokens by checking the signature of the token. The tokens are signed with a private key associated with a realm and the application has access to the public key and can then verity the signature. If everything is fine the application can establish a session and the user is logged ok from now on.


***Web SSO with OIDS: Authenticated User***
![sso-oidc-authenticated-user](https://i.imgur.com/Fp7ZLEe.png)


Tokens contain User information + Metadata
- signed self-contained JSON Web Tokens - value tokens - all user info is already encoded in the token(other option is by reference)
- issued by Keycloak, signed with Realm Private Key
- limited lifespan; can be revoked

Tokens can be verified by Clients
-  by checking their signature with Realm Public Key
-  or via a HTTP POST to Keycloaks /token_introspection_endpoint

Multiple Token Types

- **Access-Token**: short-lived(Minutes), used for accessing Resources
- **Refresh-Toke**: long-lived(Days), used for requesting new Tokens
- **Offline-token**: special Refresh-Token that "never" expires
- **IDToken**: contains information about User(OpenID Connect)

JWT is encoded not enctypted - in the header the "kid", key id reference the private/public key which was used to sign the token. Is used by the "Resource Serve" to determine which public key they must use to verify the signature. "sub" is the user id because it supports changeable username

Calling Backend Services with Access-Token
![callbeservice-with-access-token](https://i.imgur.com/aXc9rm2.png)




