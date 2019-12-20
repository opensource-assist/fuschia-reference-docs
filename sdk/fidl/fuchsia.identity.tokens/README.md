[TOC]

# fuchsia.identity.tokens

<p>Defines the data types and protocols used to request user authorization
tokens and identity information from service providers and identity
providers.</p>
<p>The actual interaction with these providers is through lower level protocols
defined in <code>fuchsia.id.external</code>.</p>

## **PROTOCOLS**

## AuthenticationContextProvider {#AuthenticationContextProvider}
*Defined in [fuchsia.identity.tokens/token_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/token_manager.fidl#97)*

<p>Implemented by a privileged system component with the ability to display UI
to the end user.</p>
<p>This is provided during the initialization of TokenManager service and is
used for any subsequent authorize calls. The UI contexts created by this
interface are used to display OAuth login and permission screens to the end
user.</p>

### GetAuthenticationUIContext {#GetAuthenticationUIContext}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.auth/'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/#AuthenticationUIContext'>AuthenticationUIContext</a>&gt;</code>
            </td>
        </tr></table>



## TokenManagerFactory {#TokenManagerFactory}
*Defined in [fuchsia.identity.tokens/token_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/token_manager.fidl#105)*

<p>This interface provides a discoverable mechanism to create TokenManager
instances for each user, and to supply auth provider configuration
information using the structs defined in <code>auth_provider.fidl</code>.</p>

### GetTokenManager {#GetTokenManager}

<p>Creates an OAuth TokenManager instance scoped for the component specified
by <code>application_url</code>, the Fuchsia user specified by <code>user_id</code>, and the list
of auth providers specified in <code>auth_provider_configs</code>.</p>
<p><code>auth_context_provider</code> is used to generate AuthenticationUIContexts during
TokenManager methods that require UI, unless the caller of those methods
supplies an alternative AuthenticationUIContext.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>user_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>application_url</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>auth_provider_configs</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#AuthProviderConfig'>AuthProviderConfig</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>auth_context_provider</code></td>
            <td>
                <code><a class='link' href='#AuthenticationContextProvider'>AuthenticationContextProvider</a></code>
            </td>
        </tr><tr>
            <td><code>token_manager</code></td>
            <td>
                <code>request&lt;<a class='link' href='#TokenManager'>TokenManager</a>&gt;</code>
            </td>
        </tr></table>



## TokenManager {#TokenManager}
*Defined in [fuchsia.identity.tokens/token_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/token_manager.fidl#129)*

<p>This interface manages OAuth tokens at the Fuchsia system level for different
auth identity providers.</p>
<p>If user authorization is required for minting tokens, TokenManager uses the
<code>auth_context_provider's</code> UI context for displaying OAuth UI to the end user.</p>
<p>After initialization, TokenManager handles are typically handed out by
Framework to components like Ledger and Agents. These components fetch
OAuth tokens from any configured auth provider, and use the
<code>auth_context_provider</code> initialized above for new authorizations.</p>

### Authorize {#Authorize}

<p>The first step of OAuth is to get authorization from the user. For Fuchsia
components, this is accomplished by displaying OAuth permissions in a view
provided by the caller. This view will use <code>auth_ui_context</code> if supplied,
or the <code>auth_context_provider</code> supplied at TokenManager creation if not.
The component's OAuth configuration is provided in <code>app_config</code> and
<code>app_scopes</code>. An optional <code>user_profile_id</code> that uniquely identifies an
account for a given auth provider may be provided to identify an existing
account during a re-auth flow.</p>
<p>IoT ID authorization includes a mode where the user authorizes on a second
device and that device acquires an auth code from the auth provider.
In this mode, the auth code may be supplied in <code>auth_code</code> and no local
user interface will be displayed.</p>
<p>After the user has successfully authorized, Token manager receives and
securely stores a persistent credential, such as an OAuth refresh token,
for the intended scopes. TokenManager later uses this credential for
minting short lived tokens.</p>
<p>If the operation is successful, an OK status is returned along with user
profile information in <code>user_profile_info</code> such as the user's email,
image_url, profile_url, and first and last names as configured on the auth
provider backend system.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>app_config</code></td>
            <td>
                <code><a class='link' href='#AppConfig'>AppConfig</a></code>
            </td>
        </tr><tr>
            <td><code>auth_ui_context</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/#AuthenticationUIContext'>AuthenticationUIContext</a>?</code>
            </td>
        </tr><tr>
            <td><code>app_scopes</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr><tr>
            <td><code>user_profile_id</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr><tr>
            <td><code>auth_code</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr><tr>
            <td><code>user_profile_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/#UserProfileInfo'>UserProfileInfo</a>?</code>
            </td>
        </tr></table>

### GetAccessToken {#GetAccessToken}

<p>Returns a downscoped access token from an auth provider for the given user
<code>user_profile_id</code> and <code>scopes</code> to a Fuchsia component. The component's
OAuth configuration is provided in <code>app_config</code> and the <code>user_profile_id</code>
is the unique user identifier returned by the Authorize() call.</p>
<p>In the interests of performance, Token Manager does not place the supplied
scopes in a canonical order during caching. To benefit from caching of
tokens, clients must request the same scopes in the same order across
calls.</p>
<p>The access token is returned from cache if possible, otherwise the auth
provider is used to exchange the persistent credential for a new access
token.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>app_config</code></td>
            <td>
                <code><a class='link' href='#AppConfig'>AppConfig</a></code>
            </td>
        </tr><tr>
            <td><code>user_profile_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>app_scopes</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr><tr>
            <td><code>access_token</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr></table>

### GetIdToken {#GetIdToken}

<p>Returns a JWT identity token from an auth provider to a Fuchsia component
intended for the given <code>audience</code>. The component's OAuth configuration is
supplied in <code>app_config</code>, the intended recipient of the id_token is
supplied in <code>audience</code>, and <code>user_profile_id</code> is a unique account
identifier returned by the Authorize() or ListProfileIds() calls.</p>
<p><code>user_profile_id</code> is the unique user identifier returned by the
Authorize() call.</p>
<p>The identity token is returned from cache if possible, otherwise the auth
provider is used to exchange the persistant credential for a new identity
token.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>app_config</code></td>
            <td>
                <code><a class='link' href='#AppConfig'>AppConfig</a></code>
            </td>
        </tr><tr>
            <td><code>user_profile_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>audience</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr><tr>
            <td><code>id_token</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr></table>

### GetFirebaseToken {#GetFirebaseToken}

<p>Returns a Firebase token from an auth provider for the given account and
Fuchsia component, and Firebase client. The component's OAuth configuration
is supplied in <code>app_config</code>, the Firebase client is supplied in
<code>firebase_api_key</code>, and <code>user_profile_id</code> is a unique account identifier
returned by the Authorize() or ListProfileIds() calls.</p>
<p>This api invokes firebase auth's VerifyAssertion endpoint that takes an
OAuth IdToken as the fuchsia.ui.input. Audience is the intended recipient
of the firebase id token.</p>
<p>The Firebase auth token is returned from cache if possible, otherwise it is
refreshed from the auth provider.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>app_config</code></td>
            <td>
                <code><a class='link' href='#AppConfig'>AppConfig</a></code>
            </td>
        </tr><tr>
            <td><code>user_profile_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>audience</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>firebase_api_key</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr><tr>
            <td><code>firebase_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/#FirebaseToken'>FirebaseToken</a>?</code>
            </td>
        </tr></table>

### DeleteAllTokens {#DeleteAllTokens}

<p>Deletes and revokes all long lived and short lived tokens generated for
an account and on behalf of a Fuchsia component. The component's OAuth
configuration is provided in <code>app_config</code> and <code>user_profile_id</code>
is a unique account identifier returned by the Authorize() or
ListProfileIds() calls.</p>
<p>Deletion of tokens involves three steps:</p>
<ol>
<li>Revoking credentials remotely at the auth provider.</li>
<li>Deleting short lived tokens from the in-memory cache.</li>
<li>Deleting persistent credentials stored locally on disk.</li>
</ol>
<p>If <code>force</code> is false then a failure at step 1 will terminate the method,
ensuring client and server state remain consistent. If <code>force</code> is true
then steps 2&amp;3 will be performed and the method will return OK even if
step 1 fails, ensuring the local credentials are wiped in all
circumstances.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>app_config</code></td>
            <td>
                <code><a class='link' href='#AppConfig'>AppConfig</a></code>
            </td>
        </tr><tr>
            <td><code>user_profile_id</code></td>
            <td>
                <code>string</code>
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
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>

### ListProfileIds {#ListProfileIds}

<p>Returns a vector of all currently authorized user_profile_ids for a
component's OAuth configuration provided in <code>app_config</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>app_config</code></td>
            <td>
                <code><a class='link' href='#AppConfig'>AppConfig</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr><tr>
            <td><code>user_profile_ids</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr></table>



## **STRUCTS**

### AuthProviderConfig {#AuthProviderConfig}
*Defined in [fuchsia.identity.tokens/token_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/token_manager.fidl#51)*



<p>Stores configuration parameters required to connect to available
<code>AuthProvider</code>s. It is used by TokenManager to instantiate all auth providers
during startup.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>auth_provider_type</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>Type of OAuth Identity provider. An identity provider authenticates and
authorizes users for accessing their services. They also provide unique
identifiers for users to interact with the system and may provide
information about the user that is known to the provider.</p>
<p>Sample auth provider types include:
Dev : An identity provider that's used for development and testing.
Google: Uses Google as the identity provider. Authorization from Google
requires a working network connection and a web view.
Spotify: Uses Spotify as an identity provider.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>url</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>Url of the Fuchsia component implementing the AuthProvider.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>params</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
            <td><p>Optional parameters specified during AuthProvider startup.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### AppConfig {#AppConfig}
*Defined in [fuchsia.identity.tokens/token_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/token_manager.fidl#73)*



<p>Stores OAuth configuration details for a given client application. These
details are used in the OAuth authorization step.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>auth_provider_type</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>An OAuth identity provider matching a configuration set in
AuthProviderConfig.auth_provider_type.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>client_id</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>OAuth client id.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>client_secret</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>OAuth client secret.
This field is optional and will only be used on calls to Authorize.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>redirect_uri</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>OAuth application's redirect uri.
This field is optional and will only be used on calls to Authorize.</p>
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### Status {#Status}
Type: <code>uint32</code>

*Defined in [fuchsia.identity.tokens/token_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/token_manager.fidl#10)*

<p>Specifies the success/failure status of TokenManager calls.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OK</code></td>
            <td><code>0</code></td>
            <td><p>The command completed successfully</p>
</td>
        </tr><tr>
            <td><code>AUTH_PROVIDER_SERVICE_UNAVAILABLE</code></td>
            <td><code>1</code></td>
            <td><p>The command referred to a missing, misconfigured, or failed auth provider.
Retrying is not recommended.</p>
</td>
        </tr><tr>
            <td><code>AUTH_PROVIDER_SERVER_ERROR</code></td>
            <td><code>2</code></td>
            <td><p>The auth server was reachable but responded with an error. These errors
are typically caused by a configuration problem or a revoked token and so
should not be retried.</p>
</td>
        </tr><tr>
            <td><code>INTERNAL_ERROR</code></td>
            <td><code>3</code></td>
            <td><p>An internal error occurred. This usually indicates a bug within the Token
Manager itself. Retry is optional.</p>
</td>
        </tr><tr>
            <td><code>INVALID_AUTH_CONTEXT</code></td>
            <td><code>4</code></td>
            <td><p>An invalid or non-functional AuthContextProvider was provided. Retrying is
unlikely to correct this error.</p>
</td>
        </tr><tr>
            <td><code>INVALID_REQUEST</code></td>
            <td><code>5</code></td>
            <td><p>The request was malformed in some way, such as using an empty string for
the user_profile_id. The request should not be retried.</p>
</td>
        </tr><tr>
            <td><code>USER_NOT_FOUND</code></td>
            <td><code>6</code></td>
            <td><p>The requested user profile could not be found in the database. The request
should not be retried.</p>
</td>
        </tr><tr>
            <td><code>IO_ERROR</code></td>
            <td><code>7</code></td>
            <td><p>A local error occurred such as disk I/O or memory allocation. Retry, after
a delay, is recommended.</p>
</td>
        </tr><tr>
            <td><code>UNKNOWN_ERROR</code></td>
            <td><code>8</code></td>
            <td><p>Some other problem occurred that cannot be classified using one of the more
specific statuses. Retry is optional.</p>
</td>
        </tr><tr>
            <td><code>REAUTH_REQUIRED</code></td>
            <td><code>9</code></td>
            <td><p>The auth server requires that the user reauthenticate. The client should
call the Authorize method.</p>
</td>
        </tr><tr>
            <td><code>USER_CANCELLED</code></td>
            <td><code>10</code></td>
            <td><p>The user cancelled the flow. User consent is required before any retry.</p>
</td>
        </tr><tr>
            <td><code>NETWORK_ERROR</code></td>
            <td><code>11</code></td>
            <td><p>A network error occurred while communicating with the auth server. Retry,
after a delay, is recommended.</p>
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
            <td><p>The time on <code>ZX_CLOCK_UTC</code> at which the token will expire. If the field is
absent the token does not have a fixed expiry time.</p>
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
            <td><p>The time on <code>ZX_CLOCK_UTC</code> at which the token will expire. If the field is
absent the token does not have a fixed expiry time.</p>
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









## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="MAX_ACCOUNT_ID_SIZE">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/common.fidl#8">MAX_ACCOUNT_ID_SIZE</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum length of an account ID string, in bytes.</p>
</td>
        </tr>
    <tr id="MAX_CLIENT_ID_SIZE">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/common.fidl#17">MAX_CLIENT_ID_SIZE</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum length of an OAuth client ID, in bytes.
We reserve the right to increase this size in future.</p>
</td>
        </tr>
    <tr id="MAX_SCOPE_SIZE">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/common.fidl#24">MAX_SCOPE_SIZE</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum length of an OAuth scope, in bytes.
We reserve the right to increase this size in future.</p>
</td>
        </tr>
    <tr id="MAX_SCOPE_COUNT">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/common.fidl#31">MAX_SCOPE_COUNT</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum number of OAuth scopes that may be requested for a single token.
We reserve the right to increase this value in future.</p>
</td>
        </tr>
    <tr id="MAX_AUDIENCE_SIZE">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/common.fidl#35">MAX_AUDIENCE_SIZE</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum length of an OpenID audience string, in bytes.
We reserve the right to increase this size in future.</p>
</td>
        </tr>
    <tr id="MAX_AUDIENCE_COUNT">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/common.fidl#42">MAX_AUDIENCE_COUNT</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum number of audiences that may be requested for a single ID token.
We reserve the right to increase this value in future.</p>
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
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/common.fidl#20">ClientId</a></td>
            <td>
                <code>string</code>[<code><a class='link' href='#MAX_CLIENT_ID_SIZE'>MAX_CLIENT_ID_SIZE</a></code>]</td>
            <td><p>An OAuth client ID string.</p>
</td>
        </tr><tr id="Scope">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/common.fidl#27">Scope</a></td>
            <td>
                <code>string</code>[<code><a class='link' href='#MAX_SCOPE_SIZE'>MAX_SCOPE_SIZE</a></code>]</td>
            <td><p>An OAuth scope string.</p>
</td>
        </tr><tr id="Audience">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/common.fidl#38">Audience</a></td>
            <td>
                <code>string</code>[<code><a class='link' href='#MAX_AUDIENCE_SIZE'>MAX_AUDIENCE_SIZE</a></code>]</td>
            <td><p>An OpenID audience string.</p>
</td>
        </tr></table>

