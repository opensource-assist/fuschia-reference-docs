Project: /_project.yaml
Book: /_book.yaml

# fuchsia.hardware.pty


## **PROTOCOLS**

## Device {:#Device}
*Defined in [fuchsia.hardware.pty/pty.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-pty/pty.fidl#40)*


### OpenClient {:#OpenClient}

 Open a client PTY device with a unique `id`. `client` should be a handle
 to one endpoint of a channel that (on success) will become an open
 connection to the newly created device. On failure, the channel will be
 closed. Closing the channel will close the connection and release the
 device. If the provided `id` is 0, then the new client is a controlling
 client and has the capability to open additional clients. If the
 current device is not a controlling client, ZX_ERR_ACCESS_DENIED will be
 returned. If `id` is not unique, ZX_ERR_INVALID_ARGS will be returned.
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
                <code><a class='link' href='../fuchsia.hardware.pty/index.html#WindowSize'>WindowSize</a></code>
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
                <code><a class='link' href='../fuchsia.hardware.pty/index.html#WindowSize'>WindowSize</a></code>
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
*Defined in [fuchsia.hardware.pty/pty.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-pty/pty.fidl#22)*





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
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-pty/pty.fidl#20">FEATURE_RAW</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-pty/pty.fidl#28">EVENT_HANGUP</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-pty/pty.fidl#30">EVENT_INTERRUPT</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-pty/pty.fidl#32">EVENT_SUSPEND</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-pty/pty.fidl#34">EVENT_MASK</a></td>
            <td>
                    <code>7</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-pty/pty.fidl#37">SIGNAL_EVENT</a></td>
            <td>
                    <code>33554432</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    
</table>

