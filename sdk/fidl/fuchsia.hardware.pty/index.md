Project: /_project.yaml
Book: /_book.yaml

# fuchsia.hardware.pty

 A PTY (pseudoterminal) emulates terminal devices, with a "server" side
 (which represents the keyboard+monitor side of the terminal and is obtained
 by opening /dev/misc/ptmx) and a number of "client" sides which are obtained
 by calling `OpenClient`.

 Client PTYs are identified by the `id` used in the `OpenClient` call. The
 first Client PTY *must* be 0, and it is the only Client PTY that is allowed
 to create additional Client PTYs, receive Events, etc. It is the
 Controlling PTY.

## **PROTOCOLS**

## Device {:#Device}
*Defined in [fuchsia.hardware.pty/pty.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-pty/pty.fidl#41)*


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

### Read {:#Read}

 Reads `count` bytes at the seek offset.
 The seek offset is moved forward by the number of bytes read.

 This method requires following rights: `OPEN_RIGHT_READABLE`.

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

### ReadAt {:#ReadAt}

 Reads `count` bytes at the provided offset.
 Does not affect the seek offset.

 This method requires following rights: `OPEN_RIGHT_READABLE`.

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

### Write {:#Write}

 Writes data at the seek offset.
 The seek offset is moved forward by the number of bytes written.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

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

### WriteAt {:#WriteAt}

 Writes data to the provided offset.
 Does not affect the seek offset.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

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

### Seek {:#Seek}

 Moves the offset at which the next invocation of `Read()` or `Write()` will
 occur.

 This method does not require any rights.

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
                <code><a class='link' href='../fuchsia.io/index.html'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/index.html#SeekOrigin'>SeekOrigin</a></code>
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

### Truncate {:#Truncate}

 Shrinks the file size to 'length' bytes.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

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

### GetFlags {:#GetFlags}

 Acquires the `Directory.Open` rights and flags used to access this file.

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
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### SetFlags {:#SetFlags}

 Changes the `Directory.Open` flags used to access the file.
 Supported flags which can be turned on / off:
 - `OPEN_FLAG_APPEND`

 This method does not require any rights.

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

### GetBuffer {:#GetBuffer}

 Acquires a buffer representing this file, if there is one, with the
 requested access rights.

 `flags` may be any of `VMO_FLAG_*`.

 This method requires following rights:

 - `OPEN_RIGHT_WRITABLE` if `flags` includes `VMO_FLAG_WRITE`.
 - `OPEN_RIGHT_READABLE` if `flags` includes `VMO_FLAG_READ` or `VMO_FLAG_EXEC`.

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
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a>?</code>
            </td>
        </tr></table>

### OpenClient {:#OpenClient}

 Open a client PTY device with a unique `id`. `client` should be a handle
 to one endpoint of a channel that (on success) will become an open
 connection to the newly created device. On failure, the channel will be
 closed. Closing the channel will close the connection and release the
 device. If the provided `id` is 0, then the new client is a controlling
 client and has the capability to open additional clients. If the
 current device is not a controlling client, `ZX_ERR_ACCESS_DENIED` will be
 returned. If `id` is not unique, `ZX_ERR_INVALID_ARGS` will be returned.
 Otherwise the status code from `device_add` is passed on.

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

### ClrSetFeature {:#ClrSetFeature}

 allowed on Client PTYs
 -----------------------------
 Clear and/or Set PTY Features

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

### GetWindowSize {:#GetWindowSize}

 Obtain the window size (in character cells)

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

### MakeActive {:#MakeActive}

 allowed on the Controlling PTY
 -------------------------------------
 Select which Client PTY receives input.
 Reads will simply block on non-active PTYs.

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

### ReadEvents {:#ReadEvents}

 Returns pending OOB events, simultaneously clearing them

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

### SetWindowSize {:#SetWindowSize}

 allowed on the Server PTY
 --------------------------------
 Sets the window size

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

### WindowSize {:#WindowSize}
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
            <td> When Feature Raw is enabled, OOB Events like ^c, ^z, etc are not generated.
 Instead the character is read from the read() input path.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-pty/pty.fidl#29">EVENT_HANGUP</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td> The terminal has no active client.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-pty/pty.fidl#31">EVENT_INTERRUPT</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td> The terminal received a ^C control character.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-pty/pty.fidl#33">EVENT_SUSPEND</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
            <td> The terminal received a ^Z control character.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-pty/pty.fidl#35">EVENT_MASK</a></td>
            <td>
                    <code>7</code>
                </td>
                <td><code>uint32</code></td>
            <td> All events
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-pty/pty.fidl#38">SIGNAL_EVENT</a></td>
            <td>
                    <code>33554432</code>
                </td>
                <td><code>uint32</code></td>
            <td> When an event is pending, this signal is asserted on the Controlling PTY.
</td>
        </tr>
    
</table>

