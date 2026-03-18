# Secure APIs using JWT (Self Contained) Access Tokens

WSO2 Integrator: MI supports RFC 9068-compliant, self-contained JWT access tokens as secure API credentials. JSON Web Token (JWT) is an open standard of transmitting information securely between two parties. Because these tokens are digitally signed, they provide a tamper-proof mechanism for transmitting authorization data directly within the request.

JWT access tokens are ideal as API credentials because they function as self-contained security assertions. By carrying specific claims such as resource scopes, intended audience, and issuer details, etc. directly within the token, they provide the necessary context for delegated authorization. This allows the WSO2 Integrator: MI to inspect the token’s internal data and enforce granular security policies locally, ensuring that requests are authorized based on the specific permissions granted by the user.

## Prerequisites for JWT based tokens

The following prerequisites have to be satisfied for JWT based tokens to work.

-   Only signed JWT access tokens are allowed.

-   The expected token format is as follows:

    `base64(header).base64(payload).base64(signature)`

-   Mandatory Claims: The token must include iss, sub, aud, jti, iat, and exp.

-   The JWT header should ideally contain "typ": "at+jwt" or "typ": "application/at+jwt" to indicate that the token is a JWT access token.

-   WSO2 Integrator: MI must have network access to the IdP's JSON Web Key Set (/jwks) endpoint for digital signature verification purposes. 
  
-   If using a static public key instead of JWKS, the IdP’s public certificate must be imported into the WSO2 Integrator: MI's truststore (client-truststore.jks) with the alias configured in the handler. For more information, see [Importing SSL certificates to a truststore.]({{base_path}}/install-and-setup/setup/security/importing-ssl-certificate/#importing-ssl-certificates-to-a-truststore)


## Mandatory attributes of a JWT access token

The following are the mandatory attributes that are required for a JWT access token.

- `Header`
   <table>
      <tbody>
         <tr>
            <td>`alg`</td>
            <td>The algorithm which signs the token (e.g., RS256).</td>
         </tr>
         <tr>
            <td>`typ`</td>
            <td>The media type of the complete JWS (e.g., at+jwt or application/at+jwt).</td>
         </tr>
      </tbody>
   </table>

- `Payload`
   <table>
      <tbody>
         <tr>
            <td>`sub`</td>
            <td>The subject of the token, which identifies as to whom the token refers to.</td>
         </tr>
         <tr>
            <td>`iat`</td>
            <td>Token issued time</td>
         </tr>
         <tr>
            <td>`exp`</td>
            <td>The expiry time of the token.</td>
         </tr>
         <tr>
            <td>`iss`</td>
            <td>The principal that issued the JWT.</td>
         </tr>
         <tr>
            <td>`aud`</td>
            <td>The recipients that the JWT is intended for.</td>
         </tr>
         <tr>
            <td>`jti`</td>
            <td>The unique identifier of the JWT.</td>
         </tr>
      </tbody>
   </table>

## Validation Pipeline

### 1. Header Metadata Validation
   Before verifying the signature, the handler inspects the JWT header for two critical security markers:

   - Type Check (`typ`): The handler confirms that the typ header is set to `at+jwt` (or `application/at+jwt`). This prevents "Token Confusion" attacks where an ID token might be mistakenly presented as an Access Token.

   - Algorithm Check (`alg`): The handler enforces the use of strong asymmetric algorithms (e.g., RS256). Any tokens using the `none` algorithm or weak symmetric algorithms (HMAC) are rejected immediately to prevent signature bypass.

### 2. Integrity & Authenticity Check

Once the header is validated, the process moves to **Digital Signature Verification**. Using the `kid` (Key ID) found in the JWT header, the handler retrieves the corresponding public key from the configured **JWKS endpoint**. This step confirms that the token was indeed issued by a trusted Identity Provider and has not been altered in transit. 

### 3. Temporal Policy Enforcement
   Once the signature is verified, the handler enforces time-based security policies. It validates the Expiration (`exp`) claim to ensure the token is currently active, while also checking the Issued-At (`iat`) claim. The `iat` check ensures the token is not "from the future" (accounting for the `clock_skew_seconds` parameter) and that it hasn't exceeded the `max_issued_at_age_seconds` policy, which limits the total lifespan of a token regardless of its official expiration.

### 4. Audience validation
   The handler then validates that the token is intended for this specific API by inspecting the Audience (`aud`) claim. If the configured audience is not present in the token's audience list, the request is rejected. This method is particularly useful when APIs are shared across multiple clients or services, and you want to ensure that each token is issued for a specific intended audience.

### 5. Scope validation 
   The WSO2 Integrator: MI validates the scopes coming in the `scope` claim of the JWT. The handler ensures the scope claim contains the necessary permissions (defined in the Open API spec) required to access the specific resource.

### 5. Sender Constrain & Proof-of-Possession
   The final layer of the pipeline is the Confirmation (`cnf`) check. If **mTLS** is enabled, the handler extracts the thumbprint of the client certificate used during the TLS handshake and compares it with the x5t#S256 value inside the token. This Proof-of-Possession check ensures that even if a JWT is intercepted, it cannot be used by any party other than the original client to whom it was issued.

## Handler Configuration Reference

The following table provides a reference for the configurable parameters of the JWT access token handler.

| Parameter Name | Description                                                                                                                                                                                                            | Required/Optional | Default Value   |
| --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------| --- |-----------------|
| `jwksEndpoint` | The URL of the JWKS endpoint where the handler can retrieve the public keys for signature verification.                                                                                                                | Required | None            |
| `authorizationHeader` | The HTTP header containing the token.                                                                                                                                                                                  | Optional | "Authorization" |
| `trustedIssuers` | A comma-separated list of trusted token issuers. The handler will only accept tokens that have an `iss` claim matching one of these values.                                                                            | Optional | None            |
| `allowedAlgorithms` | A comma-separated list of allowed signing algorithms (e.g., RS256, ES256). Tokens signed with algorithms not in this list will be rejected.                                                                            | Optional | RS256           |
| `audience` | The expected audience value that must be present in the `aud` claim of the JWT. This ensures the token is intended for this API.                                                                                       | Optional | None            |
| `clock_skew_seconds` | The amount of clock skew (in seconds) to allow when validating the `iat` and `exp` claim. This accounts for minor time discrepancies between the token issuer and the WSO2 Integrator: MI.                             | Optional | 60 seconds      |
| `max_issued_at_age_seconds` | Defines the maximum lifespan allowed for a token since it was issued (`iat`), regardless of the expiration time.                           | Optional | None            |
| `removeOAuthHeadersFromOutMessage` | A flag to indicate whether to remove the OAuth-related headers (e.g., Authorization header) from the message before sending it to the backend. This can help prevent sensitive information from being exposed to backend services. | Optional | true            |
| `tokenRevocationHandler` | The fully qualified class name of a custom token revocation handler that implements the `TokenRevocationHandler` interface. This allows you to plug in custom logic to check if a token has been revoked (e.g., by checking a database or cache). | Optional | None            |
| `enable_mtls` | A flag to enable or disable mTLS-based sender constraint. When enabled, the handler will perform a Proof-of-Possession check by comparing the client certificate thumbprint with the value in the token's `cnf` claim. | Optional | false           |
| `client_cert_alias` | If mTLS is enabled, this parameter specifies the alias of the client certificate in the WSO2 Integrator: MI's truststore (client-truststore.jks) that should be used for the Proof-of-Possession check.                | Optional (required if `enable_mtls` is true) | None            | 

### Sender-Constrained (mTLS) Properties

When `enable_mtls` is set to true, the handler will enforce sender constraint by performing a Proof-of-Possession check. In this case, the following additional properties are relevant:

| Parameter Name | Description                                                                                                                                                                                                         | Required/Optional | Default Value   |
| --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------| --- |-----------------|
| `disableCNFValidation` | Set to false to enable Proof-of-Possession checks. It validates the cnf claim against the client's certificate.                                                                                                     | Optional | false           |
| `enableClientCertificateValidation` | Toggles the extraction and validation of the client certificate from the transport layer.                                                                                                                           | Optional | true            |
| `clientCertificateHeader` | The HTTP header from which to extract the client certificate. This is typically used in scenarios where the client certificate is forwarded by a reverse proxy or LB. | Optional | "X-Client-Certificate" |
| `clientCertificateEncode` | This property specifies the encoding format used for the client certificate when it is passed through HTTP headers (via the `clientCertificateHeader`). It ensures the handler can correctly decode the certificate string back into its original `X.509` format before performing the `cnf` (confirmation) thumbprint validation. | Optional | false           |

### HTTP Client & Proxy Configuration

The handler uses an internal HTTP client to retrieve public keys from the Identity Provider's JWKS metadata. Proper configuration of these settings is vital to prevent latency issues or connection failures during the token validation process.

#### Configuration Levels

1. **Handler Level (API Definition):**
By defining these properties within the <handler> tag of a specific API, you can override the global settings. This is useful for APIs that need to connect to an internal IdP (bypassing the proxy) or for critical services that require shorter timeout durations to fail fast.

2. **Global Level (deployment.toml):**
Configurations defined here act as the default settings for every instance of the OAuth2AuthorizationHandler across the entire WSO2 Integrator: MI instance. This is the recommended place for corporate proxy settings that apply to the whole network.

Precedence: The handler will always check for a property in its local configuration first. If not found, it will fall back to the value defined in `deployment.toml`.

| Handle Level Configuration Name | Global Level Configuration Name                 | Description                                                                                                  | Required/Optional | Default Value |
|-----------------------------|-------------------------------------------------|--------------------------------------------------------------------------------------------------------------| --- |---------------|
| `connectionTimeout`         | `http_client.global_connection_timeout`         | The timeout (in milliseconds) for establishing a connection to the JWKS endpoint.                            | Optional | 5000 ms       |
| `socketTimeout`             | `http_client.global_socket_timeout`             | The timeout (in milliseconds) for waiting for data from the JWKS endpoint after a connection is established. | Optional | 5000 ms       |
| `connectionRequestTimeout`  | `http_client.global_connection_request_timeout` | The timeout (in milliseconds) for waiting to obtain a connection from the internal connection pool.          | Optional | 5000 ms       |
| `enableProxy`               | `http_client.global_proxy_enabled`              | Set to `true` to route JWKS requests through a proxy server.                                                 | Optional | false         |
| `proxyHost`                 | `http_client.global_proxy_host`                 | The hostname of the proxy server to use when connecting to the JWKS endpoint.                                | Optional | None          |
| `proxyPort`                 | `http_client.global_proxy_port`                 | The port number of the proxy server.                                                                         | Optional | None          |
| `proxyProtocol`             | `http_client.global_proxy_protocol`             | The protocol to use when connecting to the proxy server (e.g., `http` or `https`).                           | Optional | http          |
| `proxyUsername`             | `http_client.global_proxy_username`             | The username for authenticating with the proxy server, if required.                                          | Optional | None          |
| `proxyPassword`             | `http_client.global_proxy_password`             | The password for authenticating with the proxy server, if required.                                          | Optional | None          |



Follow the instructions below to secure APIs with JWT (Self Contained) access tokens for delegate access for REST APIs in WSO2 Integrator: MI.

1. Follow the steps in [create integration project]({{base_path}}/develop/create-integration-project/) guide to set up the Integration Project.
2. Define the OpenAPI Specification with Scopes.

   To enable Scope Validation, you must define the required scopes within your API’s OpenAPI (Swagger) definition. The handler will look for these definitions to determine if the incoming token has the necessary permissions.


   **Assign the scope to a specific API resource (path):**

   ```yaml
     paths:
        /orders:
          get:
            security:
              - OAuth2:
                - read:orders
            responses:
              '200':
                description: OK
  ```


