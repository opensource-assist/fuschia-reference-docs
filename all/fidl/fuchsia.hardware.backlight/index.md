Project: /_project.yaml
Book: /_book.yaml

# fuchsia.hardware.backlight


## **PROTOCOLS**

## Device {:#Device}
*Defined in [fuchsia.hardware.backlight/backlight.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-backlight/backlight.fidl#17)*


### GetState {:#GetState}

 Gets the current backlight brightness

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

### SetState {:#SetState}

 Sets the current backlight brightness

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#State'>State</a></code>
            </td>
        </tr></table>





## **STRUCTS**

### State {:#State}
*Defined in [fuchsia.hardware.backlight/backlight.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-backlight/backlight.fidl#8)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>backlight_on</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>brightness</code></td>
            <td>
                <code>float64</code>
            </td>
            <td> The unitless brightness value on a linear scale where 0.0 is the minimum
 brightness and 1.0 is the maximum brightness - represents the current /
 desired brightness as a percentage within the supported range.
</td>
            <td>No default</td>
        </tr>
</table>













