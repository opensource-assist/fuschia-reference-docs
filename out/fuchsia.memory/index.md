Project: /_project.yaml
Book: /_book.yaml

# fuchsia.memory


## **PROTOCOLS**

## Monitor {:#Monitor}
*Defined in [fuchsia.memory/monitor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.memory/monitor.fidl#8)*

 Interface used to register for memory notifications.

### Watch {:#Watch}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='../fuchsia.memory/index.html#Watcher'>Watcher</a></code>
            </td>
        </tr></table>



## Watcher {:#Watcher}
*Defined in [fuchsia.memory/monitor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.memory/monitor.fidl#47)*

 A watcher for memory changes

### OnChange {:#OnChange}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>stats</code></td>
            <td>
                <code><a class='link' href='../fuchsia.memory/index.html#Stats'>Stats</a></code>
            </td>
        </tr></table>





## **STRUCTS**

### Stats {:#Stats}
*Defined in [fuchsia.memory/monitor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.memory/monitor.fidl#12)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>total_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The total amount of physical memory available to the system.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>free_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The amount of unallocated memory.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>wired_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The amount of memory reserved by and mapped into the kernel for reasons
 not covered by other fields in this struct. Typically for readonly data
 like the ram disk and kernel image, and for early-boot dynamic memory.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>total_heap_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The amount of memory allocated to the kernel heap.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>free_heap_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The portion of `total_heap_bytes` that is not in use.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>vmo_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The amount of memory committed to VMOs, both kernel and user.
 A superset of all userspace memory.
 Does not include certain VMOs that fall under `wired_bytes`.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>mmu_overhead_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The amount of memory used for architecture-specific MMU metadata
 like page tables.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>ipc_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The amount of memory in use by IPC.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>other_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Non-free memory that isn't accounted for in any other field.
</td>
            <td>No default</td>
        </tr>
</table>













