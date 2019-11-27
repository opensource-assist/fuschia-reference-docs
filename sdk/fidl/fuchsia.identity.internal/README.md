[TOC]

# fuchsia.identity.internal


## **PROTOCOLS**

## AccountHandlerControl {#AccountHandlerControl}
*Defined in [fuchsia.identity.internal/account_handler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/identity/fidl/account_handler.fidl#81)*

<p>The control channel for an AccountHandler component.</p>
<p>This interface is intended only for use by the AccountManager component that
starts instances of AccountHandler. We define which account the handler
should be handling one time via this channel rather than via startup flags to
provide additional flexibility given the range of scenarios:</p>
<ul>
<li>The account is completely new</li>
<li>The account is being added to the current device for the first time</li>
<li>Account information is already present on the local disk and is readable</li>
<li>Account information is already present on the local disk but is not yet
readable because the disk is not yet decrypted.</li>
</ul>
<p>A given Account Handler progresses through the following state machine:</p>
<pre><code>                                       |
                                       V
                               +---------------+
                +--------------| Uninitialized |
                |              +---------------+
                |                      |
                | PrepareForTransfer   |
                V                      |
      +------------------+             |
      | PendingTransfer  |             |
      +------------------+             |
                |                      |
                | PerformTransfer      | CreateAccount/
                V                      | LoadAccount
      +------------------+             |
      |   Transferred    |             |
      +------------------+             |
                |                      |
                | FinalizeTransfer     |
                |                      V
                |              +---------------+
                +-------------&gt;|  Initialized  |
                               +---------------+
                                       |
                                       | Terminate
                                       V
                               +---------------+
                               |   Finished    |
                               +---------------+
</code></pre>
<ul>
<li><code>Uninitialized</code> - the handler has just been instantiated and contains no
account information.</li>
<li><code>PendingTranfer</code> - the handler is awaiting an account transfer.  It has
created a public key pair that will be associated with the account on this
device, but contains no other account information.</li>
<li><code>Transferred</code> - the handler has received transferred account information
and is holding it in memory.  In this state, the account transfer is not
yet known to be valid, and is pending further validation from account
manager.  The account is not available for use, and regardless of the
intended lifetime of the account on this device, the account is not
saved to disk.</li>
<li><code>Initialized</code> - the handler has loaded account information and is ready
to serve requests for the <code>Account</code> interface.  If the account is
persistent on this device, then it is saved to disk.</li>
<li><code>Finished</code> - the handler is in the process of shutting down and will soon
terminate.</li>
</ul>

### CreateAccount {#CreateAccount}

<p>Creates a completely new Fuchsia account.</p>
<p><code>account_id</code> The new account's local identifier.
<code>auth_mechanism_id</code> An <code>AuthMechanismId</code> for a storage
unlock-capable authentication mechanism. If
provided, a single enrollment of that
mechanism will be created for storage
unlock.</p>
<p>Fails with FAILED_PRECONDITION if the AccountHandler is not in the <code>Uninitialized</code>
state.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>account_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>auth_mechanism_id</code></td>
            <td>
                <code>string[2083]?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#AccountHandlerControl_CreateAccount_Result'>AccountHandlerControl_CreateAccount_Result</a></code>
            </td>
        </tr></table>

### LoadAccount {#LoadAccount}

<p>Loads information about a Fuchsia account that was previously provisioned
on the current device.</p>
<p><code>id</code> The account's local identifier.</p>
<p>Fails with FAILED_PRECONDITION if the AccountHandler is not in the <code>Uninitialized</code>
state.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#AccountHandlerControl_LoadAccount_Result'>AccountHandlerControl_LoadAccount_Result</a></code>
            </td>
        </tr></table>

### PrepareForAccountTransfer {#PrepareForAccountTransfer}

<p>Prepares the AccountHandler to receive an account from another device through
direct transfer.  This moves the AccountHandler from the <code>Uninitialized</code>
state to the <code>PendingTransfer</code> state.</p>
<p><code>PrepareForAccountTransfer</code> should be used in conjunction with
<code>PerformAccountTransfer</code>, <code>FinalizeAccountTransfer</code>, and
<code>EncryptAccountData</code> to provision an existing account on another device
(source) to this device (target).</p>
<p>The expected sequence of calls to setup an AccountHandler with a transferred
account is as follows:</p>
<ol>
<li><code>PrepareForAccountTransfer</code> is called on the target device.</li>
<li>The public key for the target device is retrieved using <code>GetPublicKey</code>
and handed to the source device.</li>
<li>Account data is encrypted on the source device using the public key
with <code>EncryptAccountData</code>.</li>
<li>The encrypted account data is passed in to AccountHandler on the target
device with <code>PerformAccountTransfer</code>.</li>
<li>After any validation, the transfer is finalized on the target device
with a call to <code>FinalizeAccountTransfer</code>.</li>
</ol>
<p>Fails with FAILED_PRECONDITION if the AccountHandler is not in the <code>Uninitialized</code>
state.</p>

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
                <code><a class='link' href='#AccountHandlerControl_PrepareForAccountTransfer_Result'>AccountHandlerControl_PrepareForAccountTransfer_Result</a></code>
            </td>
        </tr></table>

### PerformAccountTransfer {#PerformAccountTransfer}

<p>Loads the encrypted account into memory, but does not make it available
for use yet.  The account data passed in is expected to be serialized as
an <code>AccountTransferContainer</code> and encrypted using the public key
retrieved from <code>GetPublicKey</code>.  This format of account data is provided
by <code>EncryptAccountData</code> on the source device.</p>
<p>Moves the AccountHandler from the <code>PendingTransfer</code> state to the
<code>Transferred</code> state.</p>
<p><code>encrypted_account_data</code> Account data retrieved on the source device
using <code>EncryptAccountData</code>.</p>
<p>Fails with FAILED_PRECONDITION if the AccountHandler is not in the
<code>PendingTransfer</code> state.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>encrypted_account_data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[16000]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#AccountHandlerControl_PerformAccountTransfer_Result'>AccountHandlerControl_PerformAccountTransfer_Result</a></code>
            </td>
        </tr></table>

### FinalizeAccountTransfer {#FinalizeAccountTransfer}

<p>Completes the account transfer started through
<code>PrepareForAccountTransfer</code> and <code>PerformAccountTransfer</code>.  This saves
the account to disk if the account is persistent and makes it available
for use.</p>
<p>Moves the AccountHandler from the <code>Transferred</code> state to the
<code>Initialized</code> state.</p>
<p><code>id</code> The account's local identifier.</p>
<p>Fails with FAILED_PRECONDITION if the AccountHandler is not in the <code>Transferred</code>
state.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#AccountHandlerControl_FinalizeAccountTransfer_Result'>AccountHandlerControl_FinalizeAccountTransfer_Result</a></code>
            </td>
        </tr></table>

### EncryptAccountData {#EncryptAccountData}

<p>Serializes and encrypts the account contained in the AccountHandler for
transfer.  The account will be serialized as <code>AccountData</code> and
encrypted using <code>target_public_key</code>.  The resulting
<code>EncryptedAccountData</code> should be passed to AccountHandler on the target
device using <code>PerformAccountTransfer</code>.</p>
<p><code>target_public_key</code> The public key used to encrypt the account data.</p>
<p>Returns: <code>encrypted_account_data</code> Bytes containing the encrypted account</p>
<p>Fails with FAILED_PRECONDITION if the AccountHandler is not in the <code>Initialized</code>
state.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>target_public_key</code></td>
            <td>
                <code><a class='link' href='../fuchsia.kms/'>fuchsia.kms</a>/<a class='link' href='../fuchsia.kms/#PublicKey'>PublicKey</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#AccountHandlerControl_EncryptAccountData_Result'>AccountHandlerControl_EncryptAccountData_Result</a></code>
            </td>
        </tr></table>

### RemoveAccount {#RemoveAccount}

<p>Deletes all persistent information about the Fuchsia account handled by
this handler, including all credentials and global identifiers.
Credential revocation is attempted before deletion. After a
successful call to RemoveAccount, all other open interfaces for this
account handler will be closed and any subsequent calls on the current
interface will fail.</p>
<p><code>force</code> If true, continues removing the account even if revocation of
credentials fails. If false, any revocation failure will result
in an error and the account will remain. In this case, a subset
of the credentials may have been deleted.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
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
                <code><a class='link' href='#AccountHandlerControl_RemoveAccount_Result'>AccountHandlerControl_RemoveAccount_Result</a></code>
            </td>
        </tr></table>

### GetAccount {#GetAccount}

<p>Connects an interface to read properties of and perform operations on
the account handled by this handler. The AccountHandler must be in the
<code>Initialized</code> state.</p>
<p><code>context_provider</code> An <code>AuthenticationContextProvider</code> capable of
supplying UI contexts used for interactive
authentication on this account
<code>account</code> The server end of an <code>Account</code> channel</p>
<p>Fails with FAILED_PRECONDITION if the AccountHandler is not in the <code>Initialized</code>
state.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>auth_context_provider</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/#AuthenticationContextProvider'>AuthenticationContextProvider</a></code>
            </td>
        </tr><tr>
            <td><code>account</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.identity.account/'>fuchsia.identity.account</a>/<a class='link' href='../fuchsia.identity.account/#Account'>Account</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#AccountHandlerControl_GetAccount_Result'>AccountHandlerControl_GetAccount_Result</a></code>
            </td>
        </tr></table>

### GetPublicKey {#GetPublicKey}

<p>Retrieves the public key associated with this account on this device.
The public key is exposed so that the target AccountHandler's key can
be distributed to the source AccountHandler during an account transfer.
This allows the source AccountHandler to encrypt account data such that
only the target AccountHandler can decrypt the data.</p>
<p>Returns: <code>public_key</code> Public key in an asymmetric key pair associated
with this account on this device.</p>
<p>Fails with FAILED_PRECONDITION is the AccountHandler is not in one of
<code>PendingTransfer</code>, <code>Transferred</code>, or <code>Initialized</code> states.</p>

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
                <code><a class='link' href='#AccountHandlerControl_GetPublicKey_Result'>AccountHandlerControl_GetPublicKey_Result</a></code>
            </td>
        </tr></table>

### GetGlobalIdHash {#GetGlobalIdHash}

<p>Generates a hash of the global account ID using the provided salt.
Returning a hash of the global ID lets the account system determine
whether two locally provisioned accounts represent the same account
without storing every account's global ID. A salt is added so that
accounts cannot be easily correlated across devices.</p>
<p>The AccountHandler must be in either the <code>Transferred</code> or <code>Initialized</code>
states.</p>
<p><code>salt</code> Bytes used as a salt while hashing global ID.</p>
<p>Returns: <code>id_hash</code> A hash of the global ID of the contained account</p>
<p>Fails with FAILED_PRECONDITION if the AccountHandler is not in one of
<code>Transferred</code> or <code>Initialized</code> states.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>salt</code></td>
            <td>
                <code>uint8[32]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#AccountHandlerControl_GetGlobalIdHash_Result'>AccountHandlerControl_GetGlobalIdHash_Result</a></code>
            </td>
        </tr></table>

### Terminate {#Terminate}

<p>Signals that the AccountHandler should tear itself down. After the
receiver responds by closing its handle, the caller may terminate the
component if it hasn't already exited.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## AccountHandlerContext {#AccountHandlerContext}
*Defined in [fuchsia.identity.internal/account_handler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/identity/fidl/account_handler.fidl#261)*

<p>An interface that supplies the account and authentication services that
an AccountHandler needs to perform its role in the system.</p>
<p>This service is supplied into the namespace of AccountHandler by the
component that launches it (i.e. the AccountManager).</p>

### GetAuthProvider {#GetAuthProvider}

<p>Connects to the <code>AuthProvider</code> implementation for a particular service
provider, launching it if necessary.  This method will soon be removed
along with the <code>AuthProvider</code> protocol.</p>
<p><code>auth_provider_type</code> An OAuth identity provider matching a configuration
set in an AuthProviderConfig.auth_provider_type
<code>auth_provider</code> The server end of an <code>AuthProvider</code> channel</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>auth_provider_type</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>auth_provider</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.auth/'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/#AuthProvider'>AuthProvider</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#AccountHandlerContext_GetAuthProvider_Result'>AccountHandlerContext_GetAuthProvider_Result</a></code>
            </td>
        </tr></table>

### GetOauth {#GetOauth}

<p>Connects to the <code>Oauth</code> implementation for a particular service provider,
launching it if necessary.</p>
<p><code>auth_provider_type</code> An OAuth identity provider matching a configuration
set in an AuthProviderConfig.auth_provider_type
<code>oauth</code> The server end of an <code>Oauth</code> channel</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>auth_provider_type</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>oauth</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.identity.external/'>fuchsia.identity.external</a>/<a class='link' href='../fuchsia.identity.external/#Oauth'>Oauth</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#AccountHandlerContext_GetOauth_Result'>AccountHandlerContext_GetOauth_Result</a></code>
            </td>
        </tr></table>

### GetOpenIdConnect {#GetOpenIdConnect}

<p>Connects to the <code>OpenIdConnect</code> implementation for a particular service
provider, launching it if necessary.</p>
<p><code>auth_provider_type</code> An OpenID Connect identity provider matching a
configuration set in an
AuthProviderConfig.auth_provider_type
<code>open_id_connect</code> The server end of an <code>OpenIDConnect</code> channel</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>auth_provider_type</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>open_id_connect</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.identity.external/'>fuchsia.identity.external</a>/<a class='link' href='../fuchsia.identity.external/#OpenIdConnect'>OpenIdConnect</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#AccountHandlerContext_GetOpenIdConnect_Result'>AccountHandlerContext_GetOpenIdConnect_Result</a></code>
            </td>
        </tr></table>

### GetOauthOpenIdConnect {#GetOauthOpenIdConnect}

<p>Connects to the <code>OauthOpenIdConnect</code> implementation for a particular
service provider, launching it if necessary.</p>
<p><code>auth_provider_type</code> An OpenID Connect identity provider matching a
configuration set in an
AuthProviderConfig.auth_provider_type
<code>oauth_open_id_connect</code> The server end of an <code>OauthOpenIDConnect</code> channel</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>auth_provider_type</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>oauth_open_id_connect</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.identity.external/'>fuchsia.identity.external</a>/<a class='link' href='../fuchsia.identity.external/#OauthOpenIdConnect'>OauthOpenIdConnect</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#AccountHandlerContext_GetOauthOpenIdConnect_Result'>AccountHandlerContext_GetOauthOpenIdConnect_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### AccountHandlerControl_CreateAccount_Response {#AccountHandlerControl_CreateAccount_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### AccountHandlerControl_LoadAccount_Response {#AccountHandlerControl_LoadAccount_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### AccountHandlerControl_PrepareForAccountTransfer_Response {#AccountHandlerControl_PrepareForAccountTransfer_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### AccountHandlerControl_PerformAccountTransfer_Response {#AccountHandlerControl_PerformAccountTransfer_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### AccountHandlerControl_FinalizeAccountTransfer_Response {#AccountHandlerControl_FinalizeAccountTransfer_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### AccountHandlerControl_EncryptAccountData_Response {#AccountHandlerControl_EncryptAccountData_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>encrypted_account_data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[16000]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AccountHandlerControl_RemoveAccount_Response {#AccountHandlerControl_RemoveAccount_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### AccountHandlerControl_GetAccount_Response {#AccountHandlerControl_GetAccount_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### AccountHandlerControl_GetPublicKey_Response {#AccountHandlerControl_GetPublicKey_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>public_key</code></td>
            <td>
                <code><a class='link' href='../fuchsia.kms/'>fuchsia.kms</a>/<a class='link' href='../fuchsia.kms/#PublicKey'>PublicKey</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AccountHandlerControl_GetGlobalIdHash_Response {#AccountHandlerControl_GetGlobalIdHash_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id_hash</code></td>
            <td>
                <code>uint8[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AccountHandlerContext_GetAuthProvider_Response {#AccountHandlerContext_GetAuthProvider_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### AccountHandlerContext_GetOauth_Response {#AccountHandlerContext_GetOauth_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### AccountHandlerContext_GetOpenIdConnect_Response {#AccountHandlerContext_GetOpenIdConnect_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### AccountHandlerContext_GetOauthOpenIdConnect_Response {#AccountHandlerContext_GetOauthOpenIdConnect_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>





## **TABLES**

### AccountData {#AccountData}


*Defined in [fuchsia.identity.internal/account_handler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/identity/fidl/account_handler.fidl#308)*

<p>Contents of an account, used for serialization during account transfer.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>global_id</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
            </td>
            <td><p>A globally unique identifier for the account.</p>
</td>
        </tr></table>



## **UNIONS**

### AccountHandlerControl_CreateAccount_Result {#AccountHandlerControl_CreateAccount_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#AccountHandlerControl_CreateAccount_Response'>AccountHandlerControl_CreateAccount_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.identity.account/'>fuchsia.identity.account</a>/<a class='link' href='../fuchsia.identity.account/#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### AccountHandlerControl_LoadAccount_Result {#AccountHandlerControl_LoadAccount_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#AccountHandlerControl_LoadAccount_Response'>AccountHandlerControl_LoadAccount_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.identity.account/'>fuchsia.identity.account</a>/<a class='link' href='../fuchsia.identity.account/#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### AccountHandlerControl_PrepareForAccountTransfer_Result {#AccountHandlerControl_PrepareForAccountTransfer_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#AccountHandlerControl_PrepareForAccountTransfer_Response'>AccountHandlerControl_PrepareForAccountTransfer_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.identity.account/'>fuchsia.identity.account</a>/<a class='link' href='../fuchsia.identity.account/#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### AccountHandlerControl_PerformAccountTransfer_Result {#AccountHandlerControl_PerformAccountTransfer_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#AccountHandlerControl_PerformAccountTransfer_Response'>AccountHandlerControl_PerformAccountTransfer_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.identity.account/'>fuchsia.identity.account</a>/<a class='link' href='../fuchsia.identity.account/#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### AccountHandlerControl_FinalizeAccountTransfer_Result {#AccountHandlerControl_FinalizeAccountTransfer_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#AccountHandlerControl_FinalizeAccountTransfer_Response'>AccountHandlerControl_FinalizeAccountTransfer_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.identity.account/'>fuchsia.identity.account</a>/<a class='link' href='../fuchsia.identity.account/#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### AccountHandlerControl_EncryptAccountData_Result {#AccountHandlerControl_EncryptAccountData_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#AccountHandlerControl_EncryptAccountData_Response'>AccountHandlerControl_EncryptAccountData_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.identity.account/'>fuchsia.identity.account</a>/<a class='link' href='../fuchsia.identity.account/#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### AccountHandlerControl_RemoveAccount_Result {#AccountHandlerControl_RemoveAccount_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#AccountHandlerControl_RemoveAccount_Response'>AccountHandlerControl_RemoveAccount_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.identity.account/'>fuchsia.identity.account</a>/<a class='link' href='../fuchsia.identity.account/#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### AccountHandlerControl_GetAccount_Result {#AccountHandlerControl_GetAccount_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#AccountHandlerControl_GetAccount_Response'>AccountHandlerControl_GetAccount_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.identity.account/'>fuchsia.identity.account</a>/<a class='link' href='../fuchsia.identity.account/#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### AccountHandlerControl_GetPublicKey_Result {#AccountHandlerControl_GetPublicKey_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#AccountHandlerControl_GetPublicKey_Response'>AccountHandlerControl_GetPublicKey_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.identity.account/'>fuchsia.identity.account</a>/<a class='link' href='../fuchsia.identity.account/#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### AccountHandlerControl_GetGlobalIdHash_Result {#AccountHandlerControl_GetGlobalIdHash_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#AccountHandlerControl_GetGlobalIdHash_Response'>AccountHandlerControl_GetGlobalIdHash_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.identity.account/'>fuchsia.identity.account</a>/<a class='link' href='../fuchsia.identity.account/#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### AccountHandlerContext_GetAuthProvider_Result {#AccountHandlerContext_GetAuthProvider_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#AccountHandlerContext_GetAuthProvider_Response'>AccountHandlerContext_GetAuthProvider_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.identity.account/'>fuchsia.identity.account</a>/<a class='link' href='../fuchsia.identity.account/#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### AccountHandlerContext_GetOauth_Result {#AccountHandlerContext_GetOauth_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#AccountHandlerContext_GetOauth_Response'>AccountHandlerContext_GetOauth_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.identity.account/'>fuchsia.identity.account</a>/<a class='link' href='../fuchsia.identity.account/#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### AccountHandlerContext_GetOpenIdConnect_Result {#AccountHandlerContext_GetOpenIdConnect_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#AccountHandlerContext_GetOpenIdConnect_Response'>AccountHandlerContext_GetOpenIdConnect_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.identity.account/'>fuchsia.identity.account</a>/<a class='link' href='../fuchsia.identity.account/#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### AccountHandlerContext_GetOauthOpenIdConnect_Result {#AccountHandlerContext_GetOauthOpenIdConnect_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#AccountHandlerContext_GetOauthOpenIdConnect_Response'>AccountHandlerContext_GetOauthOpenIdConnect_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.identity.account/'>fuchsia.identity.account</a>/<a class='link' href='../fuchsia.identity.account/#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/src/identity/fidl/account_handler.fidl#12">HASH_SIZE</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/src/identity/fidl/account_handler.fidl#13">HASH_SALT_SIZE</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    
</table>

