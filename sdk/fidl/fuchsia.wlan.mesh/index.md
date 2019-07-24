Project: /_project.yaml
Book: /_book.yaml

# fuchsia.wlan.mesh




## **STRUCTS**

### MeshPath {:#MeshPath}
*Defined in [fuchsia.wlan.mesh/wlan_mesh.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mesh/wlan_mesh.fidl#9)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>dest_address</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>next_hop</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>metric</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MeshPathTable {:#MeshPathTable}
*Defined in [fuchsia.wlan.mesh/wlan_mesh.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mesh/wlan_mesh.fidl#15)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>paths</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#MeshPath'>MeshPath</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>













