Project: /_project.yaml
Book: /_book.yaml

# fuchsia.auth.account


## **PROTOCOLS**

## AccountManager {:#AccountManager}
*Defined in [fuchsia.auth.account/account_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.auth.account/account_manager.fidl#102)*

 AccountManager manages the overall state of Fuchsia accounts and personae on
 a Fuchsia device, installation of the AuthProviders that are used to obtain
 authentication tokens for these accounts, and access to TokenManagers for
 these accounts.

 The AccountManager is the most powerful interface in the authentication
 system and is intended only for use by the most trusted parts of the system.

### GetAccountIds {:#GetAccountIds}

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
                <code>vector&lt;<a class='link' href='#LocalAccountId'>LocalAccountId</a>&gt;[128]</code>
            </td>
        </tr></table>

### GetAccountAuthStates {:#GetAccountAuthStates}

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
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr><tr>
            <td><code>account_auth_states</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#AccountAuthState'>AccountAuthState</a>&gt;[128]</code>
            </td>
        </tr></table>

### GetAccount {:#GetAccount}

 Connects an interface to read properties of and perform operations on
 one account.

 `id` The account's identifier as returned by GetAccountIds()
 `context_provider` An `AuthenticationContextProvider` capable of
                    supplying UI contexts used for interactive
                    authentication on this account
 `account` The server end of an `Account` channel

 Returns: `status` A `Status` indicating whether the operation was
                   successful

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='#LocalAccountId'>LocalAccountId</a></code>
            </td>
        </tr><tr>
            <td><code>auth_context_provider</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/index.html'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/index.html#AuthenticationContextProvider'>AuthenticationContextProvider</a></code>
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
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>

### RegisterAccountListener {:#RegisterAccountListener}

 Connects an interface that will receive changes in the provisioned
 accounts and their authentication state. Optionally this interface will
 also receive the initial set of accounts and authentication states onto
 which changes may be applied.

 `listener` The client end of an `AccountListener` channel
 `options` An `AccountListenerOptions` that defines the set of events to
           be sent to the listener.

 Returns: `status` A `Status` indicating whether the operation was
                   successful

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
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>

### RemoveAccount {:#RemoveAccount}

 Removes a provisioned Fuchsia account from the current device, revoking
 any credentials that are held for the account.

 `id` The account's identifier as returned by GetAccountIds()
 `force` If true, continues removing the account even if revocation of
         credentials fails. If false, any revocation failure will result
         in an error and the account will remain. In this case, a subset
         of the credentials may have been deleted.

 Returns: `status` A `Status` indicating whether the operation was
                   successful

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='#LocalAccountId'>LocalAccountId</a></code>
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

### ProvisionFromAuthProvider {:#ProvisionFromAuthProvider}

 Adds a Fuchsia account to the current device based on authenticating
 to a service provider (such as Google). If the service provider account
 is not already a recovery account for any Fuchsia account, a new Fuchsia
 account will be created with its recovery account set to the service
 provider account.

 `auth_context_provider` An `AuthenticationContextProvider` capable of
                         supplying UI contexts used for interactive
                         authentication
 `auth_provider_type` A unique identifier for an installed `AuthProvider`
                      that should be used to authenticate with the service
                      provider
 `lifetime` The lifetime of the account.

 Returns: `status` A `Status` indicating whether the operation was
                   successful
          `account_id` The identifier of the newly added account, if the
                       operation was successful.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>auth_context_provider</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/index.html'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/index.html#AuthenticationContextProvider'>AuthenticationContextProvider</a></code>
            </td>
        </tr><tr>
            <td><code>auth_provider_type</code></td>
            <td>
                <code>string</code>
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
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr><tr>
            <td><code>account_id</code></td>
            <td>
                <code><a class='link' href='#LocalAccountId'>LocalAccountId</a>?</code>
            </td>
        </tr></table>

### ProvisionNewAccount {:#ProvisionNewAccount}

 Adds a new, initially empty, Fuchsia account to the current device.

 `lifetime` The lifetime of the account.

 Returns: `status` A `Status` indicating whether the operation was
                   successful
          `account_id` The identifier of the newly added account, if the
                       operation was successful.

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
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr><tr>
            <td><code>account_id</code></td>
            <td>
                <code><a class='link' href='#LocalAccountId'>LocalAccountId</a>?</code>
            </td>
        </tr></table>

## AccountListener {:#AccountListener}
*Defined in [fuchsia.auth.account/account_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.auth.account/account_manager.fidl#234)*

 An interface to receive events when the set of accounts on a device or the
 authentication states of these accounts change.

 AccountListeners may be registered through the AccountManager interface
 and this registration also defines which types of event should be sent to
 the listener. Optionally, the AccountListener will recieve an initial state
 event onto which the change events may be safely accumulated.

 All methods include an empty response to follow the "Throttle push using
 acknowledgements" FIDL design pattern.

### OnInitialize {:#OnInitialize}

 A method that is called to communicate the initial set of accounts and
 their authentication states. OnInitialize is called exactly once if and
 only if AccountListenerOptions.initial_state was set when creating the
 AccountListener. When called, it will always be the first call on the
 interface. If no accounts are present on the device the vector will be
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

### OnAccountAdded {:#OnAccountAdded}

 A method that is called when a new account is added to the device.
 This method is only called if AccountListenerOptions.add_account was
 set when creating the AccountListener.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='#LocalAccountId'>LocalAccountId</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### OnAccountRemoved {:#OnAccountRemoved}

 A method that is called when a provisioned account is removed.
 This method is only called if AccountListenerOptions.remove_account was
 set when creating the AccountListener.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='#LocalAccountId'>LocalAccountId</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### OnAuthStateChanged {:#OnAuthStateChanged}

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

## AuthListener {:#AuthListener}
*Defined in [fuchsia.auth.account/account_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.auth.account/account_manager.fidl#270)*

 An interface to receive events when the authentication state of an account
 changes.

 AuthListeners may be registered through the `AuthTarget` interface and this
 registration also defines the types of authentication state changes that
 should be sent to the listener.

 All methods include an empty response to follow the "Throttle push using
 acknowledgements" FIDL design pattern.

### OnInitialize {:#OnInitialize}

 A method that is called when the AccountListener is first connected.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>auth_state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/index.html'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/index.html#AuthState'>AuthState</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### OnAuthStateChanged {:#OnAuthStateChanged}

 A method that is called when the authentication state of the account
 changes.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>auth_state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/index.html'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/index.html#AuthState'>AuthState</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## AuthTarget {:#AuthTarget}
*Defined in [fuchsia.auth.account/account_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.auth.account/account_manager.fidl#286)*

 An interface that is extended by other interfaces defining an entity
 (referred to as the "target") with an authentication state, such as a
 Fuchsia account or persona.

 AuthTarget defines a set of methods to monitor the current authentication
 state of an entity and to request changes in that authentication state.

### GetAuthState {:#GetAuthState}

 Returns the current `AuthState` of the target.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr><tr>
            <td><code>auth_state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/index.html'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/index.html#AuthState'>AuthState</a>?</code>
            </td>
        </tr></table>

### RegisterAuthListener {:#RegisterAuthListener}

 Connects an interface that will receive changes in the authentication
 state of the target.

 `listener` The client end of an `AuthListener` channel
 `initial_state` If true, the listener will receive the initial auth state
                 in addition to any changes.
 `granularity` An `AuthChangeGranularity` expressing the magnitude of
               change in authentication state than should lead to a
               callback

 Returns: `status` A `Status` indicating whether the operation was
                   successful

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
                <code><a class='link' href='../fuchsia.auth/index.html'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/index.html#AuthChangeGranularity'>AuthChangeGranularity</a></code>
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

## Account {:#Account}
*Defined in [fuchsia.auth.account/account_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.auth.account/account_manager.fidl#319)*

 An Account exposes information about the personae and recovery account for
 a Fuchsia account, and provides methods to manipulate these.

 An Account provides access to sensitive long term identifiers and is only
 intended only for use by a small number of trusted system components.

### GetAuthState {:#GetAuthState}

 Returns the current `AuthState` of the target.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr><tr>
            <td><code>auth_state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/index.html'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/index.html#AuthState'>AuthState</a>?</code>
            </td>
        </tr></table>

### RegisterAuthListener {:#RegisterAuthListener}

 Connects an interface that will receive changes in the authentication
 state of the target.

 `listener` The client end of an `AuthListener` channel
 `initial_state` If true, the listener will receive the initial auth state
                 in addition to any changes.
 `granularity` An `AuthChangeGranularity` expressing the magnitude of
               change in authentication state than should lead to a
               callback

 Returns: `status` A `Status` indicating whether the operation was
                   successful

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
                <code><a class='link' href='../fuchsia.auth/index.html'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/index.html#AuthChangeGranularity'>AuthChangeGranularity</a></code>
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

### GetAccountName {:#GetAccountName}

 Returns a human readable name for the account. Account names are set by
 a human and are not guaranteed to be meaningful or unique, even among the
 accounts on a single device.

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

### GetLifetime {:#GetLifetime}

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

### GetPersonaIds {:#GetPersonaIds}

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
                <code>vector&lt;<a class='link' href='#LocalPersonaId'>LocalPersonaId</a>&gt;[128]</code>
            </td>
        </tr></table>

### GetDefaultPersona {:#GetDefaultPersona}

 Connects an interface to read properties of and access tokens for
 the default persona for the account.

 `persona` The client end of a `Persona` channel

 Returns: `status` A `Status` indicating whether the operation was
                   successful
          `id` The identifier for the default persona if the operation
               was successful

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
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='#LocalPersonaId'>LocalPersonaId</a>?</code>
            </td>
        </tr></table>

### GetPersona {:#GetPersona}

 Connects an interface to read properties of and access tokens for
 one of the personae for the account.

 `id` The persona's identifier as returned by GetPersonaIds()
 `persona` The client end of a `Persona` channel

 Returns: `status` A `Status` indicating whether the operation was
                   successful

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='#LocalPersonaId'>LocalPersonaId</a></code>
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
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>

### GetRecoveryAccount {:#GetRecoveryAccount}

 Returns the service provider account that can be used to access the
 Fuchsia account if more direct methods of authentication are not
 available, provided such an account exists.

 Returns: `status` A `Status` indicating whether the operation was
                   successful
          The `ServiceProviderAccount` used for recovery if the operation
          was successful and a recovery account exists.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr><tr>
            <td><code>account</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/index.html'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/index.html#ServiceProviderAccount'>ServiceProviderAccount</a>?</code>
            </td>
        </tr></table>

### SetRecoveryAccount {:#SetRecoveryAccount}

 Sets the service provider account that can be used to access the Fuchsia
 account if more direct methods of authentication are not available.

 `account` The `ServiceProviderAccount` to use as the recovery account.
           This must be an existing account that has already been
           provisioned on the current device using TokenManager.

 Returns: `status` A `Status` indicating whether the operation was
                   successful

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>account</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/index.html'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/index.html#ServiceProviderAccount'>ServiceProviderAccount</a></code>
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

## Persona {:#Persona}
*Defined in [fuchsia.auth.account/account_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.auth.account/account_manager.fidl#396)*

 A Persona exposes basic information about a Fuchsia persona and access to the
 authentication tokens that are visible through it.

 Note a Persona purposefully does not provide access to a long term identifier
 for the persona. This is to support components in the system that work with
 short lived identifiers (e.g. SessionManager), but note that long term
 identifiers can usually still be derived via the TokenManger interface.

### GetAuthState {:#GetAuthState}

 Returns the current `AuthState` of the target.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr><tr>
            <td><code>auth_state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/index.html'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/index.html#AuthState'>AuthState</a>?</code>
            </td>
        </tr></table>

### RegisterAuthListener {:#RegisterAuthListener}

 Connects an interface that will receive changes in the authentication
 state of the target.

 `listener` The client end of an `AuthListener` channel
 `initial_state` If true, the listener will receive the initial auth state
                 in addition to any changes.
 `granularity` An `AuthChangeGranularity` expressing the magnitude of
               change in authentication state than should lead to a
               callback

 Returns: `status` A `Status` indicating whether the operation was
                   successful

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
                <code><a class='link' href='../fuchsia.auth/index.html'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/index.html#AuthChangeGranularity'>AuthChangeGranularity</a></code>
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

### GetLifetime {:#GetLifetime}

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

### GetTokenManager {:#GetTokenManager}

 Connects an interface to acquire and revoke authentication tokens for
 service provider (aka cloud service) accounts that are visible through
 this persona.

 `application_url` A url for the Fuchsia agent that this interface will be
                   used by. Applications are only allowed to access tokens
                   that they created.
 `token_manager` The client end of a `Persona` channel

 Returns: `status` A `Status` indicating whether the operation was
                   successful

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>application_url</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>token_manager</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.auth/index.html'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/index.html#TokenManager'>TokenManager</a>&gt;</code>
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



## **STRUCTS**

### GlobalAccountId {:#GlobalAccountId}
*Defined in [fuchsia.auth.account/account_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.auth.account/account_manager.fidl#66)*



 A globally unique identifier for a Fuchsia account that is constant across
 the devices that the account is provisioned on. Identifiers are not human
 readable.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### LocalAccountId {:#LocalAccountId}
*Defined in [fuchsia.auth.account/account_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.auth.account/account_manager.fidl#75)*



 A unique identifier for a Fuchsia account on the current device. If the
 account is removed and re-added it will receive a different LocalAccountId.
 The same account will have different LocalAccountIds on different devices
 and a particular LocalAccountId value may refer to different accounts on
 different devices.


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

### LocalPersonaId {:#LocalPersonaId}
*Defined in [fuchsia.auth.account/account_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.auth.account/account_manager.fidl#84)*



 A unique identifier for a Persona of a Fuchsia account on the current device.
 If the account is removed and re-added its personae will receive different
 LocalPersonaIds. A particular LocalPersonaId value may refer to different
 personae and/or different accounts on different devices. The LocalAccountId
 for an account cannot be derived from the LocalPersonaId of its personae.


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

### AccountAuthState {:#AccountAuthState}
*Defined in [fuchsia.auth.account/account_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.auth.account/account_manager.fidl#89)*



 An `AuthState` along with the account that it applies to.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>account_id</code></td>
            <td>
                <code><a class='link' href='#LocalAccountId'>LocalAccountId</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>auth_state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/index.html'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/index.html#AuthState'>AuthState</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AccountListenerOptions {:#AccountListenerOptions}
*Defined in [fuchsia.auth.account/account_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.auth.account/account_manager.fidl#211)*



 The configuration for an AccountListener, defining the set of events that it
 will receive.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>initial_state</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, the listener will receive the initial auth state for all accounts.
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
                <code><a class='link' href='../fuchsia.auth/index.html'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/index.html#AuthChangeGranularity'>AuthChangeGranularity</a></code>
            </td>
            <td> An `AuthChangeGranularity` expressing the magnitude of change in
 authentication state that will lead to AuthStateChange events.
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### Status {:#Status}
Type: <code>uint32</code>

*Defined in [fuchsia.auth.account/account_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.auth.account/account_manager.fidl#25)*

 Specifies the success/failure status of AccountManager calls.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OK</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>INTERNAL_ERROR</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVALID_REQUEST</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>IO_ERROR</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>NETWORK_ERROR</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>NOT_FOUND</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNKNOWN_ERROR</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>REMOVAL_IN_PROGRESS</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr></table>

### Lifetime {:#Lifetime}
Type: <code>uint8</code>

*Defined in [fuchsia.auth.account/account_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.auth.account/account_manager.fidl#55)*

 Provides an upper bound to how long a Fuchsia account can live on the device.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>EPHEMERAL</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>PERSISTENT</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>











## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.auth.account/account_manager.fidl#11">MAX_ACCOUNTS_PER_DEVICE</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.auth.account/account_manager.fidl#15">MAX_PERSONAE_PER_ACCOUNT</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.auth.account/account_manager.fidl#19">MAX_ID_SIZE</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.auth.account/account_manager.fidl#22">MAX_NAME_SIZE</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    
</table>

