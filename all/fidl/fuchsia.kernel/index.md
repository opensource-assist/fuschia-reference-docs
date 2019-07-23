Project: /_project.yaml
Book: /_book.yaml

# fuchsia.kernel


## **PROTOCOLS**

## DebugBroker {:#DebugBroker}
*Defined in [fuchsia.kernel/kernel-debug.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-kernel/kernel-debug.fidl#14)*

 Acts on behalf of the caller to interact with privileged debug system calls.

### SendDebugCommand {:#SendDebugCommand}

 Pass debug command through to the kernel shell.
 Look at zx_debug_send_command syscall handling to find valid values.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>command</code></td>
            <td>
                <code>string[1024]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### SetTracingEnabled {:#SetTracingEnabled}

 Sets whether kernel tracing (ktrace) is enabled or disabled.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>enabled</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

## MexecBroker {:#MexecBroker}
*Defined in [fuchsia.kernel/kernel-mexec.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-kernel/kernel-mexec.fidl#9)*

 Acts on behalf of the caller to interact with privileged mexec system call.

### PerformMexec {:#PerformMexec}

 Perform an mexec with the given kernel and bootdata.
 See ZX-2069 for the thoughts on deprecating mexec.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>kernel</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr><tr>
            <td><code>bootdata</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr></table>

















## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-kernel/kernel-debug.fidl#10">DEBUG_COMMAND_MAX</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    
</table>

