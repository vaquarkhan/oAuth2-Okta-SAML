## OAuth2-Okta-SAML


## JWT:
JSON Web Tokens are an open, industry standard RFC 7519 method for representing claims securely between two parties.


![Alt Text](https://backstage.forgerock.com/docs/am/7/oauth2-guide/images/oauth2-jwt-bearer-authn.svg)

### Token 
![Alt Text](https://research.securitum.com/wp-content/uploads/sites/2/2019/10/jwt_ng1_en.png)
The issuer returns a signed JWT to the client. The JWT must contain, at least, the following claims in the payload:

         - iss. Specifies the unique identifier of the JWT issuer. This could also be the client, or a third party.

         - sub. Specifies the principal who is the subject of the JWT. Must be set to the client ID.

         - aud. Specifies the authorization server that is the intended audience of the JWT. Must be set to the authorization server's token endpoint. For example,            https://openam.example.com:8443/openam/oauth2/realms/root/access_token.

         - exp. Specifies the expiration time,providing a JWT with an expiry time greater than 30 minutes causes AM to return a JWT expiration time is unreasonable error message.

         - jti. Specifies a random, unique identifier for the JWT.


### What problem JWT solve :

HTTP is a stateless protocol, when a user makes a request that requires authentication to  web application they will have to pass in their credentials so we can implement a state mechanism, which brings us to sessions

 - Server side session : Server creates a session object on authenication which contains a unique session id, session expiry date, information about the user such as the user id, and any other information you may want to store.

                                    { 
                                            "id": "qw1e34rt5y", 
                                            "userId": "abcdxxxaasa",  
                                            "username": "vkhan", 
                                            "loginAttempts": 1,
                                            "expiryDate": "2021-07-08T23:28:56.782Z"
                                    }
  ### Issue with session managment 
                  Problem : If application scale up load balancer can forward call to any server and session management happened in one server 
                  Solution :  use Redis cache and save all session into Redis so all server can access it.

                  Problem :Redis cache single point of failure , if raids down all session gone
                  Solution use sticky session on load balancer 
                  
  When request JWT to the server then  server will then create a token with a secret key and send it back. The browser stores this token and sends it in the Authorization header   of every subsequent request.

### Understand JWT in debug
- https://jwt.io/

------------------------------------
## OAuth 2.0

The OAuth 2.0 authorization framework is a protocol that allows a user to grant a third-party web site or application access to the user's protected resources.

------------------------------------

### OAuth Terminology

- Access token - A token used to access protected resources.

- Authorization code - An intermediary token generated when a user authorizes a client to access protected resources on their behalf. The client receives this token and exchanges it for an access token.

- Authorization server - A server which issues access tokens after successfully authenticating a client and resource owner, and authorizing the request.
Client - An application which accesses protected resources on behalf of the resource owner (such as a user). The client could be hosted on a server, desktop, mobile or other device.

- Grant - A grant is a method of acquiring an access token, following are grant type.
            - Authorization code grant
            - Implicit grant
            - Client credentials grant
            - Resource owner password credentials grant
            - Refresh grant

![Alt Text]https://oauth2.thephpleague.com/images/grants.min.svg)

Grant flow (courtesy: oauth2.thephpleague.com).


- Resource server - A server which sits in front of protected resources (for example “tweets”, users’ photos, or personal data) and is capable of accepting and responding to protected resource requests using access tokens.
- 
- Resource owner - The user who authorizes an application to access their account. The application’s access to the user’s account is limited to the “scope” of the authorization granted (e.g. read or write access).

- Scope - A permission.
-
- JWT - A JSON Web Token is a method for representing claims securely between two parties as defined in RFC 7519.


### Role
 
- Resource Owner − Resource owner is defined as an entity having the ability to grant access to their own data hosted on the resource server. When the resource owner is a person, it is called the end-user. 
- 
- Client Application − Client is an application making protected resource requests to perform actions on behalf of the resource owner.

- Resource Server − Resource server is API server that can be used to access the user's information. It has the capability of accepting and responding to protected resource requests with the help of access tokens.

- Authentication Server − The authentication server gets permission from the resource owner and distributes the access tokens to clients, to access protected resource hosted by the resource server.


### Scopes
Scopes are what you see on the authorization screens when an app requests permissions. They’re bundles of permissions asked for by the client when requesting a token. These are coded by the application developer when writing the application.


# OAuth 2.0 Flows
         1. Authorization Code Flow
         2. Implicit Flow
         3. Resource Owner Password Credentials Flow
         4. Client Credentials Flow
         5. Refresh Token Flow

- https://darutk.medium.com/diagrams-and-movies-of-all-the-oauth-2-0-flows-194f3c3ade85


------------------------------------
# JWT VS OAUTH

-  https://github.com/vaquarkhan/vaquarkhan/wiki/JWT-vs-OAuth

------------------------------------
# OKTA

------------------------------------


- https://oauth2.thephpleague.com/
- https://www.tutorialspoint.com/oauth2.0
- https://www.deviantart.com/developers/authentication
- https://developer.okta.com/blog/2017/06/21/what-the-heck-is-oauth
- http://www.passportjs.org/docs/
