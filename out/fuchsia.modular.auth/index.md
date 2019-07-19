Project: /_project.yaml
Book: /_book.yaml

# fuchsia.modular.auth


## **PROTOCOLS**

## AccountProvider {:#AccountProvider}
*Defined in [fuchsia.modular.auth/account_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.auth/account_provider.fidl#48)*


### AddAccount {:#AddAccount}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>identity_provider</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular.auth/index.html#IdentityProvider'>IdentityProvider</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>account</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular.auth/index.html#Account'>Account</a>?</code>
            </td>
        </tr><tr>
            <td><code>error_code</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr></table>

### RemoveAccount {:#RemoveAccount}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>account</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular.auth/index.html#Account'>Account</a></code>
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
                <code><a class='link' href='../fuchsia.modular.auth/index.html#AuthErr'>AuthErr</a></code>
            </td>
        </tr></table>

### Terminate {:#Terminate}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>





## **STRUCTS**

### Account {:#Account}
*Defined in [fuchsia.modular.auth/account.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.auth/account/account.fidl#11)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>identity_provider</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular.auth/index.html#IdentityProvider'>IdentityProvider</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>profile_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>display_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>url</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>image_url</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AuthErr {:#AuthErr}
*Defined in [fuchsia.modular.auth/account_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.auth/account_provider.fidl#9)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular.auth/index.html#Status'>Status</a></code>
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











