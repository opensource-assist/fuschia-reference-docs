[TOC]

# fuchsia.perfmon.cpu


## **PROTOCOLS**

## Controller {#Controller}
*Defined in [fuchsia.perfmon.cpu/perfmon.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-perfmon-cpu/perfmon.fidl#134)*


### GetProperties {#GetProperties}

<p>Fetch the performance monitor properties of the system.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>properties</code></td>
            <td>
                <code><a class='link' href='#Properties'>Properties</a></code>
            </td>
        </tr></table>

### Initialize {#Initialize}

<p>Create a trace, allocating the needed trace buffers and other resources.
&quot;other resources&quot; is basically a catch-all for other things that will
be needed. This does not include reserving the events, that is done
later by <code>StageConfig()</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>allocation</code></td>
            <td>
                <code><a class='link' href='#Allocation'>Allocation</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Controller_Initialize_Result'>Controller_Initialize_Result</a></code>
            </td>
        </tr></table>

### Terminate {#Terminate}

<p>Free all trace buffers and any other resources allocated for the trace.
This is also done when the connection is closed.
Tracing is first stopped if not already stopped.
May be called multiple times.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### GetAllocation {#GetAllocation}

<p>Return the trace allocation configuration, if there is one.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>allocation</code></td>
            <td>
                <code><a class='link' href='#Allocation'>Allocation</a>?</code>
            </td>
        </tr></table>

### StageConfig {#StageConfig}

<p>Stage performance monitor specification for a cpu.
Must be called with data collection off and after <code>Initialize()</code>.
Note: This doesn't actually configure the h/w, this just stages
the values for subsequent use by <code>Start()</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='#Config'>Config</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Controller_StageConfig_Result'>Controller_StageConfig_Result</a></code>
            </td>
        </tr></table>

### GetConfig {#GetConfig}

<p>Fetch performance monitor specification for a cpu, if it exists.
Must be called with data collection off and after <code>StageConfig()</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='#Config'>Config</a>?</code>
            </td>
        </tr></table>

### GetBufferHandle {#GetBufferHandle}

<p>Return a handle of a trace buffer, if it exists, and if <code>descriptor</code>
is valid.
<code>descriptor</code> is (0, 1, 2, ..., <code>num_buffers</code>-1)</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>descriptor</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;?</code>
            </td>
        </tr></table>

### Start {#Start}

<p>Turn on data collection.
Must be called after <code>Initialize()</code> + <code>StageConfig()</code> and with data
collection off.</p>

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
                <code><a class='link' href='#Controller_Start_Result'>Controller_Start_Result</a></code>
            </td>
        </tr></table>

### Stop {#Stop}

<p>Turn off data collection.
May be called any time after <code>Initialize()</code> has been called and before
<code>Terminate()</code>. If called at other times the call is ignored.
May be called multiple times.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## **STRUCTS**

### Controller_Initialize_Response {#Controller_Initialize_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Controller_StageConfig_Response {#Controller_StageConfig_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Controller_Start_Response {#Controller_Start_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Properties {#Properties}
*Defined in [fuchsia.perfmon.cpu/perfmon.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-perfmon-cpu/perfmon.fidl#34)*



<p>The properties of this system.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>api_version</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>S/W API version = <code>API_VERSION</code>.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>pm_version</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>The H/W Performance Monitor version.
This is the version defined by the architecture.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_num_events</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>The maximum number of events that can be simultaneously supported.
The combination of events that can be simultaneously supported is
architecture/model specific.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_num_fixed_events</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>The maximum number of fixed events that can be simultaneously
supported, and their maximum width.
These values are for informational/display purposes.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_fixed_counter_width</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_num_programmable_events</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>The maximum number of programmable events that can be simultaneously
supported, and their maximum width.
These values are for informational/display purposes.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_programmable_counter_width</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_num_misc_events</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>The maximum number of misc events that can be simultaneously
supported, and their maximum width.
These values are for informational/display purposes.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_misc_counter_width</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>flags</code></td>
            <td>
                <code><a class='link' href='#PropertyFlags'>PropertyFlags</a></code>
            </td>
            <td><p>Various flags.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### EventConfig {#EventConfig}
*Defined in [fuchsia.perfmon.cpu/perfmon.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-perfmon-cpu/perfmon.fidl#95)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>event</code></td>
            <td>
                <code><a class='link' href='#EventId'>EventId</a></code>
            </td>
            <td><p>Event to collect data for.
The values are architecture specific ids.
Each event may appear at most once.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>rate</code></td>
            <td>
                <code><a class='link' href='#EventRate'>EventRate</a></code>
            </td>
            <td><p>Sampling rate.</p>
<ul>
<li>If rate is non-zero then when the event gets this many hits data is
collected (e.g., pc, time).
The rate can be non-zero for counting based events only.</li>
<li>If rate is zero then:
If there is a timebase event then data for this event is collected
when data for the timebase event is collected.
Otherwise data for the event is collected once, when tracing stops.</li>
</ul>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>flags</code></td>
            <td>
                <code><a class='link' href='#EventConfigFlags'>EventConfigFlags</a></code>
            </td>
            <td><p>Flags for the event.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### Config {#Config}
*Defined in [fuchsia.perfmon.cpu/perfmon.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-perfmon-cpu/perfmon.fidl#116)*



<p>Passed to <code>StageConfig()</code> to select the data to be collected.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>events</code></td>
            <td>
                <code>[32]</code>
            </td>
            <td><p>Events to collect data for.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### Allocation {#Allocation}
*Defined in [fuchsia.perfmon.cpu/perfmon.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-perfmon-cpu/perfmon.fidl#124)*



<p>The allocation configuration for a data collection run.
This is generally the first call to allocate resources for a trace,
&quot;trace&quot; is used generically here: == &quot;data collection run&quot;.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>num_buffers</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>The number of buffers to allocate for trace data.
This must be #cpus for now.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>buffer_size_in_pages</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>The size of each buffer in 4K pages.
Each cpu gets same buffer size.</p>
</td>
            <td>No default</td>
        </tr>
</table>







## **UNIONS**

### Controller_Initialize_Result {#Controller_Initialize_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Controller_Initialize_Response'>Controller_Initialize_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### Controller_StageConfig_Result {#Controller_StageConfig_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Controller_StageConfig_Response'>Controller_StageConfig_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### Controller_Start_Result {#Controller_Start_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Controller_Start_Response'>Controller_Start_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>





## **BITS**

### PropertyFlags {#PropertyFlags}
Type: <code>uint64</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>HAS_LAST_BRANCH</td>
            <td>1</td>
            <td><p>The architecture supports LBR records (Last Branch Records).</p>
</td>
        </tr></table>

### EventConfigFlags {#EventConfigFlags}
Type: <code>uint32</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>COLLECT_OS</td>
            <td>1</td>
            <td><p>Collect data when running in kernel mode.</p>
</td>
        </tr><tr>
            <td>COLLECT_USER</td>
            <td>2</td>
            <td><p>Collect data when running in userspace mode.</p>
</td>
        </tr><tr>
            <td>COLLECT_PC</td>
            <td>4</td>
            <td><p>Collect aspace+pc values.</p>
</td>
        </tr><tr>
            <td>IS_TIMEBASE</td>
            <td>8</td>
            <td><p>If set for an event then the event is used as the &quot;timebase&quot;: data
for events with a zero rate is collected when data for the timebase
event is collected.
It is an error to have this set and have the event's rate be zero.
At most one event may be the timebase event.</p>
</td>
        </tr><tr>
            <td>COLLECT_LAST_BRANCH</td>
            <td>16</td>
            <td><p>Collect the available set of last branches.
Branch data is emitted as LastBranch records.
This is only available when the underlying system supports it.</p>
</td>
        </tr></table>



## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="API_VERSION">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-perfmon-cpu/perfmon.fidl#21">API_VERSION</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr id="MAX_NUM_EVENTS">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-perfmon-cpu/perfmon.fidl#25">MAX_NUM_EVENTS</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint16</code></td>
            <td><p>The maximum number of events we support simultaneously.
Typically the h/w supports less than this, e.g., 7 or so.</p>
</td>
        </tr>
    
</table>



## **TYPE ALIASES**

<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr id="EventRate">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-perfmon-cpu/perfmon.fidl#10">EventRate</a></td>
            <td>
                <code>uint32</code></td>
            <td></td>
        </tr><tr id="EventId">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-perfmon-cpu/perfmon.fidl#19">EventId</a></td>
            <td>
                <code>uint16</code></td>
            <td></td>
        </tr></table>

