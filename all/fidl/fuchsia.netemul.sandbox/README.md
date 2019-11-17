[TOC]

# fuchsia.netemul.sandbox


## **PROTOCOLS**

## Sandbox {#Sandbox}
*Defined in [fuchsia.netemul.sandbox/sandbox.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/sandbox.fidl#21)*

<p>Every connection to <code>Sandbox</code> represents a self-contained
context where ManagedEnvironments can be created. The
NetworkContext and SyncManager instances offered by it are
the same that are exposed to any ManagedEnvironment created
by the Sandbox.
The lifetime of the created environments (and the context
services) is bound to the connection to the Sandbox service.
If the channel is closed, all the environments and the
components created within them will be terminated.</p>

### CreateEnvironment {#CreateEnvironment}

<p>Creates a new empty environment <code>root_env</code> configured by <code>options</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>root_env</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.netemul.environment/'>fuchsia.netemul.environment</a>/<a class='link' href='../fuchsia.netemul.environment/#ManagedEnvironment'>ManagedEnvironment</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='../fuchsia.netemul.environment/'>fuchsia.netemul.environment</a>/<a class='link' href='../fuchsia.netemul.environment/#EnvironmentOptions'>EnvironmentOptions</a></code>
            </td>
        </tr></table>



### GetNetworkContext {#GetNetworkContext}

<p>Gets this sandbox's NetworkContext.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>network_context</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.netemul.network/'>fuchsia.netemul.network</a>/<a class='link' href='../fuchsia.netemul.network/#NetworkContext'>NetworkContext</a>&gt;</code>
            </td>
        </tr></table>



### GetSyncManager {#GetSyncManager}

<p>Gets this sandbox's SyncManager.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>sync_manager</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.netemul.sync/'>fuchsia.netemul.sync</a>/<a class='link' href='../fuchsia.netemul.sync/#SyncManager'>SyncManager</a>&gt;</code>
            </td>
        </tr></table>

















