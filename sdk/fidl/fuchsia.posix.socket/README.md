[TOC]

# fuchsia.posix.socket


## **PROTOCOLS**

## Control {#Control}
*Defined in [fuchsia.posix.socket/socket.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-posix-socket/socket.fidl#26)*

<p>The control plane for a network socket.</p>
<p>Once a socket has been retrieved from a <code>Provider</code>, this interface is then used to further
configure and use the socket. This interface is essentially POSIX. Its implementation must
support Linux-specific arguments to {Get,Set}SockOpt.</p>
<p><em>Warning:</em> This protocol is not yet ready for direct use by clients. Instead, clients should
use the BSD sockets API to interact with sockets. We plan to change this protocol substantially
and clients that couple directly to this protocol will make those changes more difficult.</p>

### Clone {#Clone}

<p>Create another connection to the same remote object.</p>
<p><code>flags</code> may be any of:</p>
<ul>
<li><code>OPEN_RIGHT_*</code></li>
<li><code>OPEN_FLAG_APPEND</code></li>
<li><code>OPEN_FLAG_NO_REMOTE</code></li>
<li><code>OPEN_FLAG_DESCRIBE</code></li>
<li><code>CLONE_FLAG_SAME_RIGHTS</code></li>
</ul>
<p>All other flags are ignored.</p>
<p>The <code>OPEN_RIGHT_*</code> bits in <code>flags</code> request corresponding rights over the resulting
cloned object.
The cloned object must have rights less than or equal to the original object.
Alternatively, pass <code>CLONE_FLAG_SAME_RIGHTS</code> to inherit the rights on the source connection.
It is invalid to pass any of the <code>OPEN_RIGHT_*</code> flags together with
<code>CLONE_FLAG_SAME_RIGHTS</code>.</p>

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
                <code>request&lt;<a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#Node'>Node</a>&gt;</code>
            </td>
        </tr></table>



### Close {#Close}

<p>Terminates connection with object.</p>
<p>This method does not require any rights.</p>

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

### Describe {#Describe}

<p>Returns extra information about the type of the object.
If the <code>Describe</code> operation fails, the connection is closed.</p>
<p>This method does not require any rights.</p>

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
                <code><a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#NodeInfo'>NodeInfo</a></code>
            </td>
        </tr></table>

### OnOpen {#OnOpen}

<p>An event produced eagerly by a FIDL server if requested by <code>OPEN_FLAG_DESCRIBE</code>.</p>
<p>Indicates the success or failure of the open operation, and optionally describes the
object. If the status is <code>ZX_OK</code>, <code>info</code> contains descriptive information about the object
(the same as would be returned by <code>Describe</code>).</p>



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
                <code><a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#NodeInfo'>NodeInfo</a>?</code>
            </td>
        </tr></table>

### Sync {#Sync}

<p>Synchronizes updates to the node to the underlying media, if it exists.</p>
<p>This method does not require any rights.</p>

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

### GetAttr {#GetAttr}

<p>Acquires information about the node.</p>
<p>This method does not require any rights.</p>

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
                <code><a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#NodeAttributes'>NodeAttributes</a></code>
            </td>
        </tr></table>

### SetAttr {#SetAttr}

<p>Updates information about the node.
<code>flags</code> may be any of <code>NODE_ATTRIBUTE_FLAG_*</code>.</p>
<p>This method requires following rights: <code>OPEN_RIGHT_WRITABLE</code>.</p>

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
                <code><a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#NodeAttributes'>NodeAttributes</a></code>
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

### NodeGetFlags {#NodeGetFlags}

<p>Acquires the <code>Directory.Open</code> rights and flags used to access this file.</p>
<p>This method does not require any rights.
This method has the same functionality as GetFlags for File and is
meant as an in-progress replacement.</p>

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

### NodeSetFlags {#NodeSetFlags}

<p>Changes the <code>Directory.Open</code> flags used to access the file.
Supported flags which can be turned on / off:</p>
<ul>
<li><code>OPEN_FLAG_APPEND</code></li>
</ul>
<p>This method does not require any rights.
This method has the same functionality as SetFlags for File and is
meant as an in-progress replacement.</p>

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

### Bind {#Bind}

<p>Sets the local address used for the socket.</p>

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

### Connect {#Connect}

<p>Initiates a connection to a remote address.</p>

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

### Listen {#Listen}

<p>Begins listening for new incoming connections. At most <code>backlog</code> connections will be
buffered.</p>

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

### Accept {#Accept}

<p>Accepts a buffered incoming connection.</p>

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

### GetSockName {#GetSockName}

<p>Retrieves the local socket address.</p>

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

### GetPeerName {#GetPeerName}

<p>Retrieves the remote socket address.</p>

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

### SetSockOpt {#SetSockOpt}

<p>Sets the value of a socket option.</p>

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

### GetSockOpt {#GetSockOpt}

<p>Retrieves the value of a socket option.</p>

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

## Provider {#Provider}
*Defined in [fuchsia.posix.socket/socket.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-posix-socket/socket.fidl#50)*

<p>Provider implements the POSIX sockets API.</p>

### Socket {#Socket}

<p>Requests a socket with the specified parameters. Values for <code>code</code> are defined in errno.h.</p>

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

















## **TYPE ALIASES**

<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-posix-socket/socket.fidl#10">sockaddr</a></td>
            <td>
                <code>vector</code></td>
            <td><p>Chosen to match <code>sizeof(struct sockaddr_storage)</code>.</p>
</td>
        </tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-posix-socket/socket.fidl#15">sockopt</a></td>
            <td>
                <code>vector</code></td>
            <td><p>Chosen to be large enough to hold whatever we might want to cram in it. So long as we support
socket options, we don't have a good sense of what we might want to send as payload.</p>
</td>
        </tr></table>

