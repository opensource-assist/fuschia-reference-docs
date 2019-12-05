[TOC]

# fuchsia.virtualconsole


## **PROTOCOLS**

## SessionManager {#SessionManager}
*Defined in [fuchsia.virtualconsole/session-manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-virtualconsole/session-manager.fidl#12)*

<p>Manages virtual console sessions.</p>

### CreateSession {#CreateSession}

<p>Create a new virtual console session.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>session</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.hardware.pty/'>fuchsia.hardware.pty</a>/<a class='link' href='../fuchsia.hardware.pty/#Device'>Device</a>&gt;</code>
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

### HasPrimaryConnected {#HasPrimaryConnected}

<p>Returns true if virtcon currently has a display that it can display something on.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>connected</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

















