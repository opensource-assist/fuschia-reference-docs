[TOC]

# fuchsia.storage.metrics




## **STRUCTS**

### CallStatRaw {#CallStatRaw}
*Defined in [fuchsia.storage.metrics/storage-metrics.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-storage-metrics/storage-metrics.fidl#10)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>minimum_latency</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>maximum_latency</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>total_time_spent</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>total_calls</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bytes_transferred</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### CallStat {#CallStat}
*Defined in [fuchsia.storage.metrics/storage-metrics.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-storage-metrics/storage-metrics.fidl#40)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>success</code></td>
            <td>
                <code><a class='link' href='#CallStatRaw'>CallStatRaw</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>failure</code></td>
            <td>
                <code><a class='link' href='#CallStatRaw'>CallStatRaw</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FsMetrics {#FsMetrics}
*Defined in [fuchsia.storage.metrics/storage-metrics.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-storage-metrics/storage-metrics.fidl#50)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>create</code></td>
            <td>
                <code><a class='link' href='#CallStat'>CallStat</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>read</code></td>
            <td>
                <code><a class='link' href='#CallStat'>CallStat</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>write</code></td>
            <td>
                <code><a class='link' href='#CallStat'>CallStat</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>truncate</code></td>
            <td>
                <code><a class='link' href='#CallStat'>CallStat</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>unlink</code></td>
            <td>
                <code><a class='link' href='#CallStat'>CallStat</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>rename</code></td>
            <td>
                <code><a class='link' href='#CallStat'>CallStat</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>lookup</code></td>
            <td>
                <code><a class='link' href='#CallStat'>CallStat</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>open</code></td>
            <td>
                <code><a class='link' href='#CallStat'>CallStat</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>













