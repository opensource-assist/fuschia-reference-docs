Project: /_project.yaml
Book: /_book.yaml

# test.inspect.validate

 The Inspect VMO Validator program starts and controls a "puppet" program to
 exercise each Inspect library. This file defines the protocol to exercise
 the library (and report the result of commands). (After executing some
 commands, the Validator program will analyze the VMO contents for
 correctness and memory-packing efficiency.)

## **PROTOCOLS**

## Validate {:#Validate}
*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#53)*


### Initialize {:#Initialize}

 Initializes the Inspect library being tested by the puppet.

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

### Act {:#Act}

 Modifies the contents of the VMO.

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

### CreateNode {:#CreateNode}
*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#35)*



 Tells the puppet to create a Node with the given name, parentage, and ID
 (the id is specified so other nodes can later be created under it).


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

### DeleteNode {:#DeleteNode}
*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#42)*



 Tells the puppet to delete the given node.


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



## **ENUMS**

### TestResult {:#TestResult}
Type: <code>uint32</code>

*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#18)*

 TestResult tells the result of executing an Initialize or Act command.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OK</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>NOT_IMPLEMENTED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>FAILED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>ILLEGAL</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### InitializationParams {:#InitializationParams}


*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#13)*

 InitializationParams tells how to initialize the Inspect library.


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

### Action {:#Action}
*Defined in [test.inspect.validate/validate.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#47)*

 Tells the puppet to do something to modify the VMO.

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
        </tr></table>





## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/inspect_validator/fidl/validate.test.fidl#31">ROOT_ID</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint32</code></td>
            <td> The data in the VMO is tree-structured, so some nodes are under the root.
 ROOT_ID identifies the root node.
</td>
        </tr>
    
</table>

