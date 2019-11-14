[TOC]

# fuchsia.diagnostics.streaming




## **STRUCTS**

### Record {#Record}
*Defined in [fuchsia.diagnostics.streaming/record.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/streams/record.fidl#22)*



<p>A record in the diagnostic stream.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>timestamp</code></td>
            <td>
                <code>int64</code>
            </td>
            <td><p>The monotonic time at which the record was generated.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>arguments</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Argument'>Argument</a>&gt;[15]</code>
            </td>
            <td><p>The key-value pairs which make up this record.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### Argument {#Argument}
*Defined in [fuchsia.diagnostics.streaming/record.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/streams/record.fidl#31)*



<p>A named key-value pair in the diagnostic record.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[256]</code>
            </td>
            <td><p>The name of the argument.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#Value'>Value</a></code>
            </td>
            <td><p>The value of the argument.</p>
</td>
            <td>No default</td>
        </tr>
</table>









## **XUNIONS**

### Value {#Value}
*Defined in [fuchsia.diagnostics.streaming/record.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/streams/record.fidl#40)*

<p>An argument value which can be one of several types.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>signed</code></td>
            <td>
                <code>int64</code>
            </td>
            <td><p>A signed integral argument.</p>
</td>
        </tr><tr>
            <td><code>unsigned</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>An unsigned integral argument.</p>
</td>
        </tr><tr>
            <td><code>floating</code></td>
            <td>
                <code>float64</code>
            </td>
            <td><p>A double-precision floating-point argument.</p>
</td>
        </tr><tr>
            <td><code>text</code></td>
            <td>
                <code>string[32768]</code>
            </td>
            <td><p>A UTF8 text argument.</p>
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
            <td><p>Maximum number of arguments that can be encoded per record, as specified by the tracing format:</p>
<p>https://fuchsia.dev/fuchsia-src/development/tracing/trace-format#arguments</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/streams/record.fidl#15">MAX_ARG_NAME_LENGTH</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>A small(ish) limit on the length of argument names is used because argument names are expected
to be used repeatedly, many times.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/src/diagnostics/streams/record.fidl#18">MAX_TEXT_ARG_LENGTH</a></td>
            <td>
                    <code>32768</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum string length which we can encode into the tracing format.</p>
</td>
        </tr>
    
</table>

