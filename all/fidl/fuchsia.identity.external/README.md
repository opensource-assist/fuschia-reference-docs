[TOC]

# fuchsia.identity.external

<p>Defines the protocols used to interface with non-Fuchsia forms of identity,
such as OAuth and OpenID identity providers.</p>
<p>New identity providers or service providers may be added to the system by
implementing the server side of one or more of these protocols, the core
identity system will act as the client.</p>
<p>Clients wishing to acquire tokens should use the system token management
protocols in <code>fuchsia.identity.tokens</code> instead of depending on this library
directly.</p>

## **PROTOCOLS**

## Oauth {#Oauth}
*Defined in [fuchsia.identity.external/auth_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.external/auth_provider.fidl#36)*

<p>A protocol to request the creation, exchange, and revokation of Oauth 2.0
tokens.</p>

### CreateRefreshToken {#CreateRefreshToken}

<p>Creates a new refresh token. If this request is successful
the refresh token will be returned. Optionally an access token with
the default client ID and scope may also be returned (if no token is
available the fields in access_token will be unpopulated).</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code><a class='link' href='#OauthRefreshTokenRequest'>OauthRefreshTokenRequest</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Oauth_CreateRefreshToken_Result'>Oauth_CreateRefreshToken_Result</a></code>
            </td>
        </tr></table>

### GetAccessTokenFromRefreshToken {#GetAccessTokenFromRefreshToken}

<p>Exchanges a refresh token for an access token.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code><a class='link' href='#OauthAccessTokenFromOauthRefreshTokenRequest'>OauthAccessTokenFromOauthRefreshTokenRequest</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Oauth_GetAccessTokenFromRefreshToken_Result'>Oauth_GetAccessTokenFromRefreshToken_Result</a></code>
            </td>
        </tr></table>

### RevokeRefreshToken {#RevokeRefreshToken}

<p>Attempts to revoke the supplied refresh token.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>refresh_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.identity.tokens/'>fuchsia.identity.tokens</a>/<a class='link' href='../fuchsia.identity.tokens/#OauthRefreshToken'>OauthRefreshToken</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Oauth_RevokeRefreshToken_Result'>Oauth_RevokeRefreshToken_Result</a></code>
            </td>
        </tr></table>

### RevokeAccessToken {#RevokeAccessToken}

<p>Attempts to revoke the supplied access token.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>access_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.identity.tokens/'>fuchsia.identity.tokens</a>/<a class='link' href='../fuchsia.identity.tokens/#OauthAccessToken'>OauthAccessToken</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Oauth_RevokeAccessToken_Result'>Oauth_RevokeAccessToken_Result</a></code>
            </td>
        </tr></table>

## OpenIdConnect {#OpenIdConnect}
*Defined in [fuchsia.identity.external/auth_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.external/auth_provider.fidl#60)*

<p>A protocol to request the creation, exchange, and revokation of OpenID
Connect tokens.</p>

### RevokeIdToken {#RevokeIdToken}

<p>Attempts to revoke the supplied ID token.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.identity.tokens/'>fuchsia.identity.tokens</a>/<a class='link' href='../fuchsia.identity.tokens/#OpenIdToken'>OpenIdToken</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#OpenIdConnect_RevokeIdToken_Result'>OpenIdConnect_RevokeIdToken_Result</a></code>
            </td>
        </tr></table>

## OauthOpenIdConnect {#OauthOpenIdConnect}
*Defined in [fuchsia.identity.external/auth_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.external/auth_provider.fidl#85)*

<p>A protocol to perform exchanges between Oauth 2.0 and OpenID Connect tokens.</p>

### GetIdTokenFromRefreshToken {#GetIdTokenFromRefreshToken}

<p>Exchanges an OAuth refresh token for an OpenID Connect ID token.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code><a class='link' href='#OpenIdTokenFromOauthRefreshTokenRequest'>OpenIdTokenFromOauthRefreshTokenRequest</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#OauthOpenIdConnect_GetIdTokenFromRefreshToken_Result'>OauthOpenIdConnect_GetIdTokenFromRefreshToken_Result</a></code>
            </td>
        </tr></table>

### GetUserInfoFromAccessToken {#GetUserInfoFromAccessToken}

<p>Exchanges an OAuth access token for an OpenID Connect UserInfo.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code><a class='link' href='#OpenIdUserInfoFromOauthAccessTokenRequest'>OpenIdUserInfoFromOauthAccessTokenRequest</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#OauthOpenIdConnect_GetUserInfoFromAccessToken_Result'>OauthOpenIdConnect_GetUserInfoFromAccessToken_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Oauth_CreateRefreshToken_Response {#Oauth_CreateRefreshToken_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>refresh_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.identity.tokens/'>fuchsia.identity.tokens</a>/<a class='link' href='../fuchsia.identity.tokens/#OauthRefreshToken'>OauthRefreshToken</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>access_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.identity.tokens/'>fuchsia.identity.tokens</a>/<a class='link' href='../fuchsia.identity.tokens/#OauthAccessToken'>OauthAccessToken</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Oauth_GetAccessTokenFromRefreshToken_Response {#Oauth_GetAccessTokenFromRefreshToken_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>access_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.identity.tokens/'>fuchsia.identity.tokens</a>/<a class='link' href='../fuchsia.identity.tokens/#OauthAccessToken'>OauthAccessToken</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Oauth_RevokeRefreshToken_Response {#Oauth_RevokeRefreshToken_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Oauth_RevokeAccessToken_Response {#Oauth_RevokeAccessToken_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### OpenIdConnect_RevokeIdToken_Response {#OpenIdConnect_RevokeIdToken_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### OauthOpenIdConnect_GetIdTokenFromRefreshToken_Response {#OauthOpenIdConnect_GetIdTokenFromRefreshToken_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.identity.tokens/'>fuchsia.identity.tokens</a>/<a class='link' href='../fuchsia.identity.tokens/#OpenIdToken'>OpenIdToken</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### OauthOpenIdConnect_GetUserInfoFromAccessToken_Response {#OauthOpenIdConnect_GetUserInfoFromAccessToken_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>user_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.identity.tokens/'>fuchsia.identity.tokens</a>/<a class='link' href='../fuchsia.identity.tokens/#OpenIdUserInfo'>OpenIdUserInfo</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### Error {#Error}
Type: <code>uint32</code>

*Defined in [fuchsia.identity.external/common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.external/common.fidl#8)*

<p>Specifies the reason that a fuchsia.identity.external method failed.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>1</code></td>
            <td><p>Some other problem occurred that cannot be classified using one of the
more specific statuses.</p>
</td>
        </tr><tr>
            <td><code>INTERNAL</code></td>
            <td><code>2</code></td>
            <td><p>An internal error occurred. This usually indicates a bug within the
component implementation.</p>
</td>
        </tr><tr>
            <td><code>CONFIG</code></td>
            <td><code>3</code></td>
            <td><p>The component instance was not configured correctly at initialization
and is unable to perform useful work.</p>
</td>
        </tr><tr>
            <td><code>UNSUPPORTED_OPERATION</code></td>
            <td><code>4</code></td>
            <td><p>The requested operation is not supported by this implementation. An
example is requesting a type of token that the service provider does not
support.</p>
</td>
        </tr><tr>
            <td><code>INVALID_REQUEST</code></td>
            <td><code>5</code></td>
            <td><p>The method request was not valid or was malformed in some way, such as
omitting required fields. Invalid requests for unsupported operations
will return <code>UNSUPPORTED_OPERATION</code>.</p>
</td>
        </tr><tr>
            <td><code>RESOURCE</code></td>
            <td><code>6</code></td>
            <td><p>A local resource error occurred such as an I/O, FIDL, or memory
allocation failure.</p>
</td>
        </tr><tr>
            <td><code>NETWORK</code></td>
            <td><code>7</code></td>
            <td><p>A network error occurred while communicating with the auth server or the
server was unreachable.</p>
</td>
        </tr><tr>
            <td><code>SERVER</code></td>
            <td><code>8</code></td>
            <td><p>The auth server returned a failure or an invalid response. This may
indicate either a failure of the server itself or an incompatibility
between the server and the component implementation.</p>
</td>
        </tr><tr>
            <td><code>INVALID_TOKEN</code></td>
            <td><code>9</code></td>
            <td><p>The token supplied to perform an exchange operation is not valid and
should be discarded. This can occur following server-side revocation.</p>
</td>
        </tr><tr>
            <td><code>INSUFFICIENT_TOKEN</code></td>
            <td><code>10</code></td>
            <td><p>The token supplied to perform an exchange operation was valid but was
not sufficiently powerful to complete the requested exchange.</p>
</td>
        </tr><tr>
            <td><code>ABORTED</code></td>
            <td><code>11</code></td>
            <td><p>The user cancelled or failed an interactive authentication operation.</p>
</td>
        </tr></table>



## **TABLES**

### OauthRefreshTokenRequest {#OauthRefreshTokenRequest}


*Defined in [fuchsia.identity.external/auth_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.external/auth_provider.fidl#11)*

<p>The request format used to create a new OAuth 2.0 Refresh Token.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>account_id</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>The account to create the token for, if known. If omitted, the user will
be prompted to specify an account.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>ui_context</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/#AuthenticationUIContext'>AuthenticationUIContext</a></code>
            </td>
            <td><p>A UI Context used to overlay a view in which the user can interactively
authenticate. This field is required.</p>
</td>
        </tr></table>

### OauthAccessTokenFromOauthRefreshTokenRequest {#OauthAccessTokenFromOauthRefreshTokenRequest}


*Defined in [fuchsia.identity.external/auth_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.external/auth_provider.fidl#22)*

<p>The request format used to exchange an OAuth 2.0 Refresh Token for an
Access Token.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>refresh_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.identity.tokens/'>fuchsia.identity.tokens</a>/<a class='link' href='../fuchsia.identity.tokens/#OauthRefreshToken'>OauthRefreshToken</a></code>
            </td>
            <td><p>The Refresh token to exchange. This field is required.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>client_id</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>The OAuth ClientID for the component requesting the token. If absent, a
default ClientID defined by the implementation will be used.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>scopes</code></td>
            <td>
                <code>vector&lt;string&gt;[128]</code>
            </td>
            <td><p>The list of OAuth scope strings to request. If absent or empty, a
default set of scopes defined by the implementation will be used.</p>
</td>
        </tr></table>

### OpenIdTokenFromOauthRefreshTokenRequest {#OpenIdTokenFromOauthRefreshTokenRequest}


*Defined in [fuchsia.identity.external/auth_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.external/auth_provider.fidl#67)*

<p>The request format used to exchange an OAuth 2.0 Refresh Token for an
OpenID Connect ID token.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>refresh_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.identity.tokens/'>fuchsia.identity.tokens</a>/<a class='link' href='../fuchsia.identity.tokens/#OauthRefreshToken'>OauthRefreshToken</a></code>
            </td>
            <td><p>The refresh token to exchange. This field is required.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>audiences</code></td>
            <td>
                <code>vector&lt;string&gt;[16]</code>
            </td>
            <td><p>The OpenID audience strings that the ID token should be issued to. If
absent or empty, a default set of scopes defined by the implementation
will be used.</p>
</td>
        </tr></table>

### OpenIdUserInfoFromOauthAccessTokenRequest {#OpenIdUserInfoFromOauthAccessTokenRequest}


*Defined in [fuchsia.identity.external/auth_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.external/auth_provider.fidl#78)*

<p>The request format used to exchange an OAuth 2.0 Access Token for a User
Info response as defined by OpenID Connect.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>access_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.identity.tokens/'>fuchsia.identity.tokens</a>/<a class='link' href='../fuchsia.identity.tokens/#OauthAccessToken'>OauthAccessToken</a></code>
            </td>
            <td><p>The Access token to exchange. This field is required.</p>
</td>
        </tr></table>



## **UNIONS**

### Oauth_CreateRefreshToken_Result {#Oauth_CreateRefreshToken_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Oauth_CreateRefreshToken_Response'>Oauth_CreateRefreshToken_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Oauth_GetAccessTokenFromRefreshToken_Result {#Oauth_GetAccessTokenFromRefreshToken_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Oauth_GetAccessTokenFromRefreshToken_Response'>Oauth_GetAccessTokenFromRefreshToken_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Oauth_RevokeRefreshToken_Result {#Oauth_RevokeRefreshToken_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Oauth_RevokeRefreshToken_Response'>Oauth_RevokeRefreshToken_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Oauth_RevokeAccessToken_Result {#Oauth_RevokeAccessToken_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Oauth_RevokeAccessToken_Response'>Oauth_RevokeAccessToken_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### OpenIdConnect_RevokeIdToken_Result {#OpenIdConnect_RevokeIdToken_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#OpenIdConnect_RevokeIdToken_Response'>OpenIdConnect_RevokeIdToken_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### OauthOpenIdConnect_GetIdTokenFromRefreshToken_Result {#OauthOpenIdConnect_GetIdTokenFromRefreshToken_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#OauthOpenIdConnect_GetIdTokenFromRefreshToken_Response'>OauthOpenIdConnect_GetIdTokenFromRefreshToken_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### OauthOpenIdConnect_GetUserInfoFromAccessToken_Result {#OauthOpenIdConnect_GetUserInfoFromAccessToken_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#OauthOpenIdConnect_GetUserInfoFromAccessToken_Response'>OauthOpenIdConnect_GetUserInfoFromAccessToken_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>







