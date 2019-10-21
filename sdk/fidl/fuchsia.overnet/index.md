Project: /_project.yaml
Book: /_book.yaml

# fuchsia.overnet


## **PROTOCOLS**

## ServiceConsumer {:#ServiceConsumer}
*Defined in [fuchsia.overnet/overnet.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet/overnet.fidl#14)*

 Interfaces applicable to consuming services from other devices

### ListPeers {:#ListPeers}

 Returns a list of all peers that are connected to this Overnet.
 If this list has not been updated since the last call to this method, it waits until
 new data is available.
 Concurrent calls to ListPeers will result in channel closure.

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

### ConnectToService {:#ConnectToService}

 Connect `chan` to some external service on `node` with name `service_name`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>node</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/index.html'>fuchsia.overnet.protocol</a>/<a class='link' href='../fuchsia.overnet.protocol/index.html#NodeId'>NodeId</a></code>
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



## ServicePublisher {:#ServicePublisher}
*Defined in [fuchsia.overnet/overnet.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet/overnet.fidl#28)*

 Interfaces applicable to sharing services with ServiceConsumer's

### PublishService {:#PublishService}

 Register a new service to be exported by Overnet.
 If an existing service has the same `service_name`, it's replaced by this service.

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



## MeshController {:#MeshController}
*Defined in [fuchsia.overnet/overnet.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet/overnet.fidl#37)*

 Interfaces applicable to controlling an Overnet mesh

### AttachSocketLink {:#AttachSocketLink}

 Attach a socket as a new link.

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



## Overnet {:#Overnet}
*Defined in [fuchsia.overnet/overnet.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet/overnet.fidl#45)*

 Legacy Overnet interface for applications that did not distinguish between ServiceConsumer and
 ServicePublisher

### ListPeers {:#ListPeers}

 Returns a list of all peers that are connected to this Overnet.
 If this list has not been updated since the last call to this method, it waits until
 new data is available.
 Concurrent calls to ListPeers will result in channel closure.

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

### ConnectToService {:#ConnectToService}

 Connect `chan` to some external service on `node` with name `service_name`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>node</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/index.html'>fuchsia.overnet.protocol</a>/<a class='link' href='../fuchsia.overnet.protocol/index.html#NodeId'>NodeId</a></code>
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



### PublishService {:#PublishService}

 Register a new service to be exported by Overnet.
 If an existing service has the same `service_name`, it's replaced by this service.

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



## ServiceProvider {:#ServiceProvider}
*Defined in [fuchsia.overnet/overnet.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet/overnet.fidl#51)*

 A ServiceProvider is a factory for one service.

### ConnectToService {:#ConnectToService}

 Connect `chan` to the service (called in response to Overnet.ConnectToService).
 `info` provides additional data about the connection request.

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

### Peer {:#Peer}
*Defined in [fuchsia.overnet/overnet.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet/overnet.fidl#58)*



 A `Peer` describes one device on the Overnet mesh.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/index.html'>fuchsia.overnet.protocol</a>/<a class='link' href='../fuchsia.overnet.protocol/index.html#NodeId'>NodeId</a></code>
            </td>
            <td> The address of the peer on the Overnet mesh.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>is_self</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> A special peer is returned for this device, and is marked with `is_self` true.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>description</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/index.html'>fuchsia.overnet.protocol</a>/<a class='link' href='../fuchsia.overnet.protocol/index.html#PeerDescription'>PeerDescription</a></code>
            </td>
            <td> A description of the peer (includes, for example, a service list).
</td>
            <td>No default</td>
        </tr>
</table>





## **TABLES**

### SocketLinkOptions {:#SocketLinkOptions}


*Defined in [fuchsia.overnet/overnet.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet/overnet.fidl#68)*

 Extra arguments for attaching a socket link to an Overnet mesh.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>connection_label</code></td>
            <td>
                <code>string[32]</code>
            </td>
            <td> A label that might be used for debugging purposes.
</td>
        </tr></table>

### ConnectionInfo {:#ConnectionInfo}


*Defined in [fuchsia.overnet/overnet.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet/overnet.fidl#74)*

 Information provided to a ServiceProvider about an incoming connection.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>peer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/index.html'>fuchsia.overnet.protocol</a>/<a class='link' href='../fuchsia.overnet.protocol/index.html#NodeId'>NodeId</a></code>
            </td>
            <td> The peer address initiating this connection.
</td>
        </tr></table>









