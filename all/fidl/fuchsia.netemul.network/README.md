[TOC]

# fuchsia.netemul.network


## **PROTOCOLS**

## NetworkManager {#NetworkManager}
*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#44)*

<p>Manages virtual networks.</p>

### ListNetworks {#ListNetworks}

<p>Lists emulated networks by name.</p>

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

### CreateNetwork {#CreateNetwork}

<p>Creates a new network with given name and config.</p>

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
                <code><a class='link' href='#NetworkConfig'>NetworkConfig</a></code>
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
                <code><a class='link' href='#Network'>Network</a>?</code>
            </td>
        </tr></table>

### GetNetwork {#GetNetwork}

<p>Gets a handle to a network.</p>

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
                <code><a class='link' href='#Network'>Network</a>?</code>
            </td>
        </tr></table>

## EndpointManager {#EndpointManager}
*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#71)*

<p>Manages virtual endpoints.</p>

### ListEndpoints {#ListEndpoints}

<p>Lists endpoints by name.</p>

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

### CreateEndpoint {#CreateEndpoint}

<p>Creates endpoint with given name and config.</p>

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
                <code><a class='link' href='#EndpointConfig'>EndpointConfig</a></code>
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
                <code><a class='link' href='#Endpoint'>Endpoint</a>?</code>
            </td>
        </tr></table>

### GetEndpoint {#GetEndpoint}

<p>Gets a handle to an endpoint.</p>

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
                <code><a class='link' href='#Endpoint'>Endpoint</a>?</code>
            </td>
        </tr></table>

## FakeEndpoint {#FakeEndpoint}
*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#81)*

<p>Fake endpoint can be added to a network to snoop or inject packets.</p>

### Write {#Write}

<p>Write Data packet to network.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr></table>



### OnData {#OnData}

<p>Called when network receives a data packet.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr></table>

## Network {#Network}
*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#89)*

<p>Virtual network.</p>

### GetConfig {#GetConfig}

<p>Gets network configuration.</p>

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
                <code><a class='link' href='#NetworkConfig'>NetworkConfig</a></code>
            </td>
        </tr></table>

### GetName {#GetName}

<p>Gets network name.</p>

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

### SetConfig {#SetConfig}

<p>Updates network configuration.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='#NetworkConfig'>NetworkConfig</a></code>
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

### AttachEndpoint {#AttachEndpoint}

<p>Attaches endpoint with given name to network.</p>

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

### RemoveEndpoint {#RemoveEndpoint}

<p>Removes endpoint with given name from network.</p>

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

### CreateFakeEndpoint {#CreateFakeEndpoint}

<p>Injects a fake endpoint.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ep</code></td>
            <td>
                <code>request&lt;<a class='link' href='#FakeEndpoint'>FakeEndpoint</a>&gt;</code>
            </td>
        </tr></table>



## DeviceProxy {#DeviceProxy}
*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#105)*

<p>Simple interface to serve devices over fidl.</p>

### ServeDevice {#ServeDevice}

<p>Fulfills the device request.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



## Endpoint {#Endpoint}
*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#111)*

<p>Virtual ethernet endpoint.</p>

### GetConfig {#GetConfig}


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
                <code><a class='link' href='#EndpointConfig'>EndpointConfig</a></code>
            </td>
        </tr></table>

### GetName {#GetName}

<p>Gets endpoint name.</p>

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

### SetLinkUp {#SetLinkUp}

<p>Sends link up or down signal</p>

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

### GetEthernetDevice {#GetEthernetDevice}

<p>Opens channel with zircon ethernet device.</p>

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
                <code><a class='link' href='../fuchsia.hardware.ethernet/'>fuchsia.hardware.ethernet</a>/<a class='link' href='../fuchsia.hardware.ethernet/#Device'>Device</a></code>
            </td>
        </tr></table>

### GetProxy {#GetProxy}

<p>Gets a proxy to open requests with zircon ethernet device.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>proxy</code></td>
            <td>
                <code>request&lt;<a class='link' href='#DeviceProxy'>DeviceProxy</a>&gt;</code>
            </td>
        </tr></table>



## SetupHandle {#SetupHandle}
*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#147)*

<p>Handle returned when using NetworkContext.Setup for quick network configuration.
Networks and endpoints created by Setup are tied to the lifecycle of the SetupHandle's channel.</p>

## NetworkContext {#NetworkContext}
*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#152)*

<p>Main entry point to manage virtual networks and endpoints.</p>

### GetNetworkManager {#GetNetworkManager}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>net_manager</code></td>
            <td>
                <code>request&lt;<a class='link' href='#NetworkManager'>NetworkManager</a>&gt;</code>
            </td>
        </tr></table>



### GetEndpointManager {#GetEndpointManager}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>endp_manager</code></td>
            <td>
                <code>request&lt;<a class='link' href='#EndpointManager'>EndpointManager</a>&gt;</code>
            </td>
        </tr></table>



### Setup {#Setup}

<p>Creates a collection of networks described by <code>networks</code>.
<code>status</code> is <code>ZX_OK</code> for success
<code>setup_handle</code> is a resource that references and maintains the lifecycle of
the created networks and endpoints.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>networks</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#NetworkSetup'>NetworkSetup</a>&gt;</code>
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
                <code><a class='link' href='#SetupHandle'>SetupHandle</a>?</code>
            </td>
        </tr></table>



## **STRUCTS**

### LatencyConfig {#LatencyConfig}
*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#10)*



<p>Provides emulated latency configuration.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>average</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Average latency, in ms.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>std_dev</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Latency standard deviation, in ms.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### ReorderConfig {#ReorderConfig}
*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#25)*



<p>Provides emulated packet reordering configuration.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>store_buff</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Size of buffer, in packets, to store and forward with randomized order.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>tick</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Tick/deadline in ms to empty buffer, regardless of full state.
0 will cause buffer to flush only when full (dangerous).</p>
</td>
            <td>No default</td>
        </tr>
</table>

### EndpointConfig {#EndpointConfig}
*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#60)*



<p>Configuration used to create an endpoint.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>mtu</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>Fake ethernet mtu.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>mac</code></td>
            <td>
                <code><a class='link' href='../fuchsia.hardware.ethernet/'>fuchsia.hardware.ethernet</a>/<a class='link' href='../fuchsia.hardware.ethernet/#MacAddress'>MacAddress</a>?</code>
            </td>
            <td><p>Fake ethernet mac address, if not provided will be set to randomized local mac,
using endpoint name as seed.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>backing</code></td>
            <td>
                <code><a class='link' href='#EndpointBacking'>EndpointBacking</a></code>
            </td>
            <td><p>Backing type of emulated endpoint.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### NetworkSetup {#NetworkSetup}
*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#125)*



<p>Convenience struct for creating entire network setups.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>Network name, must be unique in network context.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='#NetworkConfig'>NetworkConfig</a></code>
            </td>
            <td><p>NetworkConfig to use when creating network.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>endpoints</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#EndpointSetup'>EndpointSetup</a>&gt;</code>
            </td>
            <td><p>Collection of endpoints to create and attach to network.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### EndpointSetup {#EndpointSetup}
*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#135)*



<p>Convenience struct for creating endpoints along with network setup.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>Endpoint name, must be unique in network context.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='#EndpointConfig'>EndpointConfig</a>?</code>
            </td>
            <td><p>Optional endpoint config, if not provided defaults will be used.
Default values are: mtu = 1500, backing = ETHERTAP, mac = randomized.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>link_up</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Start endpoint with link status up.</p>
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### EndpointBacking {#EndpointBacking}
Type: <code>uint32</code>

*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#54)*

<p>Backing of an emulated endpoint.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ETHERTAP</code></td>
            <td><code>1</code></td>
            <td><p>Endpoint backed by ethertap device.</p>
</td>
        </tr></table>



## **TABLES**

### NetworkConfig {#NetworkConfig}


*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#34)*

<p>Used to configure a network with emulated adversity conditions.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>latency</code></td>
            <td>
                <code><a class='link' href='#LatencyConfig'>LatencyConfig</a></code>
            </td>
            <td><p>Latency configuration.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>packet_loss</code></td>
            <td>
                <code><a class='link' href='#LossConfig'>LossConfig</a></code>
            </td>
            <td><p>Packet loss configuration.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>reorder</code></td>
            <td>
                <code><a class='link' href='#ReorderConfig'>ReorderConfig</a></code>
            </td>
            <td><p>Packet reordering configuration.</p>
</td>
        </tr></table>



## **UNIONS**

### LossConfig {#LossConfig}
*Defined in [fuchsia.netemul.network/network.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/network.fidl#19)*

<p>Provides emulated packet loss configuration.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>random_rate</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td><p>Rate of packet loss expressed as independent drop probability [0-100].</p>
</td>
        </tr></table>







