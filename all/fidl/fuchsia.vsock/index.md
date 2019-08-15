Project: /_project.yaml
Book: /_book.yaml

# fuchsia.vsock


## **PROTOCOLS**

## Connection {:#Connection}
*Defined in [fuchsia.vsock/connector.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.vsock/connector.fidl#22)*

 Interface for manipulating the state of an active connection.

### Shutdown {:#Shutdown}

 Trigger asynchronous shutdown. The underlying channel will be closed
 once shutdown is complete. Shutdown has an implicit barrier as any already
 queued sends will complete, but any additional sends will generate errors

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SendVmo {:#SendVmo}

 Send a VMO. The reply indicates that the VMO send has finished and that
 data may be queued on the socket again without causing races.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr><tr>
            <td><code>off</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>len</code></td>
            <td>
                <code>uint64</code>
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

## Acceptor {:#Acceptor}
*Defined in [fuchsia.vsock/connector.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.vsock/connector.fidl#33)*

 Interface presented by a listener to accept or reject connections

### Accept {:#Accept}

 The response is either a `ConnectionTransport` to indicate that the connection
 is accepted, or none to indicate that it should be rejected.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>addr</code></td>
            <td>
                <code><a class='link' href='../fuchsia.hardware.vsock/index.html'>fuchsia.hardware.vsock</a>/<a class='link' href='../fuchsia.hardware.vsock/index.html#Addr'>Addr</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>con</code></td>
            <td>
                <code><a class='link' href='#ConnectionTransport'>ConnectionTransport</a>?</code>
            </td>
        </tr></table>

## Connector {:#Connector}
*Defined in [fuchsia.vsock/connector.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.vsock/connector.fidl#43)*

 Exposed by a service that can act as a bridge to the underlying vsock driver and
 provides the ability for listeners to be multiplexed by port and manages dynamic
 port allocation for outbound connections.

### Connect {:#Connect}

 Attempt to establish a connection to the specified remote cid/port pair.
 No local port is specified as an ephemeral one will automatically be allocated.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>remote_cid</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>remote_port</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>con</code></td>
            <td>
                <code><a class='link' href='#ConnectionTransport'>ConnectionTransport</a></code>
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
            <td><code>local_port</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### Listen {:#Listen}

 Registers a listener for a local port. There can only be one listener for
 a single port at a time.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>local_port</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>acceptor</code></td>
            <td>
                <code><a class='link' href='#Acceptor'>Acceptor</a></code>
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



## **STRUCTS**

### ConnectionTransport {:#ConnectionTransport}
*Defined in [fuchsia.vsock/connector.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.vsock/connector.fidl#11)*



 Collection of objects that represent an open connection.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>data</code></td>
            <td>
                <code>handle&lt;socket&gt;</code>
            </td>
            <td> `data` socket that is ultimately given to the underlying vsock driver and
 is where all incoming data can be received from.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>con</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Connection'>Connection</a>&gt;</code>
            </td>
            <td> `Connection` interface that is retained by a vsock service that can be
 used to manipulate the state of a connection or perform more complex
 operations than just sending and receiving on a socket.
</td>
            <td>No default</td>
        </tr>
</table>













