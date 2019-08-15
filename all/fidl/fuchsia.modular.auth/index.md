Project: /_project.yaml
Book: /_book.yaml

# fuchsia.modular.auth


## **PROTOCOLS**

## AccountProvider {:#AccountProvider}
*Defined in [fuchsia.modular.auth/account_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.auth/account_provider.fidl#48)*

 An interface that allows the Framework to talk to the token manager service
 to add new accounts and be able to mint the corresponding `TokenManager`
 specialized instances for thid party agents and first party ledger client.

 This is only meant to be used by the Framework and will be replaced with
 `AccountManager` in the near future.

### AddAccount {:#AddAccount}

 Adds a new user account. This involves talking to the identity provider and
 fetching profile attributes.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>identity_provider</code></td>
            <td>
                <code><a class='link' href='#IdentityProvider'>IdentityProvider</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>account</code></td>
            <td>
                <code><a class='link' href='#Account'>Account</a>?</code>
            </td>
        </tr><tr>
            <td><code>error_code</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr></table>

### RemoveAccount {:#RemoveAccount}

 Removes an existing user account. This involves talking to account's
 identity provider and revoking user credentials both locally and remotely.
 This operation also deletes cached tokens for the given account.

 If `revoke_all` is set to true, then all device credentials are revoked
 both locally and remotely on the backend server and user is logged out from
 all devices. If `revoke_all` is set to false, then credentials stored
 locally are wiped. This includes cached tokens such as access/id and
 firebase tokens and the locally persisted refresh token. By default,
 `revoke_all` is set to false and deletes account only from that given
 device.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>account</code></td>
            <td>
                <code><a class='link' href='#Account'>Account</a></code>
            </td>
        </tr><tr>
            <td><code>revoke_all</code></td>
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
                <code><a class='link' href='#AuthErr'>AuthErr</a></code>
            </td>
        </tr></table>

### Terminate {:#Terminate}

 This signals `AccountProvider` to teardown itself. After the
 AccountProvider responds by closing its handle, the caller may terminate
 the `AccountProvider` application if it hasn't already exited.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>





## **STRUCTS**

### Account {:#Account}
*Defined in [fuchsia.modular.auth/account.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.auth/account/account.fidl#11)*



 Stores attributes related to an account that is exposed to base shell.
 A list of existing account(s) can be obtained via
 UserProvider.PreviousUsers() and a new account can be added via
 UserProvider.AddAccount().


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>string</code>
            </td>
            <td> A randomly generated identifier that is used to identify this
 account on this device. This is meant to be used by base shell when it
 wants to login as a user who has previously logged in.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>identity_provider</code></td>
            <td>
                <code><a class='link' href='#IdentityProvider'>IdentityProvider</a></code>
            </td>
            <td> The identity provider that was used to authenticate the user on this
 device.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>profile_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Unique identifier configured for the given user at the Identity provider.
 Profile id is fetched from user profile attributes as configured by the
 user at the given identity provider.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>display_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The name that is displayed on the base shell while logging in. Display
 name is fetched from user profile attributes as configured by the user at
 the given identity provider.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>url</code></td>
            <td>
                <code>string</code>
            </td>
            <td> User's profile url that is used by the base shell while logging in.
 Profile url is fetched from user profile attributes as configured by the
 user at the given identity provider.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>image_url</code></td>
            <td>
                <code>string</code>
            </td>
            <td> User's profile image url that is used by the base shell while logging in.
 Profile image url is fetched from user profile attributes as configured by
 the user at the given identity provider.
</td>
            <td>No default</td>
        </tr>
</table>

### AuthErr {:#AuthErr}
*Defined in [fuchsia.modular.auth/account_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.auth/account_provider.fidl#9)*



 Authentication errors returned by AccountProvider. It contains error status
 code along with a detailed error message.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>message</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### IdentityProvider {:#IdentityProvider}
Type: <code>uint32</code>

*Defined in [fuchsia.modular.auth/account.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.auth/account/account.fidl#45)*

 The currently supported identity providers. An identity provider provides
 identifiers for users to interact with the system and may provide information
 about the user that is known to the provider.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DEV</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>GOOGLE</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### Status {:#Status}
Type: <code>uint32</code>

*Defined in [fuchsia.modular.auth/account_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.auth/account_provider.fidl#15)*

 Specifies the success/failure status.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OK</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>BAD_REQUEST</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>BAD_RESPONSE</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>OAUTH_SERVER_ERROR</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>USER_CANCELLED</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>NETWORK_ERROR</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>INTERNAL_ERROR</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr></table>











