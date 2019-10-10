Project: /_project.yaml
Book: /_book.yaml

# fuchsia.exception


## **PROTOCOLS**

## Handler {:#Handler}
*Defined in [fuchsia.exception/handler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-exception/handler.fidl#12)*

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

## ProcessLimbo {:#ProcessLimbo}
*Defined in [fuchsia.exception/process_limbo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-exception/process_limbo.fidl#17)*

 Protocol meant for clients interested in obtaining processes that are
 suspended waiting for an exception handler (in limbo). This is the core
 feature that enables Just In Time (JIT) debugging.

### ListProcessesWaitingOnException {:#ListProcessesWaitingOnException}

 Returns information on all the processes currently waiting on an exception.
 The information provided is intended to correctly identify an exception
 and determine whether the caller wants to actually handle it.
 To retrieve an exception, use the |GetException| call.

 NOTE: The |process| and |thread| handle will only have the ZX_RIGHT_READ
       right, so no modification will be able to be done on them.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>exception_list</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ProcessExceptionMetadata'>ProcessExceptionMetadata</a>&gt;[32]</code>
            </td>
        </tr></table>

### RetrieveException {:#RetrieveException}

 Removes the process from limbo and retrieves the exception handle and
 associated metadata from an exception.

 Use |ListProcessesWaitingOnException| to choose a |process_koid| from the
 list of available exceptions.

 Returns ZX_ERR_NOT_FOUND if the process is not waiting on an exception.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>process_koid</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#ProcessLimbo_RetrieveException_Result'>ProcessLimbo_RetrieveException_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### ExceptionInfo {:#ExceptionInfo}
*Defined in [fuchsia.exception/handler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-exception/handler.fidl#31)*



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

### ProcessLimbo_RetrieveException_Response {:#ProcessLimbo_RetrieveException_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>process_exception</code></td>
            <td>
                <code><a class='link' href='#ProcessException'>ProcessException</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### ExceptionType {:#ExceptionType}
Type: <code>uint32</code>

*Defined in [fuchsia.exception/handler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-exception/handler.fidl#62)*

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



## **TABLES**

### ProcessException {:#ProcessException}


*Defined in [fuchsia.exception/handler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-exception/handler.fidl#43)*

 Generic wrapper over a thread exception. Mirrors closely the information
 given by an exception channel.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>exception</code></td>
            <td>
                <code>handle&lt;exception&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#ExceptionInfo'>ExceptionInfo</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>process</code></td>
            <td>
                <code>handle&lt;process&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>thread</code></td>
            <td>
                <code>handle&lt;thread&gt;</code>
            </td>
            <td></td>
        </tr></table>

### ProcessExceptionMetadata {:#ProcessExceptionMetadata}


*Defined in [fuchsia.exception/process_limbo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-exception/process_limbo.fidl#42)*

 Intended to be read only metadada associated with an exception waiting in
 limbo. The handles provided will only have read-only access to the resource,
 so no modification can be done to them.

 NOTE: Both |process| and |thread| will be valid if present.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#ExceptionInfo'>ExceptionInfo</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>process</code></td>
            <td>
                <code>handle&lt;process&gt;</code>
            </td>
            <td> Only has ZX_RIGHT_READ and ZX_RIGHT_GET_PROPERTY rights.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>thread</code></td>
            <td>
                <code>handle&lt;thread&gt;</code>
            </td>
            <td> The thread that generated the exception.
 The process may have other threads that are not reflected here.
 Only has ZX_RIGHT_READ and ZX_RIGHT_GET_PROPERTY rights.
</td>
        </tr></table>



## **UNIONS**

### ProcessLimbo_RetrieveException_Result {:#ProcessLimbo_RetrieveException_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#ProcessLimbo_RetrieveException_Response'>ProcessLimbo_RetrieveException_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-exception/process_limbo.fidl#11">MAX_EXCEPTIONS_PER_CALL</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint64</code></td>
            <td> The maximum amount of exceptions that will be listed at any given time by a
 call to |ListProcessesWaitingOnException|.
</td>
        </tr>
    
</table>

