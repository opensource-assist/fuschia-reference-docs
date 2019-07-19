Project: /_project.yaml
Book: /_book.yaml

# fuchsia.virtualconsole


## **PROTOCOLS**

## SessionManager {:#SessionManager}
*Defined in [fuchsia.virtualconsole/session-manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-virtualconsole/session-manager.fidl#12)*

 Manages virtual console sessions.

### CreateSession {:#CreateSession}

 Create a new virtual console session.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>session</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.hardware.pty/index.html'>fuchsia.hardware.pty</a>/<a class='link' href='../fuchsia.hardware.pty/index.html#Device'>Device</a>&gt;</code>
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















