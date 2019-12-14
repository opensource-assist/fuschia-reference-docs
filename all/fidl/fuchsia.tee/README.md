[TOC]

# fuchsia.tee


## **PROTOCOLS**

## Device {#Device}
*Defined in [fuchsia.tee/tee.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tee/tee.fidl#106)*


### GetOsInfo {#GetOsInfo}

<p>Obtain information about the TEE OS</p>

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

### OpenSession {#OpenSession}

<p>Initiates a communication session with the specified trusted application.</p>

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
            <td><code>op_result</code></td>
            <td>
                <code><a class='link' href='#OpResult'>OpResult</a></code>
            </td>
        </tr></table>

### InvokeCommand {#InvokeCommand}

<p>Requests the trusted application perform the provided command. The command is unique to the
trusted application.</p>

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
            <td><code>op_result</code></td>
            <td>
                <code><a class='link' href='#OpResult'>OpResult</a></code>
            </td>
        </tr></table>

### CloseSession {#CloseSession}

<p>Closes an established session.</p>

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

### Uuid {#Uuid}
*Defined in [fuchsia.tee/tee.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tee/tee.fidl#11)*



<p>UUID identifiers are used to identify the TEE Operating System and individual Trusted
Applications. This structure matches the UUID type as defined by RFC4122.</p>


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

### None {#None}
*Defined in [fuchsia.tee/tee.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tee/tee.fidl#41)*



<p>An empty parameter type is used as a placeholder for elements in the parameter set that are not
used.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>



## **ENUMS**

### Direction {#Direction}
Type: <code>uint32</code>

*Defined in [fuchsia.tee/tee.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tee/tee.fidl#32)*

<p>Communication with the TEE OS and Trusted Applications is performed using opaque parameters.
These parameters can be a mix of small values (Value type) or a buffer reference (Buffer type).
A parameter will be tagged as either an input, output or both (inout).</p>


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

### ReturnOrigin {#ReturnOrigin}
Type: <code>uint32</code>

*Defined in [fuchsia.tee/tee.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tee/tee.fidl#89)*

<p>Each operation must flow through the device driver and the trusted operating system before
reaching the trusted application (and back). The ReturnOrigin indicates which layer provided the
return code.</p>


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



## **TABLES**

### OsRevision {#OsRevision}


*Defined in [fuchsia.tee/tee.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tee/tee.fidl#18)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>major</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>minor</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr></table>

### OsInfo {#OsInfo}


*Defined in [fuchsia.tee/tee.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tee/tee.fidl#23)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>uuid</code></td>
            <td>
                <code><a class='link' href='#Uuid'>Uuid</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>revision</code></td>
            <td>
                <code><a class='link' href='#OsRevision'>OsRevision</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>is_global_platform_compliant</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr></table>

### Buffer {#Buffer}


*Defined in [fuchsia.tee/tee.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tee/tee.fidl#45)*

<p>Represents a buffer parameter.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>direction</code></td>
            <td>
                <code><a class='link' href='#Direction'>Direction</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
            <td><p>The VMO is allowed to be not present for situations where the TEE allows for buffer size
checks.</p>
<p>For example, if the operation to be performed needs an output buffer, but the user cannot
calculate how large that output buffer should be, they can attempt the operation without
a vmo and the Trusted Application will populate the size field so that the operation can
be performed again with an appropriately sized buffer.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>offset</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr></table>

### Value {#Value}


*Defined in [fuchsia.tee/tee.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tee/tee.fidl#61)*

<p>Represents a direct value parameter.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>direction</code></td>
            <td>
                <code><a class='link' href='#Direction'>Direction</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>a</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>This value is optional. If not set, a zero value is sent in its place if it is required by
the calling convention.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>b</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>This value is optional. If not set, a zero value is sent in its place if it is required by
the calling convention.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>c</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>This value is optional. If not set, a zero value is sent in its place if it is required by
the calling convention.</p>
</td>
        </tr></table>

### OpResult {#OpResult}


*Defined in [fuchsia.tee/tee.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tee/tee.fidl#99)*

<p>The result of an operation will include a return code, the origin of the result, and the return
of the parameter set. The returned parameter set will be a copy of the input parameter set, but
with the INOUT and OUTPUT parameters updated. If the parameter is a Buffer, it will update the
Buffer.size to the number of bytes written.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>return_code</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>return_origin</code></td>
            <td>
                <code><a class='link' href='#ReturnOrigin'>ReturnOrigin</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>parameter_set</code></td>
            <td>
                <code><a class='link' href='#ParameterSet'>ParameterSet</a></code>
            </td>
            <td></td>
        </tr></table>





## **XUNIONS**

### Parameter {#Parameter}
*Defined in [fuchsia.tee/tee.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tee/tee.fidl#77)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>none</code></td>
            <td>
                <code><a class='link' href='#None'>None</a></code>
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





## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="MAX_PARAMETERSET_COUNT">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tee/tee.fidl#83">MAX_PARAMETERSET_COUNT</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    
</table>



## **TYPE ALIASES**

<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr id="ParameterSet">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tee/tee.fidl#84">ParameterSet</a></td>
            <td>
                <code>vector</code>[<code><a class='link' href='#MAX_PARAMETERSET_COUNT'>MAX_PARAMETERSET_COUNT</a></code>]</td>
            <td></td>
        </tr></table>

