[TOC]

# fuchsia.kernel


## **PROTOCOLS**

## Counter {#Counter}
*Defined in [fuchsia.kernel/kernel-counter.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-kernel/kernel-counter.fidl#12)*

<p>Protocol for retrieving kcounter information.</p>

### GetInspectVmo {#GetInspectVmo}

<p>Retrives a VMO containining summarized kcounter data. The vmo returned
in |buffer| is in &quot;inspect-vmo&quot; format, documented elsewhere.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
        </tr></table>

### UpdateInspectVmo {#UpdateInspectVmo}

<p>Request that the previously-returned VMO buffer's data be updated. The
data may not be updated if it was already recently updated (updates are
limited to an unspecified rate, but approximately every few seconds).</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

## DebugBroker {#DebugBroker}
*Defined in [fuchsia.kernel/kernel-debug.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-kernel/kernel-debug.fidl#14)*

<p>Acts on behalf of the caller to interact with privileged debug system calls.</p>

### SendDebugCommand {#SendDebugCommand}

<p>Pass debug command through to the kernel shell.
Look at zx_debug_send_command syscall handling to find valid values.</p>

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
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

### SetTracingEnabled {#SetTracingEnabled}

<p>Sets whether kernel tracing (ktrace) is enabled or disabled.</p>

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
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

## MexecBroker {#MexecBroker}
*Defined in [fuchsia.kernel/kernel-mexec.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-kernel/kernel-mexec.fidl#9)*

<p>Acts on behalf of the caller to interact with privileged mexec system call.</p>

### PerformMexec {#PerformMexec}

<p>Perform an mexec with the given kernel and bootdata.
See ZX-2069 for the thoughts on deprecating mexec.</p>

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



## Stats {#Stats}
*Defined in [fuchsia.kernel/kernel-stats.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-kernel/kernel-stats.fidl#57)*

<p>Protocol for providing kernel stats. This is roughly a wrapper around zx_object_get_info for
the ZX_INFO_KMEM_STATS and ZX_INFO_CPU_STATS topics, which today require the very powerful
'Root Resource' capability to obtain. Instead of vending out that capability, programs that
just want stats should use this service instead. If for some reason the protocol fails to
retrieve stats, which will be an un-recoverable error, it will close the channel.</p>

### GetMemoryStats {#GetMemoryStats}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>stats</code></td>
            <td>
                <code><a class='link' href='#MemoryStats'>MemoryStats</a></code>
            </td>
        </tr></table>

### GetCpuStats {#GetCpuStats}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>stats</code></td>
            <td>
                <code><a class='link' href='#CpuStats'>CpuStats</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### CpuStats {#CpuStats}
*Defined in [fuchsia.kernel/kernel-stats.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-kernel/kernel-stats.fidl#43)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>actual_num_cpus</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>per_cpu_stats</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#PerCpuStats'>PerCpuStats</a>&gt;[512]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>





## **TABLES**

### MemoryStats {#MemoryStats}


*Defined in [fuchsia.kernel/kernel-stats.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-kernel/kernel-stats.fidl#11)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>total_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>free_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>wired_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>total_heap_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>free_heap_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>6</td>
            <td><code>vmo_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>7</td>
            <td><code>mmu_overhead_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>8</td>
            <td><code>ipc_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>9</td>
            <td><code>other_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr></table>

### PerCpuStats {#PerCpuStats}


*Defined in [fuchsia.kernel/kernel-stats.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-kernel/kernel-stats.fidl#25)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>cpu_number</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>idle_time</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#duration'>duration</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>reschedules</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>context_switches</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>6</td>
            <td><code>irq_preempts</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>7</td>
            <td><code>yields</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>8</td>
            <td><code>ints</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>9</td>
            <td><code>timer_ints</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>10</td>
            <td><code>timers</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>11</td>
            <td><code>page_faults</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>12</td>
            <td><code>exceptions</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>13</td>
            <td><code>syscalls</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>14</td>
            <td><code>reschedule_ipis</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>15</td>
            <td><code>generic_ipis</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr></table>









## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="DEBUG_COMMAND_MAX">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-kernel/kernel-debug.fidl#10">DEBUG_COMMAND_MAX</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Maximum number of bytes in a command string</p>
</td>
        </tr>
    
</table>



