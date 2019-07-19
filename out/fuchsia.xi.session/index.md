Project: /_project.yaml
Book: /_book.yaml

# fuchsia.xi.session


## **PROTOCOLS**

## XiSessionManager {:#XiSessionManager}
*Defined in [fuchsia.xi.session/xi_session.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/xi/xi_session_agent/fidl/xi_session.fidl#9)*


### NewSession {:#NewSession}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>session_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

### CloseSession {:#CloseSession}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>session_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### ConnectSession {:#ConnectSession}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>session_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>sock</code></td>
            <td>
                <code>handle&lt;socket&gt;</code>
            </td>
        </tr></table>



### GetContents {:#GetContents}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>session_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr></table>















