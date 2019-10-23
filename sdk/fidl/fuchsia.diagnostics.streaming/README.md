[TOC]

# fuchsia.diagnostics.streaming




## **STRUCTS**

### Record {#Record}
*Defined in [fuchsia.diagnostics.streaming/record.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/streams/record.fidl#22)*



 A record in the diagnostic stream.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>timestamp</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> The monotonic time at which the record was generated.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>arguments</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Argument'>Argument</a>&gt;[15]</code>
            </td>
            <td> The key-value pairs which make up this record.
</td>
            <td>No default</td>
        </tr>
</table>

### Argument {#Argument}
*Defined in [fuchsia.diagnostics.streaming/record.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/streams/record.fidl#31)*



 A named key-value pair in the diagnostic record.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[256]</code>
            </td>
            <td> The name of the argument.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#Value'>Value</a></code>
            </td>
            <td> The value of the argument.
</td>
            <td>No default</td>
        </tr>
</table>









## **XUNIONS**

### Value {#Value}
*Defined in [fuchsia.diagnostics.streaming/record.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/streams/record.fidl#40)*

 An argument value which can be one of several types.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>signed</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> A signed integral argument.
</td>
        </tr><tr>
            <td><code>unsigned</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> An unsigned integral argument.
</td>
        </tr><tr>
            <td><code>floating</code></td>
            <td>
                <code>float64</code>
            </td>
            <td> A double-precision floating-point argument.
</td>
        </tr><tr>
            <td><code>text</code></td>
            <td>
                <code>string[32768]</code>
            </td>
            <td> A UTF8 text argument.
</td>
        </tr></table>





## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/streams/record.fidl#11">MAX_ARGS</a></td>
            <td>
                    <code>15</code>
                </td>
                <td><code>uint32</code></td>
            <td> Maximum number of arguments that can be encoded per record, as specified by the tracing format:

 https://fuchsia.dev/fuchsia-src/development/tracing/trace-format#arguments
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/streams/record.fidl#15">MAX_ARG_NAME_LENGTH</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint32</code></td>
            <td> A small(ish) limit on the length of argument names is used because argument names are expected
 to be used repeatedly, many times.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/streams/record.fidl#18">MAX_TEXT_ARG_LENGTH</a></td>
            <td>
                    <code>32768</code>
                </td>
                <td><code>uint32</code></td>
            <td> The maximum string length which we can encode into the tracing format.
</td>
        </tr>
    
</table>

