Project: /_project.yaml
Book: /_book.yaml

# fuchsia.tee.manager


## **PROTOCOLS**

## ServiceProvider {:#ServiceProvider}
*Defined in [fuchsia.tee.manager/provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tee-manager/provider.fidl#13)*

 ServiceProvider provides service access and support to the TEE driver
 for things like persistent storage, since the TEE may make upward RPC-like
 requests to the REE.

### RequestPersistentStorage {:#RequestPersistentStorage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>dir</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.io/index.html'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/index.html#Directory'>Directory</a>&gt;</code>
            </td>
        </tr></table>

















