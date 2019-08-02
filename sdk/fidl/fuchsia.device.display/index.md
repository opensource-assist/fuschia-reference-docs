Project: /_project.yaml
Book: /_book.yaml

# fuchsia.device.display


## **PROTOCOLS**

## Manager {:#Manager}
*Defined in [fuchsia.device.display/display.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.device.display/display.fidl#8)*

 An interface for accessing and modifying display state.

### GetBrightness {:#GetBrightness}

 Retrieves the current brightness of the display. The brightness is
 specified as a percentage of the maximum brightness.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>success</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>brightness</code></td>
            <td>
                <code>float64</code>
            </td>
        </tr></table>

### SetBrightness {:#SetBrightness}

 Sets the brightness of the display. The brightness is specified a
 percentage of the maximum brightness.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>brightness</code></td>
            <td>
                <code>float64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>success</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>















