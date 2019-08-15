Project: /_project.yaml
Book: /_book.yaml

# fuchsia.netemul.sync


## **PROTOCOLS**

## Bus {:#Bus}
*Defined in [fuchsia.netemul.sync/sync.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/sync.fidl#17)*

 Represents a named bus:
    a bus is a broadcast pub/sub network that distributes Events.
    Events are not stored, only forwarded to attached clients.

### Publish {:#Publish}

 Publishes event on the bus.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='#Event'>Event</a></code>
            </td>
        </tr></table>



### EnsurePublish {:#EnsurePublish}

 Publishes data on bus and only returns when data has been dispatched.
 Use this if you need guarantees that the data was broadcast before continuing.
 Note that this ensures that the data will be *published* to all listening clients,
 but it cannot guarantee that all clients will have observed the event before it returns.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='#Event'>Event</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### OnBusData {:#OnBusData}

 Notifies client of new event.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='#Event'>Event</a></code>
            </td>
        </tr></table>

### GetClients {:#GetClients}

 Get list of named clients.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>clients</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr></table>

### OnClientAttached {:#OnClientAttached}

 Notifies a client is now attached.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>client</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

### OnClientDetached {:#OnClientDetached}

 Notifies a client was detached.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>client</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

### WaitForClients {:#WaitForClients}

 Waits for up to `timeout` (nsec) for all the clients in `clients`.
 Returns true if all clients are present on the bus before timeout expired.
 If `result` is false, `absent` will contain the entries in `clients` that still weren't
 present on the bus when the timout expired.
 Use `timeout` <= 0 for indefinite wait.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>clients</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr><tr>
            <td><code>timeout</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>absent</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
        </tr></table>

### WaitForEvent {:#WaitForEvent}

 Waits for up to `timeout` (nsec) for an event that matches `data`.
 Event equality is performed by comparing *all* set fields in `data`.
 Returns true if event was received before timeout expired.
 Use `timeout` <= 0 for indefinite wait.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='#Event'>Event</a></code>
            </td>
        </tr><tr>
            <td><code>timeout</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

## SyncManager {:#SyncManager}
*Defined in [fuchsia.netemul.sync/sync.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/sync.fidl#50)*

 The SyncManager is the entry point to attach a client to a bus or use other synchronization
 primitives.
 The client's 'ticket' to remain on the bus is the channel obtained through the 'BusSubscribe' call.

### BusSubscribe {:#BusSubscribe}

 Subscribes to bus 'busName' with a given client name.
 Duplicate client names are disallowed and will cause the request to return unfulfilled.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>busName</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>clientName</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>bus</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Bus'>Bus</a>&gt;</code>
            </td>
        </tr></table>



### WaitForBarrierThreshold {:#WaitForBarrierThreshold}

 Waits on a named counter barrier with name `barrierName`.
 Functon will return true if the number of waits pending on the barrier matches or exceeds
 `threshold` before  `timeout` (nsec) expires.
 Use `timeout` <= 0 for indefinite wait.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>barrierName</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>threshold</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>timeout</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>







## **TABLES**

### Event {:#Event}


*Defined in [fuchsia.netemul.sync/sync.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/sync.fidl#5)*

 Simple data structure passed on netemul bus.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>code</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> User-defined event code.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>message</code></td>
            <td>
                <code>string</code>
            </td>
            <td> string message.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>arguments</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td> serialized arguments.
</td>
        </tr></table>









