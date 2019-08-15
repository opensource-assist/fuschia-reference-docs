Project: /_project.yaml
Book: /_book.yaml

# fuchsia.overnet.routingtablefuzzer




## **STRUCTS**

### RoutingTableFuzzPlan {:#RoutingTableFuzzPlan}
*Defined in [fuchsia.overnet.routingtablefuzzer/routing_table_fuzzer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/overnet/deprecated/lib/routing/routing_table_fuzzer.test.fidl#9)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>actions</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#RoutingTableAction'>RoutingTableAction</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Void {:#Void}
*Defined in [fuchsia.overnet.routingtablefuzzer/routing_table_fuzzer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/overnet/deprecated/lib/routing/routing_table_fuzzer.test.fidl#13)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>









## **XUNIONS**

### RoutingTableAction {:#RoutingTableAction}
*Defined in [fuchsia.overnet.routingtablefuzzer/routing_table_fuzzer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/overnet/deprecated/lib/routing/routing_table_fuzzer.test.fidl#15)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>step_time</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>update_node</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/index.html'>fuchsia.overnet.protocol</a>/<a class='link' href='../fuchsia.overnet.protocol/index.html#NodeStatus'>NodeStatus</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>update_link</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/index.html'>fuchsia.overnet.protocol</a>/<a class='link' href='../fuchsia.overnet.protocol/index.html#LinkStatus'>LinkStatus</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>update_flush</code></td>
            <td>
                <code><a class='link' href='#Void'>Void</a></code>
            </td>
            <td></td>
        </tr></table>





