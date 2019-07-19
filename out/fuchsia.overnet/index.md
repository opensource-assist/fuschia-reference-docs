Project: /_project.yaml
Book: /_book.yaml

# fuchsia.overnet


## **PROTOCOLS**

## Overnet {:#Overnet}
*Defined in [fuchsia.overnet/overnet.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet/overnet.fidl#10)*


### ListPeers {:#ListPeers}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>last_seen_version</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>version</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>peers</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.overnet/index.html#Peer'>Peer</a>&gt;</code>
            </td>
        </tr></table>

### RegisterService {:#RegisterService}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>provider</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet/index.html#ServiceProvider'>ServiceProvider</a></code>
            </td>
        </tr></table>



### ConnectToService {:#ConnectToService}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>node</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/index.html'>fuchsia.overnet.protocol</a>/<a class='link' href='../fuchsia.overnet.protocol/index.html#NodeId'>NodeId</a></code>
            </td>
        </tr><tr>
            <td><code>service_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>chan</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



## ServiceProvider {:#ServiceProvider}
*Defined in [fuchsia.overnet/overnet.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet/overnet.fidl#19)*


### ConnectToService {:#ConnectToService}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>chan</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>





## **STRUCTS**

### Peer {:#Peer}
*Defined in [fuchsia.overnet/overnet.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet/overnet.fidl#23)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/index.html'>fuchsia.overnet.protocol</a>/<a class='link' href='../fuchsia.overnet.protocol/index.html#NodeId'>NodeId</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>is_self</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>description</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/index.html'>fuchsia.overnet.protocol</a>/<a class='link' href='../fuchsia.overnet.protocol/index.html#PeerDescription'>PeerDescription</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>













