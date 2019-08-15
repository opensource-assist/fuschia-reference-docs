Project: /_project.yaml
Book: /_book.yaml

# fuchsia.ledger.cloud.test


## **PROTOCOLS**

## CloudControllerFactory {:#CloudControllerFactory}
*Defined in [fuchsia.ledger.cloud.test/cloud_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/bin/fidl/cloud_controller.fidl#15)*

 Service providing a controller for cloud connections sharing the same
 network state.

 All connections derived from this factory share the same data, and are
 closed when the factory is disconnected.

### Build {:#Build}

 Builds a new controller with its own network state.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>controller</code></td>
            <td>
                <code>request&lt;<a class='link' href='#CloudController'>CloudController</a>&gt;</code>
            </td>
        </tr></table>



## CloudController {:#CloudController}
*Defined in [fuchsia.ledger.cloud.test/cloud_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/bin/fidl/cloud_controller.fidl#36)*

 Service controlling some CloudProvider connections sharing the same network
 state.

 Closing this interface closes the CloudProviders created from it.

### SetNetworkState {:#SetNetworkState}

 Sets the network state of the CloudProvider.

 After this returns, all requests on the CloudProviders created from this
 controller are guaranteed to see the network state `state`.

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

### Connect {:#Connect}

 Creates a new CloudProvider managed by this controller.

 This CloudProvider shares the network state of all CloudProviders
 created from this CloudController, and the data of all CloudProviders
 created from the same CloudControllerFactory.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>provider</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.ledger.cloud/index.html'>fuchsia.ledger.cloud</a>/<a class='link' href='../fuchsia.ledger.cloud/index.html#CloudProvider'>CloudProvider</a>&gt;</code>
            </td>
        </tr></table>







## **ENUMS**

### NetworkState {:#NetworkState}
Type: <code>int32</code>

*Defined in [fuchsia.ledger.cloud.test/cloud_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/bin/fidl/cloud_controller.fidl#21)*

 Possible network states.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DISCONNECTED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>CONNECTED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>INJECT_NETWORK_ERRORS</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>











