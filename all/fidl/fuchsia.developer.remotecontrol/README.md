[TOC]

# fuchsia.developer.remotecontrol


## **PROTOCOLS**

## FdbRemoteControl {#FdbRemoteControl}
*Defined in [fuchsia.developer.remotecontrol/remote-control.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/developer/remote-control/service/remote-control.fidl#25)*


### RunComponent {#RunComponent}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>component_url</code></td>
            <td>
                <code>string[2083]</code>
            </td>
        </tr><tr>
            <td><code>args</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#RunComponentResponse'>RunComponentResponse</a></code>
            </td>
        </tr></table>

### RebootDevice {#RebootDevice}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>







## **TABLES**

### RunComponentResponse {#RunComponentResponse}


*Defined in [fuchsia.developer.remotecontrol/remote-control.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/developer/remote-control/service/remote-control.fidl#13)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>exit_code</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>component_stdout</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>component_stderr</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr></table>









## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="MAX_URL_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/src/developer/remote-control/service/remote-control.fidl#10">MAX_URL_LENGTH</a></td>
            <td>
                    <code>2083</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    
</table>



