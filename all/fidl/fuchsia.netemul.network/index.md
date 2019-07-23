Project: /_project.yaml
Book: /_book.yaml

# fuchsia.netemul.network


## **PROTOCOLS**

## NetworkManager {:#NetworkManager}
*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#44)*

 Manages virtual networks.

### ListNetworks {:#ListNetworks}

 Lists emulated networks by name.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>nets</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr></table>

### CreateNetwork {:#CreateNetwork}

 Creates a new network with given name and config.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.netemul.network/index.html#NetworkConfig'>NetworkConfig</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>net</code></td>
            <td>
                <code><a class='link' href='../fuchsia.netemul.network/index.html#Network'>Network</a>?</code>
            </td>
        </tr></table>

### GetNetwork {:#GetNetwork}

 Gets a handle to a network.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>net</code></td>
            <td>
                <code><a class='link' href='../fuchsia.netemul.network/index.html#Network'>Network</a>?</code>
            </td>
        </tr></table>

## EndpointManager {:#EndpointManager}
*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#71)*

 Manages virtual endpoints.

### ListEndpoints {:#ListEndpoints}

 Lists endpoints by name.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>endp</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr></table>

### CreateEndpoint {:#CreateEndpoint}

 Creates endpoint with given name and config.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.netemul.network/index.html#EndpointConfig'>EndpointConfig</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>endpoint</code></td>
            <td>
                <code><a class='link' href='../fuchsia.netemul.network/index.html#Endpoint'>Endpoint</a>?</code>
            </td>
        </tr></table>

### GetEndpoint {:#GetEndpoint}

 Gets a handle to an endpoint.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>endpoint</code></td>
            <td>
                <code><a class='link' href='../fuchsia.netemul.network/index.html#Endpoint'>Endpoint</a>?</code>
            </td>
        </tr></table>

## FakeEndpoint {:#FakeEndpoint}
*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#81)*

 Fake endpoint can be added to a network to snoop or inject packets.

### Write {:#Write}

 Write Data packet to network.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr></table>



### OnData {:#OnData}

 Called when network receives a data packet.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr></table>

## Network {:#Network}
*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#89)*

 Virtual network.

### GetConfig {:#GetConfig}

 Gets network configuration.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.netemul.network/index.html#NetworkConfig'>NetworkConfig</a></code>
            </td>
        </tr></table>

### GetName {:#GetName}

 Gets network name.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

### SetConfig {:#SetConfig}

 Updates network configuration.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.netemul.network/index.html#NetworkConfig'>NetworkConfig</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### AttachEndpoint {:#AttachEndpoint}

 Attaches endpoint with given name to network.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### RemoveEndpoint {:#RemoveEndpoint}

 Removes endpoint with given name from network.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### CreateFakeEndpoint {:#CreateFakeEndpoint}

 Injects a fake endpoint.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ep</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.netemul.network/index.html#FakeEndpoint'>FakeEndpoint</a>&gt;</code>
            </td>
        </tr></table>



## DeviceProxy {:#DeviceProxy}
*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#105)*

 Simple interface to serve devices over fidl.

### ServeDevice {:#ServeDevice}

 Fulfills the device request.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



## Endpoint {:#Endpoint}
*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#111)*

 Virtual ethernet endpoint.

### GetConfig {:#GetConfig}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.netemul.network/index.html#EndpointConfig'>EndpointConfig</a></code>
            </td>
        </tr></table>

### GetName {:#GetName}

 Gets endpoint name.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

### SetLinkUp {:#SetLinkUp}

 Sends link up or down signal

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>up</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### GetEthernetDevice {:#GetEthernetDevice}

 Opens channel with zircon ethernet device.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device</code></td>
            <td>
                <code><a class='link' href='../fuchsia.hardware.ethernet/index.html'>fuchsia.hardware.ethernet</a>/<a class='link' href='../fuchsia.hardware.ethernet/index.html#Device'>Device</a></code>
            </td>
        </tr></table>

### GetProxy {:#GetProxy}

 Gets a proxy to open requests with zircon ethernet device.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>proxy</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.netemul.network/index.html#DeviceProxy'>DeviceProxy</a>&gt;</code>
            </td>
        </tr></table>



## SetupHandle {:#SetupHandle}
*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#147)*

 Handle returned when using NetworkContext.Setup for quick network configuration.
 Networks and endpoints created by Setup are tied to the lifecycle of the SetupHandle's channel.

## NetworkContext {:#NetworkContext}
*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#152)*

 Main entry point to manage virtual networks and endpoints.

### GetNetworkManager {:#GetNetworkManager}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>net_manager</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.netemul.network/index.html#NetworkManager'>NetworkManager</a>&gt;</code>
            </td>
        </tr></table>



### GetEndpointManager {:#GetEndpointManager}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>endp_manager</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.netemul.network/index.html#EndpointManager'>EndpointManager</a>&gt;</code>
            </td>
        </tr></table>



### Setup {:#Setup}

 Creates a collection of networks described by `networks`.
 `status` is ZX_OK for success
 `setup_handle` is a resource that references and maintains the lifecycle of
                the created networks and endpoints.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>networks</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.netemul.network/index.html#NetworkSetup'>NetworkSetup</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>setup_handle</code></td>
            <td>
                <code><a class='link' href='../fuchsia.netemul.network/index.html#SetupHandle'>SetupHandle</a>?</code>
            </td>
        </tr></table>



## **STRUCTS**

### LatencyConfig {:#LatencyConfig}
*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#10)*



 Provides emulated latency configuration.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>average</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Average latency, in ms.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>std_dev</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Latency standard deviation, in ms.
</td>
            <td>No default</td>
        </tr>
</table>

### ReorderConfig {:#ReorderConfig}
*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#25)*



 Provides emulated packet reordering configuration.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>store_buff</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Size of buffer, in packets, to store and forward with randomized order.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>tick</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Tick/deadline in ms to empty buffer, regardless of full state.
 0 will cause buffer to flush only when full (dangerous).
</td>
            <td>No default</td>
        </tr>
</table>

### EndpointConfig {:#EndpointConfig}
*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#60)*



 Configuration used to create an endpoint.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>mtu</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td> Fake ethernet mtu.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>mac</code></td>
            <td>
                <code><a class='link' href='../fuchsia.hardware.ethernet/index.html'>fuchsia.hardware.ethernet</a>/<a class='link' href='../fuchsia.hardware.ethernet/index.html#MacAddress'>MacAddress</a>?</code>
            </td>
            <td> Fake ethernet mac address, if not provided will be set to randomized local mac,
 using endpoint name as seed.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>backing</code></td>
            <td>
                <code><a class='link' href='../fuchsia.netemul.network/index.html#EndpointBacking'>EndpointBacking</a></code>
            </td>
            <td> Backing type of emulated endpoint.
</td>
            <td>No default</td>
        </tr>
</table>

### NetworkSetup {:#NetworkSetup}
*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#125)*



 Convenience struct for creating entire network setups.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Network name, must be unique in network context.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.netemul.network/index.html#NetworkConfig'>NetworkConfig</a></code>
            </td>
            <td> NetworkConfig to use when creating network.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>endpoints</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.netemul.network/index.html#EndpointSetup'>EndpointSetup</a>&gt;</code>
            </td>
            <td> Collection of endpoints to create and attach to network.
</td>
            <td>No default</td>
        </tr>
</table>

### EndpointSetup {:#EndpointSetup}
*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#135)*



 Convenience struct for creating endpoints along with network setup.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Endpoint name, must be unique in network context.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.netemul.network/index.html#EndpointConfig'>EndpointConfig</a>?</code>
            </td>
            <td> Optional endpoint config, if not provided defaults will be used.
 Default values are: mtu = 1500, backing = ETHERTAP, mac = randomized.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>link_up</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Start endpoint with link status up.
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### EndpointBacking {:#EndpointBacking}
Type: <code>uint32</code>

*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#54)*

 Backing of an emulated endpoint.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ETHERTAP</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### NetworkConfig {:#NetworkConfig}


*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#34)*

 Used to configure a network with emulated adversity conditions.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>latency</code></td>
            <td>
                <code><a class='link' href='../fuchsia.netemul.network/index.html#LatencyConfig'>LatencyConfig</a></code>
            </td>
            <td> Latency configuration.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>packet_loss</code></td>
            <td>
                <code><a class='link' href='../fuchsia.netemul.network/index.html#LossConfig'>LossConfig</a></code>
            </td>
            <td> Packet loss configuration.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>reorder</code></td>
            <td>
                <code><a class='link' href='../fuchsia.netemul.network/index.html#ReorderConfig'>ReorderConfig</a></code>
            </td>
            <td> Packet reordering configuration.
</td>
        </tr></table>



## **UNIONS**

### LossConfig {:#LossConfig}
*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#19)*

 Provides emulated packet loss configuration.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>random_rate</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td> Rate of packet loss expressed as independent drop probability [0-100].
</td>
        </tr></table>







