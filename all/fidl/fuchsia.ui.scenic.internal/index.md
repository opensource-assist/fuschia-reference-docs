Project: /_project.yaml
Book: /_book.yaml

# fuchsia.ui.scenic.internal


## **PROTOCOLS**

## Snapshot {:#Snapshot}
*Defined in [fuchsia.ui.scenic.internal/snapshot.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic.internal/snapshot.fidl#20)*

 Defines an internal interface to take snapshots of the entire scene graph. This
 is only to be used by trusted clients.

### TakeSnapshot {:#TakeSnapshot}

 Takes a snapshot of the entire scene-graph, starting with the first
 compositor found. A separate buffer is returned for each compositor,
 with an empty array being returned if no compositors were found at all.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>snapshots</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#SnapshotResult'>SnapshotResult</a>&gt;</code>
            </td>
        </tr></table>



## **STRUCTS**

### SnapshotResult {:#SnapshotResult}
*Defined in [fuchsia.ui.scenic.internal/snapshot.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic.internal/snapshot.fidl#12)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>success</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>













