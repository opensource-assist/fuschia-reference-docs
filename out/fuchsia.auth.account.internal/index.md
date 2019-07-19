Project: /_project.yaml
Book: /_book.yaml

# fuchsia.auth.account.internal


## **PROTOCOLS**

## AccountHandlerControl {:#AccountHandlerControl}
*Defined in [fuchsia.auth.account.internal/account_handler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/identity/fidl/account_handler.fidl#22)*


### CreateAccount {:#CreateAccount}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>context</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth.account.internal/index.html#AccountHandlerContext'>AccountHandlerContext</a></code>
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


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>context</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth.account.internal/index.html#AccountHandlerContext'>AccountHandlerContext</a></code>
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


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## AccountHandlerContext {:#AccountHandlerContext}
*Defined in [fuchsia.auth.account.internal/account_handler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/identity/fidl/account_handler.fidl#99)*


### GetAuthProvider {:#GetAuthProvider}


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















