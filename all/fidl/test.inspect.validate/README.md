[TOC]

# test.inspect.validate

<p>The Inspect VMO Validator program starts and controls a &quot;puppet&quot; program to
exercise each Inspect library. This file defines the protocol to exercise
the library (and report the result of commands). (After executing some
commands, the Validator program will analyze the VMO contents for
correctness and memory-packing efficiency.)</p>

## **PROTOCOLS**

## Validate {#Validate}
*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#192)*


### Initialize {#Initialize}

<p>Initializes the Inspect library being tested by the puppet.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>params</code></td>
            <td>
                <code><a class='link' href='#InitializationParams'>InitializationParams</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;handle&gt;?</code>
            </td>
        </tr><tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#TestResult'>TestResult</a></code>
            </td>
        </tr></table>

### Act {#Act}

<p>Modifies the contents of the VMO.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>action</code></td>
            <td>
                <code><a class='link' href='#Action'>Action</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#TestResult'>TestResult</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### CreateNode {#CreateNode}
*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#35)*



<p>Tells the puppet to create a Node with the given name, parentage, and ID
(the id is specified so other nodes can later be created under it).</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>parent</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DeleteNode {#DeleteNode}
*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#42)*



<p>Tells the puppet to delete the given node.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### CreateNumericProperty {#CreateNumericProperty}
*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#59)*



<p>Tells the puppet to create a property with the given numeric value.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>parent</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#Number'>Number</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### CreateBytesProperty {#CreateBytesProperty}
*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#67)*



<p>Tells the puppet to create a property with the given byte array value.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>parent</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### CreateStringProperty {#CreateStringProperty}
*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#75)*



<p>Tells the puppet to create a property with the given string value.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>parent</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DeleteProperty {#DeleteProperty}
*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#83)*



<p>Tells the puppet to delete an existing property.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AddNumber {#AddNumber}
*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#87)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#Number'>Number</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SubtractNumber {#SubtractNumber}
*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#92)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#Number'>Number</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetNumber {#SetNumber}
*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#97)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#Number'>Number</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetBytes {#SetBytes}
*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#102)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetString {#SetString}
*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#107)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### CreateArrayProperty {#CreateArrayProperty}
*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#112)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>parent</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>slots</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>number_type</code></td>
            <td>
                <code><a class='link' href='#NumberType'>NumberType</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ArraySet {#ArraySet}
*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#120)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>index</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#Number'>Number</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ArrayAdd {#ArrayAdd}
*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#126)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>index</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#Number'>Number</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ArraySubtract {#ArraySubtract}
*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#132)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>index</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#Number'>Number</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### CreateLinearHistogram {#CreateLinearHistogram}
*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#138)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>parent</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>floor</code></td>
            <td>
                <code><a class='link' href='#Number'>Number</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>step_size</code></td>
            <td>
                <code><a class='link' href='#Number'>Number</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>buckets</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### CreateExponentialHistogram {#CreateExponentialHistogram}
*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#147)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>parent</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>floor</code></td>
            <td>
                <code><a class='link' href='#Number'>Number</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>initial_step</code></td>
            <td>
                <code><a class='link' href='#Number'>Number</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>step_multiplier</code></td>
            <td>
                <code><a class='link' href='#Number'>Number</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>buckets</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Insert {#Insert}
*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#157)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#Number'>Number</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### InsertMultiple {#InsertMultiple}
*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#162)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#Number'>Number</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>count</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### TestResult {#TestResult}
Type: <code>uint32</code>

*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#18)*

<p>TestResult tells the result of executing an Initialize or Act command.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OK</code></td>
            <td><code>0</code></td>
            <td><p>The function call completed without error.</p>
</td>
        </tr><tr>
            <td><code>UNIMPLEMENTED</code></td>
            <td><code>1</code></td>
            <td><p>The Inspect library doesn't implement a requested feature.</p>
</td>
        </tr><tr>
            <td><code>FAILED</code></td>
            <td><code>2</code></td>
            <td><p>The Inspect library reported a failure executing the function.</p>
</td>
        </tr><tr>
            <td><code>ILLEGAL</code></td>
            <td><code>3</code></td>
            <td><p>The driver and/or puppet-wrapper was in an illegal state.</p>
</td>
        </tr></table>

### NumberType {#NumberType}
Type: <code>uint8</code>

*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#46)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INT</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>UINT</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>DOUBLE</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### InitializationParams {#InitializationParams}


*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#13)*

<p>InitializationParams tells how to initialize the Inspect library.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>vmoSize</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr></table>





## **XUNIONS**

### Number {#Number}
*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#52)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>int_t</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>uint_t</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>double_t</code></td>
            <td>
                <code>float64</code>
            </td>
            <td></td>
        </tr></table>

### Action {#Action}
*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#169)*

<p>Tells the puppet to do something to modify the VMO.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>create_node</code></td>
            <td>
                <code><a class='link' href='#CreateNode'>CreateNode</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>delete_node</code></td>
            <td>
                <code><a class='link' href='#DeleteNode'>DeleteNode</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>create_numeric_property</code></td>
            <td>
                <code><a class='link' href='#CreateNumericProperty'>CreateNumericProperty</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>create_bytes_property</code></td>
            <td>
                <code><a class='link' href='#CreateBytesProperty'>CreateBytesProperty</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>create_string_property</code></td>
            <td>
                <code><a class='link' href='#CreateStringProperty'>CreateStringProperty</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>delete_property</code></td>
            <td>
                <code><a class='link' href='#DeleteProperty'>DeleteProperty</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_number</code></td>
            <td>
                <code><a class='link' href='#SetNumber'>SetNumber</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_string</code></td>
            <td>
                <code><a class='link' href='#SetString'>SetString</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_bytes</code></td>
            <td>
                <code><a class='link' href='#SetBytes'>SetBytes</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>add_number</code></td>
            <td>
                <code><a class='link' href='#AddNumber'>AddNumber</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>subtract_number</code></td>
            <td>
                <code><a class='link' href='#SubtractNumber'>SubtractNumber</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>create_array_property</code></td>
            <td>
                <code><a class='link' href='#CreateArrayProperty'>CreateArrayProperty</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>array_set</code></td>
            <td>
                <code><a class='link' href='#ArraySet'>ArraySet</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>array_add</code></td>
            <td>
                <code><a class='link' href='#ArrayAdd'>ArrayAdd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>array_subtract</code></td>
            <td>
                <code><a class='link' href='#ArraySubtract'>ArraySubtract</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>create_linear_histogram</code></td>
            <td>
                <code><a class='link' href='#CreateLinearHistogram'>CreateLinearHistogram</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>create_exponential_histogram</code></td>
            <td>
                <code><a class='link' href='#CreateExponentialHistogram'>CreateExponentialHistogram</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>insert</code></td>
            <td>
                <code><a class='link' href='#Insert'>Insert</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>insert_multiple</code></td>
            <td>
                <code><a class='link' href='#InsertMultiple'>InsertMultiple</a></code>
            </td>
            <td></td>
        </tr></table>





## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#31">ROOT_ID</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The data in the VMO is tree-structured, and
ROOT_ID identifies the (virtual) root node.</p>
</td>
        </tr>
    
</table>

