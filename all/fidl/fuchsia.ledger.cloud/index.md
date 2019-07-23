Project: /_project.yaml
Book: /_book.yaml

# fuchsia.ledger.cloud


## **PROTOCOLS**

## CloudProvider {:#CloudProvider}
*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#34)*

 Cloud service that powers cloud sync for a single user. Top-level interface
 of this file.

 Closing the client connection to CloudProvider shuts down all controllers
 (DeviceSets, PageClouds) that were produced by it.

### GetDeviceSet {:#GetDeviceSet}

 Retrieves the controller for the user device set.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_set</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.ledger.cloud/index.html#DeviceSet'>DeviceSet</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ledger.cloud/index.html#Status'>Status</a></code>
            </td>
        </tr></table>

### GetPageCloud {:#GetPageCloud}

 Retrieves the controller for cloud sync of a particular page.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>app_id</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr><tr>
            <td><code>page_id</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr><tr>
            <td><code>page_cloud</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.ledger.cloud/index.html#PageCloud'>PageCloud</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ledger.cloud/index.html#Status'>Status</a></code>
            </td>
        </tr></table>

## DeviceSet {:#DeviceSet}
*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#47)*

 Cloud registry of devices participating in cloud sync.

 Closing the client connection to DeviceSet disconnects all watchers set on
 it.

### CheckFingerprint {:#CheckFingerprint}

 Verifies that the device fingerprint in the cloud is still in the list of
 devices, ensuring that the cloud was not erased since the last sync.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>fingerprint</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ledger.cloud/index.html#Status'>Status</a></code>
            </td>
        </tr></table>

### SetFingerprint {:#SetFingerprint}

 Adds the device fingerprint to the list of devices in the cloud.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>fingerprint</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ledger.cloud/index.html#Status'>Status</a></code>
            </td>
        </tr></table>

### SetWatcher {:#SetWatcher}

 Watches the given `fingerprint` in the cloud so that `watcher` is notified
 when the fingerprint is erased.

 At most one watcher can be set at any given time. If more than one watcher
 is set, only the one set most recently receives notifications.

 The returned status is:

   - OK, if setting the watcher succeeded,
   - NOT_FOUND, if the fingerprint was not found in the cloud
   - NETWORK_ERROR, if the watcher couldn't be set due to a network error

 If the returned status is not OK, the corresponding error call is also made
 on the watcher.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>fingerprint</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr><tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ledger.cloud/index.html#DeviceSetWatcher'>DeviceSetWatcher</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ledger.cloud/index.html#Status'>Status</a></code>
            </td>
        </tr></table>

### Erase {:#Erase}

 Erases the entire registry of devices. This makes all devices detect that
 cloud has been erased.

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
                <code><a class='link' href='../fuchsia.ledger.cloud/index.html#Status'>Status</a></code>
            </td>
        </tr></table>

## DeviceSetWatcher {:#DeviceSetWatcher}
*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#79)*

 Watcher for push notifications from the cloud registry of devices
 participating in cloud sync.

### OnCloudErased {:#OnCloudErased}

 Called when cloud provider detects that the cloud storage was erased. No
 further calls are made on the watcher after this is called.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### OnError {:#OnError}

 Called when an error occured. Most common errors are:
   - NOT_FOUND, if the fingerprint was not found in the cloud when registering the watcher.
   - NETWORK_ERROR if the network connection is lost.

 No further calls are made on the watcher after this is called.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ledger.cloud/index.html#Status'>Status</a></code>
            </td>
        </tr></table>



## PageCloud {:#PageCloud}
*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#139)*

 Handler for cloud sync of a single page.

 Implementation of this class manages a *commit log*, which is an append-only
 list of commits produced by all devices that participate in syncing this
 page. Position of commits within the log are references using position
 tokens, allowing the caller to retrieve the commits added to the cloud since
 the previous read. (plus possibly more - see comments for GetCommits() and
 SetWatcher().)

 Closing the client connection to PageCloud disconnects all watchers set on
 it.

### AddCommits {:#AddCommits}

 Adds the given commits to the commit log in the cloud.

 The commits are added in one batch, on the receiving side they are
 delivered in the same order in a single OnNewCommits() call.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>commits</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ledger.cloud/index.html#CommitPack'>CommitPack</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ledger.cloud/index.html#Status'>Status</a></code>
            </td>
        </tr></table>

### GetCommits {:#GetCommits}

 Retrieves commits from the cloud.

 All commits newer than `min_position_token` are guaranteed to be returned.
 In addition to that, the response may include additional commits older
 than or at `min_position_token`. Passing null `min_position_token`
 retrieves all commits.

 If the resulting `status` is `OK`, `commits` contains all matching commits
 (might be empty) and `position_token` contains the position token of the
 most recent of the `commits` (equivalent to `min_position_token` if
 `commits` is empty).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>min_position_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ledger.cloud/index.html#PositionToken'>PositionToken</a>?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ledger.cloud/index.html#Status'>Status</a></code>
            </td>
        </tr><tr>
            <td><code>commits</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ledger.cloud/index.html#CommitPack'>CommitPack</a>?</code>
            </td>
        </tr><tr>
            <td><code>position_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ledger.cloud/index.html#PositionToken'>PositionToken</a>?</code>
            </td>
        </tr></table>

### AddObject {:#AddObject}

 Uploads the given object to the cloud under the given id.

 If the object already exists in the cloud this method returns OK.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
        </tr><tr>
            <td><code>references</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ledger.cloud/index.html#ReferencePack'>ReferencePack</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ledger.cloud/index.html#Status'>Status</a></code>
            </td>
        </tr></table>

### GetObject {:#GetObject}

 Retrieves the object of the given id from the cloud.

 If the resulting `status` is `OK`, `buffer` will contain the object
 content. If the resulting `status` is not `OK`, `buffer` will be null.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ledger.cloud/index.html#Status'>Status</a></code>
            </td>
        </tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a>?</code>
            </td>
        </tr></table>

### SetWatcher {:#SetWatcher}

 Watches the cloud for push notifications.

 At most one watcher can be set at any given time. If more than one watcher
 is set, only the one set most recently receives notifications.

 All commits newer than `min_position_token` added to the cloud before or
 after making this call are guaranteed to be delivered to `watcher`. In
 addition to that, additional commits older than or at `min_position_token`
 may be delivered to. If `min_position_token` is null, notifications for
 all commits are delivered.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>min_position_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ledger.cloud/index.html#PositionToken'>PositionToken</a>?</code>
            </td>
        </tr><tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ledger.cloud/index.html#PageCloudWatcher'>PageCloudWatcher</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ledger.cloud/index.html#Status'>Status</a></code>
            </td>
        </tr></table>

## PageCloudWatcher {:#PageCloudWatcher}
*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#188)*

 Watcher for push notifications from cloud sync of a single page.

### OnNewCommits {:#OnNewCommits}

 Called when new commits are added to the commit log in the cloud.

 The method takes the list of new `commits` along with the `position_token`
 of the most recent of them.

 No subsequent calls are made until the client calls the callback of the
 previous one.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>commits</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ledger.cloud/index.html#CommitPack'>CommitPack</a></code>
            </td>
        </tr><tr>
            <td><code>position_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ledger.cloud/index.html#PositionToken'>PositionToken</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### OnNewObject {:#OnNewObject}

 Called when a new object is added to the cloud.

 The method takes the `id` and the content of the new object.

 No subsequent calls are made until the client calls the callback of the
 previous one.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### OnError {:#OnError}

 Called when an error occurs.

 No further calls are made on the watcher after this is called. The client
 can then re-establish the watcher by calling SetWatcher() again.

 The status is one of:

   - AUTH_ERROR, if the auth token needs a refresh
   - NETWORK_ERROR, if the connection was dropped
   - PARSE_ERROR, if an invalid server notification was received

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ledger.cloud/index.html#Status'>Status</a></code>
            </td>
        </tr></table>





## **STRUCTS**

### CommitPack {:#CommitPack}
*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#93)*



 Contains a Buffer containing the FIDL serialization of Commits.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### PositionToken {:#PositionToken}
*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#99)*



 An opaque representation of a position in the stream of commits handled by
 a PageCloud instance.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>opaque_id</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Commits {:#Commits}
*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#112)*



 A list of commits for serialization in CommitPack.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>commits</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.ledger.cloud/index.html#Commit'>Commit</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### References {:#References}
*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#117)*



 A list of references for serialization in ReferencePack.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>references</code></td>
            <td>
                <code>vector&lt;vector&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ReferencePack {:#ReferencePack}
*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#124)*



 Contains a Buffer containing the FIDL serialization of References.

 If the Buffer is absent, the reference list is treated as empty.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### Status {:#Status}
Type: <code>int32</code>

*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#16)*

 Response status for cloud provider operations.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OK</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>AUTH_ERROR</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>ARGUMENT_ERROR</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>INTERNAL_ERROR</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>NETWORK_ERROR</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>NOT_FOUND</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>PARSE_ERROR</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>SERVER_ERROR</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNKNOWN_ERROR</code></td>
            <td><code>-1</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### Commit {:#Commit}


*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#104)*

 A commit as seen by the cloud.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>id</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
        </tr></table>









## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#13">NO_LINT</a></td>
            <td>
                    <code>4294967295</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    
</table>

