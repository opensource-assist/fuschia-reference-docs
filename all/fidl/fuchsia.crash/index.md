Project: /_project.yaml
Book: /_book.yaml

# fuchsia.crash


## **PROTOCOLS**

## Analyzer {:#Analyzer}
*Defined in [fuchsia.crash/analyzer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-crash/analyzer.fidl#12)*

 Analyzes string exceptions from managed runtimes.

### OnManagedRuntimeException {:#OnManagedRuntimeException}

 Requests that the crash analyzer handles the exception thrown by the
 Requests that the crash analyzer handles the exception thrown in the
 managed runtime.

 `component_url` is the full Fuchsia URL of the component that crashed.

 A typical implementation might print the exception message and stack
 trace to the system log or upload a crash report to a server.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>component_url</code></td>
            <td>
                <code>string[1024]</code>
            </td>
        </tr><tr>
            <td><code>exception</code></td>
            <td>
                <code><a class='link' href='#ManagedRuntimeException'>ManagedRuntimeException</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Analyzer_OnManagedRuntimeException_Result'>Analyzer_OnManagedRuntimeException_Result</a></code>
            </td>
        </tr></table>

## Analyzer {:#Analyzer}
*Defined in [fuchsia.crash/analyzer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-crash/analyzer.fidl#12)*

 Analyzes string exceptions from managed runtimes.

### OnManagedRuntimeException {:#OnManagedRuntimeException}

 Requests that the crash analyzer handles the exception thrown by the
 Requests that the crash analyzer handles the exception thrown in the
 managed runtime.

 `component_url` is the full Fuchsia URL of the component that crashed.

 A typical implementation might print the exception message and stack
 trace to the system log or upload a crash report to a server.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>component_url</code></td>
            <td>
                <code>string[1024]</code>
            </td>
        </tr><tr>
            <td><code>exception</code></td>
            <td>
                <code><a class='link' href='#ManagedRuntimeException'>ManagedRuntimeException</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Analyzer_OnManagedRuntimeException_Result'>Analyzer_OnManagedRuntimeException_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Analyzer_OnManagedRuntimeException_Response {:#Analyzer_OnManagedRuntimeException_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### UnknownException {:#UnknownException}
*Defined in [fuchsia.crash/analyzer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-crash/analyzer.fidl#40)*



 Represents a language-agnostic exception.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
            <td> A general buffer to hold some exception data.
</td>
            <td>No default</td>
        </tr>
</table>

### GenericException {:#GenericException}
*Defined in [fuchsia.crash/analyzer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-crash/analyzer.fidl#47)*



 Represents a generic exception that works for many managed runtime languages.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>type</code></td>
            <td>
                <code>uint8[128]</code>
            </td>
            <td> Exception type, e.g., "FileSystemException".
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>message</code></td>
            <td>
                <code>uint8[1024]</code>
            </td>
            <td> Exception message, e.g., "cannot open file".
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>stack_trace</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
            <td> Text representation of the stack trace.
</td>
            <td>No default</td>
        </tr>
</table>

### Analyzer_OnManagedRuntimeException_Response {:#Analyzer_OnManagedRuntimeException_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### UnknownException {:#UnknownException}
*Defined in [fuchsia.crash/analyzer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-crash/analyzer.fidl#40)*



 Represents a language-agnostic exception.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
            <td> A general buffer to hold some exception data.
</td>
            <td>No default</td>
        </tr>
</table>

### GenericException {:#GenericException}
*Defined in [fuchsia.crash/analyzer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-crash/analyzer.fidl#47)*



 Represents a generic exception that works for many managed runtime languages.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>type</code></td>
            <td>
                <code>uint8[128]</code>
            </td>
            <td> Exception type, e.g., "FileSystemException".
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>message</code></td>
            <td>
                <code>uint8[1024]</code>
            </td>
            <td> Exception message, e.g., "cannot open file".
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>stack_trace</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
            <td> Text representation of the stack trace.
</td>
            <td>No default</td>
        </tr>
</table>







## **UNIONS**

### Analyzer_OnManagedRuntimeException_Result {:#Analyzer_OnManagedRuntimeException_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Analyzer_OnManagedRuntimeException_Response'>Analyzer_OnManagedRuntimeException_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### ManagedRuntimeException {:#ManagedRuntimeException}
*Defined in [fuchsia.crash/analyzer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-crash/analyzer.fidl#33)*

 Represents a managed runtime exception.

 unknown is intended to capture any language, meaning the handling will be
 language-agnostic. Choose a more specific member if available for handling
 that language more specifically.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>unknown</code></td>
            <td>
                <code><a class='link' href='#UnknownException'>UnknownException</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>dart</code></td>
            <td>
                <code><a class='link' href='#GenericException'>GenericException</a></code>
            </td>
            <td></td>
        </tr></table>

### Analyzer_OnManagedRuntimeException_Result {:#Analyzer_OnManagedRuntimeException_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Analyzer_OnManagedRuntimeException_Response'>Analyzer_OnManagedRuntimeException_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### ManagedRuntimeException {:#ManagedRuntimeException}
*Defined in [fuchsia.crash/analyzer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-crash/analyzer.fidl#33)*

 Represents a managed runtime exception.

 unknown is intended to capture any language, meaning the handling will be
 language-agnostic. Choose a more specific member if available for handling
 that language more specifically.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>unknown</code></td>
            <td>
                <code><a class='link' href='#UnknownException'>UnknownException</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>dart</code></td>
            <td>
                <code><a class='link' href='#GenericException'>GenericException</a></code>
            </td>
            <td></td>
        </tr></table>







