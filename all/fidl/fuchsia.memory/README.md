[TOC]

# fuchsia.memory


## **PROTOCOLS**

## Monitor {#Monitor}
*Defined in [fuchsia.memory/monitor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.memory/monitor.fidl#8)*

<p>Interface used to register for memory notifications.</p>

### Watch {#Watch}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#Watcher'>Watcher</a></code>
            </td>
        </tr></table>



## Watcher {#Watcher}
*Defined in [fuchsia.memory/monitor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.memory/monitor.fidl#47)*

<p>A watcher for memory changes</p>

### OnChange {#OnChange}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>stats</code></td>
            <td>
                <code><a class='link' href='#Stats'>Stats</a></code>
            </td>
        </tr></table>





## **STRUCTS**

### Stats {#Stats}
*Defined in [fuchsia.memory/monitor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.memory/monitor.fidl#12)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>total_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The total amount of physical memory available to the system.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>free_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The amount of unallocated memory.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>wired_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The amount of memory reserved by and mapped into the kernel for reasons
not covered by other fields in this struct. Typically for readonly data
like the ram disk and kernel image, and for early-boot dynamic memory.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>total_heap_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The amount of memory allocated to the kernel heap.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>free_heap_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The portion of <code>total_heap_bytes</code> that is not in use.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>vmo_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The amount of memory committed to VMOs, both kernel and user.
A superset of all userspace memory.
Does not include certain VMOs that fall under <code>wired_bytes</code>.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>mmu_overhead_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The amount of memory used for architecture-specific MMU metadata
like page tables.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>ipc_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The amount of memory in use by IPC.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>other_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Non-free memory that isn't accounted for in any other field.</p>
</td>
            <td>No default</td>
        </tr>
</table>













