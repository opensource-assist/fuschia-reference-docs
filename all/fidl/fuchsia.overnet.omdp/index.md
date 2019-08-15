Project: /_project.yaml
Book: /_book.yaml

# fuchsia.overnet.omdp

 This protocol is sent on UDP packets to announce Overnet nodes to the world.



## **STRUCTS**

### Beacon {:#Beacon}
*Defined in [fuchsia.overnet.omdp/omdp.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.omdp/omdp.fidl#10)*



 A beacon announces one node to the world.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>node_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Overnet node id of the beacon's source.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>detail</code></td>
            <td>
                <code><a class='link' href='#BeaconDetail'>BeaconDetail</a></code>
            </td>
            <td> Extra data about this node.
</td>
            <td>No default</td>
        </tr>
</table>





## **TABLES**

### BeaconDetail {:#BeaconDetail}


*Defined in [fuchsia.overnet.omdp/omdp.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.omdp/omdp.fidl#18)*

 Placeholder for extra details about a node.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    </table>









