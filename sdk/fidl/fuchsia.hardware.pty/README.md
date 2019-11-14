[TOC]

# fuchsia.hardware.pty

<p>A PTY (pseudoterminal) emulates terminal devices, with a &quot;server&quot; side
(which represents the keyboard+monitor side of the terminal and is obtained
by opening /dev/misc/ptmx) and a number of &quot;client&quot; sides which are obtained
by calling <code>OpenClient</code>.</p>
<p>Client PTYs are identified by the <code>id</code> used in the <code>OpenClient</code> call. The
first Client PTY <em>must</em> be 0, and it is the only Client PTY that is allowed
to create additional Client PTYs, receive Events, etc. It is the
Controlling PTY.</p>

## **PROTOCOLS**

## Device {#Device}
*Defined in [fuchsia.hardware.pty/pty.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-pty/pty.fidl#41)*


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

### Read {#Read}

<p>Reads <code>count</code> bytes at the seek offset.
The seek offset is moved forward by the number of bytes read.</p>
<p>This method requires following rights: <code>OPEN_RIGHT_READABLE</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>count</code></td>
            <td>
                <code>uint64</code>
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
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>

### ReadAt {#ReadAt}

<p>Reads <code>count</code> bytes at the provided offset.
Does not affect the seek offset.</p>
<p>This method requires following rights: <code>OPEN_RIGHT_READABLE</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>count</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>offset</code></td>
            <td>
                <code>uint64</code>
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
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>

### Write {#Write}

<p>Writes data at the seek offset.
The seek offset is moved forward by the number of bytes written.</p>
<p>This method requires following rights: <code>OPEN_RIGHT_WRITABLE</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
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
        </tr><tr>
            <td><code>actual</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### WriteAt {#WriteAt}

<p>Writes data to the provided offset.
Does not affect the seek offset.</p>
<p>This method requires following rights: <code>OPEN_RIGHT_WRITABLE</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr><tr>
            <td><code>offset</code></td>
            <td>
                <code>uint64</code>
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
        </tr><tr>
            <td><code>actual</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### Seek {#Seek}

<p>Moves the offset at which the next invocation of <code>Read()</code> or <code>Write()</code> will
occur.</p>
<p>This method does not require any rights.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>offset</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>start</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#SeekOrigin'>SeekOrigin</a></code>
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
        </tr><tr>
            <td><code>offset</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### Truncate {#Truncate}

<p>Shrinks the file size to 'length' bytes.</p>
<p>This method requires following rights: <code>OPEN_RIGHT_WRITABLE</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>length</code></td>
            <td>
                <code>uint64</code>
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

### GetFlags {#GetFlags}

<p>Acquires the <code>Directory.Open</code> rights and flags used to access this file.</p>
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
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### SetFlags {#SetFlags}

<p>Changes the <code>Directory.Open</code> flags used to access the file.
Supported flags which can be turned on / off:</p>
<ul>
<li><code>OPEN_FLAG_APPEND</code></li>
</ul>
<p>This method does not require any rights.</p>

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

### GetBuffer {#GetBuffer}

<p>Acquires a buffer representing this file, if there is one, with the
requested access rights.</p>
<p><code>flags</code> may be any of <code>VMO_FLAG_*</code>.</p>
<p>This method requires following rights:</p>
<ul>
<li><code>OPEN_RIGHT_WRITABLE</code> if <code>flags</code> includes <code>VMO_FLAG_WRITE</code>.</li>
<li><code>OPEN_RIGHT_READABLE</code> if <code>flags</code> includes <code>VMO_FLAG_READ</code> or <code>VMO_FLAG_EXEC</code>.</li>
</ul>

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
        </tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a>?</code>
            </td>
        </tr></table>

### OpenClient {#OpenClient}

<p>Open a client PTY device with a unique <code>id</code>. <code>client</code> should be a handle
to one endpoint of a channel that (on success) will become an open
connection to the newly created device. On failure, the channel will be
closed. Closing the channel will close the connection and release the
device. If the provided <code>id</code> is 0, then the new client is a controlling
client and has the capability to open additional clients. If the
current device is not a controlling client, <code>ZX_ERR_ACCESS_DENIED</code> will be
returned. If <code>id</code> is not unique, <code>ZX_ERR_INVALID_ARGS</code> will be returned.
Otherwise the status code from <code>device_add</code> is passed on.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>client</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
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

### ClrSetFeature {#ClrSetFeature}

<h2>allowed on Client PTYs</h2>
<p>Clear and/or Set PTY Features</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>clr</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>set</code></td>
            <td>
                <code>uint32</code>
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
            <td><code>features</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### GetWindowSize {#GetWindowSize}

<p>Obtain the window size (in character cells)</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>size</code></td>
            <td>
                <code><a class='link' href='#WindowSize'>WindowSize</a></code>
            </td>
        </tr></table>

### MakeActive {#MakeActive}

<h2>allowed on the Controlling PTY</h2>
<p>Select which Client PTY receives input.
Reads will simply block on non-active PTYs.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>client_pty_id</code></td>
            <td>
                <code>uint32</code>
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

### ReadEvents {#ReadEvents}

<p>Returns pending OOB events, simultaneously clearing them</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>events</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### SetWindowSize {#SetWindowSize}

<h2>allowed on the Server PTY</h2>
<p>Sets the window size</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>size</code></td>
            <td>
                <code><a class='link' href='#WindowSize'>WindowSize</a></code>
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

### WindowSize {#WindowSize}
*Defined in [fuchsia.hardware.pty/pty.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-pty/pty.fidl#23)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>width</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>













## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-pty/pty.fidl#21">FEATURE_RAW</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>When Feature Raw is enabled, OOB Events like ^c, ^z, etc are not generated.
Instead the character is read from the read() input path.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-pty/pty.fidl#29">EVENT_HANGUP</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The terminal has no active client.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-pty/pty.fidl#31">EVENT_INTERRUPT</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The terminal received a ^C control character.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-pty/pty.fidl#33">EVENT_SUSPEND</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The terminal received a ^Z control character.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-pty/pty.fidl#35">EVENT_MASK</a></td>
            <td>
                    <code>7</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>All events</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-pty/pty.fidl#38">SIGNAL_EVENT</a></td>
            <td>
                    <code>33554432</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>When an event is pending, this signal is asserted on the Controlling PTY.</p>
</td>
        </tr>
    
</table>

