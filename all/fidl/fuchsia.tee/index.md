Project: /_project.yaml
Book: /_book.yaml

# fuchsia.tee


## **PROTOCOLS**

## Device {:#Device}
*Defined in [fuchsia.tee/tee.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tee/tee.fidl#94)*


### GetOsInfo {:#GetOsInfo}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#OsInfo'>OsInfo</a></code>
            </td>
        </tr></table>

### OpenSession {:#OpenSession}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>trusted_app</code></td>
            <td>
                <code><a class='link' href='#Uuid'>Uuid</a></code>
            </td>
        </tr><tr>
            <td><code>parameter_set</code></td>
            <td>
                <code><a class='link' href='#ParameterSet'>ParameterSet</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>session_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>OpResult</code></td>
            <td>
                <code><a class='link' href='#OpResult'>OpResult</a></code>
            </td>
        </tr></table>

### InvokeCommand {:#InvokeCommand}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>session_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>command_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>parameter_set</code></td>
            <td>
                <code><a class='link' href='#ParameterSet'>ParameterSet</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>OpResult</code></td>
            <td>
                <code><a class='link' href='#OpResult'>OpResult</a></code>
            </td>
        </tr></table>

### CloseSession {:#CloseSession}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>session_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## **STRUCTS**

### Uuid {:#Uuid}
*Defined in [fuchsia.tee/tee.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tee/tee.fidl#11)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>time_low</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>time_mid</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>time_hi_and_version</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>clock_seq_and_node</code></td>
            <td>
                <code>uint8[8]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### OsRevision {:#OsRevision}
*Defined in [fuchsia.tee/tee.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tee/tee.fidl#18)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>major</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>minor</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### OsInfo {:#OsInfo}
*Defined in [fuchsia.tee/tee.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tee/tee.fidl#23)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>uuid</code></td>
            <td>
                <code><a class='link' href='#Uuid'>Uuid</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>revision</code></td>
            <td>
                <code><a class='link' href='#OsRevision'>OsRevision</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>is_global_platform_compliant</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Empty {:#Empty}
*Defined in [fuchsia.tee/tee.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tee/tee.fidl#42)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Buffer {:#Buffer}
*Defined in [fuchsia.tee/tee.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tee/tee.fidl#44)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>direction</code></td>
            <td>
                <code><a class='link' href='#Direction'>Direction</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>offset</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Value {:#Value}
*Defined in [fuchsia.tee/tee.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tee/tee.fidl#56)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>direction</code></td>
            <td>
                <code><a class='link' href='#Direction'>Direction</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>a</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>b</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>c</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ParameterSet {:#ParameterSet}
*Defined in [fuchsia.tee/tee.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tee/tee.fidl#69)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>count</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>parameters</code></td>
            <td>
                <code>[4]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### OpResult {:#OpResult}
*Defined in [fuchsia.tee/tee.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tee/tee.fidl#87)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>return_code</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>return_origin</code></td>
            <td>
                <code><a class='link' href='#ReturnOrigin'>ReturnOrigin</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>parameter_set</code></td>
            <td>
                <code><a class='link' href='#ParameterSet'>ParameterSet</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### Direction {:#Direction}
Type: <code>uint32</code>

*Defined in [fuchsia.tee/tee.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tee/tee.fidl#34)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INPUT</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>OUTPUT</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>INOUT</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### ReturnOrigin {:#ReturnOrigin}
Type: <code>uint32</code>

*Defined in [fuchsia.tee/tee.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tee/tee.fidl#77)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>COMMUNICATION</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>TRUSTED_OS</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>TRUSTED_APPLICATION</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>





## **UNIONS**

### Parameter {:#Parameter}
*Defined in [fuchsia.tee/tee.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tee/tee.fidl#63)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>empty</code></td>
            <td>
                <code><a class='link' href='#Empty'>Empty</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='#Buffer'>Buffer</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#Value'>Value</a></code>
            </td>
            <td></td>
        </tr></table>







