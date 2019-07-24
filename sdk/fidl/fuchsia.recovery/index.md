Project: /_project.yaml
Book: /_book.yaml

# fuchsia.recovery


## **PROTOCOLS**

## FactoryReset {:#FactoryReset}
*Defined in [fuchsia.recovery/factory_reset.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.recovery/factory_reset.fidl#11)*

 A protocol for intitiating a factory reset which wipes mutable data from disk.

### Reset {:#Reset}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

## FactoryResetStateNotifier {:#FactoryResetStateNotifier}
*Defined in [fuchsia.recovery/factory_reset.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.recovery/factory_reset.fidl#29)*

 A protocol for observing changes to factory reset state, such as beginning or cancelling the
 count down to factory reset.

### SetWatcher {:#SetWatcher}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#FactoryResetStateWatcher'>FactoryResetStateWatcher</a></code>
            </td>
        </tr></table>



## FactoryResetStateWatcher {:#FactoryResetStateWatcher}
*Defined in [fuchsia.recovery/factory_reset.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.recovery/factory_reset.fidl#34)*


### OnStateChanged {:#OnStateChanged}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#FactoryResetState'>FactoryResetState</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>







## **TABLES**

### FactoryResetState {:#FactoryResetState}


*Defined in [fuchsia.recovery/factory_reset.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.recovery/factory_reset.fidl#17)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>reset_deadline</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> The deadline of when factory reset will be triggered. This field is populated if
</td>
        </tr><tr>
            <td>2</td>
            <td><code>counting_down</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> True if factory reset is counting down.
</td>
        </tr></table>









