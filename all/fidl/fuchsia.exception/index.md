Project: /_project.yaml
Book: /_book.yaml

# fuchsia.exception


## **PROTOCOLS**

## Handler {:#Handler}
*Defined in [fuchsia.exception/handler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-exception/handler.fidl#11)*

 Protocol meant for clients interested in handling exceptions for a
 particular service.

### OnException {:#OnException}

 This exception mirrors closely the information provided by exception
 channels. The design is to have clients of this API behave as closely as
 possible to native exception handlers that are listening to an exception
 channel.

 `exception` is an exception handle, which controls the exception's
 lifetime. See exception zircon docs for more information.

 `info` represents basic exception information as provided by the
 exception channel.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>exception</code></td>
            <td>
                <code>handle&lt;exception&gt;</code>
            </td>
        </tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#ExceptionInfo'>ExceptionInfo</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## **STRUCTS**

### ExceptionInfo {:#ExceptionInfo}
*Defined in [fuchsia.exception/handler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-exception/handler.fidl#30)*



 Basic exception information associated with a particular exception.
 Maps to `zx_exception_info_t`.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>process_koid</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>thread_koid</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#ExceptionType'>ExceptionType</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### ExceptionType {:#ExceptionType}
Type: <code>uint32</code>

*Defined in [fuchsia.exception/handler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-exception/handler.fidl#46)*

 What type of exception was triggered.
 Maps to the types defined in `zx_excp_type_t`.
 If zircon/syscalls/exception.h changes, this needs to be updates as well to
 reflect that.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>GENERAL</code></td>
            <td><code>8</code></td>
            <td></td>
        </tr><tr>
            <td><code>FATAL_PAGE_FAULT</code></td>
            <td><code>264</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNDEFINED_INSTRUCTION</code></td>
            <td><code>520</code></td>
            <td></td>
        </tr><tr>
            <td><code>SW_BREAKPOINT</code></td>
            <td><code>776</code></td>
            <td></td>
        </tr><tr>
            <td><code>HW_BREAKPOINT</code></td>
            <td><code>1032</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNALIGNED_ACCESS</code></td>
            <td><code>1288</code></td>
            <td></td>
        </tr><tr>
            <td><code>THREAD_STARTING</code></td>
            <td><code>32776</code></td>
            <td></td>
        </tr><tr>
            <td><code>THREAD_EXITING</code></td>
            <td><code>33032</code></td>
            <td></td>
        </tr><tr>
            <td><code>POLICY_ERROR</code></td>
            <td><code>33288</code></td>
            <td></td>
        </tr><tr>
            <td><code>PROCESS_STARTING</code></td>
            <td><code>33544</code></td>
            <td></td>
        </tr></table>











