[TOC]

# fuchsia.ledger


## **PROTOCOLS**

## Syncable {#Syncable}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger/ledger.fidl#34)*

<p>Base interface for all services offered by the Ledger.</p>
<p>In case of an unexpected error on one of the service offered by the Ledger,
the service will close the connected channel, sending a <code>zx.status</code> as an epitaph.</p>
<p>If a client needs to ensure a sequence of operation has been processed by
the service, it can issue a <code>Sync</code> command. The response will be send once
all request started before the <code>Sync</code> request has been processed by the
service.</p>

### Sync {#Sync}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## Ledger {#Ledger}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger/ledger.fidl#39)*


### Sync {#Sync}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### GetPage {#GetPage}

<p>Retrieves the page with the given identifier, creating it if needed, and binds
<code>page_request</code> to it. A <code>null</code> identifier can be passed to create a new page with a random
unique identifier. It is allowed to connect to the same page concurrently multiple times.</p>
<p>Parameters:
<code>id</code> the identifier of the page, or <code>null</code> to create a new page with a random identifier.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='#PageId'>PageId</a>?</code>
            </td>
        </tr><tr>
            <td><code>page_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Page'>Page</a>&gt;</code>
            </td>
        </tr></table>



### GetRootPage {#GetRootPage}

<p>Gets the page with identifier
[0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0].
This is a convenience method equivalent to:
GetPage([0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], page_request).</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>page_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Page'>Page</a>&gt;</code>
            </td>
        </tr></table>



### SetConflictResolverFactory {#SetConflictResolverFactory}

<p>Sets the <code>ConflictResolverFactory</code> to use for resolving conflicts on pages.
If this method has never been called, a last-one-wins policy will be used
for every page. If this method is called multiple times, the factories are
kept and conflict resolver requests are sent to one of the connected
factories. If all factories are later disconnected, pages that already have
a conflict resolution strategy (because they were opened before the factory
disconnected) will continue using their current strategy. The pages for
which no conflict resolution is set up will not get their conflicts
resolved until this method is called again.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>factory</code></td>
            <td>
                <code><a class='link' href='#ConflictResolverFactory'>ConflictResolverFactory</a></code>
            </td>
        </tr></table>



## Page {#Page}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger/ledger.fidl#89)*

<p>A page is the smallest unit of syncable data.</p>

### Sync {#Sync}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### GetId {#GetId}

<p>Returns the identifier for the page.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='#PageId'>PageId</a></code>
            </td>
        </tr></table>

### GetSnapshot {#GetSnapshot}

<p>Creates a snapshot of the page, allowing the client app to read a
consistent view of the content of the page. If <code>key_prefix</code> is provided,
the resulting snapshot includes only the entries with matching keys.</p>
<p>If <code>watcher</code> is provided, it will receive notifications for changes of the
page state on this page connection newer than the resulting snapshot.
Change notifications will only contain the entries matching <code>key_prefix</code>.
To receive all changes, use an empty <code>key_prefix</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>snapshot_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#PageSnapshot'>PageSnapshot</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>key_prefix</code></td>
            <td>
                <code><a class='link' href='#Key'>Key</a></code>
            </td>
        </tr><tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#PageWatcher'>PageWatcher</a>?</code>
            </td>
        </tr></table>



### Put {#Put}

<p>Mutations are bundled together into atomic commits. If a transaction is in
progress, the list of mutations bundled together is tied to the current
transaction. If no transaction is in progress, mutations will be bundled
with the following rules:</p>
<ul>
<li>A call to either <code>GetSnapshot()</code> or <code>StartTransaction()</code> will
commit any pending mutations.</li>
<li>All pending mutations will regularly be bundled together and committed.
They are guaranteed to be persisted as soon as the client receives a
successful status.
<code>Put()</code> and <code>PutWithPriority()</code> can be used for small values that
fit inside a FIDL message. If the value is bigger, a reference must be
first created using <code>CreateReferenceFromSocket()</code> or
<code>CreateReferenceFromBuffer()</code> and then <code>PutReference()</code> can be used.
<code>PutWithPriority()</code> and <code>PutReference()</code> have an additional <code>priority</code>
parameter managing the synchronization policy for this value. <code>Put()</code> uses
a default priority of <code>Priority.EAGER</code>. For the list of available
priorities and their definition, see <code>Priority</code>.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code><a class='link' href='#Key'>Key</a></code>
            </td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr></table>



### PutWithPriority {#PutWithPriority}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code><a class='link' href='#Key'>Key</a></code>
            </td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr><tr>
            <td><code>priority</code></td>
            <td>
                <code><a class='link' href='#Priority'>Priority</a></code>
            </td>
        </tr></table>



### PutReference {#PutReference}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code><a class='link' href='#Key'>Key</a></code>
            </td>
        </tr><tr>
            <td><code>reference</code></td>
            <td>
                <code><a class='link' href='#Reference'>Reference</a></code>
            </td>
        </tr><tr>
            <td><code>priority</code></td>
            <td>
                <code><a class='link' href='#Priority'>Priority</a></code>
            </td>
        </tr></table>



### Delete {#Delete}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code><a class='link' href='#Key'>Key</a></code>
            </td>
        </tr></table>



### Clear {#Clear}

<p>Deletes all entries in the page.
Outside of a transaction, this operation is equivalent to deleting every
key currently present on the page in a single transaction.
In a transaction, this operation is equivalent to deleting every key
present in the page before the transaction, as well as any new key added
since the transaction started.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### CreateReferenceFromSocket {#CreateReferenceFromSocket}

<p>Creates a new reference. The object is not part of any commit. It must be
associated with a key using <code>PutReference()</code>. The content of the reference
will be the content of the socket. The content size must be equal to
<code>size</code>, otherwise the call will fail.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>size</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code>handle&lt;socket&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Page_CreateReferenceFromSocket_Result'>Page_CreateReferenceFromSocket_Result</a></code>
            </td>
        </tr></table>

### CreateReferenceFromBuffer {#CreateReferenceFromBuffer}

<p>Creates a new reference. The object is not part of any commit. It must be
associated with a key using <code>PutReference()</code>. The content of the reference
will be the content of the buffer.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Page_CreateReferenceFromBuffer_Result'>Page_CreateReferenceFromBuffer_Result</a></code>
            </td>
        </tr></table>

### StartTransaction {#StartTransaction}

<p>Transactions allow the client to ensures changes are seen atomically by
observers of this page. Once a transaction is started with
<code>StartTransaction()</code>, every call to <code>Put(...)</code> and <code>Delete(...)</code> will not
be visible until either <code>Commit()</code> is called, and all changes are applied
in a single commit, or <code>Rollback()</code> is called and all changes are
discarded.</p>
<p>Parallel transactions on the same <em>page connection</em> are not allowed, and
calling <code>StartTransaction()</code> when a transaction is already in progress
returns an error. However, a client is free to connect to the same page
multiple times, and run parallel transactions on the same page using
separate connections. In this case, committing each transaction creates
divergent commits, which are later subject to conflict resolution.</p>
<p>When a transaction is in progress, the page content visible <em>on this page
connection</em> is pinned to the state from when <code>StartTransaction()</code> was
called. In particular, no watch notifications are delivered, and the
conflict resolution is not invoked while the transaction is in progress. If
conflicting changes are made or synced while the transaction is in
progress, conflict resolution is invoked after the transaction is
committed.</p>
<p>Starting a transaction will block until all watchers registered on this
page connection have received the current page state, ie. the one that
will be used as the base of the transaction. Put (with all its variants)
and Delete calls may be pipelined while StartTransaction() is pending and
will be taken into account in the transaction while it is pending.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Commit {#Commit}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Rollback {#Rollback}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SetSyncStateWatcher {#SetSyncStateWatcher}

<p>Sets a watcher to track the synchronisation state of this page. The
current state is immediately sent to the watcher when this method is
called.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#SyncWatcher'>SyncWatcher</a></code>
            </td>
        </tr></table>



### WaitForConflictResolution {#WaitForConflictResolution}

<p>Waits until all conflicts are resolved before calling the callback.
The client can call this method multiple times, even before the previous
calls are completed. Callbacks will be executed in the order they were
added and indicate whether a merge happened between the callback
registration and its execution.
If there are no pending conflicts at the time this is called, the callback
gets executed right away.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>wait_status</code></td>
            <td>
                <code><a class='link' href='#ConflictResolutionWaitStatus'>ConflictResolutionWaitStatus</a></code>
            </td>
        </tr></table>

## PageSnapshot {#PageSnapshot}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger/ledger.fidl#252)*

<p>The content of a page at a given time. Closing the connection to a <code>Page</code>
interface closes all <code>PageSnapshot</code> interfaces it created. The contents
provided by this interface are limited to the prefix provided to the
Page.GetSnapshot() call.</p>

### Sync {#Sync}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### GetEntries {#GetEntries}

<p>Returns the entries in the page with keys greater or equal to <code>key_start</code>
using the lexicographic order. If <code>key_start</code> is empty, all entries are
returned. If the result fits in a single fidl message, <code>next_token</code> will
be equal to NULL. Otherwise, <code>next_token</code> will have a non-NULL value. To
retrieve the remaining results, another call to <code>GetEntries</code> should be
made, initializing the optional <code>token</code> argument with the value of
<code>next_token</code> returned in the previous call. <code>next_token</code> will not be
NULL as long as there are more results and NULL once finished.
Only <code>EAGER</code> values are guaranteed to be returned inside <code>entries</code>.
Missing <code>LAZY</code> values can be retrieved over the network using Fetch().
The returned <code>entries</code> are sorted by <code>key</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key_start</code></td>
            <td>
                <code><a class='link' href='#Key'>Key</a></code>
            </td>
        </tr><tr>
            <td><code>token</code></td>
            <td>
                <code><a class='link' href='#Token'>Token</a>?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>entries</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Entry'>Entry</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>next_token</code></td>
            <td>
                <code><a class='link' href='#Token'>Token</a>?</code>
            </td>
        </tr></table>

### GetEntriesInline {#GetEntriesInline}

<p>Same as <code>GetEntries()</code>. The connection will be closed with a
<code>ZX_ERR_BAD_STATE</code> epitaph if a value does not fit in a FIDL message.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key_start</code></td>
            <td>
                <code><a class='link' href='#Key'>Key</a></code>
            </td>
        </tr><tr>
            <td><code>token</code></td>
            <td>
                <code><a class='link' href='#Token'>Token</a>?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>entries</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#InlinedEntry'>InlinedEntry</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>next_token</code></td>
            <td>
                <code><a class='link' href='#Token'>Token</a>?</code>
            </td>
        </tr></table>

### GetKeys {#GetKeys}

<p>Returns the keys of all entries in the page which are greater or equal to
<code>key_start</code> using the lexicographic order. If <code>key_start</code> is empty, all
keys are returned. The returned <code>keys</code> are sorted. If the result fits in
a single fidl message, <code>next_token</code> will be equal to NULL. Otherwise,
<code>next_token</code> will have a non-NULL value. To retrieve the remaining
results, another call to <code>GetKeys</code> should be made, initializing the
optional <code>token</code> argument with the value of <code>next_token</code> returned in the
previous call. <code>next_token</code> will not be NULL as long as there are more
results and NULL once finished.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key_start</code></td>
            <td>
                <code><a class='link' href='#Key'>Key</a></code>
            </td>
        </tr><tr>
            <td><code>token</code></td>
            <td>
                <code><a class='link' href='#Token'>Token</a>?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>keys</code></td>
            <td>
                <code>vector&lt;vector&gt;</code>
            </td>
        </tr><tr>
            <td><code>next_token</code></td>
            <td>
                <code><a class='link' href='#Token'>Token</a>?</code>
            </td>
        </tr></table>

### Get {#Get}

<p>Returns the value of a given key.
Only <code>EAGER</code> values are guaranteed to be returned. Calls when the value is
<code>LAZY</code> and not available will return a <code>NEEDS_FETCH</code> status. The value can
be retrieved over the network using a Fetch() call.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code><a class='link' href='#Key'>Key</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#PageSnapshot_Get_Result'>PageSnapshot_Get_Result</a></code>
            </td>
        </tr></table>

### GetInline {#GetInline}

<p>Returns the value of a given key if it fits in a FIDL message.
The connection will be closed with a <code>ZX_ERR_BAD_STATE</code> epitaph if the
value does not fit in a FIDL message.
See <code>Get()</code> for additional information.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code><a class='link' href='#Key'>Key</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#PageSnapshot_GetInline_Result'>PageSnapshot_GetInline_Result</a></code>
            </td>
        </tr></table>

### Fetch {#Fetch}

<p>Fetches the value of a given key, over the network if not already present
locally. <code>NETWORK_ERROR</code> is returned if the download fails (e.g.: network
is not available).</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code><a class='link' href='#Key'>Key</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#PageSnapshot_Fetch_Result'>PageSnapshot_Fetch_Result</a></code>
            </td>
        </tr></table>

### FetchPartial {#FetchPartial}

<p>Fetches the value of a given key, over the network if not already present
locally, and returns a shared handle of a part of the value of a given
key, starting at the position that is specified by <code>offset</code>. If <code>offset</code>
is less than 0, starts at <code>-offset</code> from the end of the value.
Returns at most <code>max_size</code> bytes. If <code>max_size</code> is less than 0, returns
everything.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code><a class='link' href='#Key'>Key</a></code>
            </td>
        </tr><tr>
            <td><code>offset</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>max_size</code></td>
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
                <code><a class='link' href='#PageSnapshot_FetchPartial_Result'>PageSnapshot_FetchPartial_Result</a></code>
            </td>
        </tr></table>

## PageWatcher {#PageWatcher}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger/ledger.fidl#338)*

<p>Interface to watch changes to a page. The client will receive changes made by
itself, as well as other clients or synced from other devices. The contents
of a transaction will never be split across multiple OnChange() calls, but
the contents of multiple transactions may be merged into one OnChange() call.</p>

### OnChange {#OnChange}

<p>Called for changes made on the page. If the result fits in a single fidl
message, <code>result_state</code> will be <code>COMPLETED</code>. Otherwise, OnChange will be
called multiple times and <code>result_state</code> will be <code>PARTIAL_STARTED</code> the
first time, <code>PARTIAL_CONTINUED</code> the following ones and finally
<code>PARTIAL_COMPLETED</code> on the last call. No new OnChange() call will be made
while the previous one is still active. If clients are interested in the
full content of the page at the time of the change, they can request a
PageSnapshot in the callback. This request is optional and can be requested
in any partial (started, continued or completed) and/or COMPLETED OnChange
call. In any case, all requests made on a sequence of OnChange calls for
the same page change, will always return the same snapshot: the one
including all changes.</p>
<p>Note that calls to Page.StartTransaction() on the page connection on which
the watcher was registered will block until all OnChange() calls have
finished.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>page_change</code></td>
            <td>
                <code><a class='link' href='#PageChange'>PageChange</a></code>
            </td>
        </tr><tr>
            <td><code>result_state</code></td>
            <td>
                <code><a class='link' href='#ResultState'>ResultState</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>snapshot</code></td>
            <td>
                <code>request&lt;<a class='link' href='#PageSnapshot'>PageSnapshot</a>&gt;?</code>
            </td>
        </tr></table>

## ConflictResolverFactory {#ConflictResolverFactory}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger/ledger.fidl#362)*

<p>This interface lets clients control the conflict resolution policy of the
ledger. It allows them to either use pre-defined policies, or provide their
own implementation. This can be decided on a page-by-page basis.</p>

### GetPolicy {#GetPolicy}

<p>Returns the conflict resolution policy for the given page.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>page_id</code></td>
            <td>
                <code><a class='link' href='#PageId'>PageId</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>policy</code></td>
            <td>
                <code><a class='link' href='#MergePolicy'>MergePolicy</a></code>
            </td>
        </tr></table>

### NewConflictResolver {#NewConflictResolver}

<p>Returns a <code>ConflictResolver</code> to use for the given page. This will only be
called if <code>GetPolicy</code> for the same page returned <code>AUTOMATIC_WITH_FALLBACK</code>
or <code>CUSTOM</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>page_id</code></td>
            <td>
                <code><a class='link' href='#PageId'>PageId</a></code>
            </td>
        </tr><tr>
            <td><code>resolver</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ConflictResolver'>ConflictResolver</a>&gt;</code>
            </td>
        </tr></table>



## MergeResultProvider {#MergeResultProvider}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger/ledger.fidl#445)*

<p>A merge result provider, obtained from <code>ConflictResolver.Resolve()</code>. Can be
used to retrieve data about the conflict, and provide the merge result. When
all changes have been sent, <code>Done()</code> should be called to mark the end of
incoming merge changes.</p>

### Sync {#Sync}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### GetFullDiff {#GetFullDiff}

<p><code>GetFullDiff</code> returns the set of all key/value pairs (entries) that
have been modified between the common ancestor (see
<code>ConflictResolver.Resolve()</code>) and the left and right branches.</p>
<p>Values of <code>LAZY</code> keys may not be present on the device. In that case, the
corresponding Value objects within DiffEntry will have a NULL <code>value</code>
field. If needed, <code>left</code> and <code>right</code>, provided by the
<code>ConflictResolver.Resolve()</code> method can be used by clients to Fetch these
values. If a key is not present at all in one of the branches, its
corresponding Value object will be NULL.</p>
<p>The first call to get the <code>DiffEntry</code>s should be done using a NULL
token. If the result does not fit in a single fidl message, <code>next_token</code>
will have a non-NULL value, which can be used to retrieve the rest of
the results by calling <code>GetFullDiff()</code> with that token.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>token</code></td>
            <td>
                <code><a class='link' href='#Token'>Token</a>?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>changes</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#DiffEntry'>DiffEntry</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>next_token</code></td>
            <td>
                <code><a class='link' href='#Token'>Token</a>?</code>
            </td>
        </tr></table>

### GetConflictingDiff {#GetConflictingDiff}

<p><code>GetConflictingDiff</code> returns the set of all key/value pairs that were
modified on both sides to different values, or deleted on one side and
modified on the other.</p>
<p>It behaves like <code>GetFullDiff</code> otherwise.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>token</code></td>
            <td>
                <code><a class='link' href='#Token'>Token</a>?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>changes</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#DiffEntry'>DiffEntry</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>next_token</code></td>
            <td>
                <code><a class='link' href='#Token'>Token</a>?</code>
            </td>
        </tr></table>

### Merge {#Merge}

<p>Once the result of the merge has been computed <code>Merge()</code> can be called with
all changes that resolve this conflict. If the result does not fit in a
single fidl message, <code>Merge()</code> can be called multiple times. If any of the
<code>Merge()</code> calls fails, i.e. <code>status</code> is not <code>OK</code>, all following calls will
fail with the same error.</p>
<p>If a key/value pair is sent multiple times in one or several <code>Merge()</code>
call, only the last pair is taken into account.</p>
<p>For all keys for which no merged value has been set (either here or
through <code>MergeNonConflictingEntries()</code> below), the left value will be
used. It is thus not necessary to send a MergedValue with a <code>LEFT</code> value
source, unless to overwrite a previous MergedValue.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>merge_changes</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#MergedValue'>MergedValue</a>&gt;</code>
            </td>
        </tr></table>



### MergeNonConflictingEntries {#MergeNonConflictingEntries}

<p>Automatically merges all non conflicting entries (entries that are
modified on one side only or identical on both sides). This is equivalent
to sending, through <code>Merge()</code>, a MergedValue with a <code>RIGHT</code> ValueSource
for all non-conflicting keys modified on the right side. Conflicting
entries can still be merged using the <code>Merge()</code> method.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Done {#Done}

<p>Marks the end of merge changes to resolve this conflict. After <code>Done()</code> is
called <code>MergeResultProvider</code> interface cannot be used any more.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## ConflictResolver {#ConflictResolver}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger/ledger.fidl#510)*

<p>Custom conflict resolver. If a <code>ConflictResolverFactory</code> is registered, and
<code>ConflictResolverFactory.GetPolicy()</code> returns <code>AUTOMATIC_WITH_FALLBACK</code> or
<code>CUSTOM</code> when called for a given page, the <code>NewConflictResolver</code> method will
be called and will provide a <code>ConflictResolver</code>. Each time a custom conflict
resolution is needed according to the chosen policy, the method
<code>ConflictResolver.Resolve()</code> will be called, and the client will resolve the
conflict by returning the final value for all conflicting keys as well as
values for any other key that the client wants to change.</p>

### Resolve {#Resolve}

<p>Method called when a conflict needs to be resolved. <code>left</code> and <code>right</code>
contain the snapshots of the two branches and <code>common_version</code> that of the
lowest common ancestor. <code>common_version</code> can be NULL if this version is no
longer available. The result of the merge can be given through the
<code>result_provider</code>, using the left branch as the base of the merge commit,
i.e. only key/value pairs that are different from the left version of the
page should be sent. <code>result_provider</code> can also be used to retrieve the set
of differences, i.e. conflicting keys, between the two versions.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>left</code></td>
            <td>
                <code><a class='link' href='#PageSnapshot'>PageSnapshot</a></code>
            </td>
        </tr><tr>
            <td><code>right</code></td>
            <td>
                <code><a class='link' href='#PageSnapshot'>PageSnapshot</a></code>
            </td>
        </tr><tr>
            <td><code>common_version</code></td>
            <td>
                <code><a class='link' href='#PageSnapshot'>PageSnapshot</a>?</code>
            </td>
        </tr><tr>
            <td><code>new_result_provider</code></td>
            <td>
                <code><a class='link' href='#MergeResultProvider'>MergeResultProvider</a></code>
            </td>
        </tr></table>



## SyncWatcher {#SyncWatcher}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger/ledger.fidl#544)*

<p>Watcher interface to be implemented by clients who wish to follow the
synchronization status of their ledger. SyncStateChanged callback must be
called for new state change calls to be sent.</p>

### SyncStateChanged {#SyncStateChanged}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>download_status</code></td>
            <td>
                <code><a class='link' href='#SyncState'>SyncState</a></code>
            </td>
        </tr><tr>
            <td><code>upload_status</code></td>
            <td>
                <code><a class='link' href='#SyncState'>SyncState</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## **STRUCTS**

### Page_CreateReferenceFromSocket_Response {#Page_CreateReferenceFromSocket_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>reference</code></td>
            <td>
                <code><a class='link' href='#Reference'>Reference</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Page_CreateReferenceFromBuffer_Response {#Page_CreateReferenceFromBuffer_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>reference</code></td>
            <td>
                <code><a class='link' href='#Reference'>Reference</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### PageSnapshot_Get_Response {#PageSnapshot_Get_Response}
*generated*





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

### PageSnapshot_GetInline_Response {#PageSnapshot_GetInline_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#InlinedValue'>InlinedValue</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### PageSnapshot_Fetch_Response {#PageSnapshot_Fetch_Response}
*generated*





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

### PageSnapshot_FetchPartial_Response {#PageSnapshot_FetchPartial_Response}
*generated*





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

### PageId {#PageId}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger/ledger.fidl#20)*



<p>Type of the identifier of a ledger Page.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint8[16]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Reference {#Reference}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger/ledger.fidl#69)*



<p>A reference to a value.</p>


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

### Token {#Token}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger/ledger.fidl#74)*



<p>A continuation token for paginated requests.</p>


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

### Entry {#Entry}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger/ledger.fidl#217)*



<p>A pair of key and value.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code><a class='link' href='#Key'>Key</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a>?</code>
            </td>
            <td><p><code>value</code> is null if the value requested has the LAZY priority and is not
present on the device. Clients must use a Fetch call to retrieve the
contents.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>priority</code></td>
            <td>
                <code><a class='link' href='#Priority'>Priority</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### InlinedValue {#InlinedValue}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger/ledger.fidl#227)*



<p>A value inlined in a message.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### InlinedEntry {#InlinedEntry}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger/ledger.fidl#232)*



<p>A pair of key and an inlined value.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code><a class='link' href='#Key'>Key</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>inlined_value</code></td>
            <td>
                <code><a class='link' href='#InlinedValue'>InlinedValue</a>?</code>
            </td>
            <td><p><code>value</code> is null if the value requested has the LAZY priority and is not
present on the device. Clients must use a Fetch call to retrieve the
contents.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>priority</code></td>
            <td>
                <code><a class='link' href='#Priority'>Priority</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### PageChange {#PageChange}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger/ledger.fidl#321)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>timestamp</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#time'>time</a></code>
            </td>
            <td><p>The timestamp of this change. This represents the number of nanoseconds
since Unix epoch (i.e., since &quot;1970-01-01 00:00 UTC&quot;, ignoring leap
seconds). This value is set by the device that created the change and is
not synchronized across devices. In particular, there is no guarantee that
the <code>timestamp</code> of a follow up change is greater than this one's.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>changed_entries</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Entry'>Entry</a>&gt;</code>
            </td>
            <td><p>List of new and modified entries. <code>changed_entries</code> are sorted by <code>key</code>.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>deleted_keys</code></td>
            <td>
                <code>vector&lt;vector&gt;</code>
            </td>
            <td><p>List of deleted keys, in sorted order.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### MergedValue {#MergedValue}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger/ledger.fidl#412)*



<p>A change in the page. If <code>source</code> is set to <code>NEW</code>, <code>new_value</code> must be set
to the new value. If <code>source</code> is not <code>NEW</code>, <code>new_value</code> and <code>priority</code> are
ignored.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code><a class='link' href='#Key'>Key</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#ValueSource'>ValueSource</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>new_value</code></td>
            <td>
                <code><a class='link' href='#BytesOrReference'>BytesOrReference</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>priority</code></td>
            <td>
                <code><a class='link' href='#Priority'>Priority</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DiffEntry {#DiffEntry}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger/ledger.fidl#424)*



<p>An entry in a diff, as returned by <code>MergeResultProvider</code>.</p>
<p>If <code>base</code>, <code>left</code> or <code>right</code> are NULL, this means that the corresponding key
was not present in the base, left or right (respectively) branch of the
page.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code><a class='link' href='#Key'>Key</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>base</code></td>
            <td>
                <code><a class='link' href='#Value'>Value</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>left</code></td>
            <td>
                <code><a class='link' href='#Value'>Value</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>right</code></td>
            <td>
                <code><a class='link' href='#Value'>Value</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Value {#Value}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger/ledger.fidl#436)*



<p>A value in a DiffEntry.</p>
<p>If the value is LAZY and is not present locally, <code>value</code> will be NULL. The
value can be retrieved using a <code>Fetch()</code> call on a corresponding snapshot.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>priority</code></td>
            <td>
                <code><a class='link' href='#Priority'>Priority</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### ConflictResolutionWaitStatus {#ConflictResolutionWaitStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger/ledger.fidl#80)*

<p>The result of a wait for conflict resolution. See
<code>Page.WaitForConflictResolution</code> for details.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NO_CONFLICTS</code></td>
            <td><code>0</code></td>
            <td><p>No conflict was observed when the callback was registered.</p>
</td>
        </tr><tr>
            <td><code>CONFLICTS_RESOLVED</code></td>
            <td><code>1</code></td>
            <td><p>Some conflicts were observed when the callback was registered, and all
have been resolved.</p>
</td>
        </tr></table>

### Priority {#Priority}
Type: <code>uint32</code>

*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger/ledger.fidl#206)*

<p>The synchronization priority of a reference.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>EAGER</code></td>
            <td><code>0</code></td>
            <td><p>EAGER values will be downloaded with the commit and have the same
availability.</p>
</td>
        </tr><tr>
            <td><code>LAZY</code></td>
            <td><code>1</code></td>
            <td><p>LAZY values will not be downloaded with their commit, but only on demand.
A LAZY value thus may not be available when requested, for example if the
device has no internet connection at request time.</p>
</td>
        </tr></table>

### Error {#Error}
Type: <code>uint32</code>

*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger/ledger.fidl#242)*

<p>Error returned by the different PageSnapshot methods.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>KEY_NOT_FOUND</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>NEEDS_FETCH</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>NETWORK_ERROR</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### ResultState {#ResultState}
Type: <code>uint32</code>

*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger/ledger.fidl#314)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>COMPLETED</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>PARTIAL_STARTED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>PARTIAL_CONTINUED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>PARTIAL_COMPLETED</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### MergePolicy {#MergePolicy}
Type: <code>uint32</code>

*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger/ledger.fidl#372)*

<p>Strategy to be used when resolving conflicts.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>LAST_ONE_WINS</code></td>
            <td><code>0</code></td>
            <td><p>Last one wins. When 2 commits are merged, the resulting commit contains:</p>
<ul>
<li>all keys/values that do not conflict</li>
<li>all keys/values of the commit with the biggest timestamp (or biggest
id, if the timestamps are the same)</li>
</ul>
</td>
        </tr><tr>
            <td><code>AUTOMATIC_WITH_FALLBACK</code></td>
            <td><code>1</code></td>
            <td><p>Commits are automatically merged when no key has been modified on both
sides. When a key has been modified by both commits, conflict resolution is
delegated to a user-provided <code>ConflictResolver</code> that is created by calling
<code>ConflictResolverFactory.NewConflictResolver</code>. A single <code>ConflictResolver</code>
is created for each page. When the <code>ConflictResolver</code> is disconnected, a
new one is requested.</p>
</td>
        </tr><tr>
            <td><code>CUSTOM</code></td>
            <td><code>2</code></td>
            <td><p>All merges are resolved by a user-provided <code>ConflictResolver</code> as described
above, even when commits to be merged change a disjoined set of keys.</p>
</td>
        </tr></table>

### ValueSource {#ValueSource}
Type: <code>uint32</code>

*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger/ledger.fidl#403)*

<p>Source of the value used to resolve a conflict.</p>
<p><code>DELETE</code> deletes the key; <code>NEW</code> creates a new value; <code>RIGHT</code>
selects the value from the right branch. If no value is sent, the left
branch is selected.
Used by <code>MergedValue</code>.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>RIGHT</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>NEW</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>DELETE</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### SyncState {#SyncState}
Type: <code>uint32</code>

*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger/ledger.fidl#524)*

<p>Synchronization state.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>IDLE</code></td>
            <td><code>0</code></td>
            <td><p>There are no pending operations.</p>
</td>
        </tr><tr>
            <td><code>PENDING</code></td>
            <td><code>1</code></td>
            <td><p>There are pending operations, but there is no syncing in progress. This
could be because of (possibly a combination of):</p>
<ul>
<li>waiting for better connectivity</li>
<li>waiting due to internal policies (e.g. batching network requests,
waiting for a merge to happen before uploading)</li>
<li>waiting to determine if synchronization is needed (e.g. during initial
setup)</li>
</ul>
</td>
        </tr><tr>
            <td><code>IN_PROGRESS</code></td>
            <td><code>2</code></td>
            <td><p>Synchronization is in progress.</p>
</td>
        </tr><tr>
            <td><code>ERROR</code></td>
            <td><code>3</code></td>
            <td><p>An internal error occurred while trying to sync.</p>
</td>
        </tr></table>





## **UNIONS**

### Page_CreateReferenceFromSocket_Result {#Page_CreateReferenceFromSocket_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Page_CreateReferenceFromSocket_Response'>Page_CreateReferenceFromSocket_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### Page_CreateReferenceFromBuffer_Result {#Page_CreateReferenceFromBuffer_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Page_CreateReferenceFromBuffer_Response'>Page_CreateReferenceFromBuffer_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### PageSnapshot_Get_Result {#PageSnapshot_Get_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#PageSnapshot_Get_Response'>PageSnapshot_Get_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### PageSnapshot_GetInline_Result {#PageSnapshot_GetInline_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#PageSnapshot_GetInline_Response'>PageSnapshot_GetInline_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### PageSnapshot_Fetch_Result {#PageSnapshot_Fetch_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#PageSnapshot_Fetch_Response'>PageSnapshot_Fetch_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### PageSnapshot_FetchPartial_Result {#PageSnapshot_FetchPartial_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#PageSnapshot_FetchPartial_Response'>PageSnapshot_FetchPartial_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### BytesOrReference {#BytesOrReference}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger/ledger.fidl#392)*

<p>A value that is either small enough to be directly embedded in <code>bytes</code> or
that is referenced by <code>reference</code>.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>bytes</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>reference</code></td>
            <td>
                <code><a class='link' href='#Reference'>Reference</a></code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="PAGE_ID_SIZE">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger/ledger.fidl#17">PAGE_ID_SIZE</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Size in bytes of Page IDs.</p>
</td>
        </tr>
    
</table>



## **TYPE ALIASES**

<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr id="Key">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger/ledger.fidl#14">Key</a></td>
            <td>
                <code>vector</code></td>
            <td><p>Type of the keys in a ledger Page.</p>
</td>
        </tr></table>

