[TOC]

# fuchsia.ledger.cloud.test


## **PROTOCOLS**

## CloudControllerFactory {#CloudControllerFactory}
*Defined in [fuchsia.ledger.cloud.test/cloud_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/bin/fidl/cloud_controller.fidl#15)*

<p>Service providing a controller for cloud connections sharing the same
network state.</p>
<p>All connections derived from this factory share the same data, and are
closed when the factory is disconnected.</p>

### Build {#Build}

<p>Builds a new controller with its own network state.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>controller</code></td>
            <td>
                <code>request&lt;<a class='link' href='#CloudController'>CloudController</a>&gt;</code>
            </td>
        </tr></table>



## CloudController {#CloudController}
*Defined in [fuchsia.ledger.cloud.test/cloud_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/bin/fidl/cloud_controller.fidl#53)*

<p>Service controlling some CloudProvider connections sharing the same network
state.</p>
<p>Closing this interface closes the CloudProviders created from it.</p>

### SetNetworkState {#SetNetworkState}

<p>Sets the network state of the CloudProvider.</p>
<p>After this returns, all requests on the CloudProviders created from this
controller are guaranteed to see the network state <code>state</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#NetworkState'>NetworkState</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### Connect {#Connect}

<p>Creates a new CloudProvider managed by this controller.</p>
<p>This CloudProvider shares the network state of all CloudProviders
created from this CloudController, and the data of all CloudProviders
created from the same CloudControllerFactory.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>provider</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.ledger.cloud/'>fuchsia.ledger.cloud</a>/<a class='link' href='../fuchsia.ledger.cloud/#CloudProvider'>CloudProvider</a>&gt;</code>
            </td>
        </tr></table>



### SetDiffSupport {#SetDiffSupport}

<p>Sets the diff support level for the controller.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>support</code></td>
            <td>
                <code><a class='link' href='#DiffSupport'>DiffSupport</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>





## **ENUMS**

### NetworkState {#NetworkState}
Type: <code>int32</code>

*Defined in [fuchsia.ledger.cloud.test/cloud_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/bin/fidl/cloud_controller.fidl#21)*

<p>Possible network states.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DISCONNECTED</code></td>
            <td><code>1</code></td>
            <td><p>The cloud answers <code>NETWORK_ERROR</code> to requests on pages.
Until LE-438 is fixed, the cloud should return OK for SetWatcher.</p>
</td>
        </tr><tr>
            <td><code>CONNECTED</code></td>
            <td><code>2</code></td>
            <td><p>The cloud behaves normally.</p>
</td>
        </tr><tr>
            <td><code>INJECT_NETWORK_ERRORS</code></td>
            <td><code>3</code></td>
            <td><p>The cloud inject network errors the first few times a request is
attempted.</p>
</td>
        </tr></table>

### DiffSupport {#DiffSupport}
Type: <code>int32</code>

*Defined in [fuchsia.ledger.cloud.test/cloud_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/bin/fidl/cloud_controller.fidl#35)*

<p>Simulated level of support for diffs.</p>
<p>This is used to test Ledger's compatibility with non diff-enabled peers and cloud providers.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ACCEPT_ALL_DIFFS</code></td>
            <td><code>1</code></td>
            <td><p>The cloud always accepts diffs sent by clients.</p>
<p>This is used to test Ledger's non-compatible mode of operation.</p>
</td>
        </tr><tr>
            <td><code>ACCEPT_DIFFS_RANDOMLY</code></td>
            <td><code>2</code></td>
            <td><p>The cloud accepts diffs sent by clients with 50% probability.</p>
<p>This is used to test the compatibility strategy: missing a diff is the observable
consequence of either having a cloud provider that did not support diffs when the commit was
uploaded, or that the commit was uploaded by a non diff-supporting Ledger.</p>
</td>
        </tr></table>











