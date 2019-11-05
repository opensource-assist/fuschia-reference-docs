[TOC]

# fuchsia.identity.internal


## **PROTOCOLS**

## AccountHandlerControl {#AccountHandlerControl}
*Defined in [fuchsia.identity.internal/account_handler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/identity/fidl/account_handler.fidl#76)*

 The control channel for an AccountHandler component.

 This interface is intended only for use by the AccountManager component that
 starts instances of AccountHandler. We define which account the handler
 should be handling one time via this channel rather than via startup flags to
 provide additional flexibility given the range of scenarios:
 * The account is completely new
 * The account is being added to the current device for the first time
 * Account information is already present on the local disk and is readable
 * Account information is already present on the local disk but is not yet
   readable because the disk is not yet decrypted.

 A given Account Handler progresses through the following state machine:
 ```
                                        |
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
                 +------------->|  Initialized  |
                                +---------------+
                                        |
                                        | Terminate
                                        V
                                +---------------+
                                |   Finished    |
                                +---------------+
 ```

 * `Uninitialized` - the handler has just been instantiated and contains no
 account information.
 * `PendingTranfer` - the handler is awaiting an account transfer.  It has
 created a public key pair that will be associated with the account on this
 device, but contains no other account information.
 * `Transferred` - the handler has received transferred account information
 and is holding it in memory.  In this state, the account transfer is not
 yet known to be valid, and is pending further validation from account
 manager.  The account is not available for use, and regardless of the
 intended lifetime of the account on this device, the account is not
 saved to disk.
 * `Initialized` - the handler has loaded account information and is ready
 to serve requests for the `Account` interface.  If the account is
 persistent on this device, then it is saved to disk.
 * `Finished` - the handler is in the process of shutting down and will soon
 terminate.

### CreateAccount {#CreateAccount}

 Creates a completely new Fuchsia account.

 `context` An `AccountHandlerContext` that can supply account and
           authentication services and contextual state.
 `id` The new account's local identifier.

 Fails with FAILED_PRECONDITION if the AccountHandler is not in the `Uninitialized`
 state.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>context</code></td>
            <td>
                <code><a class='link' href='#AccountHandlerContext'>AccountHandlerContext</a></code>
            </td>
        </tr><tr>
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
                <code><a class='link' href='#AccountHandlerControl_CreateAccount_Result'>AccountHandlerControl_CreateAccount_Result</a></code>
            </td>
        </tr></table>

### LoadAccount {#LoadAccount}

 Loads information about a Fuchsia account that was previously provisioned
 on the current device.

 `context` An `AccountHandlerContext` that can supply account and
           authentication services and contextual state.
 `id` The account's local identifier.

 Fails with FAILED_PRECONDITION if the AccountHandler is not in the `Uninitialized`
 state.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>context</code></td>
            <td>
                <code><a class='link' href='#AccountHandlerContext'>AccountHandlerContext</a></code>
            </td>
        </tr><tr>
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

 Prepares the AccountHandler to receive an account from another device through
 direct transfer.  This moves the AccountHandler from the `Uninitialized`
 state to the `PendingTransfer` state.

 `PrepareForAccountTransfer` should be used in conjunction with
 `PerformAccountTransfer`, `FinalizeAccountTransfer`, and
 `EncryptAccountData` to provision an existing account on another device
 (source) to this device (target).

 The expected sequence of calls to setup an AccountHandler with a transferred
 account is as follows:
 1. `PrepareForAccountTransfer` is called on the target device.
 2. The public key for the target device is retrieved using `GetPublicKey`
    and handed to the source device.
 3. Account data is encrypted on the source device using the public key
    with `EncryptAccountData`.
 4. The encrypted account data is passed in to AccountHandler on the target
    device with `PerformAccountTransfer`.
 5. After any validation, the transfer is finalized on the target device
    with a call to `FinalizeAccountTransfer`.

 Fails with FAILED_PRECONDITION if the AccountHandler is not in the `Uninitialized`
 state.

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

 Loads the encrypted account into memory, but does not make it available
 for use yet.  The account data passed in is expected to be serialized as
 an `AccountTransferContainer` and encrypted using the public key
 retrieved from `GetPublicKey`.  This format of account data is provided
 by `EncryptAccountData` on the source device.

 Moves the AccountHandler from the `PendingTransfer` state to the
 `Transferred` state.

 `encrypted_account_data` Account data retrieved on the source device
                          using `EncryptAccountData`.

 Fails with FAILED_PRECONDITION if the AccountHandler is not in the
 `PendingTransfer` state.

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

 Completes the account transfer started through
 `PrepareForAccountTransfer` and `PerformAccountTransfer`.  This saves
 the account to disk if the account is persistent and makes it available
 for use.

 Moves the AccountHandler from the `Transferred` state to the
 `Initialized` state.

 `context` An `AccountHandlerContext` that can supply account and
           authentication services and contextual state.
 `id` The account's local identifier.

 Fails with FAILED_PRECONDITION if the AccountHandler is not in the `Transferred`
 state.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>context</code></td>
            <td>
                <code><a class='link' href='#AccountHandlerContext'>AccountHandlerContext</a></code>
            </td>
        </tr><tr>
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

 Serializes and encrypts the account contained in the AccountHandler for
 transfer.  The account will be serialized as `AccountData` and
 encrypted using `target_public_key`.  The resulting
 `EncryptedAccountData` should be passed to AccountHandler on the target
 device using `PerformAccountTransfer`.

 `target_public_key` The public key used to encrypt the account data.

 Returns: `encrypted_account_data` Bytes containing the encrypted account

 Fails with FAILED_PRECONDITION if the AccountHandler is not in the `Initialized`
 state.

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

 Deletes all persistent information about the Fuchsia account handled by
 this handler, including all credentials and global identifiers.
 Credential revocation is attempted before deletion. After a
 successful call to RemoveAccount, all other open interfaces for this
 account handler will be closed and any subsequent calls on the current
 interface will fail.

 `force` If true, continues removing the account even if revocation of
         credentials fails. If false, any revocation failure will result
         in an error and the account will remain. In this case, a subset
         of the credentials may have been deleted.

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

 Connects an interface to read properties of and perform operations on
 the account handled by this handler. The AccountHandler must be in the
 `Initialized` state.

 `context_provider` An `AuthenticationContextProvider` capable of
                    supplying UI contexts used for interactive
                    authentication on this account
 `account` The server end of an `Account` channel

 Fails with FAILED_PRECONDITION if the AccountHandler is not in the `Initialized`
 state.

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

 Retrieves the public key associated with this account on this device.
 The public key is exposed so that the target AccountHandler's key can
 be distributed to the source AccountHandler during an account transfer.
 This allows the source AccountHandler to encrypt account data such that
 only the target AccountHandler can decrypt the data.

 Returns: `public_key` Public key in an asymmetric key pair associated
                       with this account on this device.

 Fails with FAILED_PRECONDITION is the AccountHandler is not in one of
 `PendingTransfer`, `Transferred`, or `Initialized` states.

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

 Generates a hash of the global account ID using the provided salt.
 Returning a hash of the global ID lets the account system determine
 whether two locally provisioned accounts represent the same account
 without storing every account's global ID. A salt is added so that
 accounts cannot be easily correlated across devices.

 The AccountHandler must be in either the `Transferred` or `Initialized`
 states.

 `salt` Bytes used as a salt while hashing global ID.

 Returns: `id_hash` A hash of the global ID of the contained account

 Fails with FAILED_PRECONDITION if the AccountHandler is not in one of
 `Transferred` or `Initialized` states.

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

 Signals that the AccountHandler should tear itself down. After the
 receiver responds by closing its handle, the caller may terminate the
 component if it hasn't already exited.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## AccountHandlerContext {#AccountHandlerContext}
*Defined in [fuchsia.identity.internal/account_handler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/identity/fidl/account_handler.fidl#260)*

 An interface that supplies the account and authentication services that
 an AccountHandler needs to perform its role in the system.

 In the v2 Component architecture this service will be supplied into the
 namespace of AccountHandler by the component that launches it (i.e. the
 AccountManager).  Until then an AccountHandlerContext is supplied explicitly
 in the initialization calls on the AccountHandlerControl interface.

### GetAuthProvider {#GetAuthProvider}

 Connects an interface to a particular AuthProvider, launching it if
 necessary.

 `auth_provider_type` An OAuth identity provider matching a configuration
                      set in an AuthProviderConfig.auth_provider_type
 `auth_provider` The server end of an `AuthProvider` channel

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





## **TABLES**

### AccountData {#AccountData}


*Defined in [fuchsia.identity.internal/account_handler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/identity/fidl/account_handler.fidl#273)*

 Contents of an account, used for serialization during account transfer.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>global_id</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
            </td>
            <td> A globally unique identifier for the account.
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







