Project: /_project.yaml
Book: /_book.yaml

# fuchsia.ledger.cloud.firestore


## **PROTOCOLS**

## Factory {:#Factory}
*Defined in [fuchsia.ledger.cloud.firestore/factory.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/cloud_provider_firestore/bin/fidl/factory.fidl#23)*


### GetCloudProvider {:#GetCloudProvider}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ledger.cloud.firestore/index.html#Config'>Config</a></code>
            </td>
        </tr><tr>
            <td><code>token_manager</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/index.html'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/index.html#TokenManager'>TokenManager</a>?</code>
            </td>
        </tr><tr>
            <td><code>cloud_provider</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.ledger.cloud/index.html'>fuchsia.ledger.cloud</a>/<a class='link' href='../fuchsia.ledger.cloud/index.html#CloudProvider'>CloudProvider</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ledger.cloud/index.html'>fuchsia.ledger.cloud</a>/<a class='link' href='../fuchsia.ledger.cloud/index.html#Status'>Status</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Config {:#Config}
*Defined in [fuchsia.ledger.cloud.firestore/factory.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/cloud_provider_firestore/bin/fidl/factory.fidl#11)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>server_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>api_key</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>user_profile_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>













