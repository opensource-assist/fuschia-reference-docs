Project: /_project.yaml
Book: /_book.yaml

# fuchsia.castsetup


## **PROTOCOLS**

## StateWatcher {:#StateWatcher}
*Defined in [fuchsia.castsetup/cast_setup.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.castsetup/cast_setup.fidl#9)*

 Interface that allows watching of changes to the cast setup state.

### Watch {:#Watch}

 Will immediately return on first call; subsequent calls will return on
 change.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#State'>State</a></code>
            </td>
        </tr></table>





## **ENUMS**

### State {:#State}
Type: <code>uint32</code>

*Defined in [fuchsia.castsetup/cast_setup.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.castsetup/cast_setup.fidl#16)*

 Enum of different possible setup states


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>0</code></td>
            <td> State is not determined.
</td>
        </tr><tr>
            <td><code>IN_PROGRESS</code></td>
            <td><code>1</code></td>
            <td> Setup is not complete and is in progress.
</td>
        </tr><tr>
            <td><code>OFFLINE</code></td>
            <td><code>2</code></td>
            <td> Configured once but disconnected for now.
</td>
        </tr><tr>
            <td><code>COMPLETE</code></td>
            <td><code>3</code></td>
            <td> Setup is complete and device is connected.
</td>
        </tr></table>











