Project: /_project.yaml
Book: /_book.yaml

# fuchsia.auth.account.internal


## **PROTOCOLS**

## AccountHandlerControl {:#AccountHandlerControl}
*Defined in [fuchsia.auth.account.internal/account_handler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/identity/fidl/account_handler.fidl#22)*

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

### CreateAccount {:#CreateAccount}

 Creates a completely new Fuchsia account.

 `context` An `AccountHandlerContext` that can supply account and
           authentication services and contextual state.
 `id` The new account's local identifier.

 Returns: `status` A `Status` indicating whether the operation was
                   successful

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
                <code><a class='link' href='../fuchsia.auth.account/index.html'>fuchsia.auth.account</a>/<a class='link' href='../fuchsia.auth.account/index.html#LocalAccountId'>LocalAccountId</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth.account/index.html'>fuchsia.auth.account</a>/<a class='link' href='../fuchsia.auth.account/index.html#Status'>Status</a></code>
            </td>
        </tr></table>

### LoadAccount {:#LoadAccount}

 Loads information about a Fuchsia account that was previously provisioned
 on the current device.

 `context` An `AccountHandlerContext` that can supply account and
           authentication services and contextual state.
 `id` The account's local identifier.

 Returns: `status` A `Status` indicating whether the operation was
                   successful

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
                <code><a class='link' href='../fuchsia.auth.account/index.html'>fuchsia.auth.account</a>/<a class='link' href='../fuchsia.auth.account/index.html#LocalAccountId'>LocalAccountId</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth.account/index.html'>fuchsia.auth.account</a>/<a class='link' href='../fuchsia.auth.account/index.html#Status'>Status</a></code>
            </td>
        </tr></table>

### RemoveAccount {:#RemoveAccount}

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

 Returns: `status` A `Status` indicating whether the operation was
                   successful

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
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth.account/index.html'>fuchsia.auth.account</a>/<a class='link' href='../fuchsia.auth.account/index.html#Status'>Status</a></code>
            </td>
        </tr></table>

### GetAccount {:#GetAccount}

 Connects an interface to read properties of and perform operations on
 the account handled by this handler. The account must have previously
 been initialized using CreateAccount or LoadAccount, otherwise the call
 will fail with a status of NOT_FOUND.

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
            <td><code>auth_context_provider</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/index.html'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/index.html#AuthenticationContextProvider'>AuthenticationContextProvider</a></code>
            </td>
        </tr><tr>
            <td><code>account</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.auth.account/index.html'>fuchsia.auth.account</a>/<a class='link' href='../fuchsia.auth.account/index.html#Account'>Account</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth.account/index.html'>fuchsia.auth.account</a>/<a class='link' href='../fuchsia.auth.account/index.html#Status'>Status</a></code>
            </td>
        </tr></table>

### Terminate {:#Terminate}

 Signals that the AccountHandler should tear itself down. After the
 receiver responds by closing its handle, the caller may terminate the
 component if it hasn't already exited.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## AccountHandlerContext {:#AccountHandlerContext}
*Defined in [fuchsia.auth.account.internal/account_handler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/identity/fidl/account_handler.fidl#99)*

 An interface that supplies the account and authentication services that
 an AccountHandler needs to perform its role in the system.

 In the v2 Component architecture this service will be supplied into the
 namespace of AccountHandler by the component that launches it (i.e. the
 AccountManager).  Until then an AccountHandlerContext is supplied explicitly
 in the initialization calls on the AccountHandlerControl interface.

### GetAuthProvider {:#GetAuthProvider}

 Connects an interface to a particular AuthProvider, launching it if
 necessary.

 `auth_provider_type` An OAuth identity provider matching a configuration
                      set in an AuthProviderConfig.auth_provider_type
 `auth_provider` The server end of an `AuthProvider` channel

 Returns: `status` A `Status` indicating whether the operation was
                   successful

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
                <code>request&lt;<a class='link' href='../fuchsia.auth/index.html'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/index.html#AuthProvider'>AuthProvider</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth.account/index.html'>fuchsia.auth.account</a>/<a class='link' href='../fuchsia.auth.account/index.html#Status'>Status</a></code>
            </td>
        </tr></table>















