Project: /_project.yaml
Book: /_book.yaml

# fuchsia.posix.socket


## **PROTOCOLS**

## Control {:#Control}
*Defined in [fuchsia.posix.socket/socket.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-posix-socket/socket.fidl#26)*

 The control plane for a network socket.

 Once a socket has been retrieved from a `Provider`, this interface is then used to further
 configure and use the socket. This interface is essentially POSIX. Its implementation must
 support Linux-specific arguments to {Get,Set}SockOpt.

 *Warning:* This protocol is not yet ready for direct use by clients. Instead, clients should
 use the BSD sockets API to interact with sockets. We plan to change this protocol substantially
 and clients that couple directly to this protocol will make those changes more difficult.

### Clone {:#Clone}

 Create another connection to the same remote object.

 `flags` may be any of:

 - `OPEN_RIGHT_*`
 - `OPEN_FLAG_APPEND`
 - `OPEN_FLAG_NO_REMOTE`
 - `OPEN_FLAG_DESCRIBE`
 - `CLONE_FLAG_SAME_RIGHTS`

 All other flags are ignored.

 The `OPEN_RIGHT_*` bits in `flags` request corresponding rights over the resulting
 cloned object.
 The cloned object must have rights less than or equal to the original object.
 Alternatively, pass `CLONE_FLAG_SAME_RIGHTS` to inherit the rights on the source connection.
 It is invalid to pass any of the `OPEN_RIGHT_*` flags together with
 `CLONE_FLAG_SAME_RIGHTS`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>object</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.io/index.html'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/index.html#Node'>Node</a>&gt;</code>
            </td>
        </tr></table>



### Close {:#Close}

 Terminates connection with object.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Describe {:#Describe}

 Returns extra information about the type of the object.
 If the `Describe` operation fails, the connection is closed.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io/index.html'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/index.html#NodeInfo'>NodeInfo</a></code>
            </td>
        </tr></table>

### OnOpen {:#OnOpen}

 An event produced eagerly by a FIDL server if requested by `OPEN_FLAG_DESCRIBE`.

 Indicates the success or failure of the open operation, and optionally describes the
 object. If the status is `ZX_OK`, `info` contains descriptive information about the object
 (the same as would be returned by `Describe`).



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io/index.html'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/index.html#NodeInfo'>NodeInfo</a>?</code>
            </td>
        </tr></table>

### Sync {:#Sync}

 Synchronizes updates to the node to the underlying media, if it exists.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### GetAttr {:#GetAttr}

 Acquires information about the node.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io/index.html'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/index.html#NodeAttributes'>NodeAttributes</a></code>
            </td>
        </tr></table>

### SetAttr {:#SetAttr}

 Updates information about the node.
 `flags` may be any of `NODE_ATTRIBUTE_FLAG_*`.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io/index.html'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/index.html#NodeAttributes'>NodeAttributes</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### NodeGetFlags {:#NodeGetFlags}

 Acquires the `Directory.Open` rights and flags used to access this file.

 This method does not require any rights.
 This method has the same functionality as GetFlags for File and is
 meant as an in-progress replacement.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### NodeSetFlags {:#NodeSetFlags}

 Changes the `Directory.Open` flags used to access the file.
 Supported flags which can be turned on / off:
 - `OPEN_FLAG_APPEND`

 This method does not require any rights.
 This method has the same functionality as SetFlags for File and is
 meant as an in-progress replacement.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Bind {:#Bind}

 Sets the local address used for the socket.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>addr</code></td>
            <td>
                <code>vector&lt;uint8&gt;[128]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>code</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr></table>

### Connect {:#Connect}

 Initiates a connection to a remote address.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>addr</code></td>
            <td>
                <code>vector&lt;uint8&gt;[128]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>code</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr></table>

### Listen {:#Listen}

 Begins listening for new incoming connections. At most `backlog` connections will be
 buffered.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>backlog</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>code</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr></table>

### Accept {:#Accept}

 Accepts a buffered incoming connection.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>code</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr><tr>
            <td><code>s</code></td>
            <td>
                <code><a class='link' href='#Control'>Control</a>?</code>
            </td>
        </tr></table>

### GetSockName {:#GetSockName}

 Retrieves the local socket address.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>code</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr><tr>
            <td><code>addr</code></td>
            <td>
                <code>vector&lt;uint8&gt;[128]</code>
            </td>
        </tr></table>

### GetPeerName {:#GetPeerName}

 Retrieves the remote socket address.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>code</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr><tr>
            <td><code>addr</code></td>
            <td>
                <code>vector&lt;uint8&gt;[128]</code>
            </td>
        </tr></table>

### SetSockOpt {:#SetSockOpt}

 Sets the value of a socket option.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>level</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr><tr>
            <td><code>optname</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr><tr>
            <td><code>optval</code></td>
            <td>
                <code>vector&lt;uint8&gt;[900]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>code</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr></table>

### GetSockOpt {:#GetSockOpt}

 Retrieves the value of a socket option.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>level</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr><tr>
            <td><code>optname</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>code</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr><tr>
            <td><code>optval</code></td>
            <td>
                <code>vector&lt;uint8&gt;[900]</code>
            </td>
        </tr></table>

## Provider {:#Provider}
*Defined in [fuchsia.posix.socket/socket.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-posix-socket/socket.fidl#50)*

 Provider implements the POSIX sockets API.

### Socket {:#Socket}

 Requests a socket with the specified parameters. Values for `code` are defined in errno.h.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>domain</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr><tr>
            <td><code>protocol</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>code</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr><tr>
            <td><code>s</code></td>
            <td>
                <code><a class='link' href='#Control'>Control</a>?</code>
            </td>
        </tr></table>

## Control {:#Control}
*Defined in [fuchsia.posix.socket/socket.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-posix-socket/socket.fidl#26)*

 The control plane for a network socket.

 Once a socket has been retrieved from a `Provider`, this interface is then used to further
 configure and use the socket. This interface is essentially POSIX. Its implementation must
 support Linux-specific arguments to {Get,Set}SockOpt.

 *Warning:* This protocol is not yet ready for direct use by clients. Instead, clients should
 use the BSD sockets API to interact with sockets. We plan to change this protocol substantially
 and clients that couple directly to this protocol will make those changes more difficult.

### Clone {:#Clone}

 Create another connection to the same remote object.

 `flags` may be any of:

 - `OPEN_RIGHT_*`
 - `OPEN_FLAG_APPEND`
 - `OPEN_FLAG_NO_REMOTE`
 - `OPEN_FLAG_DESCRIBE`
 - `CLONE_FLAG_SAME_RIGHTS`

 All other flags are ignored.

 The `OPEN_RIGHT_*` bits in `flags` request corresponding rights over the resulting
 cloned object.
 The cloned object must have rights less than or equal to the original object.
 Alternatively, pass `CLONE_FLAG_SAME_RIGHTS` to inherit the rights on the source connection.
 It is invalid to pass any of the `OPEN_RIGHT_*` flags together with
 `CLONE_FLAG_SAME_RIGHTS`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>object</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.io/index.html'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/index.html#Node'>Node</a>&gt;</code>
            </td>
        </tr></table>



### Close {:#Close}

 Terminates connection with object.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Describe {:#Describe}

 Returns extra information about the type of the object.
 If the `Describe` operation fails, the connection is closed.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io/index.html'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/index.html#NodeInfo'>NodeInfo</a></code>
            </td>
        </tr></table>

### OnOpen {:#OnOpen}

 An event produced eagerly by a FIDL server if requested by `OPEN_FLAG_DESCRIBE`.

 Indicates the success or failure of the open operation, and optionally describes the
 object. If the status is `ZX_OK`, `info` contains descriptive information about the object
 (the same as would be returned by `Describe`).



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io/index.html'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/index.html#NodeInfo'>NodeInfo</a>?</code>
            </td>
        </tr></table>

### Sync {:#Sync}

 Synchronizes updates to the node to the underlying media, if it exists.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### GetAttr {:#GetAttr}

 Acquires information about the node.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io/index.html'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/index.html#NodeAttributes'>NodeAttributes</a></code>
            </td>
        </tr></table>

### SetAttr {:#SetAttr}

 Updates information about the node.
 `flags` may be any of `NODE_ATTRIBUTE_FLAG_*`.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io/index.html'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/index.html#NodeAttributes'>NodeAttributes</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### NodeGetFlags {:#NodeGetFlags}

 Acquires the `Directory.Open` rights and flags used to access this file.

 This method does not require any rights.
 This method has the same functionality as GetFlags for File and is
 meant as an in-progress replacement.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### NodeSetFlags {:#NodeSetFlags}

 Changes the `Directory.Open` flags used to access the file.
 Supported flags which can be turned on / off:
 - `OPEN_FLAG_APPEND`

 This method does not require any rights.
 This method has the same functionality as SetFlags for File and is
 meant as an in-progress replacement.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Bind {:#Bind}

 Sets the local address used for the socket.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>addr</code></td>
            <td>
                <code>vector&lt;uint8&gt;[128]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>code</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr></table>

### Connect {:#Connect}

 Initiates a connection to a remote address.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>addr</code></td>
            <td>
                <code>vector&lt;uint8&gt;[128]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>code</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr></table>

### Listen {:#Listen}

 Begins listening for new incoming connections. At most `backlog` connections will be
 buffered.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>backlog</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>code</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr></table>

### Accept {:#Accept}

 Accepts a buffered incoming connection.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>code</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr><tr>
            <td><code>s</code></td>
            <td>
                <code><a class='link' href='#Control'>Control</a>?</code>
            </td>
        </tr></table>

### GetSockName {:#GetSockName}

 Retrieves the local socket address.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>code</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr><tr>
            <td><code>addr</code></td>
            <td>
                <code>vector&lt;uint8&gt;[128]</code>
            </td>
        </tr></table>

### GetPeerName {:#GetPeerName}

 Retrieves the remote socket address.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>code</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr><tr>
            <td><code>addr</code></td>
            <td>
                <code>vector&lt;uint8&gt;[128]</code>
            </td>
        </tr></table>

### SetSockOpt {:#SetSockOpt}

 Sets the value of a socket option.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>level</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr><tr>
            <td><code>optname</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr><tr>
            <td><code>optval</code></td>
            <td>
                <code>vector&lt;uint8&gt;[900]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>code</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr></table>

### GetSockOpt {:#GetSockOpt}

 Retrieves the value of a socket option.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>level</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr><tr>
            <td><code>optname</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>code</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr><tr>
            <td><code>optval</code></td>
            <td>
                <code>vector&lt;uint8&gt;[900]</code>
            </td>
        </tr></table>

## Provider {:#Provider}
*Defined in [fuchsia.posix.socket/socket.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-posix-socket/socket.fidl#50)*

 Provider implements the POSIX sockets API.

### Socket {:#Socket}

 Requests a socket with the specified parameters. Values for `code` are defined in errno.h.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>domain</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr><tr>
            <td><code>protocol</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>code</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr><tr>
            <td><code>s</code></td>
            <td>
                <code><a class='link' href='#Control'>Control</a>?</code>
            </td>
        </tr></table>















