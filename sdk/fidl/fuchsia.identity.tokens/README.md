[TOC]

# fuchsia.identity.tokens

<p>Defines the data types and protocols used to request user authorization
tokens and identity information from service providers and identity
providers.</p>
<p>The actual interaction with these providers is through lower level protocols
defined in <code>fuchsia.id.external</code>.</p>







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
                <code>string[1024]</code>
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
                <code>int64</code>
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
                <code>int64</code>
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
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/common.fidl#8">MAX_ACCOUNT_ID_SIZE</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum length of an account ID string, in bytes.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/common.fidl#17">MAX_CLIENT_ID_SIZE</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum length of an OAuth client ID, in bytes.
We reserve the right to increase this size in future.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/common.fidl#24">MAX_SCOPE_SIZE</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum length of an OAuth scope, in bytes.
We reserve the right to increase this size in future.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/common.fidl#31">MAX_SCOPE_COUNT</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum number of OAuth scopes that may be requested for a single token.
We reserve the right to increase this value in future.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/common.fidl#35">MAX_AUDIENCE_SIZE</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum length of an OpenID audience string, in bytes.
We reserve the right to increase this size in future.</p>
</td>
        </tr>
    <tr>
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
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/common.fidl#13">AccountId</a></td>
            <td>
                <code>string</code>[<code><a class='link' href='#MAX_ACCOUNT_ID_SIZE'>MAX_ACCOUNT_ID_SIZE</a></code>]</td>
            <td><p>An identifier for the account that a token is issued against, as specified
by the authorization server. Account identifiers are guaranteed to be unique
within an auth provider type.</p>
</td>
        </tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/common.fidl#20">ClientId</a></td>
            <td>
                <code>string</code>[<code><a class='link' href='#MAX_CLIENT_ID_SIZE'>MAX_CLIENT_ID_SIZE</a></code>]</td>
            <td><p>An OAuth client ID string.</p>
</td>
        </tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/common.fidl#27">Scope</a></td>
            <td>
                <code>string</code>[<code><a class='link' href='#MAX_SCOPE_SIZE'>MAX_SCOPE_SIZE</a></code>]</td>
            <td><p>An OAuth scope string.</p>
</td>
        </tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.tokens/common.fidl#38">Audience</a></td>
            <td>
                <code>string</code>[<code><a class='link' href='#MAX_AUDIENCE_SIZE'>MAX_AUDIENCE_SIZE</a></code>]</td>
            <td><p>An OpenID audience string.</p>
</td>
        </tr></table>

