Project: /_project.yaml
Book: /_book.yaml

# fuchsia.scpi

 System Control Power Interface

## **PROTOCOLS**

## SystemController {:#SystemController}
*Defined in [fuchsia.scpi/scpi.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.scpi/scpi.fidl#55)*


### GetDvfsInfo {:#GetDvfsInfo}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>power_domain</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr><tr>
            <td><code>opps</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#DvfsOpp'>DvfsOpp</a>&gt;</code>
            </td>
        </tr></table>

### GetSystemStatus {:#GetSystemStatus}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr><tr>
            <td><code>sys_status</code></td>
            <td>
                <code><a class='link' href='#SystemStatus'>SystemStatus</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### DvfsOpp {:#DvfsOpp}
*Defined in [fuchsia.scpi/scpi.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.scpi/scpi.fidl#29)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>freq_hz</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>volt_mv</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SystemStatus {:#SystemStatus}
*Defined in [fuchsia.scpi/scpi.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.scpi/scpi.fidl#34)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>big_cluster_op_index</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> operating point index for big cluster
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>small_cluster_op_index</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> operating point index for small cluster
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>temperature_celsius</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> current CPU temperature in degrees Celsius
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>fan_level</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> current Fan Level
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>cpu_utilization</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> current CPU utilization
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>memory_utilization</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> current Memory usage
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### Status {:#Status}
Type: <code>uint32</code>

*Defined in [fuchsia.scpi/scpi.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.scpi/scpi.fidl#10)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OK</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERR_DVFS_INFO</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERR_DVFS_OPP_IDX</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERR_TEMPERATURE</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERR_FAN_LEVEL</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERR_CPU_STATS</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERR_MEM_STATS</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr></table>











## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.scpi/scpi.fidl#8">MAX_DVFS_OPPS</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    
</table>

