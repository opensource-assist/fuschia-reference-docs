[TOC]

# fuchsia.identity.tokens

<p>Defines the data types and protocols used to request user authorization
tokens and identity information from service providers and identity
providers.</p>
<p>The actual interaction with these providers is through lower level protocols
defined in <code>fuchsia.id.external</code>.</p>

## **PROTOCOLS**

## TokenManager {#TokenManager}
*Defined in [fuchsia.identity.tokens/token_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/token_manager.fidl#26)*

<p><code>TokenManager</code> maintains a set of credentials for accounts with service
providers (such as Google) and provides access to standard tokens based on
these credentials (such as OAuth2 access tokens and OpenID Connect ID
tokens). This provides a &quot;single sign-on&quot; experience for these services on
Fuchsia, where multiple components can use a service without requiring that
the user signs in multiple times.</p>

### ListServiceProviders {#ListServiceProviders}

<p>Returns the list of service providers that are available through this
<code>TokenManager</code>.</p>
<ul>
<li><code>service_providers</code> a vector of available service providers.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#TokenManager_ListServiceProviders_Result'>TokenManager_ListServiceProviders_Result</a></code>
            </td>
        </tr></table>

### ListAccounts {#ListAccounts}

<p>Returns the list of currently authorized accounts for a particular
service provider.</p>
<ul>
<li><code>service_provider</code> the service provider to query.</li>
</ul>
<ul>
<li><code>account_ids</code> a vector of authorized accounts for <code>service_provider</code>.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service_provider</code></td>
            <td>
                <code><a class='link' href='#ServiceProvider'>ServiceProvider</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#TokenManager_ListAccounts_Result'>TokenManager_ListAccounts_Result</a></code>
            </td>
        </tr></table>

### AddAccount {#AddAccount}

<p>Acquires credentials for a new account from a service provider.</p>
<p>This process typically requires the user to interactively authenticate
with the service provider and authorize the requested access.</p>
<p>Once <code>AddAccount</code> has succeeded, tokens for the account may be acquired
using the other <code>TokenManager</code> methods.</p>
<ul>
<li><code>service_provider</code> The <code>ServiceProvider</code> used to authorize the new
account.</li>
<li><code>scopes</code> A list of OAuth scope strings that the caller wishes to
subsequently use in <code>GetOauthAccessToken</code>. The AuthProvider
component chooses if and how to combine these with any
default or threshold scopes.</li>
</ul>
<ul>
<li><code>account_id</code>  A unique identifier within this service provider for the
newly authorized account.</li>
</ul>
<ul>
<li>error <code>ABORTED</code> The user cancelled or failed an interactive flow.</li>
<li>error <code>SERVICE_PROVIDER_DENIED</code> The service provider refused to grant
the requested token.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service_provider</code></td>
            <td>
                <code><a class='link' href='#ServiceProvider'>ServiceProvider</a></code>
            </td>
        </tr><tr>
            <td><code>scopes</code></td>
            <td>
                <code>vector&lt;string&gt;[64]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#TokenManager_AddAccount_Result'>TokenManager_AddAccount_Result</a></code>
            </td>
        </tr></table>

### ReauthorizeAccount {#ReauthorizeAccount}

<p>Refreshes credentials or changes credential scopes for an account that
was previously authorized.</p>
<p>This process may require the user to interactively authenticate with the
service provider and authorize the requested access.</p>
<ul>
<li><code>service_provider</code> The <code>ServiceProvider</code> used to reauthorize the
account.</li>
<li><code>account_id</code>  An <code>AccountId</code> that has previously been authorized for
this <code>ServiceProvider</code>.</li>
<li><code>scopes</code> A list of OAuth scope strings that the caller wishes to
subsequently use in <code>GetOauthAccessToken</code>. The AuthProvider
component chooses if and how to combine these with any
default or threshold scopes.</li>
</ul>
<ul>
<li>error <code>ABORTED</code> The user cancelled or failed an interactive flow.</li>
<li>error <code>SERVICE_PROVIDER_DENIED</code> The service provider refused to grant
the requested token.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service_provider</code></td>
            <td>
                <code><a class='link' href='#ServiceProvider'>ServiceProvider</a></code>
            </td>
        </tr><tr>
            <td><code>account_id</code></td>
            <td>
                <code><a class='link' href='#AccountId'>AccountId</a></code>
            </td>
        </tr><tr>
            <td><code>scopes</code></td>
            <td>
                <code>vector&lt;string&gt;[64]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#TokenManager_ReauthorizeAccount_Result'>TokenManager_ReauthorizeAccount_Result</a></code>
            </td>
        </tr></table>

### GetOauthAccessToken {#GetOauthAccessToken}

<p>Returns an OAuth 2.0 access token for the specified account.</p>
<p>The access token may optionally be sidescoped (i.e. issued to a
different <code>client_id</code> than the default <code>client_id</code> used during
authorization) and may contain a smaller set of scopes than those
acquired during authorization.</p>
<p>The access token is returned from cache if possible, otherwise the auth
provider is used to exchange the persistent credential for a new access
token. In the interests of performance, Token Manager does not place the
supplied scopes in a canonical order during caching. To benefit from
caching of tokens, clients must request the same scopes in the same
order across calls.</p>
<ul>
<li><code>service_provider</code> The <code>ServiceProvider</code> from which the token should
be requested.</li>
<li><code>account_id</code> An <code>AccountId</code> that has previously been authorized for
this <code>ServiceProvider</code>.</li>
<li><code>client_id</code> The <code>ClientId</code> that the token will be used by. If ommitted
(and if supported by the auth provider component) a
default <code>client_id</code> is used.</li>
<li><code>scopes</code> A list of OAuth scopes that should be included in the token,
as defined by the service provider's API documention.</li>
</ul>
<ul>
<li><code>access_token</code> An <code>OauthAccessToken</code>.</li>
</ul>
<ul>
<li>error <code>ABORTED</code> The user rejected an interactive permission request.</li>
<li>error <code>SERVICE_PROVIDER_DENIED</code> The service provider refused to grant
the requested token.</li>
<li>error <code>SERVICE_PROVIDER_REAUTHORIZE</code> The service provider requires
that the user reauthenticate before supplying the requested
token. The client should call the <code>ReauthorizeAccount</code> method
before retrying the request.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service_provider</code></td>
            <td>
                <code><a class='link' href='#ServiceProvider'>ServiceProvider</a></code>
            </td>
        </tr><tr>
            <td><code>account_id</code></td>
            <td>
                <code><a class='link' href='#AccountId'>AccountId</a></code>
            </td>
        </tr><tr>
            <td><code>client_id</code></td>
            <td>
                <code><a class='link' href='#ClientId'>ClientId</a></code>
            </td>
        </tr><tr>
            <td><code>scopes</code></td>
            <td>
                <code>vector&lt;string&gt;[64]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#TokenManager_GetOauthAccessToken_Result'>TokenManager_GetOauthAccessToken_Result</a></code>
            </td>
        </tr></table>

### GetOpenIdUserInfo {#GetOpenIdUserInfo}

<p>Returns user information for the specified account as defined by
OpenID Connect.</p>
<ul>
<li><code>service_provider</code> The <code>ServiceProvider</code> from which the token should
be requested.</li>
<li><code>account_id</code> An <code>AccountId</code> that has previously been authorized for
this <code>ServiceProvider</code>.</li>
</ul>
<ul>
<li><code>user_info</code> An <code>OpenIdUserInfo</code> containing account information.</li>
</ul>
<ul>
<li>error <code>ABORTED</code> The user rejected an interactive permission request.</li>
<li>error <code>SERVICE_PROVIDER_REAUTHORIZE</code> The service provider requires
that the user reauthenticate before supplying the user info.</li>
<li>error <code>UNSUPPORTED_OPERATION</code> The auth provider does not support
OpenID Connect.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service_provider</code></td>
            <td>
                <code><a class='link' href='#ServiceProvider'>ServiceProvider</a></code>
            </td>
        </tr><tr>
            <td><code>account_id</code></td>
            <td>
                <code><a class='link' href='#AccountId'>AccountId</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#TokenManager_GetOpenIdUserInfo_Result'>TokenManager_GetOpenIdUserInfo_Result</a></code>
            </td>
        </tr></table>

### GetOpenIdToken {#GetOpenIdToken}

<p>Returns an OpenID Connect ID token for the specified account.</p>
<p>The identity token is returned from cache if possible, otherwise the
auth provider is used to exchange the persistant credential for a new
identity token.</p>
<ul>
<li><code>service_provider</code> The <code>ServiceProvider</code> from which the token should
be requested.</li>
<li><code>account_id</code> An <code>AccountId</code> that has previously been authorized for
this <code>ServiceProvider</code>.</li>
<li><code>audience</code> The <code>Audience</code> that the ID token will be used by. If
ommitted (and if supported by the auth provider component)
a default <code>audience</code> is used.</li>
</ul>
<ul>
<li><code>id_token</code> An <code>OpenIdToken</code>.</li>
</ul>
<ul>
<li>error <code>ABORTED</code> The user rejected an interactive permission request.</li>
<li>error <code>SERVICE_PROVIDER_DENIED</code> The service provider refused to grant
the requested token.</li>
<li>error <code>SERVICE_PROVIDER_REAUTHORIZE</code> The service provider requires
that the user reauthenticate before supplying the user info.</li>
<li>error <code>UNSUPPORTED_OPERATION</code> The auth provider does not support
OpenID Connect.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service_provider</code></td>
            <td>
                <code><a class='link' href='#ServiceProvider'>ServiceProvider</a></code>
            </td>
        </tr><tr>
            <td><code>account_id</code></td>
            <td>
                <code><a class='link' href='#AccountId'>AccountId</a></code>
            </td>
        </tr><tr>
            <td><code>audience</code></td>
            <td>
                <code><a class='link' href='#Audience'>Audience</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#TokenManager_GetOpenIdToken_Result'>TokenManager_GetOpenIdToken_Result</a></code>
            </td>
        </tr></table>

### DeleteAccount {#DeleteAccount}

<p>Deletes and revokes all long lived and short lived tokens generated for
an account.</p>
<p>Deletion of tokens involves three steps:</p>
<ol>
<li>Revoking credentials remotely at the service provider.</li>
<li>Deleting short lived tokens from the in-memory cache.</li>
<li>Deleting persistent credentials stored locally on disk.</li>
</ol>
<p>If <code>force</code> is false then a failure at step 1 terminates the method,
ensuring client and server state remain consistent. If <code>force</code> is true
then steps 2&amp;3 are performed and the method returns success even if
step 1 fails, ensuring the local credentials are wiped in all
circumstances.</p>
<ul>
<li><code>service_provider</code> The <code>ServiceProvider</code> from which the token should
be requested.</li>
<li><code>account_id</code> An <code>AccountId</code> that has previously been authorized for
this <code>ServiceProvider</code>.</li>
<li><code>force</code> Whether to force local deletion even when the remote
revocation cannot be completed.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service_provider</code></td>
            <td>
                <code><a class='link' href='#ServiceProvider'>ServiceProvider</a></code>
            </td>
        </tr><tr>
            <td><code>account_id</code></td>
            <td>
                <code><a class='link' href='#AccountId'>AccountId</a></code>
            </td>
        </tr><tr>
            <td><code>force</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#TokenManager_DeleteAccount_Result'>TokenManager_DeleteAccount_Result</a></code>
            </td>
        </tr></table>

## TokenManagerFactory {#TokenManagerFactory}
*Defined in [fuchsia.identity.tokens/token_manager_factory.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/token_manager_factory.fidl#15)*

<p><code>TokenManagerFactory</code> provides access to a global <code>TokenManager</code> on systems
that do not include an <code>AccountManager</code>.</p>
<p>On systems that do include <code>AccountManager</code>, that API should be used to
acquire a separate <code>TokenManager</code> instance for each system account.</p>

### GetTokenManager {#GetTokenManager}

<p>Connects a new <code>TokenManager</code> channel.</p>
<ul>
<li><code>ui_context_provider</code> An <code>AuthenticationContextProvider</code> capable of
generating the <code>AuthenticationUiContext</code>
channels used to display interactive
authentication and authorization flows.</li>
<li><code>token_manager</code> The server end of a <code>TokenManager</code> channel.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ui_context_provider</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/#AuthenticationContextProvider'>AuthenticationContextProvider</a></code>
            </td>
        </tr><tr>
            <td><code>token_manager</code></td>
            <td>
                <code>request&lt;<a class='link' href='#TokenManager'>TokenManager</a>&gt;</code>
            </td>
        </tr></table>





## **STRUCTS**

### TokenManager_ListServiceProviders_Response {#TokenManager_ListServiceProviders_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>service_providers</code></td>
            <td>
                <code>vector&lt;string&gt;[128]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TokenManager_ListAccounts_Response {#TokenManager_ListAccounts_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>account_ids</code></td>
            <td>
                <code>vector&lt;string&gt;[128]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TokenManager_AddAccount_Response {#TokenManager_AddAccount_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>account_id</code></td>
            <td>
                <code><a class='link' href='#AccountId'>AccountId</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TokenManager_ReauthorizeAccount_Response {#TokenManager_ReauthorizeAccount_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### TokenManager_GetOauthAccessToken_Response {#TokenManager_GetOauthAccessToken_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>access_token</code></td>
            <td>
                <code><a class='link' href='#OauthAccessToken'>OauthAccessToken</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TokenManager_GetOpenIdUserInfo_Response {#TokenManager_GetOpenIdUserInfo_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>user_info</code></td>
            <td>
                <code><a class='link' href='#OpenIdUserInfo'>OpenIdUserInfo</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TokenManager_GetOpenIdToken_Response {#TokenManager_GetOpenIdToken_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id_token</code></td>
            <td>
                <code><a class='link' href='#OpenIdToken'>OpenIdToken</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TokenManager_DeleteAccount_Response {#TokenManager_DeleteAccount_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>



## **ENUMS**

### Error {#Error}
Type: <code>uint32</code>

*Defined in [fuchsia.identity.tokens/common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/common.fidl#40)*

<p>Specifies the reason that a fuchsia.identity.tokens method failed.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>1</code></td>
            <td><p>Some other problem occurred that cannot be classified using one of the
more specific statuses. Retry is optional.</p>
</td>
        </tr><tr>
            <td><code>INTERNAL</code></td>
            <td><code>2</code></td>
            <td><p>An internal error occurred. This usually indicates a bug within the
Token Manager itself. Retry is optional.</p>
</td>
        </tr><tr>
            <td><code>UNSUPPORTED_OPERATION</code></td>
            <td><code>3</code></td>
            <td><p>The requested operation is not supported for the requested entity. For
example, some service providers may not support some types of token.
The request should not be retried.</p>
</td>
        </tr><tr>
            <td><code>INVALID_REQUEST</code></td>
            <td><code>4</code></td>
            <td><p>The request was malformed in some way, such as using an empty string for
service provider. The request should not be retried.</p>
</td>
        </tr><tr>
            <td><code>RESOURCE</code></td>
            <td><code>5</code></td>
            <td><p>A local resource error occurred such as I/O, FIDL, or memory allocation
failure. Retry, after a delay, is recommended.</p>
</td>
        </tr><tr>
            <td><code>NETWORK</code></td>
            <td><code>6</code></td>
            <td><p>A network error occurred while communicating with a server or the server
was unreachable.  Retry, after a delay, is recommended.</p>
</td>
        </tr><tr>
            <td><code>INVALID_SERVICE_PROVIDER</code></td>
            <td><code>7</code></td>
            <td><p>The request referred to a missing service provider or one where the auth
provider component is misconfigured or failed.</p>
</td>
        </tr><tr>
            <td><code>INVALID_ACCOUNT</code></td>
            <td><code>8</code></td>
            <td><p>The request referred to an account that is not found for the specified
service provider. The request should not be retried.</p>
</td>
        </tr><tr>
            <td><code>SERVICE_PROVIDER_ERROR</code></td>
            <td><code>10</code></td>
            <td><p>The service provider returned a error that indicates a failure within
the service provider itself. Retry, after a delay, is recommended.</p>
</td>
        </tr><tr>
            <td><code>SERVICE_PROVIDER_DENIED</code></td>
            <td><code>11</code></td>
            <td><p>The service provider refused to grant the requested token. The request
should not be retried.</p>
</td>
        </tr><tr>
            <td><code>SERVICE_PROVIDER_REAUTHORIZE</code></td>
            <td><code>12</code></td>
            <td><p>The service provider requires that the user reauthenticate before
supplying the requested token. The client should call the
<code>ReauthorizeAccount</code> method before retrying the request.</p>
</td>
        </tr><tr>
            <td><code>ABORTED</code></td>
            <td><code>13</code></td>
            <td><p>The user cancelled or failed an interactive flow. The caller should
gather user consent before any retry of the request.</p>
</td>
        </tr></table>



## **TABLES**

### OauthRefreshToken {#OauthRefreshToken}


*Defined in [fuchsia.identity.tokens/token_types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/token_types.fidl#10)*

<p>A long-lived OAuth 2.0 Refresh Token.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>content</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The content of the token.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>account_id</code></td>
            <td>
                <code><a class='link' href='#AccountId'>AccountId</a></code>
            </td>
            <td><p>A unique identifier for the account that the token refers to, as
specified by the authorization server.</p>
</td>
        </tr></table>

### OauthAccessToken {#OauthAccessToken}


*Defined in [fuchsia.identity.tokens/token_types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/token_types.fidl#24)*

<p>An OAuth 2.0 Access Token.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>content</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The content of the token.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>expiry_time</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#time'>time</a></code>
            </td>
            <td><p>The time on <code>ZX_CLOCK_UTC</code> at which the token will expire. If the field
is absent the token does not have a fixed expiry time.</p>
</td>
        </tr></table>

### OpenIdToken {#OpenIdToken}


*Defined in [fuchsia.identity.tokens/token_types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/token_types.fidl#38)*

<p>An OpenID Connect ID Token.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>content</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The content of the JSON Web Token.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>expiry_time</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#time'>time</a></code>
            </td>
            <td><p>The time on <code>ZX_CLOCK_UTC</code> at which the token will expire. If the field
is absent the token does not have a fixed expiry time.</p>
</td>
        </tr></table>

### OpenIdUserInfo {#OpenIdUserInfo}


*Defined in [fuchsia.identity.tokens/token_types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/token_types.fidl#51)*

<p>The reponse from an OpenID Connect UserInfo endpoint.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>subject</code></td>
            <td>
                <code>string[255]</code>
            </td>
            <td><p>The subject to which this info applies.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The user's full name.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>email</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The user's email address.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>picture</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>A URL to a profile picture for the user.</p>
</td>
        </tr></table>



## **UNIONS**

### TokenManager_ListServiceProviders_Result {#TokenManager_ListServiceProviders_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#TokenManager_ListServiceProviders_Response'>TokenManager_ListServiceProviders_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### TokenManager_ListAccounts_Result {#TokenManager_ListAccounts_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#TokenManager_ListAccounts_Response'>TokenManager_ListAccounts_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### TokenManager_AddAccount_Result {#TokenManager_AddAccount_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#TokenManager_AddAccount_Response'>TokenManager_AddAccount_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### TokenManager_ReauthorizeAccount_Result {#TokenManager_ReauthorizeAccount_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#TokenManager_ReauthorizeAccount_Response'>TokenManager_ReauthorizeAccount_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### TokenManager_GetOauthAccessToken_Result {#TokenManager_GetOauthAccessToken_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#TokenManager_GetOauthAccessToken_Response'>TokenManager_GetOauthAccessToken_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### TokenManager_GetOpenIdUserInfo_Result {#TokenManager_GetOpenIdUserInfo_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#TokenManager_GetOpenIdUserInfo_Response'>TokenManager_GetOpenIdUserInfo_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### TokenManager_GetOpenIdToken_Result {#TokenManager_GetOpenIdToken_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#TokenManager_GetOpenIdToken_Response'>TokenManager_GetOpenIdToken_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### TokenManager_DeleteAccount_Result {#TokenManager_DeleteAccount_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#TokenManager_DeleteAccount_Response'>TokenManager_DeleteAccount_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="MAX_ACCOUNT_ID_SIZE">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/common.fidl#8">MAX_ACCOUNT_ID_SIZE</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum length of an account ID string, in bytes.</p>
</td>
        </tr>
    <tr id="MAX_CLIENT_ID_SIZE">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/common.fidl#16">MAX_CLIENT_ID_SIZE</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum length of an OAuth client ID, in bytes.</p>
</td>
        </tr>
    <tr id="MAX_SCOPE_SIZE">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/common.fidl#22">MAX_SCOPE_SIZE</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum length of an OAuth scope, in bytes.</p>
</td>
        </tr>
    <tr id="MAX_SCOPE_COUNT">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/common.fidl#28">MAX_SCOPE_COUNT</a></td>
            <td>
                    <code>64</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum number of OAuth scopes that may be requested for a single token.</p>
</td>
        </tr>
    <tr id="MAX_AUDIENCE_SIZE">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/common.fidl#31">MAX_AUDIENCE_SIZE</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum length of an OpenID audience string, in bytes.</p>
</td>
        </tr>
    <tr id="MAX_AUDIENCE_COUNT">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/common.fidl#37">MAX_AUDIENCE_COUNT</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum number of audiences that may be requested for a single ID token.</p>
</td>
        </tr>
    <tr id="MAX_SERVICE_PROVIDER_COUNT">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/token_manager.fidl#9">MAX_SERVICE_PROVIDER_COUNT</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum number of service providers for which <code>AuthProvider</code> components
can be simultaneously installed.</p>
</td>
        </tr>
    <tr id="MAX_ACCOUNT_COUNT">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/token_manager.fidl#13">MAX_ACCOUNT_COUNT</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum number of Accounts that can be authorized within a service
provider for a single instance of TokenManager.</p>
</td>
        </tr>
    
</table>



## **TYPE ALIASES**

<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr id="AccountId">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/common.fidl#13">AccountId</a></td>
            <td>
                <code>string</code>[<code><a class='link' href='#MAX_ACCOUNT_ID_SIZE'>MAX_ACCOUNT_ID_SIZE</a></code>]</td>
            <td><p>An identifier for the account that a token is issued against, as specified
by the authorization server. Account identifiers are guaranteed to be unique
within an auth provider type.</p>
</td>
        </tr><tr id="ClientId">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/common.fidl#19">ClientId</a></td>
            <td>
                <code>string</code>[<code><a class='link' href='#MAX_CLIENT_ID_SIZE'>MAX_CLIENT_ID_SIZE</a></code>]</td>
            <td><p>An OAuth client ID string.</p>
</td>
        </tr><tr id="Scope">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/common.fidl#25">Scope</a></td>
            <td>
                <code>string</code>[<code><a class='link' href='#MAX_SCOPE_SIZE'>MAX_SCOPE_SIZE</a></code>]</td>
            <td><p>An OAuth scope string.</p>
</td>
        </tr><tr id="Audience">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/common.fidl#34">Audience</a></td>
            <td>
                <code>string</code>[<code><a class='link' href='#MAX_AUDIENCE_SIZE'>MAX_AUDIENCE_SIZE</a></code>]</td>
            <td><p>An OpenID audience string.</p>
</td>
        </tr><tr id="ServiceProvider">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/token_manager.fidl#18">ServiceProvider</a></td>
            <td>
                <code>string</code></td>
            <td><p>The primary domain name of the service provider used to authorize accounts.
Only one <code>AuthProvider</code> component can be installed for each service provider
at a time.</p>
</td>
        </tr></table>

