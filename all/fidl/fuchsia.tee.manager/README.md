[TOC]

# fuchsia.tee.manager


## **PROTOCOLS**

## Provider {#Provider}
*Defined in [fuchsia.tee.manager/provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tee-manager/provider.fidl#13)*

<p>Provider provides service access and support to the TEE driver
for things like persistent storage, since the TEE may make upward RPC-like
requests to the REE.</p>

### RequestPersistentStorage {#RequestPersistentStorage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>dir</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#Directory'>Directory</a>&gt;</code>
            </td>
        </tr></table>

















