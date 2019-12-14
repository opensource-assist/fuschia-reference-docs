[TOC]

# fuchsia.time


## **PROTOCOLS**

## DeprecatedNetworkSync {#DeprecatedNetworkSync}
*Defined in [fuchsia.time/deprecated_network_sync.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/timekeeper/deprecated_network_sync.fidl#12)*

<p>Emits <code>UtcUpdated</code> events when the serving program changes the UTC offset tracked by
<code>ZX_CLOCK_UTC</code>.</p>
<p>Do not take this API as a dependency, it will be deleted in the near future.</p>

### UtcUpdated {#UtcUpdated}

<p>Notifies the client that UTC has changed, along with the monotonic clock's value when the
change was made.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>update_time</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#time'>time</a></code>
            </td>
        </tr></table>

## Utc {#Utc}
*Defined in [fuchsia.time/utc.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/timekeeper/utc.fidl#10)*

<p>Metadata about a device's approximation of UTC time, commonly referred to as &quot;system time.&quot;</p>

### WatchState {#WatchState}

<p>Notifies clients of updates to the UTC timeline. The first call on a channel returns
immediately, and subsequent calls on the same channel will return when the state
has changed.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#UtcState'>UtcState</a></code>
            </td>
        </tr></table>





## **ENUMS**

### UtcSource {#UtcSource}
Type: <code>uint32</code>

*Defined in [fuchsia.time/utc.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/timekeeper/utc.fidl#26)*

<p>Describes the source from which the current UTC approximation was retrieved.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>BACKSTOP</code></td>
            <td><code>2</code></td>
            <td><p>The clock has been initialized to a known-prior reference time but may be highly inaccurate.</p>
</td>
        </tr><tr>
            <td><code>EXTERNAL</code></td>
            <td><code>3</code></td>
            <td><p>The clock has been initialized from a suitably accurate external time source. For many
devices the most common external time source is a network time server.</p>
</td>
        </tr></table>



## **TABLES**

### UtcState {#UtcState}


*Defined in [fuchsia.time/utc.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/timekeeper/utc.fidl#18)*

<p>Describes the state of the clock.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>timestamp</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#time'>time</a></code>
            </td>
            <td><p>The monotonic time at which this <code>UtcState</code> was observed.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#UtcSource'>UtcSource</a></code>
            </td>
            <td><p>The source of our current UTC approximation.</p>
</td>
        </tr></table>











