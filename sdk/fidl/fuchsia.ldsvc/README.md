[TOC]

# fuchsia.ldsvc


## **PROTOCOLS**

## Loader {#Loader}
*Defined in [fuchsia.ldsvc/ldsvc.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-ldsvc/ldsvc.fidl#18)*


### Done {#Done}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### LoadObject {#LoadObject}


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

### Config {#Config}


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

### Clone {#Clone}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>loader</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Loader'>Loader</a>&gt;</code>
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

















