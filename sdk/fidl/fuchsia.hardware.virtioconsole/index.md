Project: /_project.yaml
Book: /_book.yaml

# fuchsia.hardware.virtioconsole


## **PROTOCOLS**

## Device {:#Device}
*Defined in [fuchsia.hardware.virtioconsole/virtioconsole.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-virtioconsole/virtioconsole.fidl#9)*


### GetChannel {:#GetChannel}

 This API is temporary.  It exists because devhost multiplexes
 fuchsia.io.File on top of the device connections, and
 fuchsia.hardware.pty.Device composes with that interface.  Once
 the devhost stops the behavior, we can remove this interface and
 have virtio-console just serve fuchsia.hardware.pty.Device directly.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.hardware.pty/index.html'>fuchsia.hardware.pty</a>/<a class='link' href='../fuchsia.hardware.pty/index.html#Device'>Device</a>&gt;</code>
            </td>
        </tr></table>

















