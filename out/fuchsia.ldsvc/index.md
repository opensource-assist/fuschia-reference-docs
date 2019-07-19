Project: /_project.yaml
Book: /_book.yaml

# fuchsia.ldsvc


## **PROTOCOLS**

## Loader {:#Loader}
*Defined in [fuchsia.ldsvc/ldsvc.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-ldsvc/ldsvc.fidl#18)*


### Done {:#Done}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### LoadObject {:#LoadObject}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>object_name</code></td>
            <td>
                <code>string[1024]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rv</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>object</code></td>
            <td>
                <code>handle&lt;vmo&gt;?</code>
            </td>
        </tr></table>

### LoadScriptInterpreter {:#LoadScriptInterpreter}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>interpreter_name</code></td>
            <td>
                <code>string[1024]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rv</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>object</code></td>
            <td>
                <code>handle&lt;vmo&gt;?</code>
            </td>
        </tr></table>

### Config {:#Config}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code>string[1024]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rv</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Clone {:#Clone}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>loader</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.ldsvc/index.html#Loader'>Loader</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rv</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### DebugPublishDataSink {:#DebugPublishDataSink}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data_sink</code></td>
            <td>
                <code>string[1024]</code>
            </td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rv</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### DebugLoadConfig {:#DebugLoadConfig}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config_name</code></td>
            <td>
                <code>string[1024]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rv</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>config</code></td>
            <td>
                <code>handle&lt;vmo&gt;?</code>
            </td>
        </tr></table>















