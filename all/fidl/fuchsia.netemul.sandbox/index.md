Project: /_project.yaml
Book: /_book.yaml

# fuchsia.netemul.sandbox


## **PROTOCOLS**

## Sandbox {:#Sandbox}
*Defined in [fuchsia.netemul.sandbox/sandbox.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/sandbox.fidl#21)*

 Every connection to `Sandbox` represents a self-contained
 context where ManagedEnvironments can be created. The
 NetworkContext and SyncManager instances offered by it are
 the same that are exposed to any ManagedEnvironment created
 by the Sandbox.
 The lifetime of the created environments (and the context
 services) is bound to the connection to the Sandbox service.
 If the channel is closed, all the environments and the
 components created within them will be terminated.

### CreateEnvironment {:#CreateEnvironment}

 Creates a new empty environment `root_env` configured by `options`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>root_env</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.netemul.environment/index.html'>fuchsia.netemul.environment</a>/<a class='link' href='../fuchsia.netemul.environment/index.html#ManagedEnvironment'>ManagedEnvironment</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='../fuchsia.netemul.environment/index.html'>fuchsia.netemul.environment</a>/<a class='link' href='../fuchsia.netemul.environment/index.html#EnvironmentOptions'>EnvironmentOptions</a></code>
            </td>
        </tr></table>



### GetNetworkContext {:#GetNetworkContext}

 Gets this sandbox's NetworkContext.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>network_context</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.netemul.network/index.html'>fuchsia.netemul.network</a>/<a class='link' href='../fuchsia.netemul.network/index.html#NetworkContext'>NetworkContext</a>&gt;</code>
            </td>
        </tr></table>



### GetSyncManager {:#GetSyncManager}

 Gets this sandbox's SyncManager.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>sync_manager</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.netemul.sync/index.html'>fuchsia.netemul.sync</a>/<a class='link' href='../fuchsia.netemul.sync/index.html#SyncManager'>SyncManager</a>&gt;</code>
            </td>
        </tr></table>

















