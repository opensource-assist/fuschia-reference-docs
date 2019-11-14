[TOC]

# fuchsia.modular.auth




## **STRUCTS**

### Account {#Account}
*Defined in [fuchsia.modular.auth/account.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.auth/account/account.fidl#11)*



<p>Stores attributes related to an account that is exposed to base shell.
A list of existing account(s) can be obtained via
UserProvider.PreviousUsers() and a new account can be added via
UserProvider.AddAccount().</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>A randomly generated identifier that is used to identify this
account on this device. This is meant to be used by base shell when it
wants to login as a user who has previously logged in.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>identity_provider</code></td>
            <td>
                <code><a class='link' href='#IdentityProvider'>IdentityProvider</a></code>
            </td>
            <td><p>The identity provider that was used to authenticate the user on this
device.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>profile_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>Unique identifier configured for the given user at the Identity provider.
Profile id is fetched from user profile attributes as configured by the
user at the given identity provider.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>display_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The name that is displayed on the base shell while logging in. Display
name is fetched from user profile attributes as configured by the user at
the given identity provider.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>url</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>User's profile url that is used by the base shell while logging in.
Profile url is fetched from user profile attributes as configured by the
user at the given identity provider.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>image_url</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>User's profile image url that is used by the base shell while logging in.
Profile image url is fetched from user profile attributes as configured by
the user at the given identity provider.</p>
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### IdentityProvider {#IdentityProvider}
Type: <code>uint32</code>

*Defined in [fuchsia.modular.auth/account.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.auth/account/account.fidl#45)*

<p>The currently supported identity providers. An identity provider provides
identifiers for users to interact with the system and may provide information
about the user that is known to the provider.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DEV</code></td>
            <td><code>0</code></td>
            <td><p>An identity provider that's used for development and testing. If this
identity provider is chosen, the Framework will continue as if it has
identified the user. Note that the users that use this id provider would
not get cloud ledger access (unless done via a side channel).</p>
</td>
        </tr><tr>
            <td><code>GOOGLE</code></td>
            <td><code>1</code></td>
            <td><p>Uses Google as the identity provider. Doing this requires a working network
connection and a web view.</p>
</td>
        </tr></table>











