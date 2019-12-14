[TOC]

# fuchsia.hardware.vsock


## **PROTOCOLS**

## Callbacks {#Callbacks}
*Defined in [fuchsia.hardware.vsock/vsock.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-vsock/vsock.fidl#21)*


### Request {#Request}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>addr</code></td>
            <td>
                <code><a class='link' href='#Addr'>Addr</a></code>
            </td>
        </tr></table>



### Response {#Response}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>addr</code></td>
            <td>
                <code><a class='link' href='#Addr'>Addr</a></code>
            </td>
        </tr></table>



### Rst {#Rst}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>addr</code></td>
            <td>
                <code><a class='link' href='#Addr'>Addr</a></code>
            </td>
        </tr></table>



### Shutdown {#Shutdown}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>addr</code></td>
            <td>
                <code><a class='link' href='#Addr'>Addr</a></code>
            </td>
        </tr></table>



### TransportReset {#TransportReset}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>new_cid</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### SendVmoComplete {#SendVmoComplete}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>addr</code></td>
            <td>
                <code><a class='link' href='#Addr'>Addr</a></code>
            </td>
        </tr></table>



## Device {#Device}
*Defined in [fuchsia.hardware.vsock/vsock.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-vsock/vsock.fidl#46)*


### Start {#Start}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>cb</code></td>
            <td>
                <code><a class='link' href='#Callbacks'>Callbacks</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

### SendRequest {#SendRequest}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>addr</code></td>
            <td>
                <code><a class='link' href='#Addr'>Addr</a></code>
            </td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code>handle&lt;socket&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

### SendShutdown {#SendShutdown}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>addr</code></td>
            <td>
                <code><a class='link' href='#Addr'>Addr</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

### SendRst {#SendRst}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>addr</code></td>
            <td>
                <code><a class='link' href='#Addr'>Addr</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

### SendResponse {#SendResponse}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>addr</code></td>
            <td>
                <code><a class='link' href='#Addr'>Addr</a></code>
            </td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code>handle&lt;socket&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

### GetCid {#GetCid}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>local_cid</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### SendVmo {#SendVmo}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>addr</code></td>
            <td>
                <code><a class='link' href='#Addr'>Addr</a></code>
            </td>
        </tr><tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr><tr>
            <td><code>off</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>len</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Addr {#Addr}
*Defined in [fuchsia.hardware.vsock/vsock.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-vsock/vsock.fidl#12)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>local_port</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>remote_cid</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>remote_port</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>















