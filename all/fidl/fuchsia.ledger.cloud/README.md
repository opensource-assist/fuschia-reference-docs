[TOC]

# fuchsia.ledger.cloud


## **PROTOCOLS**

## CloudProvider {#CloudProvider}
*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#44)*

<p>Cloud service that powers cloud sync for a single user. Top-level interface
of this file.</p>
<p>Closing the client connection to CloudProvider shuts down all controllers
(DeviceSets, PageClouds) that were produced by it.</p>

### GetDeviceSet {#GetDeviceSet}

<p>Retrieves the controller for the user device set.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_set</code></td>
            <td>
                <code>request&lt;<a class='link' href='#DeviceSet'>DeviceSet</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>

### GetPageCloud {#GetPageCloud}

<p>Retrieves the controller for cloud sync of a particular page.</p>

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
                <code>request&lt;<a class='link' href='#PageCloud'>PageCloud</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>

## DeviceSet {#DeviceSet}
*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#57)*

<p>Cloud registry of devices participating in cloud sync.</p>
<p>Closing the client connection to DeviceSet disconnects all watchers set on
it.</p>

### CheckFingerprint {#CheckFingerprint}

<p>Verifies that the device fingerprint in the cloud is still in the list of
devices, ensuring that the cloud was not erased since the last sync.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>fingerprint</code></td>
            <td>
                <code>vector&lt;uint8&gt;[32]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>

### SetFingerprint {#SetFingerprint}

<p>Adds the device fingerprint to the list of devices in the cloud.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>fingerprint</code></td>
            <td>
                <code>vector&lt;uint8&gt;[32]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>

### SetWatcher {#SetWatcher}

<p>Watches the given <code>fingerprint</code> in the cloud so that <code>watcher</code> is notified
when the fingerprint is erased.</p>
<p>At most one watcher can be set at any given time. If more than one watcher
is set, only the one set most recently receives notifications.</p>
<p>The returned status is:</p>
<ul>
<li>OK, if setting the watcher succeeded,</li>
<li><code>NOT_FOUND</code>, if the fingerprint was not found in the cloud</li>
<li><code>NETWORK_ERROR</code>, if the watcher couldn't be set due to a network error</li>
</ul>
<p>If the returned status is not OK, the corresponding error call is also made
on the watcher.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>fingerprint</code></td>
            <td>
                <code>vector&lt;uint8&gt;[32]</code>
            </td>
        </tr><tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#DeviceSetWatcher'>DeviceSetWatcher</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>

### Erase {#Erase}

<p>Erases the entire registry of devices. This makes all devices detect that
cloud has been erased.</p>

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
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>

## DeviceSetWatcher {#DeviceSetWatcher}
*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#89)*

<p>Watcher for push notifications from the cloud registry of devices
participating in cloud sync.</p>

### OnCloudErased {#OnCloudErased}

<p>Called when cloud provider detects that the cloud storage was erased. No
further calls are made on the watcher after this is called.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### OnError {#OnError}

<p>Called when an error occured. Most common errors are:</p>
<ul>
<li><code>NOT_FOUND</code>, if the fingerprint was not found in the cloud when registering the watcher.</li>
<li><code>NETWORK_ERROR</code> if the network connection is lost.</li>
</ul>
<p>No further calls are made on the watcher after this is called.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>



## PageCloud {#PageCloud}
*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#222)*

<p>Handler for cloud sync of a single page.</p>
<p>Implementation of this class manages a <em>commit log</em>, which is an append-only
list of commits produced by all devices that participate in syncing this
page. Position of commits within the log are references using position
tokens, allowing the caller to retrieve the commits added to the cloud since
the previous read. (plus possibly more - see comments for GetCommits() and
SetWatcher().)</p>
<p>Closing the client connection to PageCloud disconnects all watchers set on
it.</p>

### AddCommits {#AddCommits}

<p>Adds the given commits to the commit log in the cloud.</p>
<p>The commits are added in one batch, on the receiving side they are
delivered in the same order in a single OnNewCommits() call.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>commits</code></td>
            <td>
                <code><a class='link' href='#CommitPack'>CommitPack</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>

### GetCommits {#GetCommits}

<p>Retrieves commits from the cloud.</p>
<p>All commits newer than <code>min_position_token</code> are guaranteed to be returned.
In addition to that, the response may include additional commits older
than or at <code>min_position_token</code>. Passing null <code>min_position_token</code>
retrieves all commits.</p>
<p>If the resulting <code>status</code> is <code>OK</code>, <code>commits</code> contains all matching commits
(might be empty) and <code>position_token</code> contains the position token of the
most recent of the <code>commits</code> (equivalent to <code>min_position_token</code> if
<code>commits</code> is empty).</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>min_position_token</code></td>
            <td>
                <code><a class='link' href='#PositionToken'>PositionToken</a>?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr><tr>
            <td><code>commits</code></td>
            <td>
                <code><a class='link' href='#CommitPack'>CommitPack</a>?</code>
            </td>
        </tr><tr>
            <td><code>position_token</code></td>
            <td>
                <code><a class='link' href='#PositionToken'>PositionToken</a>?</code>
            </td>
        </tr></table>

### AddObject {#AddObject}

<p>Uploads the given object to the cloud under the given id.</p>
<p>If the object already exists in the cloud this method returns OK.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>vector&lt;uint8&gt;[128]</code>
            </td>
        </tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
        </tr><tr>
            <td><code>references</code></td>
            <td>
                <code><a class='link' href='#ReferencePack'>ReferencePack</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>

### GetObject {#GetObject}

<p>Retrieves the object of the given id from the cloud.</p>
<p>If the resulting <code>status</code> is <code>OK</code>, <code>buffer</code> will contain the object
content. If the resulting <code>status</code> is not <code>OK</code>, <code>buffer</code> will be null.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>vector&lt;uint8&gt;[128]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a>?</code>
            </td>
        </tr></table>

### SetWatcher {#SetWatcher}

<p>Watches the cloud for push notifications.</p>
<p>At most one watcher can be set at any given time. If more than one watcher
is set, only the one set most recently receives notifications.</p>
<p>All commits newer than <code>min_position_token</code> added to the cloud before or
after making this call are guaranteed to be delivered to <code>watcher</code>. In
addition to that, additional commits older than or at <code>min_position_token</code>
may be delivered to. If <code>min_position_token</code> is null, notifications for
all commits are delivered.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>min_position_token</code></td>
            <td>
                <code><a class='link' href='#PositionToken'>PositionToken</a>?</code>
            </td>
        </tr><tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#PageCloudWatcher'>PageCloudWatcher</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>

### GetDiff {#GetDiff}

<p>Fetches a diff for the commit with the given |commit_id|.</p>
<p>The base of the diff is either the empty page or a commit in
<code>possible_bases</code>. The bases may be unknown to the cloud if they have
been pruned from the cloud, but not from the Ledger. During the
migration to diffs, the cloud provider may also choose as a base any
commit that has been uploaded without diff. In that case, the tree at
this commit should be downloaded using GetObject.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>commit_id</code></td>
            <td>
                <code>vector&lt;uint8&gt;[128]</code>
            </td>
        </tr><tr>
            <td><code>possible_bases</code></td>
            <td>
                <code>vector&lt;vector&gt;[32]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr><tr>
            <td><code>diff</code></td>
            <td>
                <code><a class='link' href='#DiffPack'>DiffPack</a>?</code>
            </td>
        </tr></table>

## PageCloudWatcher {#PageCloudWatcher}
*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#283)*

<p>Watcher for push notifications from cloud sync of a single page.</p>

### OnNewCommits {#OnNewCommits}

<p>Called when new commits are added to the commit log in the cloud.</p>
<p>The method takes the list of new <code>commits</code> along with the <code>position_token</code>
of the most recent of them.</p>
<p>No subsequent calls are made until Ledger calls the callback of the
previous one.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>commits</code></td>
            <td>
                <code><a class='link' href='#CommitPack'>CommitPack</a></code>
            </td>
        </tr><tr>
            <td><code>position_token</code></td>
            <td>
                <code><a class='link' href='#PositionToken'>PositionToken</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### OnNewObject {#OnNewObject}

<p>Called when a new object is added to the cloud.</p>
<p>The method takes the <code>id</code> and the content of the new object.</p>
<p>No subsequent calls are made until Ledger calls the callback of the
previous one.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>vector&lt;uint8&gt;[128]</code>
            </td>
        </tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### OnError {#OnError}

<p>Called when an error occurs.</p>
<p>No further calls are made on the watcher after this is called. Ledger
can then re-establish the watcher by calling SetWatcher() again.</p>
<p>The status is one of:</p>
<ul>
<li><code>AUTH_ERROR</code>, if the auth token needs a refresh</li>
<li><code>NETWORK_ERROR</code>, if the connection was dropped</li>
<li><code>PARSE_ERROR</code>, if an invalid server notification was received</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>





## **STRUCTS**

### CommitPack {#CommitPack}
*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#103)*



<p>Contains a Buffer containing the FIDL serialization of Commits.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### PositionToken {#PositionToken}
*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#109)*



<p>An opaque representation of a position in the stream of commits handled by
a PageCloud instance.</p>


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

### EmptyPage {#EmptyPage}
*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#144)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Commits {#Commits}
*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#190)*



<p>A list of commits for serialization in CommitPack.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>commits</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Commit'>Commit</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### References {#References}
*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#195)*



<p>A list of references for serialization in ReferencePack.</p>


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

### DiffPack {#DiffPack}
*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#200)*



<p>Contains a Buffer containing the FIDL serialization of Diff.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ReferencePack {#ReferencePack}
*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#207)*



<p>Contains a Buffer containing the FIDL serialization of References.</p>
<p>If the Buffer is absent, the reference list is treated as empty.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### Status {#Status}
Type: <code>int32</code>

*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#25)*

<p>Response status for cloud provider operations.</p>


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
            <td><code>NOT_SUPPORTED</code></td>
            <td><code>8</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNKNOWN_ERROR</code></td>
            <td><code>-1</code></td>
            <td></td>
        </tr></table>

### Operation {#Operation}
Type: <code>uint8</code>

*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#184)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INSERTION</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>DELETION</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### Commit {#Commit}


*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#114)*

<p>A commit as seen by the cloud.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>id</code></td>
            <td>
                <code>vector&lt;uint8&gt;[128]</code>
            </td>
            <td><p>A unique commit identifier, chosen by Ledger. Required.</p>
<p>Two commits uploaded with the same identifier are to be considered
identical: they will have the same parents if present, and the cloud may
return the data and the diff from any of the uploads.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td><p>Opaque data stored by Ledger. Required.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>diff</code></td>
            <td>
                <code><a class='link' href='#Diff'>Diff</a></code>
            </td>
            <td><p>A diff describing the content of the page at this commit. Optional.</p>
<p>Ledger will not send a diff for all commits: it may omit the diff when it
determines the content of the commit will not be used by any other Ledger
instance. During the transition to diffs, diff-unaware Ledgers will also
omit the diff.
The cloud provider should not include diffs in the commits it sends to
Ledger.</p>
</td>
        </tr></table>

### Diff {#Diff}


*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#153)*

<p>A diff from a base state to a commit.</p>
<p>Diffs are sequences of insertions and deletions. Updates are encoded as a
deletion followed by an insertion. The cloud can match insertions and
deletions by an entry identifier chosen by Ledger (because of encryption,
the data will not match between insertions and deletions).</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>base_state</code></td>
            <td>
                <code><a class='link' href='#PageState'>PageState</a></code>
            </td>
            <td><p>Page state used as a reference point for the diff.</p>
<p>Ledger only uses as base state a commit that is already known to the
cloud, or the empty page.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>changes</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#DiffEntry'>DiffEntry</a>&gt;</code>
            </td>
            <td><p>List of changes from the base state to the commit.</p>
<p>The changes are to be applied in order.</p>
</td>
        </tr></table>

### DiffEntry {#DiffEntry}


*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#166)*

<p>An entry in a Diff.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>entry_id</code></td>
            <td>
                <code>vector&lt;uint8&gt;[64]</code>
            </td>
            <td><p>Identifier of the entry. Required.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>operation</code></td>
            <td>
                <code><a class='link' href='#Operation'>Operation</a></code>
            </td>
            <td><p>Insertion or deletion. Required.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[512]</code>
            </td>
            <td><p>Data representing the content of the entry.</p>
<p>Required in diffs sent from Ledger. The cloud provider may omit this
information if the operation is a deletion. If an entry id was inserted/
deleted multiple times, the cloud provider can send any of the values.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>reference</code></td>
            <td>
                <code>vector&lt;uint8&gt;[128]</code>
            </td>
            <td><p>An optional reference to an object, given by its identifier.</p>
<p>Sent by Ledger when the value of the entry is not inlined in the <code>data</code>
field. The cloud provider may always omit this field in diffs.</p>
</td>
        </tr></table>





## **XUNIONS**

### PageState {#PageState}
*Defined in [fuchsia.ledger.cloud/cloud_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger.cloud/cloud_provider.fidl#136)*

<p>Specification of a page state used as base for a diff.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>empty_page</code></td>
            <td>
                <code><a class='link' href='#EmptyPage'>EmptyPage</a></code>
            </td>
            <td><p>The state is the empty page.</p>
</td>
        </tr><tr>
            <td><code>at_commit</code></td>
            <td>
                <code>vector&lt;uint8&gt;[128]</code>
            </td>
            <td><p>The state is the content of a page at the commit with the given
identifier.</p>
</td>
        </tr></table>





