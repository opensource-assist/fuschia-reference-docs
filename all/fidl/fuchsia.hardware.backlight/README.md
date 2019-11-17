[TOC]

# fuchsia.hardware.backlight


## **PROTOCOLS**

## Device {#Device}
*Defined in [fuchsia.hardware.backlight/backlight.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-backlight/backlight.fidl#20)*


### GetStateNormalized {#GetStateNormalized}

<p>Gets the current backlight brightness as a percentage value between 0.0
and 1.0</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Device_GetStateNormalized_Result'>Device_GetStateNormalized_Result</a></code>
            </td>
        </tr></table>

### SetStateNormalized {#SetStateNormalized}

<p>Sets the current backlight brightness as a percentage value between 0.0
and 1.0</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#State'>State</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Device_SetStateNormalized_Result'>Device_SetStateNormalized_Result</a></code>
            </td>
        </tr></table>

### GetStateAbsolute {#GetStateAbsolute}

<p>Gets the current backlight brightness in nits</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Device_GetStateAbsolute_Result'>Device_GetStateAbsolute_Result</a></code>
            </td>
        </tr></table>

### SetStateAbsolute {#SetStateAbsolute}

<p>Sets the current backlight brightness in nits</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#State'>State</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Device_SetStateAbsolute_Result'>Device_SetStateAbsolute_Result</a></code>
            </td>
        </tr></table>

### GetMaxAbsoluteBrightness {#GetMaxAbsoluteBrightness}

<p>Gets the maximum supported backlight brightness in nits, if known.
Otherwise returns error ZX_ERR_NOT_SUPPORTED.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Device_GetMaxAbsoluteBrightness_Result'>Device_GetMaxAbsoluteBrightness_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Device_GetStateNormalized_Response {#Device_GetStateNormalized_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#State'>State</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Device_SetStateNormalized_Response {#Device_SetStateNormalized_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Device_GetStateAbsolute_Response {#Device_GetStateAbsolute_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#State'>State</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Device_SetStateAbsolute_Response {#Device_SetStateAbsolute_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Device_GetMaxAbsoluteBrightness_Response {#Device_GetMaxAbsoluteBrightness_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>max_brightness</code></td>
            <td>
                <code>float64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### State {#State}
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
            <td><p>|brightness| can either be:</p>
<ol>
<li>The unitless brightness value on a linear scale where 0.0 is the minimum
brightness and 1.0 is the maximum brightness - represents the current /
desired brightness as a percentage within the supported range. Used
by the |GetStateNormalized| / |SetStateNormalized| calls.</li>
<li>Absolute brightness in nits. Used by the |GetStateAbsolute| /
|SetStateAbsolute| calls.</li>
</ol>
</td>
            <td>No default</td>
        </tr>
</table>







## **UNIONS**

### Device_GetStateNormalized_Result {#Device_GetStateNormalized_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Device_GetStateNormalized_Response'>Device_GetStateNormalized_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Device_SetStateNormalized_Result {#Device_SetStateNormalized_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Device_SetStateNormalized_Response'>Device_SetStateNormalized_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Device_GetStateAbsolute_Result {#Device_GetStateAbsolute_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Device_GetStateAbsolute_Response'>Device_GetStateAbsolute_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Device_SetStateAbsolute_Result {#Device_SetStateAbsolute_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Device_SetStateAbsolute_Response'>Device_SetStateAbsolute_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Device_GetMaxAbsoluteBrightness_Result {#Device_GetMaxAbsoluteBrightness_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Device_GetMaxAbsoluteBrightness_Response'>Device_GetMaxAbsoluteBrightness_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>







