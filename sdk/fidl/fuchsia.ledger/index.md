Project: /_project.yaml
Book: /_book.yaml

# fuchsia.ledger


## **PROTOCOLS**

## Syncable {:#Syncable}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#37)*

 Base interface for all services offered by the Ledger.

 In case of an unexpected error on one of the service offered by the Ledger,
 the service will close the connected channel, sending a `zx.status` as an epitaph.

 If a client needs to ensure a sequence of operation has been processed by
 the service, it can issue a `Sync` command. The response will be send once
 all request started before the `Sync` request has been processed by the
 service.

### Sync {:#Sync}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## Ledger {:#Ledger}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#42)*


### Sync {:#Sync}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### GetPage {:#GetPage}

 Retrieves the page with the given identifier, creating it if needed, and binds
 `page_request` to it. A `null` identifier can be passed to create a new page with a random
 unique identifier. It is allowed to connect to the same page concurrently multiple times.

 Parameters:
 `id` the identifier of the page, or `null` to create a new page with a random identifier.

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



### GetRootPage {:#GetRootPage}

 Gets the page with identifier
 [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0].
 This is a convenience method equivalent to:
 GetPage([0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], page_request).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>page_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Page'>Page</a>&gt;</code>
            </td>
        </tr></table>



### SetConflictResolverFactory {:#SetConflictResolverFactory}

 Sets the `ConflictResolverFactory` to use for resolving conflicts on pages.
 If this method has never been called, a last-one-wins policy will be used
 for every page. If this method is called multiple times, the factories are
 kept and conflict resolver requests are sent to one of the connected
 factories. If all factories are later disconnected, pages that already have
 a conflict resolution strategy (because they were opened before the factory
 disconnected) will continue using their current strategy. The pages for
 which no conflict resolution is set up will not get their conflicts
 resolved until this method is called again.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>factory</code></td>
            <td>
                <code><a class='link' href='#ConflictResolverFactory'>ConflictResolverFactory</a></code>
            </td>
        </tr></table>



## Page {:#Page}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#92)*

 A page is the smallest unit of syncable data.

### Sync {:#Sync}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### GetId {:#GetId}

 Returns the identifier for the page.

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

### GetSnapshot {:#GetSnapshot}

 Creates a snapshot of the page, allowing the client app to read a
 consistent view of the content of the page. If `key_prefix` is provided,
 the resulting snapshot includes only the entries with matching keys.

 If `watcher` is provided, it will receive notifications for changes of the
 page state on this page connection newer than the resulting snapshot.
 Change notifications will only contain the entries matching `key_prefix`.
 To receive all changes, use an empty `key_prefix`.

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
                <code>vector&lt;uint8&gt;[256]</code>
            </td>
        </tr><tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#PageWatcher'>PageWatcher</a>?</code>
            </td>
        </tr></table>



### Put {:#Put}

 Mutations are bundled together into atomic commits. If a transaction is in
 progress, the list of mutations bundled together is tied to the current
 transaction. If no transaction is in progress, mutations will be bundled
 with the following rules:
 - A call to either `GetSnapshot()` or `StartTransaction()` will
   commit any pending mutations.
 - All pending mutations will regularly be bundled together and committed.
   They are guaranteed to be persisted as soon as the client receives a
   successful status.
 `Put()` and `PutWithPriority()` can be used for small values that
 fit inside a FIDL message. If the value is bigger, a reference must be
 first created using `CreateReferenceFromSocket()` or
 `CreateReferenceFromBuffer()` and then `PutReference()` can be used.
 `PutWithPriority()` and `PutReference()` have an additional `priority`
 parameter managing the synchronization policy for this value. `Put()` uses
 a default priority of `Priority.EAGER`. For the list of available
 priorities and their definition, see `Priority`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
            </td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr></table>



### PutWithPriority {:#PutWithPriority}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
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



### PutReference {:#PutReference}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
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



### Delete {:#Delete}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
            </td>
        </tr></table>



### Clear {:#Clear}

 Deletes all entries in the page.
 Outside of a transaction, this operation is equivalent to deleting every
 key currently present on the page in a single transaction.
 In a transaction, this operation is equivalent to deleting every key
 present in the page before the transaction, as well as any new key added
 since the transaction started.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### CreateReferenceFromSocket {:#CreateReferenceFromSocket}

 Creates a new reference. The object is not part of any commit. It must be
 associated with a key using `PutReference()`. The content of the reference
 will be the content of the socket. The content size must be equal to
 `size`, otherwise the call will fail.

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

### CreateReferenceFromBuffer {:#CreateReferenceFromBuffer}

 Creates a new reference. The object is not part of any commit. It must be
 associated with a key using `PutReference()`. The content of the reference
 will be the content of the buffer.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
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

### StartTransaction {:#StartTransaction}

 Transactions allow the client to ensures changes are seen atomically by
 observers of this page. Once a transaction is started with
 `StartTransaction()`, every call to `Put(...)` and `Delete(...)` will not
 be visible until either `Commit()` is called, and all changes are applied
 in a single commit, or `Rollback()` is called and all changes are
 discarded.

 Parallel transactions on the same *page connection* are not allowed, and
 calling `StartTransaction()` when a transaction is already in progress
 returns an error. However, a client is free to connect to the same page
 multiple times, and run parallel transactions on the same page using
 separate connections. In this case, committing each transaction creates
 divergent commits, which are later subject to conflict resolution.

 When a transaction is in progress, the page content visible *on this page
 connection* is pinned to the state from when `StartTransaction()` was
 called. In particular, no watch notifications are delivered, and the
 conflict resolution is not invoked while the transaction is in progress. If
 conflicting changes are made or synced while the transaction is in
 progress, conflict resolution is invoked after the transaction is
 committed.

 Starting a transaction will block until all watchers registered on this
 page connection have received the current page state, ie. the one that
 will be used as the base of the transaction. Put (with all its variants)
 and Delete calls may be pipelined while StartTransaction() is pending and
 will be taken into account in the transaction while it is pending.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Commit {:#Commit}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Rollback {:#Rollback}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SetSyncStateWatcher {:#SetSyncStateWatcher}

 Sets a watcher to track the synchronisation state of this page. The
 current state is immediately sent to the watcher when this method is
 called.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#SyncWatcher'>SyncWatcher</a></code>
            </td>
        </tr></table>



### WaitForConflictResolution {:#WaitForConflictResolution}

 Waits until all conflicts are resolved before calling the callback.
 The client can call this method multiple times, even before the previous
 calls are completed. Callbacks will be executed in the order they were
 added and indicate whether a merge happened between the callback
 registration and its execution.
 If there are no pending conflicts at the time this is called, the callback
 gets executed right away.

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

## PageSnapshot {:#PageSnapshot}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#255)*

 The content of a page at a given time. Closing the connection to a `Page`
 interface closes all `PageSnapshot` interfaces it created. The contents
 provided by this interface are limited to the prefix provided to the
 Page.GetSnapshot() call.

### Sync {:#Sync}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### GetEntries {:#GetEntries}

 Returns the entries in the page with keys greater or equal to `key_start`
 using the lexicographic order. If `key_start` is empty, all entries are
 returned. If the result fits in a single fidl message, `next_token` will
 be equal to NULL. Otherwise, `next_token` will have a non-NULL value. To
 retrieve the remaining results, another call to `GetEntries` should be
 made, initializing the optional `token` argument with the value of
 `next_token` returned in the previous call. `next_token` will not be
 NULL as long as there are more results and NULL once finished.
 Only `EAGER` values are guaranteed to be returned inside `entries`.
 Missing `LAZY` values can be retrieved over the network using Fetch().
 The returned `entries` are sorted by `key`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key_start</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
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
                <code>vector&lt;<a class='link' href='#Entry'>Entry</a>&gt;[65536]</code>
            </td>
        </tr><tr>
            <td><code>next_token</code></td>
            <td>
                <code><a class='link' href='#Token'>Token</a>?</code>
            </td>
        </tr></table>

### GetEntriesInline {:#GetEntriesInline}

 Same as `GetEntries()`. The connection will be closed with a
 `ZX_ERR_BAD_STATE` epitaph if a value does not fit in a FIDL message.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key_start</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
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
                <code>vector&lt;<a class='link' href='#InlinedEntry'>InlinedEntry</a>&gt;[65536]</code>
            </td>
        </tr><tr>
            <td><code>next_token</code></td>
            <td>
                <code><a class='link' href='#Token'>Token</a>?</code>
            </td>
        </tr></table>

### GetKeys {:#GetKeys}

 Returns the keys of all entries in the page which are greater or equal to
 `key_start` using the lexicographic order. If `key_start` is empty, all
 keys are returned. The returned `keys` are sorted. If the result fits in
 a single fidl message, `next_token` will be equal to NULL. Otherwise,
 `next_token` will have a non-NULL value. To retrieve the remaining
 results, another call to `GetKeys` should be made, initializing the
 optional `token` argument with the value of `next_token` returned in the
 previous call. `next_token` will not be NULL as long as there are more
 results and NULL once finished.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key_start</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
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
                <code>vector&lt;vector&gt;[65536]</code>
            </td>
        </tr><tr>
            <td><code>next_token</code></td>
            <td>
                <code><a class='link' href='#Token'>Token</a>?</code>
            </td>
        </tr></table>

### Get {:#Get}

 Returns the value of a given key.
 Only `EAGER` values are guaranteed to be returned. Calls when the value is
 `LAZY` and not available will return a `NEEDS_FETCH` status. The value can
 be retrieved over the network using a Fetch() call.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
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

### GetInline {:#GetInline}

 Returns the value of a given key if it fits in a FIDL message.
 The connection will be closed with a `ZX_ERR_BAD_STATE` epitaph if the
 value does not fit in a FIDL message.
 See `Get()` for additional information.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
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

### Fetch {:#Fetch}

 Fetches the value of a given key, over the network if not already present
 locally. `NETWORK_ERROR` is returned if the download fails (e.g.: network
 is not available).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
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

### FetchPartial {:#FetchPartial}

 Fetches the value of a given key, over the network if not already present
 locally, and returns a shared handle of a part of the value of a given
 key, starting at the position that is specified by `offset`. If `offset`
 is less than 0, starts at `-offset` from the end of the value.
 Returns at most `max_size` bytes. If `max_size` is less than 0, returns
 everything.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
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

## PageWatcher {:#PageWatcher}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#341)*

 Interface to watch changes to a page. The client will receive changes made by
 itself, as well as other clients or synced from other devices. The contents
 of a transaction will never be split across multiple OnChange() calls, but
 the contents of multiple transactions may be merged into one OnChange() call.

### OnChange {:#OnChange}

 Called for changes made on the page. If the result fits in a single fidl
 message, `result_state` will be `COMPLETED`. Otherwise, OnChange will be
 called multiple times and `result_state` will be `PARTIAL_STARTED` the
 first time, `PARTIAL_CONTINUED` the following ones and finally
 `PARTIAL_COMPLETED` on the last call. No new OnChange() call will be made
 while the previous one is still active. If clients are interested in the
 full content of the page at the time of the change, they can request a
 PageSnapshot in the callback. This request is optional and can be requested
 in any partial (started, continued or completed) and/or COMPLETED OnChange
 call. In any case, all requests made on a sequence of OnChange calls for
 the same page change, will always return the same snapshot: the one
 including all changes.

 Note that calls to Page.StartTransaction() on the page connection on which
 the watcher was registered will block until all OnChange() calls have
 finished.

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

## ConflictResolverFactory {:#ConflictResolverFactory}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#365)*

 This interface lets clients control the conflict resolution policy of the
 ledger. It allows them to either use pre-defined policies, or provide their
 own implementation. This can be decided on a page-by-page basis.

### GetPolicy {:#GetPolicy}

 Returns the conflict resolution policy for the given page.

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

### NewConflictResolver {:#NewConflictResolver}

 Returns a `ConflictResolver` to use for the given page. This will only be
 called if `GetPolicy` for the same page returned `AUTOMATIC_WITH_FALLBACK`
 or `CUSTOM`.

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



## MergeResultProvider {:#MergeResultProvider}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#448)*

 A merge result provider, obtained from `ConflictResolver.Resolve()`. Can be
 used to retrieve data about the conflict, and provide the merge result. When
 all changes have been sent, `Done()` should be called to mark the end of
 incoming merge changes.

### Sync {:#Sync}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### GetFullDiff {:#GetFullDiff}

 `GetFullDiff` returns the set of all key/value pairs (entries) that
 have been modified between the common ancestor (see
 `ConflictResolver.Resolve()`) and the left and right branches.

 Values of `LAZY` keys may not be present on the device. In that case, the
 corresponding Value objects within DiffEntry will have a NULL `value`
 field. If needed, `left` and `right`, provided by the
 `ConflictResolver.Resolve()` method can be used by clients to Fetch these
 values. If a key is not present at all in one of the branches, its
 corresponding Value object will be NULL.

 The first call to get the `DiffEntry`s should be done using a NULL
 token. If the result does not fit in a single fidl message, `next_token`
 will have a non-NULL value, which can be used to retrieve the rest of
 the results by calling `GetFullDiff()` with that token.

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
                <code>vector&lt;<a class='link' href='#DiffEntry'>DiffEntry</a>&gt;[65536]</code>
            </td>
        </tr><tr>
            <td><code>next_token</code></td>
            <td>
                <code><a class='link' href='#Token'>Token</a>?</code>
            </td>
        </tr></table>

### GetConflictingDiff {:#GetConflictingDiff}

 `GetConflictingDiff` returns the set of all key/value pairs that were
 modified on both sides to different values, or deleted on one side and
 modified on the other.

 It behaves like `GetFullDiff` otherwise.

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
                <code>vector&lt;<a class='link' href='#DiffEntry'>DiffEntry</a>&gt;[65536]</code>
            </td>
        </tr><tr>
            <td><code>next_token</code></td>
            <td>
                <code><a class='link' href='#Token'>Token</a>?</code>
            </td>
        </tr></table>

### Merge {:#Merge}

 Once the result of the merge has been computed `Merge()` can be called with
 all changes that resolve this conflict. If the result does not fit in a
 single fidl message, `Merge()` can be called multiple times. If any of the
 `Merge()` calls fails, i.e. `status` is not `OK`, all following calls will
 fail with the same error.

 If a key/value pair is sent multiple times in one or several `Merge()`
 call, only the last pair is taken into account.

 For all keys for which no merged value has been set (either here or
 through `MergeNonConflictingEntries()` below), the left value will be
 used. It is thus not necessary to send a MergedValue with a `LEFT` value
 source, unless to overwrite a previous MergedValue.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>merge_changes</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#MergedValue'>MergedValue</a>&gt;[65536]</code>
            </td>
        </tr></table>



### MergeNonConflictingEntries {:#MergeNonConflictingEntries}

 Automatically merges all non conflicting entries (entries that are
 modified on one side only or identical on both sides). This is equivalent
 to sending, through `Merge()`, a MergedValue with a `RIGHT` ValueSource
 for all non-conflicting keys modified on the right side. Conflicting
 entries can still be merged using the `Merge()` method.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Done {:#Done}

 Marks the end of merge changes to resolve this conflict. After `Done()` is
 called `MergeResultProvider` interface cannot be used any more.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## ConflictResolver {:#ConflictResolver}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#513)*

 Custom conflict resolver. If a `ConflictResolverFactory` is registered, and
 `ConflictResolverFactory.GetPolicy()` returns `AUTOMATIC_WITH_FALLBACK` or
 `CUSTOM` when called for a given page, the `NewConflictResolver` method will
 be called and will provide a `ConflictResolver`. Each time a custom conflict
 resolution is needed according to the chosen policy, the method
 `ConflictResolver.Resolve()` will be called, and the client will resolve the
 conflict by returning the final value for all conflicting keys as well as
 values for any other key that the client wants to change.

### Resolve {:#Resolve}

 Method called when a conflict needs to be resolved. `left` and `right`
 contain the snapshots of the two branches and `common_version` that of the
 lowest common ancestor. `common_version` can be NULL if this version is no
 longer available. The result of the merge can be given through the
 `result_provider`, using the left branch as the base of the merge commit,
 i.e. only key/value pairs that are different from the left version of the
 page should be sent. `result_provider` can also be used to retrieve the set
 of differences, i.e. conflicting keys, between the two versions.

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



## SyncWatcher {:#SyncWatcher}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#547)*

 Watcher interface to be implemented by clients who wish to follow the
 synchronization status of their ledger. SyncStateChanged callback must be
 called for new state change calls to be sent.

### SyncStateChanged {:#SyncStateChanged}


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

## Syncable {:#Syncable}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#37)*

 Base interface for all services offered by the Ledger.

 In case of an unexpected error on one of the service offered by the Ledger,
 the service will close the connected channel, sending a `zx.status` as an epitaph.

 If a client needs to ensure a sequence of operation has been processed by
 the service, it can issue a `Sync` command. The response will be send once
 all request started before the `Sync` request has been processed by the
 service.

### Sync {:#Sync}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## Ledger {:#Ledger}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#42)*


### Sync {:#Sync}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### GetPage {:#GetPage}

 Retrieves the page with the given identifier, creating it if needed, and binds
 `page_request` to it. A `null` identifier can be passed to create a new page with a random
 unique identifier. It is allowed to connect to the same page concurrently multiple times.

 Parameters:
 `id` the identifier of the page, or `null` to create a new page with a random identifier.

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



### GetRootPage {:#GetRootPage}

 Gets the page with identifier
 [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0].
 This is a convenience method equivalent to:
 GetPage([0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], page_request).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>page_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Page'>Page</a>&gt;</code>
            </td>
        </tr></table>



### SetConflictResolverFactory {:#SetConflictResolverFactory}

 Sets the `ConflictResolverFactory` to use for resolving conflicts on pages.
 If this method has never been called, a last-one-wins policy will be used
 for every page. If this method is called multiple times, the factories are
 kept and conflict resolver requests are sent to one of the connected
 factories. If all factories are later disconnected, pages that already have
 a conflict resolution strategy (because they were opened before the factory
 disconnected) will continue using their current strategy. The pages for
 which no conflict resolution is set up will not get their conflicts
 resolved until this method is called again.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>factory</code></td>
            <td>
                <code><a class='link' href='#ConflictResolverFactory'>ConflictResolverFactory</a></code>
            </td>
        </tr></table>



## Page {:#Page}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#92)*

 A page is the smallest unit of syncable data.

### Sync {:#Sync}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### GetId {:#GetId}

 Returns the identifier for the page.

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

### GetSnapshot {:#GetSnapshot}

 Creates a snapshot of the page, allowing the client app to read a
 consistent view of the content of the page. If `key_prefix` is provided,
 the resulting snapshot includes only the entries with matching keys.

 If `watcher` is provided, it will receive notifications for changes of the
 page state on this page connection newer than the resulting snapshot.
 Change notifications will only contain the entries matching `key_prefix`.
 To receive all changes, use an empty `key_prefix`.

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
                <code>vector&lt;uint8&gt;[256]</code>
            </td>
        </tr><tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#PageWatcher'>PageWatcher</a>?</code>
            </td>
        </tr></table>



### Put {:#Put}

 Mutations are bundled together into atomic commits. If a transaction is in
 progress, the list of mutations bundled together is tied to the current
 transaction. If no transaction is in progress, mutations will be bundled
 with the following rules:
 - A call to either `GetSnapshot()` or `StartTransaction()` will
   commit any pending mutations.
 - All pending mutations will regularly be bundled together and committed.
   They are guaranteed to be persisted as soon as the client receives a
   successful status.
 `Put()` and `PutWithPriority()` can be used for small values that
 fit inside a FIDL message. If the value is bigger, a reference must be
 first created using `CreateReferenceFromSocket()` or
 `CreateReferenceFromBuffer()` and then `PutReference()` can be used.
 `PutWithPriority()` and `PutReference()` have an additional `priority`
 parameter managing the synchronization policy for this value. `Put()` uses
 a default priority of `Priority.EAGER`. For the list of available
 priorities and their definition, see `Priority`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
            </td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr></table>



### PutWithPriority {:#PutWithPriority}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
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



### PutReference {:#PutReference}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
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



### Delete {:#Delete}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
            </td>
        </tr></table>



### Clear {:#Clear}

 Deletes all entries in the page.
 Outside of a transaction, this operation is equivalent to deleting every
 key currently present on the page in a single transaction.
 In a transaction, this operation is equivalent to deleting every key
 present in the page before the transaction, as well as any new key added
 since the transaction started.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### CreateReferenceFromSocket {:#CreateReferenceFromSocket}

 Creates a new reference. The object is not part of any commit. It must be
 associated with a key using `PutReference()`. The content of the reference
 will be the content of the socket. The content size must be equal to
 `size`, otherwise the call will fail.

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

### CreateReferenceFromBuffer {:#CreateReferenceFromBuffer}

 Creates a new reference. The object is not part of any commit. It must be
 associated with a key using `PutReference()`. The content of the reference
 will be the content of the buffer.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
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

### StartTransaction {:#StartTransaction}

 Transactions allow the client to ensures changes are seen atomically by
 observers of this page. Once a transaction is started with
 `StartTransaction()`, every call to `Put(...)` and `Delete(...)` will not
 be visible until either `Commit()` is called, and all changes are applied
 in a single commit, or `Rollback()` is called and all changes are
 discarded.

 Parallel transactions on the same *page connection* are not allowed, and
 calling `StartTransaction()` when a transaction is already in progress
 returns an error. However, a client is free to connect to the same page
 multiple times, and run parallel transactions on the same page using
 separate connections. In this case, committing each transaction creates
 divergent commits, which are later subject to conflict resolution.

 When a transaction is in progress, the page content visible *on this page
 connection* is pinned to the state from when `StartTransaction()` was
 called. In particular, no watch notifications are delivered, and the
 conflict resolution is not invoked while the transaction is in progress. If
 conflicting changes are made or synced while the transaction is in
 progress, conflict resolution is invoked after the transaction is
 committed.

 Starting a transaction will block until all watchers registered on this
 page connection have received the current page state, ie. the one that
 will be used as the base of the transaction. Put (with all its variants)
 and Delete calls may be pipelined while StartTransaction() is pending and
 will be taken into account in the transaction while it is pending.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Commit {:#Commit}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Rollback {:#Rollback}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SetSyncStateWatcher {:#SetSyncStateWatcher}

 Sets a watcher to track the synchronisation state of this page. The
 current state is immediately sent to the watcher when this method is
 called.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#SyncWatcher'>SyncWatcher</a></code>
            </td>
        </tr></table>



### WaitForConflictResolution {:#WaitForConflictResolution}

 Waits until all conflicts are resolved before calling the callback.
 The client can call this method multiple times, even before the previous
 calls are completed. Callbacks will be executed in the order they were
 added and indicate whether a merge happened between the callback
 registration and its execution.
 If there are no pending conflicts at the time this is called, the callback
 gets executed right away.

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

## PageSnapshot {:#PageSnapshot}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#255)*

 The content of a page at a given time. Closing the connection to a `Page`
 interface closes all `PageSnapshot` interfaces it created. The contents
 provided by this interface are limited to the prefix provided to the
 Page.GetSnapshot() call.

### Sync {:#Sync}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### GetEntries {:#GetEntries}

 Returns the entries in the page with keys greater or equal to `key_start`
 using the lexicographic order. If `key_start` is empty, all entries are
 returned. If the result fits in a single fidl message, `next_token` will
 be equal to NULL. Otherwise, `next_token` will have a non-NULL value. To
 retrieve the remaining results, another call to `GetEntries` should be
 made, initializing the optional `token` argument with the value of
 `next_token` returned in the previous call. `next_token` will not be
 NULL as long as there are more results and NULL once finished.
 Only `EAGER` values are guaranteed to be returned inside `entries`.
 Missing `LAZY` values can be retrieved over the network using Fetch().
 The returned `entries` are sorted by `key`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key_start</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
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
                <code>vector&lt;<a class='link' href='#Entry'>Entry</a>&gt;[65536]</code>
            </td>
        </tr><tr>
            <td><code>next_token</code></td>
            <td>
                <code><a class='link' href='#Token'>Token</a>?</code>
            </td>
        </tr></table>

### GetEntriesInline {:#GetEntriesInline}

 Same as `GetEntries()`. The connection will be closed with a
 `ZX_ERR_BAD_STATE` epitaph if a value does not fit in a FIDL message.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key_start</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
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
                <code>vector&lt;<a class='link' href='#InlinedEntry'>InlinedEntry</a>&gt;[65536]</code>
            </td>
        </tr><tr>
            <td><code>next_token</code></td>
            <td>
                <code><a class='link' href='#Token'>Token</a>?</code>
            </td>
        </tr></table>

### GetKeys {:#GetKeys}

 Returns the keys of all entries in the page which are greater or equal to
 `key_start` using the lexicographic order. If `key_start` is empty, all
 keys are returned. The returned `keys` are sorted. If the result fits in
 a single fidl message, `next_token` will be equal to NULL. Otherwise,
 `next_token` will have a non-NULL value. To retrieve the remaining
 results, another call to `GetKeys` should be made, initializing the
 optional `token` argument with the value of `next_token` returned in the
 previous call. `next_token` will not be NULL as long as there are more
 results and NULL once finished.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key_start</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
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
                <code>vector&lt;vector&gt;[65536]</code>
            </td>
        </tr><tr>
            <td><code>next_token</code></td>
            <td>
                <code><a class='link' href='#Token'>Token</a>?</code>
            </td>
        </tr></table>

### Get {:#Get}

 Returns the value of a given key.
 Only `EAGER` values are guaranteed to be returned. Calls when the value is
 `LAZY` and not available will return a `NEEDS_FETCH` status. The value can
 be retrieved over the network using a Fetch() call.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
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

### GetInline {:#GetInline}

 Returns the value of a given key if it fits in a FIDL message.
 The connection will be closed with a `ZX_ERR_BAD_STATE` epitaph if the
 value does not fit in a FIDL message.
 See `Get()` for additional information.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
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

### Fetch {:#Fetch}

 Fetches the value of a given key, over the network if not already present
 locally. `NETWORK_ERROR` is returned if the download fails (e.g.: network
 is not available).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
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

### FetchPartial {:#FetchPartial}

 Fetches the value of a given key, over the network if not already present
 locally, and returns a shared handle of a part of the value of a given
 key, starting at the position that is specified by `offset`. If `offset`
 is less than 0, starts at `-offset` from the end of the value.
 Returns at most `max_size` bytes. If `max_size` is less than 0, returns
 everything.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
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

## PageWatcher {:#PageWatcher}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#341)*

 Interface to watch changes to a page. The client will receive changes made by
 itself, as well as other clients or synced from other devices. The contents
 of a transaction will never be split across multiple OnChange() calls, but
 the contents of multiple transactions may be merged into one OnChange() call.

### OnChange {:#OnChange}

 Called for changes made on the page. If the result fits in a single fidl
 message, `result_state` will be `COMPLETED`. Otherwise, OnChange will be
 called multiple times and `result_state` will be `PARTIAL_STARTED` the
 first time, `PARTIAL_CONTINUED` the following ones and finally
 `PARTIAL_COMPLETED` on the last call. No new OnChange() call will be made
 while the previous one is still active. If clients are interested in the
 full content of the page at the time of the change, they can request a
 PageSnapshot in the callback. This request is optional and can be requested
 in any partial (started, continued or completed) and/or COMPLETED OnChange
 call. In any case, all requests made on a sequence of OnChange calls for
 the same page change, will always return the same snapshot: the one
 including all changes.

 Note that calls to Page.StartTransaction() on the page connection on which
 the watcher was registered will block until all OnChange() calls have
 finished.

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

## ConflictResolverFactory {:#ConflictResolverFactory}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#365)*

 This interface lets clients control the conflict resolution policy of the
 ledger. It allows them to either use pre-defined policies, or provide their
 own implementation. This can be decided on a page-by-page basis.

### GetPolicy {:#GetPolicy}

 Returns the conflict resolution policy for the given page.

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

### NewConflictResolver {:#NewConflictResolver}

 Returns a `ConflictResolver` to use for the given page. This will only be
 called if `GetPolicy` for the same page returned `AUTOMATIC_WITH_FALLBACK`
 or `CUSTOM`.

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



## MergeResultProvider {:#MergeResultProvider}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#448)*

 A merge result provider, obtained from `ConflictResolver.Resolve()`. Can be
 used to retrieve data about the conflict, and provide the merge result. When
 all changes have been sent, `Done()` should be called to mark the end of
 incoming merge changes.

### Sync {:#Sync}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### GetFullDiff {:#GetFullDiff}

 `GetFullDiff` returns the set of all key/value pairs (entries) that
 have been modified between the common ancestor (see
 `ConflictResolver.Resolve()`) and the left and right branches.

 Values of `LAZY` keys may not be present on the device. In that case, the
 corresponding Value objects within DiffEntry will have a NULL `value`
 field. If needed, `left` and `right`, provided by the
 `ConflictResolver.Resolve()` method can be used by clients to Fetch these
 values. If a key is not present at all in one of the branches, its
 corresponding Value object will be NULL.

 The first call to get the `DiffEntry`s should be done using a NULL
 token. If the result does not fit in a single fidl message, `next_token`
 will have a non-NULL value, which can be used to retrieve the rest of
 the results by calling `GetFullDiff()` with that token.

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
                <code>vector&lt;<a class='link' href='#DiffEntry'>DiffEntry</a>&gt;[65536]</code>
            </td>
        </tr><tr>
            <td><code>next_token</code></td>
            <td>
                <code><a class='link' href='#Token'>Token</a>?</code>
            </td>
        </tr></table>

### GetConflictingDiff {:#GetConflictingDiff}

 `GetConflictingDiff` returns the set of all key/value pairs that were
 modified on both sides to different values, or deleted on one side and
 modified on the other.

 It behaves like `GetFullDiff` otherwise.

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
                <code>vector&lt;<a class='link' href='#DiffEntry'>DiffEntry</a>&gt;[65536]</code>
            </td>
        </tr><tr>
            <td><code>next_token</code></td>
            <td>
                <code><a class='link' href='#Token'>Token</a>?</code>
            </td>
        </tr></table>

### Merge {:#Merge}

 Once the result of the merge has been computed `Merge()` can be called with
 all changes that resolve this conflict. If the result does not fit in a
 single fidl message, `Merge()` can be called multiple times. If any of the
 `Merge()` calls fails, i.e. `status` is not `OK`, all following calls will
 fail with the same error.

 If a key/value pair is sent multiple times in one or several `Merge()`
 call, only the last pair is taken into account.

 For all keys for which no merged value has been set (either here or
 through `MergeNonConflictingEntries()` below), the left value will be
 used. It is thus not necessary to send a MergedValue with a `LEFT` value
 source, unless to overwrite a previous MergedValue.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>merge_changes</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#MergedValue'>MergedValue</a>&gt;[65536]</code>
            </td>
        </tr></table>



### MergeNonConflictingEntries {:#MergeNonConflictingEntries}

 Automatically merges all non conflicting entries (entries that are
 modified on one side only or identical on both sides). This is equivalent
 to sending, through `Merge()`, a MergedValue with a `RIGHT` ValueSource
 for all non-conflicting keys modified on the right side. Conflicting
 entries can still be merged using the `Merge()` method.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Done {:#Done}

 Marks the end of merge changes to resolve this conflict. After `Done()` is
 called `MergeResultProvider` interface cannot be used any more.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## ConflictResolver {:#ConflictResolver}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#513)*

 Custom conflict resolver. If a `ConflictResolverFactory` is registered, and
 `ConflictResolverFactory.GetPolicy()` returns `AUTOMATIC_WITH_FALLBACK` or
 `CUSTOM` when called for a given page, the `NewConflictResolver` method will
 be called and will provide a `ConflictResolver`. Each time a custom conflict
 resolution is needed according to the chosen policy, the method
 `ConflictResolver.Resolve()` will be called, and the client will resolve the
 conflict by returning the final value for all conflicting keys as well as
 values for any other key that the client wants to change.

### Resolve {:#Resolve}

 Method called when a conflict needs to be resolved. `left` and `right`
 contain the snapshots of the two branches and `common_version` that of the
 lowest common ancestor. `common_version` can be NULL if this version is no
 longer available. The result of the merge can be given through the
 `result_provider`, using the left branch as the base of the merge commit,
 i.e. only key/value pairs that are different from the left version of the
 page should be sent. `result_provider` can also be used to retrieve the set
 of differences, i.e. conflicting keys, between the two versions.

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



## SyncWatcher {:#SyncWatcher}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#547)*

 Watcher interface to be implemented by clients who wish to follow the
 synchronization status of their ledger. SyncStateChanged callback must be
 called for new state change calls to be sent.

### SyncStateChanged {:#SyncStateChanged}


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

### Page_CreateReferenceFromSocket_Response {:#Page_CreateReferenceFromSocket_Response}
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

### Page_CreateReferenceFromBuffer_Response {:#Page_CreateReferenceFromBuffer_Response}
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

### PageSnapshot_Get_Response {:#PageSnapshot_Get_Response}
*generated*





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

### PageSnapshot_GetInline_Response {:#PageSnapshot_GetInline_Response}
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

### PageSnapshot_Fetch_Response {:#PageSnapshot_Fetch_Response}
*generated*





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

### PageSnapshot_FetchPartial_Response {:#PageSnapshot_FetchPartial_Response}
*generated*





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

### PageId {:#PageId}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#23)*



 Type of the identifier of a ledger Page.


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

### Reference {:#Reference}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#72)*



 A reference to a value.


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

### Token {:#Token}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#77)*



 A continuation token for paginated requests.


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

### Entry {:#Entry}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#220)*



 A pair of key and value.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a>?</code>
            </td>
            <td> `value` is null if the value requested has the LAZY priority and is not
 present on the device. Clients must use a Fetch call to retrieve the
 contents.
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

### InlinedValue {:#InlinedValue}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#230)*



 A value inlined in a message.


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

### InlinedEntry {:#InlinedEntry}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#235)*



 A pair of key and an inlined value.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>inlined_value</code></td>
            <td>
                <code><a class='link' href='#InlinedValue'>InlinedValue</a>?</code>
            </td>
            <td> `value` is null if the value requested has the LAZY priority and is not
 present on the device. Clients must use a Fetch call to retrieve the
 contents.
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

### PageChange {:#PageChange}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#324)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>timestamp</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> The timestamp of this change. This represents the number of nanoseconds
 since Unix epoch (i.e., since "1970-01-01 00:00 UTC", ignoring leap
 seconds). This value is set by the device that created the change and is
 not synchronized across devices. In particular, there is no guarantee that
 the `timestamp` of a follow up change is greater than this one's.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>changed_entries</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Entry'>Entry</a>&gt;[65536]</code>
            </td>
            <td> List of new and modified entries. `changed_entries` are sorted by `key`.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>deleted_keys</code></td>
            <td>
                <code>vector&lt;vector&gt;[65536]</code>
            </td>
            <td> List of deleted keys, in sorted order.
</td>
            <td>No default</td>
        </tr>
</table>

### MergedValue {:#MergedValue}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#415)*



 A change in the page. If `source` is set to `NEW`, `new_value` must be set
 to the new value. If `source` is not `NEW`, `new_value` and `priority` are
 ignored.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
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

### DiffEntry {:#DiffEntry}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#427)*



 An entry in a diff, as returned by `MergeResultProvider`.

 If `base`, `left` or `right` are NULL, this means that the corresponding key
 was not present in the base, left or right (respectively) branch of the
 page.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
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

### Value {:#Value}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#439)*



 A value in a DiffEntry.

 If the value is LAZY and is not present locally, `value` will be NULL. The
 value can be retrieved using a `Fetch()` call on a corresponding snapshot.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a>?</code>
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

### Page_CreateReferenceFromSocket_Response {:#Page_CreateReferenceFromSocket_Response}
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

### Page_CreateReferenceFromBuffer_Response {:#Page_CreateReferenceFromBuffer_Response}
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

### PageSnapshot_Get_Response {:#PageSnapshot_Get_Response}
*generated*





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

### PageSnapshot_GetInline_Response {:#PageSnapshot_GetInline_Response}
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

### PageSnapshot_Fetch_Response {:#PageSnapshot_Fetch_Response}
*generated*





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

### PageSnapshot_FetchPartial_Response {:#PageSnapshot_FetchPartial_Response}
*generated*





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

### PageId {:#PageId}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#23)*



 Type of the identifier of a ledger Page.


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

### Reference {:#Reference}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#72)*



 A reference to a value.


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

### Token {:#Token}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#77)*



 A continuation token for paginated requests.


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

### Entry {:#Entry}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#220)*



 A pair of key and value.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a>?</code>
            </td>
            <td> `value` is null if the value requested has the LAZY priority and is not
 present on the device. Clients must use a Fetch call to retrieve the
 contents.
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

### InlinedValue {:#InlinedValue}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#230)*



 A value inlined in a message.


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

### InlinedEntry {:#InlinedEntry}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#235)*



 A pair of key and an inlined value.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>inlined_value</code></td>
            <td>
                <code><a class='link' href='#InlinedValue'>InlinedValue</a>?</code>
            </td>
            <td> `value` is null if the value requested has the LAZY priority and is not
 present on the device. Clients must use a Fetch call to retrieve the
 contents.
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

### PageChange {:#PageChange}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#324)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>timestamp</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> The timestamp of this change. This represents the number of nanoseconds
 since Unix epoch (i.e., since "1970-01-01 00:00 UTC", ignoring leap
 seconds). This value is set by the device that created the change and is
 not synchronized across devices. In particular, there is no guarantee that
 the `timestamp` of a follow up change is greater than this one's.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>changed_entries</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Entry'>Entry</a>&gt;[65536]</code>
            </td>
            <td> List of new and modified entries. `changed_entries` are sorted by `key`.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>deleted_keys</code></td>
            <td>
                <code>vector&lt;vector&gt;[65536]</code>
            </td>
            <td> List of deleted keys, in sorted order.
</td>
            <td>No default</td>
        </tr>
</table>

### MergedValue {:#MergedValue}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#415)*



 A change in the page. If `source` is set to `NEW`, `new_value` must be set
 to the new value. If `source` is not `NEW`, `new_value` and `priority` are
 ignored.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
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

### DiffEntry {:#DiffEntry}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#427)*



 An entry in a diff, as returned by `MergeResultProvider`.

 If `base`, `left` or `right` are NULL, this means that the corresponding key
 was not present in the base, left or right (respectively) branch of the
 page.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
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

### Value {:#Value}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#439)*



 A value in a DiffEntry.

 If the value is LAZY and is not present locally, `value` will be NULL. The
 value can be retrieved using a `Fetch()` call on a corresponding snapshot.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a>?</code>
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

### ConflictResolutionWaitStatus {:#ConflictResolutionWaitStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#83)*

 The result of a wait for conflict resolution. See
 `Page.WaitForConflictResolution` for details.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NO_CONFLICTS</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>CONFLICTS_RESOLVED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### Priority {:#Priority}
Type: <code>uint32</code>

*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#209)*

 The synchronization priority of a reference.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>EAGER</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>LAZY</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### Error {:#Error}
Type: <code>uint32</code>

*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#245)*

 Error returned by the different PageSnapshot methods.


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

### ResultState {:#ResultState}
Type: <code>uint32</code>

*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#317)*



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

### MergePolicy {:#MergePolicy}
Type: <code>uint32</code>

*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#375)*

 Strategy to be used when resolving conflicts.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>LAST_ONE_WINS</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>AUTOMATIC_WITH_FALLBACK</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>CUSTOM</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### ValueSource {:#ValueSource}
Type: <code>uint32</code>

*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#406)*

 Source of the value used to resolve a conflict.

 `DELETE` deletes the key; `NEW` creates a new value; `RIGHT`
 selects the value from the right branch. If no value is sent, the left
 branch is selected.
 Used by `MergedValue`.


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

### SyncState {:#SyncState}
Type: <code>uint32</code>

*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#527)*

 Synchronization state.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>IDLE</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>PENDING</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>IN_PROGRESS</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERROR</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### ConflictResolutionWaitStatus {:#ConflictResolutionWaitStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#83)*

 The result of a wait for conflict resolution. See
 `Page.WaitForConflictResolution` for details.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NO_CONFLICTS</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>CONFLICTS_RESOLVED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### Priority {:#Priority}
Type: <code>uint32</code>

*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#209)*

 The synchronization priority of a reference.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>EAGER</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>LAZY</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### Error {:#Error}
Type: <code>uint32</code>

*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#245)*

 Error returned by the different PageSnapshot methods.


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

### ResultState {:#ResultState}
Type: <code>uint32</code>

*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#317)*



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

### MergePolicy {:#MergePolicy}
Type: <code>uint32</code>

*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#375)*

 Strategy to be used when resolving conflicts.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>LAST_ONE_WINS</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>AUTOMATIC_WITH_FALLBACK</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>CUSTOM</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### ValueSource {:#ValueSource}
Type: <code>uint32</code>

*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#406)*

 Source of the value used to resolve a conflict.

 `DELETE` deletes the key; `NEW` creates a new value; `RIGHT`
 selects the value from the right branch. If no value is sent, the left
 branch is selected.
 Used by `MergedValue`.


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

### SyncState {:#SyncState}
Type: <code>uint32</code>

*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#527)*

 Synchronization state.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>IDLE</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>PENDING</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>IN_PROGRESS</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERROR</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>





## **UNIONS**

### Page_CreateReferenceFromSocket_Result {:#Page_CreateReferenceFromSocket_Result}
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
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Page_CreateReferenceFromBuffer_Result {:#Page_CreateReferenceFromBuffer_Result}
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
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### PageSnapshot_Get_Result {:#PageSnapshot_Get_Result}
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

### PageSnapshot_GetInline_Result {:#PageSnapshot_GetInline_Result}
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

### PageSnapshot_Fetch_Result {:#PageSnapshot_Fetch_Result}
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

### PageSnapshot_FetchPartial_Result {:#PageSnapshot_FetchPartial_Result}
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

### BytesOrReference {:#BytesOrReference}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#395)*

 A value that is either small enough to be directly embedded in `bytes` or
 that is referenced by `reference`.

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

### Page_CreateReferenceFromSocket_Result {:#Page_CreateReferenceFromSocket_Result}
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
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Page_CreateReferenceFromBuffer_Result {:#Page_CreateReferenceFromBuffer_Result}
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
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### PageSnapshot_Get_Result {:#PageSnapshot_Get_Result}
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

### PageSnapshot_GetInline_Result {:#PageSnapshot_GetInline_Result}
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

### PageSnapshot_Fetch_Result {:#PageSnapshot_Fetch_Result}
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

### PageSnapshot_FetchPartial_Result {:#PageSnapshot_FetchPartial_Result}
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

### BytesOrReference {:#BytesOrReference}
*Defined in [fuchsia.ledger/ledger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#395)*

 A value that is either small enough to be directly embedded in `bytes` or
 that is referenced by `reference`.

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
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#14">NO_LINT</a></td>
            <td>
                    <code>65536</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#20">PAGE_ID_SIZE</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
            <td> Size in bytes of Page IDs.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#14">NO_LINT</a></td>
            <td>
                    <code>65536</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ledger/ledger.fidl#20">PAGE_ID_SIZE</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
            <td> Size in bytes of Page IDs.
</td>
        </tr>
    
</table>

