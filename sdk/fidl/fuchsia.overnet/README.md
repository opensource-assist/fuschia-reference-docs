[TOC]

# fuchsia.overnet


## **PROTOCOLS**

## ServiceConsumer {#ServiceConsumer}
*Defined in [fuchsia.overnet/overnet.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet/overnet.fidl#14)*

<p>Interfaces applicable to consuming services from other devices</p>

### ListPeers {#ListPeers}

<p>Returns a list of all peers that are connected to this Overnet.
If this list has not been updated since the last call to this method, it waits until
new data is available.
Concurrent calls to ListPeers will result in channel closure.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>peers</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Peer'>Peer</a>&gt;</code>
            </td>
        </tr></table>

### ConnectToService {#ConnectToService}

<p>Connect <code>chan</code> to some external service on <code>node</code> with name <code>service_name</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>node</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/'>fuchsia.overnet.protocol</a>/<a class='link' href='../fuchsia.overnet.protocol/#NodeId'>NodeId</a></code>
            </td>
        </tr><tr>
            <td><code>service_name</code></td>
            <td>
                <code>string[255]</code>
            </td>
        </tr><tr>
            <td><code>chan</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



## ServicePublisher {#ServicePublisher}
*Defined in [fuchsia.overnet/overnet.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet/overnet.fidl#28)*

<p>Interfaces applicable to sharing services with ServiceConsumer's</p>

### PublishService {#PublishService}

<p>Register a new service to be exported by Overnet.
If an existing service has the same <code>service_name</code>, it's replaced by this service.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service_name</code></td>
            <td>
                <code>string[255]</code>
            </td>
        </tr><tr>
            <td><code>provider</code></td>
            <td>
                <code><a class='link' href='#ServiceProvider'>ServiceProvider</a></code>
            </td>
        </tr></table>



## MeshController {#MeshController}
*Defined in [fuchsia.overnet/overnet.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet/overnet.fidl#37)*

<p>Interfaces applicable to controlling an Overnet mesh</p>

### AttachSocketLink {#AttachSocketLink}

<p>Attach a socket as a new link. Bad socket options will result in the channel being closed.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>socket</code></td>
            <td>
                <code>handle&lt;socket&gt;</code>
            </td>
        </tr><tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#SocketLinkOptions'>SocketLinkOptions</a></code>
            </td>
        </tr></table>



## Overnet {#Overnet}
*Defined in [fuchsia.overnet/overnet.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet/overnet.fidl#45)*

<p>Legacy Overnet interface for applications that did not distinguish between ServiceConsumer and
ServicePublisher</p>

### ListPeers {#ListPeers}

<p>Returns a list of all peers that are connected to this Overnet.
If this list has not been updated since the last call to this method, it waits until
new data is available.
Concurrent calls to ListPeers will result in channel closure.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>peers</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Peer'>Peer</a>&gt;</code>
            </td>
        </tr></table>

### ConnectToService {#ConnectToService}

<p>Connect <code>chan</code> to some external service on <code>node</code> with name <code>service_name</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>node</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/'>fuchsia.overnet.protocol</a>/<a class='link' href='../fuchsia.overnet.protocol/#NodeId'>NodeId</a></code>
            </td>
        </tr><tr>
            <td><code>service_name</code></td>
            <td>
                <code>string[255]</code>
            </td>
        </tr><tr>
            <td><code>chan</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



### PublishService {#PublishService}

<p>Register a new service to be exported by Overnet.
If an existing service has the same <code>service_name</code>, it's replaced by this service.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service_name</code></td>
            <td>
                <code>string[255]</code>
            </td>
        </tr><tr>
            <td><code>provider</code></td>
            <td>
                <code><a class='link' href='#ServiceProvider'>ServiceProvider</a></code>
            </td>
        </tr></table>



## ServiceProvider {#ServiceProvider}
*Defined in [fuchsia.overnet/overnet.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet/overnet.fidl#51)*

<p>A ServiceProvider is a factory for one service.</p>

### ConnectToService {#ConnectToService}

<p>Connect <code>chan</code> to the service (called in response to Overnet.ConnectToService).
<code>info</code> provides additional data about the connection request.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>chan</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#ConnectionInfo'>ConnectionInfo</a></code>
            </td>
        </tr></table>





## **STRUCTS**

### Peer {#Peer}
*Defined in [fuchsia.overnet/overnet.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet/overnet.fidl#58)*



<p>A <code>Peer</code> describes one device on the Overnet mesh.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/'>fuchsia.overnet.protocol</a>/<a class='link' href='../fuchsia.overnet.protocol/#NodeId'>NodeId</a></code>
            </td>
            <td><p>The address of the peer on the Overnet mesh.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>is_self</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>A special peer is returned for this device, and is marked with <code>is_self</code> true.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>description</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/'>fuchsia.overnet.protocol</a>/<a class='link' href='../fuchsia.overnet.protocol/#PeerDescription'>PeerDescription</a></code>
            </td>
            <td><p>A description of the peer (includes, for example, a service list).</p>
</td>
            <td>No default</td>
        </tr>
</table>





## **TABLES**

### SocketLinkOptions {#SocketLinkOptions}


*Defined in [fuchsia.overnet/overnet.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet/overnet.fidl#68)*

<p>Extra arguments for attaching a socket link to an Overnet mesh.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>connection_label</code></td>
            <td>
                <code>string[32]</code>
            </td>
            <td><p>A label that might be used for debugging purposes.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>bytes_per_second</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>How many bytes per second are transferable on this link (used to tune error recovery).
If unset, error recovery will be disabled.
If set, must not be 0, or else the receiving MeshController service will close the channel
(as discussed in that protocol's documentation).</p>
</td>
        </tr></table>

### ConnectionInfo {#ConnectionInfo}


*Defined in [fuchsia.overnet/overnet.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet/overnet.fidl#79)*

<p>Information provided to a ServiceProvider about an incoming connection.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>peer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/'>fuchsia.overnet.protocol</a>/<a class='link' href='../fuchsia.overnet.protocol/#NodeId'>NodeId</a></code>
            </td>
            <td><p>The peer address initiating this connection.</p>
</td>
        </tr></table>











