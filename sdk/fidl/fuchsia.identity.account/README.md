[TOC]

# fuchsia.identity.account


## **PROTOCOLS**

## AccountManager {#AccountManager}
*Defined in [fuchsia.identity.account/account_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/account_manager.fidl#17)*

 AccountManager manages the overall state of Fuchsia accounts and personae on
 a Fuchsia device, installation of the AuthProviders that are used to obtain
 authentication tokens for these accounts, and access to TokenManagers for
 these accounts.

 The AccountManager is the most powerful protocol in the authentication
 system and is intended only for use by the most trusted parts of the system.

### GetAccountIds {#GetAccountIds}

 Returns a vector of all unlocked accounts provisioned on the current
 device.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>account_ids</code></td>
            <td>
                <code>vector&lt;uint64&gt;[128]</code>
            </td>
        </tr></table>

### GetAccountAuthStates {#GetAccountAuthStates}

 Returns a vector of all unlocked accounts provisioned on the current
 device and the current authentication state for each.

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
                <code><a class='link' href='#AccountManager_GetAccountAuthStates_Result'>AccountManager_GetAccountAuthStates_Result</a></code>
            </td>
        </tr></table>

### GetAccount {#GetAccount}

 Connects a channel to read properties of and perform operations on
 one account.

 `id` The account's identifier as returned by GetAccountIds()
 `context_provider` An `AuthenticationContextProvider` capable of
                    supplying UI contexts used for interactive
                    authentication on this account
 `account` The server end of an `Account` channel

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>context_provider</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/#AuthenticationContextProvider'>AuthenticationContextProvider</a></code>
            </td>
        </tr><tr>
            <td><code>account</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Account'>Account</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#AccountManager_GetAccount_Result'>AccountManager_GetAccount_Result</a></code>
            </td>
        </tr></table>

### RegisterAccountListener {#RegisterAccountListener}

 Connects a channel that will receive changes in the provisioned
 accounts and their authentication state. Optionally this channel will
 also receive the initial set of accounts and authentication states onto
 which changes may be applied.

 `listener` The client end of an `AccountListener` channel
 `options` An `AccountListenerOptions` that defines the set of events to
           be sent to the listener.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='#AccountListener'>AccountListener</a></code>
            </td>
        </tr><tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#AccountListenerOptions'>AccountListenerOptions</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#AccountManager_RegisterAccountListener_Result'>AccountManager_RegisterAccountListener_Result</a></code>
            </td>
        </tr></table>

### RemoveAccount {#RemoveAccount}

 Removes a provisioned Fuchsia account from the current device, revoking
 any credentials that are held for the account.

 `id` The account's identifier as returned by GetAccountIds()
 `force` If true, continues removing the account even if revocation of
         credentials fails. If false, any revocation failure will result
         in an error and the account will remain. In this case, a subset
         of the credentials may have been deleted.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
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
                <code><a class='link' href='#AccountManager_RemoveAccount_Result'>AccountManager_RemoveAccount_Result</a></code>
            </td>
        </tr></table>

### ProvisionFromAuthProvider {#ProvisionFromAuthProvider}

 Adds a Fuchsia account to the current device based on authenticating
 to a service provider (such as Google). If the service provider account
 is not already a recovery account for any Fuchsia account, a new Fuchsia
 account will be created with its recovery account set to the service
 provider account.

 `auth_context_provider` An `AuthenticationContextProvider` capable of
                         supplying UI contexts used for interactive
                         authentication
 `auth_provider_type` A unique identifier for an installed `AuthProvider`
                      that should be used to authenticate with the
                      service provider
 `lifetime` The lifetime of the account

 Returns: `account_id` The identifier of the newly added account

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>auth_context_provider</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/#AuthenticationContextProvider'>AuthenticationContextProvider</a></code>
            </td>
        </tr><tr>
            <td><code>auth_provider_type</code></td>
            <td>
                <code>string[128]</code>
            </td>
        </tr><tr>
            <td><code>lifetime</code></td>
            <td>
                <code><a class='link' href='#Lifetime'>Lifetime</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#AccountManager_ProvisionFromAuthProvider_Result'>AccountManager_ProvisionFromAuthProvider_Result</a></code>
            </td>
        </tr></table>

### ProvisionNewAccount {#ProvisionNewAccount}

 Adds a new, initially empty, Fuchsia account to the current device.

 `lifetime` The lifetime of the account

 Returns: `account_id` The identifier of the newly added account

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>lifetime</code></td>
            <td>
                <code><a class='link' href='#Lifetime'>Lifetime</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#AccountManager_ProvisionNewAccount_Result'>AccountManager_ProvisionNewAccount_Result</a></code>
            </td>
        </tr></table>

## AccountListener {#AccountListener}
*Defined in [fuchsia.identity.account/account_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/account_manager.fidl#138)*

 A protocol to receive events when the set of accounts on a device or the
 authentication states of these accounts change.

 AccountListeners may be registered through the AccountManager protocol
 and this registration also defines which types of event should be sent to
 the listener. Optionally, the AccountListener will receive an initial state
 event onto which the change events may be safely accumulated.

 All methods include an empty response to follow the "Throttle push using
 acknowledgements" FIDL design pattern.

### OnInitialize {#OnInitialize}

 A method that is called to communicate the initial set of accounts and
 their authentication states. OnInitialize is called exactly once if and
 only if AccountListenerOptions.initial_state was set when creating the
 AccountListener. When called, it will always be the first call on the
 channel. If no accounts are present on the device the vector will be
 empty.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>account_auth_states</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#AccountAuthState'>AccountAuthState</a>&gt;[128]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### OnAccountAdded {#OnAccountAdded}

 A method that is called when a new account is added to the device.
 This method is only called if AccountListenerOptions.add_account was
 set when creating the AccountListener.

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
    </table>

### OnAccountRemoved {#OnAccountRemoved}

 A method that is called when a provisioned account is removed.
 This method is only called if AccountListenerOptions.remove_account was
 set when creating the AccountListener.

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
    </table>

### OnAuthStateChanged {#OnAuthStateChanged}

 A method that is called when the authentication state of any provisioned
 account changes.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>account_auth_state</code></td>
            <td>
                <code><a class='link' href='#AccountAuthState'>AccountAuthState</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## AuthListener {#AuthListener}
*Defined in [fuchsia.identity.account/auth_target.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/auth_target.fidl#20)*

 A protocol to receive events when the authentication state of an account
 changes.

 AuthListeners may be registered through the `AuthTarget` protocol and this
 registration also defines the types of authentication state changes that
 should be sent to the listener.

 All methods include an empty response to follow the "Throttle push using
 acknowledgements" FIDL design pattern.

### OnInitialize {#OnInitialize}

 A method that is called when the AccountListener is first connected.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>auth_state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/#AuthState'>AuthState</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### OnAuthStateChanged {#OnAuthStateChanged}

 A method that is called when the authentication state of the account
 changes.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>auth_state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/#AuthState'>AuthState</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## AuthTarget {#AuthTarget}
*Defined in [fuchsia.identity.account/auth_target.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/auth_target.fidl#38)*

 A protocol that is extended by other protocols defining an entity
 (referred to as the "target") with an authentication state, such as a
 Fuchsia account or persona.

 AuthTarget defines a set of methods to monitor the current authentication
 state of an entity and to request changes in that authentication state.

### GetAuthState {#GetAuthState}

 Returns the current `AuthState` of the target.

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
                <code><a class='link' href='#AuthTarget_GetAuthState_Result'>AuthTarget_GetAuthState_Result</a></code>
            </td>
        </tr></table>

### RegisterAuthListener {#RegisterAuthListener}

 Connects a channel that will receive changes in the authentication
 state of the target.

 `listener` The client end of an `AuthListener` channel
 `initial_state` If true, the listener will receive the initial auth
                 state in addition to any changes.
 `granularity` An `AuthChangeGranularity` expressing the magnitude of
               change in authentication state than should lead to a
               callback

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='#AuthListener'>AuthListener</a></code>
            </td>
        </tr><tr>
            <td><code>initial_state</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>granularity</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/#AuthChangeGranularity'>AuthChangeGranularity</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#AuthTarget_RegisterAuthListener_Result'>AuthTarget_RegisterAuthListener_Result</a></code>
            </td>
        </tr></table>

## Account {#Account}
*Defined in [fuchsia.identity.account/auth_target.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/auth_target.fidl#68)*

 A protocol that exposes information about the personae and recovery account
 for a Fuchsia account and provides methods to manipulate these.

 An Account provides access to sensitive long term identifiers and is only
 intended only for use by a small number of trusted system components.

### GetAuthState {#GetAuthState}

 Returns the current `AuthState` of the target.

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
                <code><a class='link' href='#AuthTarget_GetAuthState_Result'>AuthTarget_GetAuthState_Result</a></code>
            </td>
        </tr></table>

### RegisterAuthListener {#RegisterAuthListener}

 Connects a channel that will receive changes in the authentication
 state of the target.

 `listener` The client end of an `AuthListener` channel
 `initial_state` If true, the listener will receive the initial auth
                 state in addition to any changes.
 `granularity` An `AuthChangeGranularity` expressing the magnitude of
               change in authentication state than should lead to a
               callback

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='#AuthListener'>AuthListener</a></code>
            </td>
        </tr><tr>
            <td><code>initial_state</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>granularity</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/#AuthChangeGranularity'>AuthChangeGranularity</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#AuthTarget_RegisterAuthListener_Result'>AuthTarget_RegisterAuthListener_Result</a></code>
            </td>
        </tr></table>

### GetAccountName {#GetAccountName}

 Returns a human readable name for the account. Account names are set by
 a human and are not guaranteed to be meaningful or unique, even among
 the accounts on a single device.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string[128]</code>
            </td>
        </tr></table>

### GetLifetime {#GetLifetime}

 Returns the account's lifetime.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>lifetime</code></td>
            <td>
                <code><a class='link' href='#Lifetime'>Lifetime</a></code>
            </td>
        </tr></table>

### GetPersonaIds {#GetPersonaIds}

 Returns a vector of all the personae defined for the account.
 NOTE: Currently all Fuchsia accounts have exactly one persona.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>persona_ids</code></td>
            <td>
                <code>vector&lt;uint64&gt;[128]</code>
            </td>
        </tr></table>

### GetDefaultPersona {#GetDefaultPersona}

 Connects a channel to read properties of and access tokens for
 the default persona for the account.

 `persona` The client end of a `Persona` channel

 Returns: `id` The identifier for the default persona

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>persona</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Persona'>Persona</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Account_GetDefaultPersona_Result'>Account_GetDefaultPersona_Result</a></code>
            </td>
        </tr></table>

### GetPersona {#GetPersona}

 Connects a channel to read properties of and access tokens for
 one of the personae for the account.

 `id` The persona's identifier as returned by GetPersonaIds()
 `persona` The client end of a `Persona` channel

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>persona</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Persona'>Persona</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Account_GetPersona_Result'>Account_GetPersona_Result</a></code>
            </td>
        </tr></table>

### GetRecoveryAccount {#GetRecoveryAccount}

 Returns the service provider account that can be used to access the
 Fuchsia account if more direct methods of authentication are not
 available, provided such an account exists.

 Returns: The `ServiceProviderAccount` used for recovery if one exists

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
                <code><a class='link' href='#Account_GetRecoveryAccount_Result'>Account_GetRecoveryAccount_Result</a></code>
            </td>
        </tr></table>

### SetRecoveryAccount {#SetRecoveryAccount}

 Sets the service provider account that can be used to access the Fuchsia
 account if more direct methods of authentication are not available.

 `account` The `ServiceProviderAccount` to use as the recovery account.
           This must be an existing account that has already been
           provisioned on the current device using TokenManager.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>account</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/#ServiceProviderAccount'>ServiceProviderAccount</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Account_SetRecoveryAccount_Result'>Account_SetRecoveryAccount_Result</a></code>
            </td>
        </tr></table>

## Persona {#Persona}
*Defined in [fuchsia.identity.account/auth_target.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/auth_target.fidl#129)*

 A protocol that exposes basic information about a Fuchsia persona and access
 to the authentication tokens that are visible through it.

 Note a Persona purposefully does not provide access to a long term
 identifier for the persona. This is to support components in the system that
 work with short lived identifiers (e.g. SessionManager), but note that long
 term identifiers can usually still be derived via the TokenManger protocol.

### GetAuthState {#GetAuthState}

 Returns the current `AuthState` of the target.

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
                <code><a class='link' href='#AuthTarget_GetAuthState_Result'>AuthTarget_GetAuthState_Result</a></code>
            </td>
        </tr></table>

### RegisterAuthListener {#RegisterAuthListener}

 Connects a channel that will receive changes in the authentication
 state of the target.

 `listener` The client end of an `AuthListener` channel
 `initial_state` If true, the listener will receive the initial auth
                 state in addition to any changes.
 `granularity` An `AuthChangeGranularity` expressing the magnitude of
               change in authentication state than should lead to a
               callback

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='#AuthListener'>AuthListener</a></code>
            </td>
        </tr><tr>
            <td><code>initial_state</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>granularity</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/#AuthChangeGranularity'>AuthChangeGranularity</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#AuthTarget_RegisterAuthListener_Result'>AuthTarget_RegisterAuthListener_Result</a></code>
            </td>
        </tr></table>

### GetLifetime {#GetLifetime}

 Returns the lifetime of this persona.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>lifetime</code></td>
            <td>
                <code><a class='link' href='#Lifetime'>Lifetime</a></code>
            </td>
        </tr></table>

### GetTokenManager {#GetTokenManager}

 Connects a channel to acquire and revoke authentication tokens for
 service provider (aka cloud service) accounts that are visible through
 this persona.

 `application_url` A url for the Fuchsia agent that this channel will be
                   used by. Applications are only allowed to access
                   tokens that they created.
 `token_manager` The client end of a `TokenManager` channel

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>application_url</code></td>
            <td>
                <code>string[2083]</code>
            </td>
        </tr><tr>
            <td><code>token_manager</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.auth/'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/#TokenManager'>TokenManager</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Persona_GetTokenManager_Result'>Persona_GetTokenManager_Result</a></code>
            </td>
        </tr></table>

### GetKeyManager {#GetKeyManager}

 Connects a channel to access and manage key material that is consistent
 across all devices with access to this persona.

 Persona key storage is a very limited resource. Only a small number of
 core components should use KeyManager, often in order to supply more
 scalable forms of synchronization to other applications (e.g. Ledger).

 `application_url` A url for the component that this channel will be
                   used by. Applications are only allowed to access
                   their own keys.
 `key_manager` The client end of a `KeyManager` channel

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>application_url</code></td>
            <td>
                <code>string[2083]</code>
            </td>
        </tr><tr>
            <td><code>key_manager</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.identity.keys/'>fuchsia.identity.keys</a>/<a class='link' href='../fuchsia.identity.keys/#KeyManager'>KeyManager</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Persona_GetKeyManager_Result'>Persona_GetKeyManager_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### AccountManager_GetAccountAuthStates_Response {#AccountManager_GetAccountAuthStates_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>account_auth_states</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#AccountAuthState'>AccountAuthState</a>&gt;[128]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AccountManager_GetAccount_Response {#AccountManager_GetAccount_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### AccountManager_RegisterAccountListener_Response {#AccountManager_RegisterAccountListener_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### AccountManager_RemoveAccount_Response {#AccountManager_RemoveAccount_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### AccountManager_ProvisionFromAuthProvider_Response {#AccountManager_ProvisionFromAuthProvider_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>account_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AccountManager_ProvisionNewAccount_Response {#AccountManager_ProvisionNewAccount_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>account_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AccountAuthState {#AccountAuthState}
*Defined in [fuchsia.identity.account/account_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/account_manager.fidl#101)*



 An `AuthState` along with the account that it applies to.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>account_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> A unique identifier for the Fuchsia account on the current device.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>auth_state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/#AuthState'>AuthState</a></code>
            </td>
            <td> An authentication state for the Fuchsia account.
</td>
            <td>No default</td>
        </tr>
</table>

### AccountListenerOptions {#AccountListenerOptions}
*Defined in [fuchsia.identity.account/account_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/account_manager.fidl#112)*



 The configuration for an AccountListener, defining the set of events that it
 will receive.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>initial_state</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, the listener will receive the initial auth state for all
 accounts.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>add_account</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, the listener will receive events when a new account is added
 to the device.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>remove_account</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, the listener will receive events.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>granularity</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/#AuthChangeGranularity'>AuthChangeGranularity</a></code>
            </td>
            <td> An `AuthChangeGranularity` expressing the magnitude of change in
 authentication state that will lead to AuthStateChange events.
</td>
            <td>No default</td>
        </tr>
</table>

### Scenario {#Scenario}
*Defined in [fuchsia.identity.account/auth_state.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/auth_state.fidl#64)*



 Defines the context to consider when creating authentication states.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>include_test</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, experimental or test authenticators are included when creating
 authentication states and MUST NOT be used to hand out sensitive user
 information.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>threat_scenario</code></td>
            <td>
                <code><a class='link' href='#ThreatScenario'>ThreatScenario</a></code>
            </td>
            <td> Defines the threat scenario to consider when creating
 authentication states.
</td>
            <td>No default</td>
        </tr>
</table>

### AuthState {#AuthState}
*Defined in [fuchsia.identity.account/auth_state.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/auth_state.fidl#98)*



 An assessment of the current presence and engagement of an account owner,
 under the provided scenario, including the system's confidence in that
 assessment and its timeliness.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>scenario</code></td>
            <td>
                <code><a class='link' href='#Scenario'>Scenario</a></code>
            </td>
            <td> The scenario that was considered when creating this authentication
 state.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>summary</code></td>
            <td>
                <code><a class='link' href='#AuthStateSummary'>AuthStateSummary</a></code>
            </td>
            <td> A high level assessment of whether the account owner is present and
 engaged.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>presence</code></td>
            <td>
                <code><a class='link' href='#Presence'>Presence</a></code>
            </td>
            <td> An assessment of whether the account owner is present.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>engagement</code></td>
            <td>
                <code><a class='link' href='#Engagement'>Engagement</a></code>
            </td>
            <td> An assessment of whether the account owner is engaged.
</td>
            <td>No default</td>
        </tr>
</table>

### AuthChangeGranularity {#AuthChangeGranularity}
*Defined in [fuchsia.identity.account/auth_state.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/auth_state.fidl#120)*



 An expression of the types of changes to an auth state that should be
 reported over listener interfaces. By default no changes will be reported.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>summary_changes</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, any changes in the `AuthStateSummary` enumeration will be
 reported.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>presence_changes</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, any changes in the `AuthState.presence` enumeration will
 be reported.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>engagement_changes</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, any changes in the `AuthState.engagement` enumeration will
 be reported.
</td>
            <td>No default</td>
        </tr>
</table>

### AuthTarget_GetAuthState_Response {#AuthTarget_GetAuthState_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>auth_state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/#AuthState'>AuthState</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AuthTarget_RegisterAuthListener_Response {#AuthTarget_RegisterAuthListener_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Account_GetDefaultPersona_Response {#Account_GetDefaultPersona_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Account_GetPersona_Response {#Account_GetPersona_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Account_GetRecoveryAccount_Response {#Account_GetRecoveryAccount_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>account</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/#ServiceProviderAccount'>ServiceProviderAccount</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Account_SetRecoveryAccount_Response {#Account_SetRecoveryAccount_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Persona_GetTokenManager_Response {#Persona_GetTokenManager_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Persona_GetKeyManager_Response {#Persona_GetKeyManager_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>



## **ENUMS**

### Presence {#Presence}
Type: <code>uint32</code>

*Defined in [fuchsia.identity.account/auth_state.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/auth_state.fidl#8)*

 An assessment of whether the account owner is present.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>LOCKED</code></td>
            <td><code>1</code></td>
            <td> The account itself is locked and inaccessible.
</td>
        </tr><tr>
            <td><code>ABSENT</code></td>
            <td><code>2</code></td>
            <td> The account owner is marked as absent.
</td>
        </tr><tr>
            <td><code>PRESENCE_UNKNOWN</code></td>
            <td><code>3</code></td>
            <td> No information (either affirming or dissenting) is available about the
 current presence of the account owner.
</td>
        </tr><tr>
            <td><code>PRESENT</code></td>
            <td><code>4</code></td>
            <td> The account owner is marked as present.
</td>
        </tr></table>

### Engagement {#Engagement}
Type: <code>uint32</code>

*Defined in [fuchsia.identity.account/auth_state.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/auth_state.fidl#24)*

 An assessment of whether the account owner is engaged.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>LOCKED</code></td>
            <td><code>1</code></td>
            <td> The account itself is locked and inaccessible.
</td>
        </tr><tr>
            <td><code>DISENGAGED</code></td>
            <td><code>2</code></td>
            <td> The account owner is marked as disengaged.
</td>
        </tr><tr>
            <td><code>ENGAGEMENT_UNKNOWN</code></td>
            <td><code>3</code></td>
            <td> No information (either affirming or dissenting) is available about the
 current engagement of the account owner.
</td>
        </tr><tr>
            <td><code>ENGAGED</code></td>
            <td><code>4</code></td>
            <td> The account owner is marked as engaged.
</td>
        </tr></table>

### ThreatScenario {#ThreatScenario}
Type: <code>uint32</code>

*Defined in [fuchsia.identity.account/auth_state.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/auth_state.fidl#40)*

 A type of attacker to consider when creating authentication states.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NONE</code></td>
            <td><code>1</code></td>
            <td> No attackers are considered.
</td>
        </tr><tr>
            <td><code>BASIC_ATTACKER</code></td>
            <td><code>2</code></td>
            <td> People that may typically and frequently gain access to a user’s device
 are considered. Examples include nefarious roommates, coworkers,
 houseguests, family members, or thieves. We assume limited technical
 skills and/or motivation and commonly available technology.

 Additionally, remote abusers performing an (initially untargeted) attack
 are considered. We assume these attackers use the standard tools of
 their trade such as password dumps, phishing toolkits, brute forcing, or
 stolen identities.
</td>
        </tr><tr>
            <td><code>ADVANCED_ATTACKER</code></td>
            <td><code>3</code></td>
            <td> Technologically capable people or organizations who are motivated to
 perform a targeted attack on a user are considered. Examples include
 freelance security professionals, organized crime, law enforcement, and
 government agencies.
</td>
        </tr></table>

### AuthStateSummary {#AuthStateSummary}
Type: <code>uint32</code>

*Defined in [fuchsia.identity.account/auth_state.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/auth_state.fidl#76)*

 A high level assessment of whether the account owner is present and engaged.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>LOCKED</code></td>
            <td><code>1</code></td>
            <td> The account itself is locked and inaccessible.
</td>
        </tr><tr>
            <td><code>NOT_KNOWN_TO_BE_PRESENT_OR_ENGAGED</code></td>
            <td><code>2</code></td>
            <td> The account owner is probably physically close to the device but cannot
 be said to be either actively using the device or be physically close
 it.
</td>
        </tr><tr>
            <td><code>PRESENT_WITHOUT_KNOWN_ENGAGEMENT</code></td>
            <td><code>3</code></td>
            <td> The account owner is probably physically close to the device but cannot
 be said to be actively using it.
</td>
        </tr><tr>
            <td><code>ENGAGED</code></td>
            <td><code>4</code></td>
            <td> The account owner is probably actively using the device.
</td>
        </tr></table>

### Lifetime {#Lifetime}
Type: <code>uint8</code>

*Defined in [fuchsia.identity.account/common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/common.fidl#27)*

 Provides an upper bound to how long a Fuchsia account can live on the
 current device.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>EPHEMERAL</code></td>
            <td><code>1</code></td>
            <td> The account lives at the longest to the end of the power cycle it
 was created in.
</td>
        </tr><tr>
            <td><code>PERSISTENT</code></td>
            <td><code>2</code></td>
            <td> The account lives on the device until it is removed.
</td>
        </tr></table>

### Error {#Error}
Type: <code>uint32</code>

*Defined in [fuchsia.identity.account/common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/common.fidl#56)*

 Specifies the reason that a fuchsia.identity.account method failed.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>1</code></td>
            <td> Some other problem occurred that cannot be classified using one of the
 more specific statuses. Retry is optional.
</td>
        </tr><tr>
            <td><code>INTERNAL</code></td>
            <td><code>2</code></td>
            <td> An internal error occurred. This usually indicates a bug within the
 account system itself. Retry is optional.
</td>
        </tr><tr>
            <td><code>UNSUPPORTED_OPERATION</code></td>
            <td><code>3</code></td>
            <td> The requested operation is not supported. This generally indicates that
 implementation of a new feature is not yet complete. The request should
 not be retried.
</td>
        </tr><tr>
            <td><code>INVALID_REQUEST</code></td>
            <td><code>4</code></td>
            <td> The request was malformed in some way, such as using an empty string for
 auth_provider_type. The request should not be retried.
</td>
        </tr><tr>
            <td><code>RESOURCE</code></td>
            <td><code>5</code></td>
            <td> A local resource error occurred such as I/O, FIDL, or memory allocation
 failure. Retry, after a delay, is recommended.
</td>
        </tr><tr>
            <td><code>NETWORK</code></td>
            <td><code>6</code></td>
            <td> A network error occurred while communicating with an auth server.
 Retry, after a delay, is recommended.
</td>
        </tr><tr>
            <td><code>NOT_FOUND</code></td>
            <td><code>7</code></td>
            <td> The requested account or persona is not present on the current device.
 The request should not be retried.
</td>
        </tr><tr>
            <td><code>REMOVAL_IN_PROGRESS</code></td>
            <td><code>8</code></td>
            <td> The request cannot be processed due to an ongoing account or persona
 removal. The removal is not guaranteed to suceed and so retry, after
 a delay, is recommended.
</td>
        </tr><tr>
            <td><code>FAILED_PRECONDITION</code></td>
            <td><code>9</code></td>
            <td> The server is not in the state required to perform the requested
 operation. The request should not be retried unless the server state
 has been corrected before the retry.
</td>
        </tr></table>





## **UNIONS**

### AccountManager_GetAccountAuthStates_Result {#AccountManager_GetAccountAuthStates_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#AccountManager_GetAccountAuthStates_Response'>AccountManager_GetAccountAuthStates_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### AccountManager_GetAccount_Result {#AccountManager_GetAccount_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#AccountManager_GetAccount_Response'>AccountManager_GetAccount_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### AccountManager_RegisterAccountListener_Result {#AccountManager_RegisterAccountListener_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#AccountManager_RegisterAccountListener_Response'>AccountManager_RegisterAccountListener_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### AccountManager_RemoveAccount_Result {#AccountManager_RemoveAccount_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#AccountManager_RemoveAccount_Response'>AccountManager_RemoveAccount_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### AccountManager_ProvisionFromAuthProvider_Result {#AccountManager_ProvisionFromAuthProvider_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#AccountManager_ProvisionFromAuthProvider_Response'>AccountManager_ProvisionFromAuthProvider_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### AccountManager_ProvisionNewAccount_Result {#AccountManager_ProvisionNewAccount_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#AccountManager_ProvisionNewAccount_Response'>AccountManager_ProvisionNewAccount_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### AuthTarget_GetAuthState_Result {#AuthTarget_GetAuthState_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#AuthTarget_GetAuthState_Response'>AuthTarget_GetAuthState_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### AuthTarget_RegisterAuthListener_Result {#AuthTarget_RegisterAuthListener_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#AuthTarget_RegisterAuthListener_Response'>AuthTarget_RegisterAuthListener_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Account_GetDefaultPersona_Result {#Account_GetDefaultPersona_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Account_GetDefaultPersona_Response'>Account_GetDefaultPersona_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Account_GetPersona_Result {#Account_GetPersona_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Account_GetPersona_Response'>Account_GetPersona_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Account_GetRecoveryAccount_Result {#Account_GetRecoveryAccount_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Account_GetRecoveryAccount_Response'>Account_GetRecoveryAccount_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Account_SetRecoveryAccount_Result {#Account_SetRecoveryAccount_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Account_SetRecoveryAccount_Response'>Account_SetRecoveryAccount_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Persona_GetTokenManager_Result {#Persona_GetTokenManager_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Persona_GetTokenManager_Response'>Persona_GetTokenManager_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Persona_GetKeyManager_Result {#Persona_GetKeyManager_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Persona_GetKeyManager_Response'>Persona_GetKeyManager_Response</a></code>
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
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/common.fidl#9">MAX_ACCOUNTS_PER_DEVICE</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
            <td> The maximum number of Fuchsia accounts that may be simultaneously
 provisioned on a device. This number may be increased in the future.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/common.fidl#13">MAX_PERSONAE_PER_ACCOUNT</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
            <td> The maximum number of personae that may be simultaneously defined within a
 Fuchsia account. This number may be increased in the future.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/common.fidl#17">MAX_ID_SIZE</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint32</code></td>
            <td> The maximum length of the global Fuchsia account and persona identifiers,
 in bytes.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/common.fidl#20">MAX_NAME_SIZE</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
            <td> The maximum length of the (UTF-8 encoded) human readable names, in bytes.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/common.fidl#23">MAX_AUTH_PROVIDER_TYPE_SIZE</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
            <td> The maximum length of an (UTF-8 encoded) auth provider type, in bytes.
</td>
        </tr>
    
</table>

