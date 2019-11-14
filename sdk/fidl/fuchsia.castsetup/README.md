[TOC]

# fuchsia.castsetup


## **PROTOCOLS**

## StateWatcher {#StateWatcher}
*Defined in [fuchsia.castsetup/cast_setup.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.castsetup/cast_setup.fidl#9)*

<p>Interface that allows watching of changes to the cast setup state.</p>

### Watch {#Watch}

<p>Will immediately return on first call; subsequent calls will return on
change.</p>

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

### State {#State}
Type: <code>uint32</code>

*Defined in [fuchsia.castsetup/cast_setup.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.castsetup/cast_setup.fidl#16)*

<p>Enum of different possible setup states</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>0</code></td>
            <td><p>State is not determined.</p>
</td>
        </tr><tr>
            <td><code>IN_PROGRESS</code></td>
            <td><code>1</code></td>
            <td><p>Setup is not complete and is in progress.</p>
</td>
        </tr><tr>
            <td><code>OFFLINE</code></td>
            <td><code>2</code></td>
            <td><p>Configured once but disconnected for now.</p>
</td>
        </tr><tr>
            <td><code>COMPLETE</code></td>
            <td><code>3</code></td>
            <td><p>Setup is complete and device is connected.</p>
</td>
        </tr></table>











