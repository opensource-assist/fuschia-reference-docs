[TOC]

# fuchsia.netemul.sync


## **PROTOCOLS**

## Bus {#Bus}
*Defined in [fuchsia.netemul.sync/sync.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/sync.fidl#17)*

<p>Represents a named bus:
a bus is a broadcast pub/sub network that distributes Events.
Events are not stored, only forwarded to attached clients.</p>

### Publish {#Publish}

<p>Publishes event on the bus.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='#Event'>Event</a></code>
            </td>
        </tr></table>



### EnsurePublish {#EnsurePublish}

<p>Publishes data on bus and only returns when data has been dispatched.
Use this if you need guarantees that the data was broadcast before continuing.
Note that this ensures that the data will be <em>published</em> to all listening clients,
but it cannot guarantee that all clients will have observed the event before it returns.</p>

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

### OnBusData {#OnBusData}

<p>Notifies client of new event.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='#Event'>Event</a></code>
            </td>
        </tr></table>

### GetClients {#GetClients}

<p>Get list of named clients.</p>

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

### OnClientAttached {#OnClientAttached}

<p>Notifies a client is now attached.
Upon subscribing to a bus, a client will always receive an <code>OnClientAttached</code> event for each
client present on the bus at the moment it joined.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>client</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

### OnClientDetached {#OnClientDetached}

<p>Notifies a client was detached.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>client</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

### WaitForClients {#WaitForClients}

<p>Waits for up to <code>timeout</code> (nsec) for all the clients in <code>clients</code>.
Returns true if all clients are present on the bus before timeout expired.
If <code>result</code> is false, <code>absent</code> will contain the entries in <code>clients</code> that still weren't
present on the bus when the timout expired.
Use <code>timeout</code> &lt;= 0 for indefinite wait.</p>

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
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#duration'>duration</a></code>
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

### WaitForEvent {#WaitForEvent}

<p>Waits for up to <code>timeout</code> (nsec) for an event that matches <code>data</code>.
Event equality is performed by comparing <em>all</em> set fields in <code>data</code>.
Returns true if event was received before timeout expired.
Use <code>timeout</code> &lt;= 0 for indefinite wait.</p>

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
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#duration'>duration</a></code>
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

## SyncManager {#SyncManager}
*Defined in [fuchsia.netemul.sync/sync.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/sync.fidl#52)*

<p>The SyncManager is the entry point to attach a client to a bus or use other synchronization
primitives.
The client's 'ticket' to remain on the bus is the channel obtained through the 'BusSubscribe' call.</p>

### BusSubscribe {#BusSubscribe}

<p>Subscribes to bus 'busName' with a given client name.
Duplicate client names are disallowed and will cause the request to return unfulfilled.</p>

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



### WaitForBarrierThreshold {#WaitForBarrierThreshold}

<p>Waits on a named counter barrier with name <code>barrierName</code>.
Functon will return true if the number of waits pending on the barrier matches or exceeds
<code>threshold</code> before  <code>timeout</code> (nsec) expires.
Use <code>timeout</code> &lt;= 0 for indefinite wait.</p>

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
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#duration'>duration</a></code>
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

### Event {#Event}


*Defined in [fuchsia.netemul.sync/sync.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/sync.fidl#5)*

<p>Simple data structure passed on netemul bus.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>code</code></td>
            <td>
                <code>int32</code>
            </td>
            <td><p>User-defined event code.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>message</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>string message.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>arguments</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td><p>serialized arguments.</p>
</td>
        </tr></table>











