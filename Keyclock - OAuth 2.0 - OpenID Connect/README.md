# 🔐 Keycloak - OAuth 2.0 - OpenID Connect

## Basics

Articles, videos and SO question to help you understand the basics and clear up things:

- ▶️ [An Illustrated Guide to OAuth and OpenID Connect](https://www.youtube.com/watch?v=t18YB3xDfXI) by OktaDev and [David Neal](https://twitter.com/reverentgeek), also blogpost here: [An Illustrated Guide to OAuth and OpenID Connect](https://developer.okta.com/blog/2019/10/21/illustrated-guide-to-oauth-and-oidc)
- 📝 [Introduction to JSON Web Tokens](https://jwt.io/introduction)
- ▶️ [ID Tokens VS Access Tokens: What's the Difference?](https://www.youtube.com/watch?v=vVM1Tpu9QB4) by OktaDev, also blogpost here: [ID Token and Access Token: What's the Difference?](https://auth0.com/blog/id-token-access-token-what-is-the-difference/) (see the notes below)
- ❔ [If you can decode JWT, how are they secure?](https://stackoverflow.com/questions/27301557/if-you-can-decode-jwt-how-are-they-secure) from Stackoverflow
- ❔ [Is it necessary to encrypt a JSON Web Token more than what is built-in?](https://security.stackexchange.com/questions/236531/is-it-necessary-to-encrypt-a-json-web-token-more-than-what-is-built-in) from Security.StackExchange
-  https://www.baeldung.com/postman-keycloak-endpoints




#### ID Token notes (from OktaDev):

 - It is **required** to be in the format of a JWT token
 - We **don't** send an ID Token to an `API` because:
     - ID Tokens are **NOT** meant for authorization
     - ID Tokens should **NOT** be sent to an API
     - ID Tokens do **NOT** have authorization information inside of them


#### Access Token notes:
 - Access tokens are **NOT** used for authentication
 - Access tokens do **NOT** guarantee that a user is logged in


## React:

 - 📝 [React Authentication By Example: Using React Router 6](https://developer.auth0.com/resources/guides/spa/react/basic-authentication)
 - [Keycloak React.JS Demo](https://github.com/dasniko/keycloak-reactjs-demo) by Niko Köbler ([@dasniko](https://github.com/dasniko))


## Fastapi (hands-on example):

 - [FastAPI Keycloak Integration](https://fastapi-keycloak.code-specialist.com/) by code-specialist.com



## Architectures:

 - [How to Build a Full-Stack Authentication App](https://api7.ai/blog/build-full-stack-authetication-app)

![](https://static.apiseven.com/uploads/2023/08/23/LgABNvi8_Global%20Community%20Meeting%20slides%20%281%29.png?imageMogr2/format/webp)

Notes on steps 4 - 5 - 6:

 4. Before processing the request, the APISIX needs to ensure that the provided token is valid, has not expired, and has the right scopes for the requested data or service. **If the APISIX cannot locally validate the token,** it sends the token introspection request to the Authgear authorization server. This request is typically made to the introspection endpoint of the server.
 5. The Authgear receives the introspection request and processes it. The server checks its records to determine the token's validity, its expiration, and associated scopes, and after determining the token’s state, it responds to APISIX.
 6. Based on Authgear’s token introspection response, the APISIX can then make an informed decision. If the token is valid, it forwards the request to the backend API, otherwise, it rejects the client’s request with an unauthorized HTTP status code.


# Questions:

> ❔ What's the point of creating **protected routes** with keycloak in a react app? Isn't the authentication/authorization supposed to always take place a the backend?

✅ While the backend is the ultimate authority for authorization decisions, performing some level of authorization on the frontend ensures that users only see the UI elements and routes that they are allowed to access. This can reduce the likelihood of making unnecessary API requests to protected endpoints. 👇

✅ **Performance Benefits**: Caching certain user information on the frontend can lead to performance benefits, as the application doesn't need to make frequent requests to the backend to determine the user's authentication status.

**Important Consideration**: While frontend authentication can offer these benefits, it's crucial to perform critical authorization checks on the **backend** to ensure the security of your application. Frontend checks should be considered as an optimization and UI enhancement, but the backend should be the ultimate authority for access control decisions.


> ❔ About JWT token `decode` vs `introspect`: Consider a React UI that uses `keycloak.js` and a keycloak instance for user authentication and authorization. When it comes to the backend service which is a Python Fastapi implementation, there can be 2 approaches:
> 
> - The first is using `decode`, something like `jwt.decode(token)`
> - The second is using `introspection`, something like `keycloak_openid.introspect(token)`
>
> Which one is the correct approach for securing your backend?


Both approaches have their own use cases and considerations.

### 1. Decoding JWT Token:

**How it works:**

-   Decoding the JWT token involves extracting and inspecting the claims (payload) of the token directly without contacting the authorization server.
-   Typically, libraries like `jwt.decode(token)` are used to decode the token and retrieve information such as user ID, roles, and other claims.

**Suitability:**

-   This approach is suitable when you want to validate the token's integrity and extract basic information without additional round-trips to the authorization server.
-   It's efficient for scenarios where the token is self-contained and contains all necessary information for authorization.

**Considerations:**

-   **Token Expiry:** You need to ensure that the token hasn't expired by checking the `exp` claim.
-   **Token Signature:** While decoding, ensure the token's signature is valid by using the appropriate verification key.
-   **Limited Information:** Decoding only provides information present in the token itself. If you need more dynamic or detailed information (like updated user roles), you may need token introspection.

### 2\. Token Introspection:

**How it works:**

-   Token introspection involves sending the token to the authorization server for validation and retrieving additional information about the token's validity and associated user.
-   This is done by making an HTTP request to the authorization server's introspection endpoint, typically something like `/auth/realms/{realm}/protocol/openid-connect/token/introspect`.

**Suitability:**

-   This approach is suitable when you need to verify the token's validity, check its status (active or revoked), and obtain dynamic user information (e.g., updated roles) from the authorization server.
-   It's useful in scenarios where token lifetimes may be long, and you need to ensure the token is still valid at the time of processing.

**Considerations:**

-   **Network Overhead:** Introspection involves an additional HTTP request to the authorization server, which introduces network overhead and latency.
-   **Authorization Server Dependency:** Your backend service relies on the availability and responsiveness of the authorization server for token validation.
-   **Security Concerns:** Introspection requests should be made securely with appropriate authentication and authorization to the authorization server's introspection endpoint.

### Recommendation:

-   For most use cases, especially where token lifetimes are short and the information in the token is sufficient for authorization, decoding the JWT token directly can be efficient and straightforward.
-   However, if your application requires real-time validation of token status or dynamic user information, token introspection might be necessary despite the added network overhead and dependency on the authorization server.

Ultimately, the choice depends on your specific requirements regarding security, performance, and the level of dynamic information needed for authorization in your backend service.


> ❔ Which is more secure?

Determining which approach is the most secure depends on various factors and considerations related to your specific application's security requirements and architecture. Let's evaluate the security aspects of both approaches:

### Decoding JWT Token:

**Security Aspects:**

1.  **Token Integrity:** Decoding the JWT token directly allows you to verify the token's integrity by checking its signature. If the signature is valid, it ensures that the token has not been tampered with.
2.  **Reduced Dependency:** Since decoding the token doesn't involve additional network requests to an external service (like introspection), it reduces the dependency on external components, potentially minimizing attack surface.
3.  **Limited Exposure:** Decoding only exposes the information contained within the token itself, reducing the risk of exposing sensitive data to external services.

**Considerations:**

-   **Token Expiry:** Ensuring that the token hasn't expired is crucial, as expired tokens should not be considered valid.
-   **Proper Key Management:** Proper management of the JWT signing keys is essential to prevent unauthorized tampering with tokens.

### Token Introspection:

**Security Aspects:**

1.  **Real-time Validation:** Introspection allows for real-time validation of tokens against the authorization server, ensuring their current validity status.
2.  **Dynamic Updates:** Introspection enables retrieval of dynamic user information from the authorization server, such as updated roles or permissions, enhancing security by ensuring that the most current user attributes are used for access control.
3.  **Revocation Checks:** Introspection can check if a token has been revoked, providing an additional layer of security, especially in scenarios where token revocation is necessary (e.g., compromised tokens).

**Considerations:**

-   **Network Security:** Introspection involves making HTTP requests to an external service, which introduces network-related security considerations such as encryption (HTTPS) and proper endpoint authentication.
-   **Authorization Server Dependency:** Introspection relies on the availability and security of the authorization server, which introduces a potential single point of failure and additional attack vectors.

### Conclusion:

-   Both approaches can be secure when implemented correctly and based on your specific security requirements.
-   Decoding JWT tokens directly may be considered more secure in some scenarios due to reduced external dependencies and potential attack vectors.
-   However, token introspection offers advantages such as real-time validation, dynamic updates, and revocation checks, which can be crucial for certain applications, especially those requiring high levels of dynamic access control.

Ultimately, the most secure approach depends on balancing security requirements, performance considerations, and architectural constraints within your application ecosystem. It's essential to thoroughly evaluate the security implications and choose the approach that best aligns with your application's needs.
