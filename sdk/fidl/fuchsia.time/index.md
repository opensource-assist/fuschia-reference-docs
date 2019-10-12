Project: /_project.yaml
Book: /_book.yaml

# fuchsia.time


## **PROTOCOLS**

## DeprecatedNetworkSync {:#DeprecatedNetworkSync}
*Defined in [fuchsia.time/deprecated_network_sync.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/timekeeper/deprecated_network_sync.fidl#12)*

 Emits `UtcUpdated` events when the serving program changes the UTC offset tracked by
 `ZX_CLOCK_UTC`.

 Do not take this API as a dependency, it will be deleted in the near future.

### UtcUpdated {:#UtcUpdated}

 Notifies the client that UTC has changed, along with the monotonic clock's value when the
 change was made.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>update_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>

## Utc {:#Utc}
*Defined in [fuchsia.time/utc.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/timekeeper/utc.fidl#10)*

 Metadata about a device's approximation of UTC time, commonly referred to as "system time."

### WatchState {:#WatchState}

 Notifies clients of updates to the UTC timeline. The first call on a channel returns
 immediately, and subsequent calls on the same channel will return when the state
 has changed.

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

### UtcSource {:#UtcSource}
Type: <code>uint32</code>

*Defined in [fuchsia.time/utc.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/timekeeper/utc.fidl#26)*

 Describes the source from which the current UTC approximation was retrieved.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>BACKSTOP</code></td>
            <td><code>2</code></td>
            <td> The clock has been initialized to a known-prior reference time but may be highly inaccurate.
</td>
        </tr><tr>
            <td><code>EXTERNAL</code></td>
            <td><code>3</code></td>
            <td> The clock has been initialized from a suitably accurate external time source. For many
 devices the most common external time source is a network time server.
</td>
        </tr></table>



## **TABLES**

### UtcState {:#UtcState}


*Defined in [fuchsia.time/utc.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/timekeeper/utc.fidl#18)*

 Describes the state of the clock.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>timestamp</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> The monotonic time at which this `UtcState` was observed.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#UtcSource'>UtcSource</a></code>
            </td>
            <td> The source of our current UTC approximation.
</td>
        </tr></table>









