[TOC]

# fuchsia.thermal


## **PROTOCOLS**

## Controller {#Controller}
*Defined in [fuchsia.thermal/thermal.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-thermal/thermal.fidl#34)*

<p>A protocol providing the API for a client service to subscribe to receive thermal state updates.</p>

### Subscribe {#Subscribe}

<p>Subscribes with the Controller to receive thermal state changes on the specified
[fuchsia.thermal/Actor] proxy handle.</p>
<p>The current thermal state will be sent immediately, with all subsequent state changes
occuring based on the changing system thermal load and specified <code>trip_points</code>.</p>
<ul>
<li>request <code>actor</code> a [fuchsia.thermal/Actor] proxy to handle the SetThermalState callbacks</li>
<li>request <code>actor_type</code> a [fuchsia.thermal/ActorType] value to indicate the type of
subsystem this actor is representing. The Controller may leverage this extra
information to thermally limit only specific subsystems as needed.</li>
<li>request <code>trip_points</code> a vector containing the points within the normalized thermal
limiting range [0 - <code>MAX_THERMAL_LOAD</code>] at which the Actor should be transitioned to
the next thermal state. The Controller will call SetThermalState on the Actor each
time these points are crossed within the normalized range. The vector must:
- have length in the range [1 - <code>MAX_TRIP_POINT_COUNT</code>]
- have values in the range [1 - <code>MAX_THERMAL_LOAD</code>]
- be monotonically increasing</li>
</ul>
<ul>
<li>error a [fuchsia.thermal/Error] value indicating the reason (if any) that Subscribe failed</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>actor</code></td>
            <td>
                <code><a class='link' href='#Actor'>Actor</a></code>
            </td>
        </tr><tr>
            <td><code>actor_type</code></td>
            <td>
                <code><a class='link' href='#ActorType'>ActorType</a></code>
            </td>
        </tr><tr>
            <td><code>trip_points</code></td>
            <td>
                <code>vector&lt;uint32&gt;[100]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Controller_Subscribe_Result'>Controller_Subscribe_Result</a></code>
            </td>
        </tr></table>

## Actor {#Actor}
*Defined in [fuchsia.thermal/thermal.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-thermal/thermal.fidl#59)*

<p>The protocol to receive thermal state updates from the fuchsia.thermal/Controller.</p>

### SetThermalState {#SetThermalState}

<p>Sets the Actor's thermal state.</p>
<p>The Actor is expected to ACK each call before subsequent calls will be made. <code>state</code> is
defined as an index into the Actor's reported thermal ranges. The Actor's thermal ranges
are defined by dividing the normalized thermal limiting range [0 - <code>MAX_THERMAL_LOAD</code>] at
the locations specified by the <code>trip_points</code> argument to Subscribe. <code>state</code> is therefore in
the range [0 - len(trip_points)]. For each value of <code>state</code>, the subsystem should remain
operational. The value of <code>state</code> should be interpreted as:
0: &quot;normal operation&quot;
1..[len(trip_points) - 1]: The subsystem is operating in such a way that each state
produces less heat than the previous state
len(trip_points): max thermal limiting while still operational</p>
<p>As a simple example, consider that Subscribe was called with a vector of two trip points:
[50, 90]. We can think of these trip points as boundaries within the normalized range
[0 - <code>MAX_THERMAL_LOAD</code>] such that three thermal ranges are created: [0 - 49], [50 - 89],
and [90 - <code>MAX_THERMAL_LOAD</code>]. Now, as the Controller observes the system thermal load
increase through the normalized range, it calls SetThermalState at the specified trip
points and indicates the index of which thermal range is now active. In this example, the
Controller would initially call <code>SetThermalState(0)</code> when there is no thermal limiting
required. As the device heats up, the Controller would call <code>SetThermalState(1)</code> and finally
<code>SetThermalState(2)</code> as the Controller observes the system thermal load cross 50 and 90,
respectively.</p>
<ul>
<li>request <code>state</code> the new thermal state as an index into the Actor's reported thermal
ranges, which are defined based on the Actor's specified <code>trip_points</code>.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>state</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## **STRUCTS**

### Controller_Subscribe_Response {#Controller_Subscribe_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>



## **ENUMS**

### ActorType {#ActorType}
Type: <code>uint32</code>

*Defined in [fuchsia.thermal/thermal.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-thermal/thermal.fidl#9)*

<p>A value to indicate which type of subsystem an Actor connection represents. The Controller may
leverage this extra information to thermally limit only specific subsystems as needed.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNSPECIFIED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>AUDIO</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### Error {#Error}
Type: <code>uint32</code>

*Defined in [fuchsia.thermal/thermal.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-thermal/thermal.fidl#15)*

<p>Error codes for the thermal protocol.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INTERNAL</code></td>
            <td><code>1</code></td>
            <td><p>The component encountered an unspecified error while performing the operation.</p>
</td>
        </tr><tr>
            <td><code>INVALID_ARGUMENTS</code></td>
            <td><code>2</code></td>
            <td><p>At least one argument was invalid.</p>
</td>
        </tr></table>





## **UNIONS**

### Controller_Subscribe_Result {#Controller_Subscribe_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Controller_Subscribe_Response'>Controller_Subscribe_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="MAX_TRIP_POINT_COUNT">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-thermal/thermal.fidl#25">MAX_TRIP_POINT_COUNT</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum number of trip points that may be specified in the <code>trip_points</code> vector argument to
<code>Subscribe</code>.</p>
</td>
        </tr>
    <tr id="MAX_THERMAL_LOAD">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-thermal/thermal.fidl#30">MAX_THERMAL_LOAD</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum value of the normalized thermal load. This value bounds the width (and therefore
also the precision) of the normalized thermal limiting range starting from 0. Trip points must
be specified within this range.</p>
</td>
        </tr>
    
</table>



