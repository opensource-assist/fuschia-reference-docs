[TOC]

# fuchsia.identity.account

<p>Defines the protocols used to interface with the core Fuchsia identity
system.</p>
<p>Clients may use these protocols to access, maintain, and authenticate the
Fuchsia accounts and personae defined by the identity system.</p>
<p>The entry point is the discoverable <code>AccountManager</code> protocol. This provides
access to all accounts of the device and should only be accessible to a
small number of privileged clients. <code>AccountManager</code> may be used to acquire
less powerful <code>Account</code> and <code>Persona</code> handles that may then be passed to
other parts of the system.</p>

## **PROTOCOLS**

## AccountManager {#AccountManager}
*Defined in [fuchsia.identity.account/account_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/account_manager.fidl#17)*

<p>AccountManager manages the overall state of Fuchsia accounts and personae on
a Fuchsia device, installation of the AuthProviders that are used to obtain
authentication tokens for these accounts, and access to TokenManagers for
these accounts.</p>
<p>The AccountManager is the most powerful protocol in the authentication
system and is intended only for use by the most trusted parts of the system.</p>

### GetAccountIds {#GetAccountIds}

<p>Returns a vector of all accounts provisioned on the current device.</p>

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

<p>Returns a vector of all accounts provisioned on the current
device and the current authentication state for each.</p>
<p><code>scenario</code> The scenario to produce authentication states for.</p>
<p>Returns: <code>account_auth_states</code> The current authentication state for each
account given the provided scenario.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>scenario</code></td>
            <td>
                <code><a class='link' href='#Scenario'>Scenario</a></code>
            </td>
        </tr></table>


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

<p>Connects a channel to read properties of and perform operations on
one account.</p>
<p><code>id</code> The account's identifier as returned by GetAccountIds()
<code>context_provider</code> An <code>AuthenticationContextProvider</code> capable of
supplying UI contexts used for interactive
authentication on this account
<code>account</code> The server end of an <code>Account</code> channel</p>

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

<p>Connects a channel that will receive changes in the provisioned
accounts and their authentication state. Optionally this channel will
also receive the initial set of accounts and authentication states onto
which changes may be applied.</p>
<p><code>listener</code> The client end of an <code>AccountListener</code> channel
<code>options</code> An <code>AccountListenerOptions</code> that defines the set of events to
be sent to the listener.</p>

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

<p>Removes a provisioned Fuchsia account from the current device, revoking
any credentials that are held for the account.</p>
<p><code>id</code> The account's identifier as returned by GetAccountIds()
<code>force</code> If true, continues removing the account even if revocation of
credentials fails. If false, any revocation failure will result
in an error and the account will remain. In this case, a subset
of the credentials may have been deleted.</p>

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

<p>Adds a Fuchsia account to the current device based on authenticating
to a service provider (such as Google). If the service provider account
is not already a recovery account for any Fuchsia account, a new Fuchsia
account will be created with its recovery account set to the service
provider account.</p>
<p><code>auth_context_provider</code> An <code>AuthenticationContextProvider</code> capable of
supplying UI contexts used for interactive
authentication
<code>auth_provider_type</code> A unique identifier for an installed <code>AuthProvider</code>
that should be used to authenticate with the
service provider
<code>lifetime</code> The lifetime of the account</p>
<p>Returns: <code>account_id</code> The identifier of the newly added account</p>

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

<p>Adds a new, initially empty, Fuchsia account to the current device.</p>
<p><code>lifetime</code> The lifetime of the account</p>
<p>Returns: <code>account_id</code> The identifier of the newly added account</p>

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
*Defined in [fuchsia.identity.account/account_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/account_manager.fidl#157)*

<p>A protocol to receive events when the set of accounts on a device or the
authentication states of these accounts change.</p>
<p>AccountListeners may be registered through the AccountManager protocol
and this registration also defines which types of event should be sent to
the listener. Optionally, the AccountListener will receive an initial state
event onto which the change events may be safely accumulated.</p>
<p>All methods include an empty response to follow the &quot;Throttle push using
acknowledgements&quot; FIDL design pattern.</p>

### OnInitialize {#OnInitialize}

<p>A method that is called to communicate the initial set of accounts and
their authentication states. OnInitialize is called exactly once if and
only if AccountListenerOptions.initial_state was set when creating the
AccountListener. When called, it will always be the first call on the
channel. If no accounts are present on the device the vector will be
empty.</p>
<p><code>account_states</code> The set of initial states.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>account_states</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#InitialAccountState'>InitialAccountState</a>&gt;[128]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### OnAccountAdded {#OnAccountAdded}

<p>A method that is called when a new account is added to the device.
This method is only called if AccountListenerOptions.add_account was
set when creating the AccountListener.</p>
<p><code>account_state</code> The initial state for the newly added account.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>account_state</code></td>
            <td>
                <code><a class='link' href='#InitialAccountState'>InitialAccountState</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### OnAccountRemoved {#OnAccountRemoved}

<p>A method that is called when a provisioned account is removed.
This method is only called if AccountListenerOptions.remove_account was
set when creating the AccountListener.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>account_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### OnAuthStateChanged {#OnAuthStateChanged}

<p>A method that is called when the authentication state of any provisioned
account changes.</p>

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

<p>A protocol to receive events when the authentication state of an account
changes.</p>
<p>AuthListeners may be registered through the <code>AuthTarget</code> protocol and this
registration also defines the types of authentication state changes that
should be sent to the listener.</p>
<p>All methods include an empty response to follow the &quot;Throttle push using
acknowledgements&quot; FIDL design pattern.</p>

### OnInitialize {#OnInitialize}

<p>A method that is called when the AccountListener is first connected.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>auth_state</code></td>
            <td>
                <code><a class='link' href='#AuthState'>AuthState</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### OnAuthStateChanged {#OnAuthStateChanged}

<p>A method that is called when the authentication state of the account
changes.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>auth_state</code></td>
            <td>
                <code><a class='link' href='#AuthState'>AuthState</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## AuthTarget {#AuthTarget}
*Defined in [fuchsia.identity.account/auth_target.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/auth_target.fidl#36)*

<p>A protocol that is extended by other protocols defining an entity
(referred to as the &quot;target&quot;) with an authentication state, such as a
Fuchsia account or persona.</p>
<p>AuthTarget defines a set of methods to monitor the current authentication
state of an entity and to request changes in that authentication state.</p>

### GetAuthState {#GetAuthState}

<p>Returns the current <code>AuthState</code> of the target.</p>
<p><code>scenario</code> The scenario to produce the authentication state for.</p>
<p>Returns: <code>auth_state</code> The target's current authentication state.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>scenario</code></td>
            <td>
                <code><a class='link' href='#Scenario'>Scenario</a></code>
            </td>
        </tr></table>


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

<p>Connects a channel that will receive changes in the authentication
state of the target.</p>
<p><code>listener</code> The client end of an <code>AuthListener</code> channel
<code>initial_state</code> If true, the listener will receive the initial auth
state in addition to any changes.
<code>granularity</code> An <code>AuthChangeGranularity</code> expressing the magnitude of
change in authentication state than should lead to a
callback</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>scenario</code></td>
            <td>
                <code><a class='link' href='#Scenario'>Scenario</a></code>
            </td>
        </tr><tr>
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
                <code><a class='link' href='#AuthChangeGranularity'>AuthChangeGranularity</a></code>
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
*Defined in [fuchsia.identity.account/auth_target.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/auth_target.fidl#69)*

<p>A protocol that exposes information about the personae and recovery account
for a Fuchsia account and provides methods to manipulate these.</p>
<p>An Account provides access to sensitive long term identifiers and is only
intended only for use by a small number of trusted system components.</p>

### GetAuthState {#GetAuthState}

<p>Returns the current <code>AuthState</code> of the target.</p>
<p><code>scenario</code> The scenario to produce the authentication state for.</p>
<p>Returns: <code>auth_state</code> The target's current authentication state.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>scenario</code></td>
            <td>
                <code><a class='link' href='#Scenario'>Scenario</a></code>
            </td>
        </tr></table>


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

<p>Connects a channel that will receive changes in the authentication
state of the target.</p>
<p><code>listener</code> The client end of an <code>AuthListener</code> channel
<code>initial_state</code> If true, the listener will receive the initial auth
state in addition to any changes.
<code>granularity</code> An <code>AuthChangeGranularity</code> expressing the magnitude of
change in authentication state than should lead to a
callback</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>scenario</code></td>
            <td>
                <code><a class='link' href='#Scenario'>Scenario</a></code>
            </td>
        </tr><tr>
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
                <code><a class='link' href='#AuthChangeGranularity'>AuthChangeGranularity</a></code>
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

<p>Returns a human readable name for the account. Account names are set by
a human and are not guaranteed to be meaningful or unique, even among
the accounts on a single device.</p>

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

<p>Returns the account's lifetime.</p>

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

<p>Returns a vector of all the personae defined for the account.
NOTE: Currently all Fuchsia accounts have exactly one persona.</p>

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

<p>Connects a channel to read properties of and access tokens for
the default persona for the account.</p>
<p><code>persona</code> The client end of a <code>Persona</code> channel</p>
<p>Returns: <code>id</code> The identifier for the default persona</p>

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

<p>Connects a channel to read properties of and access tokens for
one of the personae for the account.</p>
<p><code>id</code> The persona's identifier as returned by GetPersonaIds()
<code>persona</code> The client end of a <code>Persona</code> channel</p>

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

<p>Returns the service provider account that can be used to access the
Fuchsia account if more direct methods of authentication are not
available, provided such an account exists.</p>
<p>Returns: The <code>ServiceProviderAccount</code> used for recovery if one exists</p>

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

<p>Sets the service provider account that can be used to access the Fuchsia
account if more direct methods of authentication are not available.</p>
<p><code>account</code> The <code>ServiceProviderAccount</code> to use as the recovery account.
This must be an existing account that has already been
provisioned on the current device using TokenManager.</p>

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
*Defined in [fuchsia.identity.account/auth_target.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/auth_target.fidl#130)*

<p>A protocol that exposes basic information about a Fuchsia persona and access
to the authentication tokens that are visible through it.</p>
<p>Note a Persona purposefully does not provide access to a long term
identifier for the persona. This is to support components in the system that
work with short lived identifiers (e.g. SessionManager), but note that long
term identifiers can usually still be derived via the TokenManger protocol.</p>

### GetAuthState {#GetAuthState}

<p>Returns the current <code>AuthState</code> of the target.</p>
<p><code>scenario</code> The scenario to produce the authentication state for.</p>
<p>Returns: <code>auth_state</code> The target's current authentication state.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>scenario</code></td>
            <td>
                <code><a class='link' href='#Scenario'>Scenario</a></code>
            </td>
        </tr></table>


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

<p>Connects a channel that will receive changes in the authentication
state of the target.</p>
<p><code>listener</code> The client end of an <code>AuthListener</code> channel
<code>initial_state</code> If true, the listener will receive the initial auth
state in addition to any changes.
<code>granularity</code> An <code>AuthChangeGranularity</code> expressing the magnitude of
change in authentication state than should lead to a
callback</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>scenario</code></td>
            <td>
                <code><a class='link' href='#Scenario'>Scenario</a></code>
            </td>
        </tr><tr>
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
                <code><a class='link' href='#AuthChangeGranularity'>AuthChangeGranularity</a></code>
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

<p>Returns the lifetime of this persona.</p>

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

<p>Connects a channel to acquire and revoke authentication tokens for
service provider (aka cloud service) accounts that are visible through
this persona.</p>
<p><code>application_url</code> A url for the Fuchsia agent that this channel will be
used by. Applications are only allowed to access
tokens that they created.
<code>token_manager</code> The client end of a <code>TokenManager</code> channel</p>

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

<p>Connects a channel to access and manage key material that is consistent
across all devices with access to this persona.</p>
<p>Persona key storage is a very limited resource. Only a small number of
core components should use KeyManager, often in order to supply more
scalable forms of synchronization to other applications (e.g. Ledger).</p>
<p><code>application_url</code> A url for the component that this channel will be
used by. Applications are only allowed to access
their own keys.
<code>key_manager</code> The client end of a <code>KeyManager</code> channel</p>

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
*Defined in [fuchsia.identity.account/account_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/account_manager.fidl#105)*



<p>An <code>AuthState</code> along with the account that it applies to.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>account_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>A unique identifier for the Fuchsia account on the current device.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>auth_state</code></td>
            <td>
                <code><a class='link' href='#AuthState'>AuthState</a></code>
            </td>
            <td><p>An authentication state for the Fuchsia account.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### InitialAccountState {#InitialAccountState}
*Defined in [fuchsia.identity.account/account_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/account_manager.fidl#114)*



<p>The initial state of an account, reported through an <code>AccountListener</code>.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>account_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>A unique identifier for the Fuchsia account on the current device.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>auth_state</code></td>
            <td>
                <code><a class='link' href='#AuthState'>AuthState</a>?</code>
            </td>
            <td><p>An authentication state for the Fuchsia account. It is only populated if
<code>AccountListenerOptions.scenario</code> was specified when the listener was
created.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### AccountListenerOptions {#AccountListenerOptions}
*Defined in [fuchsia.identity.account/account_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/account_manager.fidl#126)*



<p>The configuration for an AccountListener, defining the set of events that it
will receive.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>initial_state</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>If true, the listener will receive an event containing the initial state
for all accounts. The initial auth states will be populated in this
event iff the scenario option is set.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>add_account</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>If true, the listener will receive events when a new account is added
to the device.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>remove_account</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>If true, the listener will receive events when an account is removed
from the device.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>scenario</code></td>
            <td>
                <code><a class='link' href='#Scenario'>Scenario</a>?</code>
            </td>
            <td><p>The scenario to use for all AuthState data sent to the listener. If
scenario is not supplied no AuthState data will be populated.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>granularity</code></td>
            <td>
                <code><a class='link' href='#AuthChangeGranularity'>AuthChangeGranularity</a>?</code>
            </td>
            <td><p>An <code>AuthChangeGranularity</code> expressing the magnitude of change in
authentication state that will lead to AuthStateChange events.
If granularity is not populated AuthStateChange events will not be
sent. May only be populated if a scenario is provided.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### Scenario {#Scenario}
*Defined in [fuchsia.identity.account/auth_state.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/auth_state.fidl#64)*



<p>Defines the context to consider when creating authentication states.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>include_test</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>If true, experimental or test authenticators are included when creating
authentication states and MUST NOT be used to hand out sensitive user
information.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>threat_scenario</code></td>
            <td>
                <code><a class='link' href='#ThreatScenario'>ThreatScenario</a></code>
            </td>
            <td><p>Defines the threat scenario to consider when creating
authentication states.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### AuthState {#AuthState}
*Defined in [fuchsia.identity.account/auth_state.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/auth_state.fidl#98)*



<p>An assessment of the current presence and engagement of an account owner,
under the provided scenario, including the system's confidence in that
assessment and its timeliness.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>scenario</code></td>
            <td>
                <code><a class='link' href='#Scenario'>Scenario</a></code>
            </td>
            <td><p>The scenario that was considered when creating this authentication
state.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>summary</code></td>
            <td>
                <code><a class='link' href='#AuthStateSummary'>AuthStateSummary</a></code>
            </td>
            <td><p>A high level assessment of whether the account owner is present and
engaged.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>presence</code></td>
            <td>
                <code><a class='link' href='#Presence'>Presence</a></code>
            </td>
            <td><p>An assessment of whether the account owner is present.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>engagement</code></td>
            <td>
                <code><a class='link' href='#Engagement'>Engagement</a></code>
            </td>
            <td><p>An assessment of whether the account owner is engaged.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### AuthChangeGranularity {#AuthChangeGranularity}
*Defined in [fuchsia.identity.account/auth_state.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/auth_state.fidl#120)*



<p>An expression of the types of changes to an auth state that should be
reported over listener interfaces. By default no changes will be reported.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>summary_changes</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>If true, any changes in the <code>AuthStateSummary</code> enumeration will be
reported.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>presence_changes</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>If true, any changes in the <code>AuthState.presence</code> enumeration will
be reported.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>engagement_changes</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>If true, any changes in the <code>AuthState.engagement</code> enumeration will
be reported.</p>
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
                <code><a class='link' href='#AuthState'>AuthState</a></code>
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

<p>An assessment of whether the account owner is present.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>LOCKED</code></td>
            <td><code>1</code></td>
            <td><p>The account itself is locked and inaccessible.</p>
</td>
        </tr><tr>
            <td><code>ABSENT</code></td>
            <td><code>2</code></td>
            <td><p>The account owner is marked as absent.</p>
</td>
        </tr><tr>
            <td><code>PRESENCE_UNKNOWN</code></td>
            <td><code>3</code></td>
            <td><p>No information (either affirming or dissenting) is available about the
current presence of the account owner.</p>
</td>
        </tr><tr>
            <td><code>PRESENT</code></td>
            <td><code>4</code></td>
            <td><p>The account owner is marked as present.</p>
</td>
        </tr></table>

### Engagement {#Engagement}
Type: <code>uint32</code>

*Defined in [fuchsia.identity.account/auth_state.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/auth_state.fidl#24)*

<p>An assessment of whether the account owner is engaged.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>LOCKED</code></td>
            <td><code>1</code></td>
            <td><p>The account itself is locked and inaccessible.</p>
</td>
        </tr><tr>
            <td><code>DISENGAGED</code></td>
            <td><code>2</code></td>
            <td><p>The account owner is marked as disengaged.</p>
</td>
        </tr><tr>
            <td><code>ENGAGEMENT_UNKNOWN</code></td>
            <td><code>3</code></td>
            <td><p>No information (either affirming or dissenting) is available about the
current engagement of the account owner.</p>
</td>
        </tr><tr>
            <td><code>ENGAGED</code></td>
            <td><code>4</code></td>
            <td><p>The account owner is marked as engaged.</p>
</td>
        </tr></table>

### ThreatScenario {#ThreatScenario}
Type: <code>uint32</code>

*Defined in [fuchsia.identity.account/auth_state.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/auth_state.fidl#40)*

<p>A type of attacker to consider when creating authentication states.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NONE</code></td>
            <td><code>1</code></td>
            <td><p>No attackers are considered.</p>
</td>
        </tr><tr>
            <td><code>BASIC_ATTACKER</code></td>
            <td><code>2</code></td>
            <td><p>People that may typically and frequently gain access to a user’s device
are considered. Examples include nefarious roommates, coworkers,
houseguests, family members, or thieves. We assume limited technical
skills and/or motivation and commonly available technology.</p>
<p>Additionally, remote abusers performing an (initially untargeted) attack
are considered. We assume these attackers use the standard tools of
their trade such as password dumps, phishing toolkits, brute forcing, or
stolen identities.</p>
</td>
        </tr><tr>
            <td><code>ADVANCED_ATTACKER</code></td>
            <td><code>3</code></td>
            <td><p>Technologically capable people or organizations who are motivated to
perform a targeted attack on a user are considered. Examples include
freelance security professionals, organized crime, law enforcement, and
government agencies.</p>
</td>
        </tr></table>

### AuthStateSummary {#AuthStateSummary}
Type: <code>uint32</code>

*Defined in [fuchsia.identity.account/auth_state.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/auth_state.fidl#76)*

<p>A high level assessment of whether the account owner is present and engaged.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>LOCKED</code></td>
            <td><code>1</code></td>
            <td><p>The account itself is locked and inaccessible.</p>
</td>
        </tr><tr>
            <td><code>NOT_KNOWN_TO_BE_PRESENT_OR_ENGAGED</code></td>
            <td><code>2</code></td>
            <td><p>The account owner is probably physically close to the device but cannot
be said to be either actively using the device or be physically close
it.</p>
</td>
        </tr><tr>
            <td><code>PRESENT_WITHOUT_KNOWN_ENGAGEMENT</code></td>
            <td><code>3</code></td>
            <td><p>The account owner is probably physically close to the device but cannot
be said to be actively using it.</p>
</td>
        </tr><tr>
            <td><code>ENGAGED</code></td>
            <td><code>4</code></td>
            <td><p>The account owner is probably actively using the device.</p>
</td>
        </tr></table>

### Lifetime {#Lifetime}
Type: <code>uint8</code>

*Defined in [fuchsia.identity.account/common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/common.fidl#27)*

<p>Provides an upper bound to how long a Fuchsia account can live on the
current device.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>EPHEMERAL</code></td>
            <td><code>1</code></td>
            <td><p>The account lives at the longest to the end of the power cycle it
was created in.</p>
</td>
        </tr><tr>
            <td><code>PERSISTENT</code></td>
            <td><code>2</code></td>
            <td><p>The account lives on the device until it is removed.</p>
</td>
        </tr></table>

### Error {#Error}
Type: <code>uint32</code>

*Defined in [fuchsia.identity.account/common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/common.fidl#56)*

<p>Specifies the reason that a fuchsia.identity.account method failed.</p>


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
account system itself. Retry is optional.</p>
</td>
        </tr><tr>
            <td><code>UNSUPPORTED_OPERATION</code></td>
            <td><code>3</code></td>
            <td><p>The requested operation is not supported. This generally indicates that
implementation of a new feature is not yet complete. The request should
not be retried.</p>
</td>
        </tr><tr>
            <td><code>INVALID_REQUEST</code></td>
            <td><code>4</code></td>
            <td><p>The request was malformed in some way, such as using an empty string for
auth_provider_type. The request should not be retried.</p>
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
            <td><p>A network error occurred while communicating with an auth server.
Retry, after a delay, is recommended.</p>
</td>
        </tr><tr>
            <td><code>NOT_FOUND</code></td>
            <td><code>7</code></td>
            <td><p>The requested account or persona is not present on the current device.
The request should not be retried.</p>
</td>
        </tr><tr>
            <td><code>REMOVAL_IN_PROGRESS</code></td>
            <td><code>8</code></td>
            <td><p>The request cannot be processed due to an ongoing account or persona
removal. The removal is not guaranteed to suceed and so retry, after
a delay, is recommended.</p>
</td>
        </tr><tr>
            <td><code>FAILED_PRECONDITION</code></td>
            <td><code>9</code></td>
            <td><p>The server is not in the state required to perform the requested
operation. The request should not be retried unless the server state
has been corrected before the retry.</p>
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
            <td><p>The maximum number of Fuchsia accounts that may be simultaneously
provisioned on a device. This number may be increased in the future.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/common.fidl#13">MAX_PERSONAE_PER_ACCOUNT</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum number of personae that may be simultaneously defined within a
Fuchsia account. This number may be increased in the future.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/common.fidl#17">MAX_ID_SIZE</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum length of the global Fuchsia account and persona identifiers,
in bytes.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/common.fidl#20">MAX_NAME_SIZE</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum length of the (UTF-8 encoded) human readable names, in bytes.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.account/common.fidl#23">MAX_AUTH_PROVIDER_TYPE_SIZE</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum length of an (UTF-8 encoded) auth provider type, in bytes.</p>
</td>
        </tr>
    
</table>

