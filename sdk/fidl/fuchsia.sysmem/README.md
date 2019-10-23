[TOC]

# fuchsia.sysmem


## **PROTOCOLS**

## Allocator {#Allocator}
*Defined in [fuchsia.sysmem/allocator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/allocator.fidl#11)*

 Allocates system memory buffers.


### AllocateNonSharedCollection {#AllocateNonSharedCollection}

 Allocates a BufferCollection on behalf of a single client (aka initiator)
 who is also the only participant (from the point of view of sysmem).

 This call exists mainly for temp/testing purposes.  This call skips the
 BufferCollectionToken stage, so there's no way to allow another
 participant to specify its constraints.

 Real clients are encouraged to use AllocateSharedCollection() instead,
 and to let relevant participants directly convey their own constraints to
 sysmem.

 `constraints` indicates constraints on the buffer collection, such as how
 many buffers to allocate, buffer size constraints, etc.

 `collection` is the server end of the BufferCollection FIDL channel.  The
 client can call SetConstraints() and then WaitForBuffersAllocated() on
 the client end of this channel to specify constraints and then determine
 success/failure and get the BufferCollectionInfo_2 for the
 BufferCollection.  The client should also keep the client end of
 this channel open while using the BufferCollection, and should notice
 when this channel closes and stop using the BufferCollection ASAP.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>collection</code></td>
            <td>
                <code>request&lt;<a class='link' href='#BufferCollection'>BufferCollection</a>&gt;</code>
            </td>
        </tr></table>



### AllocateSharedCollection {#AllocateSharedCollection}

 Creates a logical BufferCollectionToken which can be shared among
 participants (using BufferCollectionToken.Duplicate()), and then
 converted into a BufferCollection using BindSharedCollection().

 Success/failure to populate the BufferCollection with buffers is
 determined via the BufferCollection interface.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>token_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#BufferCollectionToken'>BufferCollectionToken</a>&gt;</code>
            </td>
        </tr></table>



### BindSharedCollection {#BindSharedCollection}

 Convert a BufferCollectionToken into a connection to the logical
 BufferCollection.  The BufferCollection hasn't yet been populated with
 buffers - the participant must first also send SetConstraints() via the
 client end of buffer_collection.

 All BufferCollectionToken(s) duplicated from a logical
 BufferCollectionToken created via AllocateSharedCollection() must be
 turned in via BindSharedCollection() before the logical BufferCollection
 will be populated with buffers.

 `token` the client endpoint of a channel whose server end was sent to
 sysmem using AllocateSharedCollection or whose server end was sent to
 sysmem using BufferCollectionToken.Duplicate().  The token is being
 "exchanged" for a channel to the logical BufferCollection.

 `buffer_collection` the server end of a BufferCollection channel.  The
 sender retains the client end as usual.  The BufferCollection channel
 is a single participant's connection to the logical BufferCollection.
 There typically will be other participants with their own
 BufferCollection channel to the logical BufferCollection.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>token</code></td>
            <td>
                <code><a class='link' href='#BufferCollectionToken'>BufferCollectionToken</a></code>
            </td>
        </tr><tr>
            <td><code>buffer_collection_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#BufferCollection'>BufferCollection</a>&gt;</code>
            </td>
        </tr></table>



## BufferCollectionToken {#BufferCollectionToken}
*Defined in [fuchsia.sysmem/collection.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/collection.fidl#17)*

 A BufferCollectionToken is not a BufferCollection, but rather a way to
 identify a potential shared BufferCollection prior to the BufferCollection
 being allocated.

 We use a channel for the BufferCollectionToken instead of a single eventpair
 (pair) because this way we can detect error conditions like a participant
 dying mid-create.

### Duplicate {#Duplicate}

 The initiator or a participant can send Duplicate() as part of creating
 another participant-side handle to the same logical
 BufferCollectionToken.

 This method is used to hand the logical token to all participants so all
 participants can provide constraints to sysmem for the overall
 BufferCollection to achieve the goal of allocating buffers compatible
 with all participants.

 The Duplicate() message is intentionally available only on
 BufferCollectionToken not BufferCollection.

 The token is separate from BufferCollection so that participants contact
 sysmem directly, so that participants are only trusting their environment
 for who sysmem is (fake token mitigation), not an initiator.  Only after
 successful BindSharedCollection does a participant know that the token
 was a real sysmem token.  In contrast, if we had Duplicate() directly on
 BufferCollection, an initiator could attempt to serve the
 BufferCollection channel itself, which would allow for some problematic
 possibilities.

 All the BufferCollectionToken channels of a logical token must be turned
 in via BindSharedCollection() for a BufferCollection to be successfully
 created.  Else the BufferCollection channel will close.

 When a client calls BindSharedCollection() to turn in a
 BufferCollectionToken, the server will process all Duplicate() messages
 before closing down the BufferCollectionToken.  This allows the client
 to Duplicate() and immediately turn in the BufferCollectionToken using
 BindSharedCollection, then later transfer the client end of token_request
 to another participant - the server will notice the existence of the
 token_request before considering this BufferCollectionToken fully closed.

 `rights_attenuation_mask` rights bits that are zero in this mask will be
 absent in the buffer VMO rights obtainable via the client end of
 token_request.  This allows an initiator or intermediary participant
 to attenuate the rights available to a participant.  This may not be the
 only mechanism that attenuates rights on the VMO handles obtainable via
 the client end of token_request.  This does not allow a participant
 to gain rights that the participant doesn't already have.

 `token_request` is the server end of a BufferCollectionToken channel.
 The client end of this channel acts as another handle to the same logical
 BufferCollectionToken.  Typically the sender of Duplicate() will transfer
 the client end corresponding to collection_request to a/another
 participant running in a separate process, but it's also fine for the
 additional logical participant to be in the same process.

 After sending one or more Duplicate() messages, and before sending the
 created tokens to other participants (or to other Allocator2 channels),
 the client should send a Sync() and wait for its response.  The Sync()
 call can be made on the token, or on the BufferCollection obtained by
 passing this token to BindSharedCollection().  Either will ensure that
 the server knows about the tokens created via Duplicate() before the
 other participant sends the token to the server via separate Allocator2
 channel.  If a client is using FIDL C generated code and doesn't want to
 block waiting for a response message, the other option is to notice
 arrival of the BufferCollectionEvents::OnBufferCollectionCreated() event
 after turning in this token for a BufferCollection.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rights_attenuation_mask</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>token_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#BufferCollectionToken'>BufferCollectionToken</a>&gt;</code>
            </td>
        </tr></table>



### Sync {#Sync}

 Ensure that previous Duplicate() messages have been received server side,
 so that it's safe to send the client end of token_request to another
 participant knowing the server will recognize the token when it's sent
 into BindSharedCollection by the other participant.

 Other options include waiting for each Duplicate() to complete
 individually, or calling Sync() on BufferCollection after this token has
 been turned in via BindSharedCollection(), or noticing arrival of
 BufferCollectionEvents::OnDuplicatedTokensKnownByServer().

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### Close {#Close}

 Normally a participant will convert the token into a BufferCollection
 view, but a particpant is also free to Close() the token (and then close
 the channel immediately or shortly later in response to server closing
 its end), which avoids causing LogicalBufferCollection failure.
 Normally an unexpected token channel close will cause
 LogicalBufferCollection failure.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## BufferCollection {#BufferCollection}
*Defined in [fuchsia.sysmem/collection.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/collection.fidl#132)*

 BufferCollection is a connection directly from a participant to sysmem re.
 a logical BufferCollection; typically the logical BufferCollection is shared
 with other participants.  In other words, an instance of the BufferCollection
 interface is a view of a "LogicalBufferCollection".

 This connection exists to facilitate async indication of when the logical
 BufferCollection has been populated with buffers.

 Also, the channel's closure by the server is an indication to the client
 that the client should close all VMO handles that were obtained from the
 BufferCollection ASAP.

 Also, this interface may in future allow specifying constraints in other
 ways, and may allow for back-and-forth negotiation of constraints to some
 degree.

 This interface may in future allow for more than 64 VMO handles per
 BufferCollection, but currently the limit is 64.

 This interface may in future allow for allocating/deallocating single
 buffers.

 Some initiators may wait a short duration until all old logical
 BufferCollection VMO handles have closed (or until the short duration times
 out) before allocating a new BufferCollection, to help control physical
 memory fragmentation and avoid overlap of buffer allocation lifetimes for
 the old and new collections. Collections can be large enough that it's worth
 avoiding allocation overlap (in time).

### SetEventSink {#SetEventSink}

 At least for now, the only way to get events from a BufferCollection is
 to set a reverse BufferCollectionEvents channel.  This can be sent up to
 once at any point during BufferCollection channel lifetime.  All events
 are one-shot events, and will be sent immediately via `events` if the
 one-shot event's condition has already become true (once true will stay
 true; only goes from false to true once).

 `events` is the client end of a BufferCollectionEvents which will be sent
 one-way messages indicating events relevant to this BufferCollection
 channel (some may be specific to this BufferCollection channel and some
 may be relevant to the overall logical BufferCollection).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>events</code></td>
            <td>
                <code><a class='link' href='#BufferCollectionEvents'>BufferCollectionEvents</a></code>
            </td>
        </tr></table>



### Sync {#Sync}

 See comments on BufferCollectionToken::Sync().

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### SetConstraints {#SetConstraints}

 Provide BufferCollectionConstraints to the logical BufferCollection.

 Participants with read but not write can only call SetConstraints() once.

 Participants with write can call SetConstraints() more than once.  The
 initial buffer allocation will use the constraints in the first call to
 SetConstraints().  Among other things, this allows a decoder to attempt
 to allocate a new buffer that's larger to hold an output frame that's
 larger.

 Sometimes the initiator is a participant only in the sense of wanting to
 keep an eye on success/failure to populate with buffers, and zx.status on
 failure.  In that case, `has_constraints` can be false, and `constraints`
 will be ignored.

 VMO handles will not be provided to the client that sends null
 constraints - that can be intentional for an initiator that doesn't need
 VMO handles.  Not having VMO handles doesn't prevent the initator from
 adjusting which portion of a buffer is considered valid and similar, but
 the initiator can't hold a VMO handle open to prevent the logical
 BufferCollection from cleaning up if the logical BufferCollection needs
 to go away regardless of the initiator's degree of involvement for
 whatever reason.

 For population of buffers to be attempted, all holders of a
 BufferCollection client channel need to call SetConstraints() before
 sysmem will attempt to allocate buffers.

 `has_constraints` if false, the constraints are effectively null, and
 `constraints` are ignored.  The sender of null constraints won't get any
 VMO handles in BufferCollectionInfo, but can still find out how many
 buffers were allocated and can still refer to buffers by their
 buffer_index.

 `constraints` are constraints on the buffer collection.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>has_constraints</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>constraints</code></td>
            <td>
                <code><a class='link' href='#BufferCollectionConstraints'>BufferCollectionConstraints</a></code>
            </td>
        </tr></table>



### WaitForBuffersAllocated {#WaitForBuffersAllocated}

 This request completes when buffers have been allocated, responds with
 some failure detail if allocation has been attempted but failed.

 The following must occur before buffers will be allocated:
   * All BufferCollectionToken(s) of the logical BufferCollectionToken
     must be turned in via BindSharedCollection().
   * All BufferCollection(s) of the logical BufferCollection must have had
     SetConstraints() sent to them.

 A caller using C generated FIDL code who wishes not to block a thread in
 a zx_channel_call() for a potentially fairly long duration on this
 message/response can use SetEventSink() and
 BufferCollectionEvents.OnBuffersPopulated() instead.

 This method is still legal to call despite use of OnBuffersPopulated(),
 but in that case the additional BufferCollectionInfo returned here will
 include handles that are redundant with other handles in the
 BufferCollectionInfo delivered via OnBuffersPopulated() (separate handle
 but same underlying VMO objects), so most clients that bother calling
 SetEventSink() will prefer to receive BufferCollectionInfo via
 OnBuffersPopulated().  This method is mostly here for clients that don't
 call SetEventSink().

 Returns `ZX_OK` if successful.
 Returns `ZX_ERR_NO_MEMORY` if the request is valid but cannot be
 fulfilled due to resource exhaustion.
 Returns `ZX_ERR_ACCESS_DENIED` if the caller is not permitted to
 obtain the buffers it requested.
 Returns `ZX_ERR_INVALID_ARGS` if the request is malformed.
 Returns `ZX_ERR_NOT_SUPPORTED` if request is valid but cannot be
 satisfied, perhaps due to hardware limitations.

 `buffer_collection_info` has the VMO handles and other related info.

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
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>buffer_collection_info</code></td>
            <td>
                <code><a class='link' href='#BufferCollectionInfo_2'>BufferCollectionInfo_2</a></code>
            </td>
        </tr></table>

### CheckBuffersAllocated {#CheckBuffersAllocated}

 This returns the same result code as WaitForBuffersAllocated if the
 buffer collection has been allocated or failed, or `ZX_ERR_UNAVAILABLE`
 if WaitForBuffersAllocated would block.

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
                <code>int32</code>
            </td>
        </tr></table>

### CloseSingleBuffer {#CloseSingleBuffer}

 The CloseBuffer() doesn't immediately force all VMO handles to that
 buffer to close, but it does close any handle held by sysmem, and does
 notify all participants of the desire to close the buffer at which point
 each participant that's listening may close their handle to the buffer.

 Only a particpant with write can do this.  Coordination among multiple
 participants with write is outside of the scope of this interface.

 `buffer_index` indicates which buffer to close.  If the buffer is already
 closed this has no effect (idempotent).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer_index</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### AllocateSingleBuffer {#AllocateSingleBuffer}

 This allocates a new buffer that is consistent with the most recent call
 to SetConstraints(), if possible.  If not possible, this indicates the
 failure via OnNewBufferAllocated().

 Only a participant with write can do this.  Coordination among multiple
 participants with write is outside the scope of this interface.

 The participant is (intentionally) never informed of other participant's
 constraints.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer_index</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### WaitForSingleBufferAllocated {#WaitForSingleBufferAllocated}

 Completes when AllocateBuffer is done.  Callers who wish to avoid
 blocking a thread while waiting can use OnAllocateSingleBufferDone()
 instead.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer_index</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>buffer_info</code></td>
            <td>
                <code><a class='link' href='#SingleBufferInfo'>SingleBufferInfo</a></code>
            </td>
        </tr></table>

### CheckSingleBufferAllocated {#CheckSingleBufferAllocated}

 A participant can use this message to have sysmem verify that this
 buffer_index exists.  This message is intentionally ignored by the
 server if the buffer_index _does_ exist.  In that case, the client will
 see OnAllocateSingleBufferDone() soon with status == `ZX_OK` (if the
 client hasn't already seen that message).  If on the other hand the
 buffer_index does not exist, this message causes the server to send
 OnAllocateSingleBufferDone() with status == `ZX_ERR_NOT_FOUND`.  A
 particpant will typically use this when the participant receives a new
 buffer_index that the participant doesn't yet know about, to ensure that
 the participant won't be waiting forever for the
 OnAllocateSingleBufferDone() message regarding this buffer_index.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer_index</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### Close {#Close}

 The server handles unexpected failure of a BufferCollection by failing
 the whole LogicalBufferCollection.  Partly this is to expedite closing
 VMO handles.  If a participant would like to cleanly close a
 BufferCollection view without causing LogicalBufferCollection failure,
 the participant can send Close() before closing the client end of the
 BufferCollection channel.  If this is the last BufferCollection view, the
 LogicalBufferCollection will still go away.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## BufferCollectionEvents {#BufferCollectionEvents}
*Defined in [fuchsia.sysmem/collection.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/collection.fidl#285)*

 This interface intentionally doesn't include any event for
 OnOldBufferClosed(), because such an event could arrive at a participant too
 soon to be useful.  Instead, such an indication should be made in-band within
 FIDL interfaces that deliver packets to downstream participants.

### OnDuplicatedTokensKnownByServer {#OnDuplicatedTokensKnownByServer}

 See comments on BufferCollectionToken::Sync().

 This message only indicates that the server has reached the point where
 it knows about previously created tokens Duplicate()ed from the token
 used to create this BufferCollection.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### OnBuffersAllocated {#OnBuffersAllocated}

 This event inidicates that buffer allocation is over, whether succesful
 or failed.

 This event will eventually be sent by the server (unless the
 BufferCollection channel closes first).

 `status`:
 `ZX_OK` if successful.
 `ZX_ERR_NO_MEMORY` if the request is valid but cannot be fulfilled due to
 resource exhaustion.
 `ZX_ERR_ACCESS_DENIED` if the caller is not permitted to obtain the
 buffers it requested.
 `ZX_ERR_INVALID_ARGS` if the request is malformed.
 `ZX_ERR_NOT_SUPPORTED` if request is valid but cannot be satisfied,
 perhaps due to hardware limitations.

 `buffer_collection_info` The buffer information, including VMO handles.
 If `status` is not `ZX_OK`, `buffer_collection_info` is default
 initialized and contains no meaningful information.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>buffer_collection_info</code></td>
            <td>
                <code><a class='link' href='#BufferCollectionInfo_2'>BufferCollectionInfo_2</a></code>
            </td>
        </tr></table>



### OnAllocateSingleBufferDone {#OnAllocateSingleBufferDone}

 A participant can learn when a new buffer is allocated via this event.
 The only participant that will see a failing status is the participant
 that attempted the single buffer allocation.  Other participants will
 only see successful single buffer allocations.

 `status`:

 `ZX_OK` if successful.  This can be seen by any participant (whether
 sender of AllocateSingleBuffer() or not.)

 `ZX_ERR_NOT_FOUND` if the buffer_index sent via
 CheckSingleBufferAllocated() isn't known to the server.  This can be seen
 by any participant (whether sender of AllocateSingleBuffer() or not.)

 These error codes are only ever seen by the sender of
 AllocateSingleBuffer():

 `ZX_ERR_NO_MEMORY` if the request is valid but cannot be fulfilled due to
 resource exhaustion.
 `ZX_ERR_ACCESS_DENIED` if the caller is not permitted to obtain the
 buffers it requested.
 `ZX_ERR_INVALID_ARGS` if the request is malformed.
 `ZX_ERR_NOT_SUPPORTED` if request is valid but cannot be satisfied,
 perhaps due to hardware limitations.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>buffer_info</code></td>
            <td>
                <code><a class='link' href='#SingleBufferInfo'>SingleBufferInfo</a></code>
            </td>
        </tr></table>



## DriverConnector {#DriverConnector}
*Defined in [fuchsia.sysmem/driver_connector.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/driver_connector.fidl#26)*

 Once a channel with this interface is established to a driver (typically in
 advance), this interface allows asynchronously sending the server end of an
 Allocator channel which will be served by the driver.

 For now, the only FIDL interface directly served via normal devhost FIDL
 dispatching code by the sysmem driver is this interface.  Other sysmem
 interfaces are served by separate dispatching code primarily because we want
 to be able to establish channels async by sending the server channel toward
 the driver without needing a round-trip open and without managing the channel
 as a file descriptor.

 A secondary current reason tracked by ZX-3091 is that the current devhost
 dispatching code doesn't permit async processing of requests, which we want
 for proper functionining of at least the BufferCollection interface since
 that interface has requests that don't complete until the devhost has
 constraints from other participants.

### Connect {#Connect}

 This one-way message sends in the server end of an Allocator channel.

 `allocator_request` will be served by the sysmem driver (or the channel
 will close).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>allocator_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Allocator'>Allocator</a>&gt;</code>
            </td>
        </tr></table>



## Heap {#Heap}
*Defined in [fuchsia.sysmem/heap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/heap.fidl#13)*

 Manages resources on a specific sysmem heap.

 Needs Layout = "Simple" because used with "FIDL Simple C Bindings".

### AllocateVmo {#AllocateVmo}

 Request a new memory allocation of `size` on heap.
 For heaps which don't permit CPU access to the buffer data, this
 will create a VMO with an official size, but which never has any
 physical pages.  For such heaps, the VMO is effectively used as
 an opaque buffer identifier.

 Heaps should defer allocation of any associated resources until
 CreateResource(), because the caller of AllocateVmo() may simply
 delete the returned VMO with no further notification to the heap.
 In contrast, after CreateResource(), the caller guarantees that
 DestroyResource() or heap channel closure will occur.

 The caller guarantees that CreateResource() will be called prior
 to the returned VMO or any associated child VMO being used.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>size</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;?</code>
            </td>
        </tr></table>

### CreateResource {#CreateResource}

 Create resources and associate heap-specific resources with the
 passed-in VMO. Resources can be hardware specific and their
 lifetime don't have to be tied to `vmo`. `vmo` must be a VMO
 (or a direct or indirect child of a VMO) acquired through a call
 to AllocateVmo method above.  If the passed-in vmo is a child VMO,
 its size must match the size of the parent VMO created by
 AllocateVmo().  For heaps that permit CPU access, the passed-in
 VMO must not have a copy-on-write relationship with the parent
 VMO, but rather a pass-through relationship. Successful return
 status indicate that Heap has established a mapping between
 VMO and hardware specific resources.

 The returned id must be passed to DestroyResource() later when
 resources associated with VMO are no longer needed, unless the
 heap channel closes first.

 The heap must not own/keep a handle to VMO, or any derived child
 VMO, or any VMAR mapping to VMO, as any of those would keep VMO
 alive beyond all sysmem participant usages of the vmo; instead
 the heap can get the vmo's koid for the heap's mapping.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### DestroyResource {#DestroyResource}

 Destroy previously created resources.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## SecureMem {#SecureMem}
*Defined in [fuchsia.sysmem/secure_mem.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/secure_mem.fidl#31)*

 SecureMem

 The client is sysmem.  The server is securemem driver.

 TEE - Trusted Execution Environment.

 REE - Rich Execution Environment.

 Enables sysmem to call the securemem driver to get any secure heaps
 configured via the TEE (or via the securemem driver), and set any physical
 secure heaps configured via sysmem.

 Presently, dynamically-allocated secure heaps are configured via sysmem, as
 it starts quite early during boot and can successfully reserve contiguous
 physical memory.  Presently, fixed-location secure heaps are configured via
 TEE, as the plumbing goes from the bootloader to the TEE.  However, this
 protocol intentionally doesn't care which heaps are dynamically-allocated
 and which are fixed-location.


### GetPhysicalSecureHeaps {#GetPhysicalSecureHeaps}

 Gets the physical address and length of any secure heap whose physical
 range is configured via the TEE.

 Presently, these will be fixed physical addresses and lengths, with the
 location plumbed via the TEE.

 This is preferred over RegisterHeap() when there isn't any special
 heap-specific per-VMO setup or teardown required.

 The physical range must be secured/protected by the TEE before the
 securemem driver responds to this request with success.

 Sysmem should only call this once.  Returning zero heaps is not a
 failure.

 Errors:
  * ZX_ERR_BAD_STATE - called more than once.
  * ZX_ERR_INTERNAL - generic internal error (such as in communication
    with TEE which doesn't generate zx_status_t errors).
  * other errors are possible, such as from communication failures or
    server propagation of zx_status_t failures

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#SecureMem_GetPhysicalSecureHeaps_Result'>SecureMem_GetPhysicalSecureHeaps_Result</a></code>
            </td>
        </tr></table>

### SetPhysicalSecureHeaps {#SetPhysicalSecureHeaps}

 This request from sysmem to the securemem driver lets the TEE know the
 physical memory address and length of any secure heap whose location is
 configured/established via sysmem.

 Only sysmem can call this because only sysmem is handed the client end
 of a FIDL channel serving this protocol, via RegisterSecureMem().  The
 securemem driver is the server end of this protocol.

 Presently, these physical ranges will be dynamically-allocated by sysmem
 early during boot.

 The heap ID is included in case that's relevant to the securemem driver,
 for more informative log messages, and for consistency with
 GetPhysicalSecureHeaps().

 The securemem driver must configure all the provided ranges as secure
 with the TEE before responding to this message with success.

 For heaps configured via sysmem, both the HeapType and heap location are
 configured via sysmem, and ZX_ERR_INVALID_ARGS will be the result if the
 securemem driver determines that the number of heaps or HeapType(s) are
 not what's supported by the securemem driver.  Typically these aspects
 are essentially fixed for a given device, so this error would typically
 imply a configuration or plumbing problem.

 Sysmem should only call this once.

 Errors:
  * ZX_ERR_BAD_STATE - called more than once
  * ZX_ERR_INVALID_ARGS - unexpected heap count or unexpected heap
  * ZX_ERR_INTERNAL - generic internal error (such as in communication
    with TEE which doesn't generate zx_status_t errors).
  * other errors are possible, such as from communication failures or
    server propagation of zx_status_t failures

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>heaps</code></td>
            <td>
                <code><a class='link' href='#PhysicalSecureHeaps'>PhysicalSecureHeaps</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#SecureMem_SetPhysicalSecureHeaps_Result'>SecureMem_SetPhysicalSecureHeaps_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### BufferCollectionInfo {#BufferCollectionInfo}
*Defined in [fuchsia.sysmem/collections_deprecated.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/collections_deprecated.fidl#9)*



 Information about a buffer collection and its buffers.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>buffer_count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The number of buffers in the collection.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>format</code></td>
            <td>
                <code><a class='link' href='#BufferFormat'>BufferFormat</a></code>
            </td>
            <td> Describes how the contents of buffers are represented.
 All buffers within the collection have the same format.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>vmos</code></td>
            <td>
                <code>vmo[64]</code>
            </td>
            <td> VMO handles for each buffer in the collection.
 The VMOs are only present when the buffers are backed by VMOs.

 If present, all the VMOs after `buffer_count` are invalid handles.
 All buffer VMO handles have identical size and access rights.
 The VMO access rights are determined based on the usages which the
 client specified when allocating the buffer collection.  For example,
 a client which expressed a read-only usage will receive VMOs without
 write rights.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>vmo_size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The size of each VMO provided.
 This property is only present when the buffers are backed by VMOs.
</td>
            <td>0</td>
        </tr>
</table>

### BufferCollectionConstraints {#BufferCollectionConstraints}
*Defined in [fuchsia.sysmem/constraints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/constraints.fidl#16)*



 Constraints on BufferCollection parameters.  These constraints can be
 specified per-participant.  The sysmem service implements aggregation of
 constraints from multiple participants.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>usage</code></td>
            <td>
                <code><a class='link' href='#BufferUsage'>BufferUsage</a></code>
            </td>
            <td> The usage is only meant as a hint to help sysmem choose a more optimal
 PixelFormat or similar when multiple compatible options exist.

 When aggregating BufferCollectionConstraints, these values bitwise-OR.

 At least one usage bit must be specified unless the whole
 BufferCollectionConstraints is logically null due to !has_constraints.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>min_buffer_count_for_camping</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Per-participant minimum number of buffers that are needed for camping
 purposes.  A participant should specify a number for min_buffer_count
 that's >= the maximum number of buffers that the participant may
 concurrently camp on for any non-transient period of time.

 For example, a video decoder would specify (at least) the maximum number
 of reference frames + 1 frame currently being decoded into.

 A participant must not camp on more buffers than specified here (except
 very transiently) else processing may get stuck.

 When aggregating BufferCollectionConstraints, these values add.

 In testing scenarios, camping on more buffers than this for any
 significant duration may (ideally will) be flagged as a failure.  In
 testing scenarios, the participant may not be provided with more buffers
 than this concurrently.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>min_buffer_count_for_dedicated_slack</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Per-participant minimum number of buffers that are needed for slack
 reasons, for better overlap of processing / better performance.

 When aggregating BufferCollectionConstraints, these values add.

 A participant should typically specify 0 or 1 here - typically 0 is
 appropriate if min_buffer_count_for_camping is already enough to keep
 the participant busy 100% of the time when the participant is slightly
 behind, while 1 can be appropriate if 1 more buffer than strictly needed
 for min-camping reasons gives enough slack to stay busy 100% of the time
 (when slightly behind, vs. lower % without the extra buffer).

 In testing scenarios, this field may be forced to 0, and all
 participants are expected to continue to work without getting stuck.  If
 a buffer is needed for forward progress reasons, that buffer should be
 accounted for in min_buffer_count_for_camping.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>min_buffer_count_for_shared_slack</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Similar to min_buffer_count_for_dedicated_slack, except when aggregating
 these values max (instead of add).  The value here is not shared with
 any participant's min_buffer_count_for_dedicated_slack.

 A participant can specify > 0 here if a participant would like to ensure
 there's some slack overall, but doesn't need that slack to be dedicated.

 The choice whether to use min_buffer_count_for_dedicated_slack or
 min_buffer_count_for_shared_slack (or both) will typically be about the
 degree to which the extra slack improves performance.

 In testing scenarios, this field may be forced to 0, and all
 participants are expected to continue to work without getting stuck.  If
 a buffer is needed for forward progress reasons, that buffer should be
 accounted for in min_buffer_count_for_camping.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>min_buffer_count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> A particularly-picky participant may unfortunately need to demand a tight
 range of buffer_count, or even a specific buffer_count.  This field
 should remain 0 unless a participant really must set this field to
 constrain the overall BufferCollectionInfo_2.buffer_count.  Any such
 participant should still fill out the min_buffer_count_for_* fields
 above.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_buffer_count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> 0 is treated as 0xFFFFFFFF.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>has_buffer_memory_constraints</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Constraints on BufferCollectionSettings.buffer_settings.

 A participant that intends to specify image_format_constraints_count > 1
 will typically specify the minimum buffer size implicitly via
 image_format_constraints, and possibly specify only the max buffer size
 via buffer_memory_constraints.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>buffer_memory_constraints</code></td>
            <td>
                <code><a class='link' href='#BufferMemoryConstraints'>BufferMemoryConstraints</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>image_format_constraints_count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Optional constraints on the image format parameters of an image stored
 in a buffer of the BufferCollection.  This includes pixel format and
 image layout.  These constraints are per-pixel-format, so more than one
 is permitted.

 When aggregating, only pixel formats that are specified by all
 particpants with non-zero image_format_constraints_count (and non-Null)
 BufferCollectionConstraints) are retained.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>image_format_constraints</code></td>
            <td>
                <code>[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### VmoBuffer {#VmoBuffer}
*Defined in [fuchsia.sysmem/constraints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/constraints.fidl#111)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;?</code>
            </td>
            <td> The same VMO can be used by more than one CodecBuffer (only of the same
 buffer_lifetime_ordinal), but each vmo_handle must be a separate handle.

 The vmo field can be 0 if this is a VmoBuffer in BufferCollectionInfo_2
 that's at or beyond BufferCollectionInfo_2.buffer_count.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>vmo_usable_start</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Offset within the VMO of the first usable byte.  Must be < the VMO's size
 in bytes, and leave sufficient room for BufferMemorySettings.size_bytes
 before the end of the VMO.
</td>
            <td>No default</td>
        </tr>
</table>

### BufferCollectionInfo_2 {#BufferCollectionInfo_2}
*Defined in [fuchsia.sysmem/constraints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/constraints.fidl#127)*



 Information about a buffer collection and its buffers.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>buffer_count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> If this is the initial buffer collection allocation, this is the total
 number of buffers.  If this is a single buffer allocation, this is zero,
 and the rest of the fields only apply to the single buffer.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>settings</code></td>
            <td>
                <code><a class='link' href='#SingleBufferSettings'>SingleBufferSettings</a></code>
            </td>
            <td> These settings apply to all the buffers in the inital buffer allocation.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>buffers</code></td>
            <td>
                <code>[64]</code>
            </td>
            <td> VMO handles (and vmo_usable_start offset) for each buffer in the
 collection.

 If present, all the VMOs at or after index `buffer_count` are invalid (0)
 handles.

 All buffer VMO handles have identical size and access rights.  The size
 is in settings.buffer_settings.size_bytes.

 The VMO access rights are determined based on the usages which the
 client specified when allocating the buffer collection.  For example,
 a client which expressed a read-only usage will receive VMOs without
 write rights.  In addition, the rights can be attenuated by the parameter
 to BufferCollectionToken.Duplicate() calls.
</td>
            <td>No default</td>
        </tr>
</table>

### SingleBufferInfo {#SingleBufferInfo}
*Defined in [fuchsia.sysmem/constraints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/constraints.fidl#153)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>settings</code></td>
            <td>
                <code><a class='link' href='#SingleBufferSettings'>SingleBufferSettings</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='#VmoBuffer'>VmoBuffer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SingleBufferSettings {#SingleBufferSettings}
*Defined in [fuchsia.sysmem/constraints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/constraints.fidl#162)*



 After the initial buffer allocation, it's allowed to close old buffers and
 allocate new buffers.  When a new buffer is allocated its settings can differ
 from the rest of the buffers in the collection, and the single buffer's
 settings are delivered via OnSingleBufferAllocated() using this struct:


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>buffer_settings</code></td>
            <td>
                <code><a class='link' href='#BufferMemorySettings'>BufferMemorySettings</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>has_image_format_constraints</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Buffers holding data that is not uncompressed image data will not have
 this field set.  Buffers holding data that is uncompressed image data
 _may_ have this field set.

 At least for now, changing the PixelFormat requires re-allocating
 buffers.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>image_format_constraints</code></td>
            <td>
                <code><a class='link' href='#ImageFormatConstraints'>ImageFormatConstraints</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### BufferMemoryConstraints {#BufferMemoryConstraints}
*Defined in [fuchsia.sysmem/constraints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/constraints.fidl#191)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>min_size_bytes</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>0</td>
        </tr><tr>
            <td><code>max_size_bytes</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>4294967295</td>
        </tr><tr>
            <td><code>physically_contiguous_required</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>false</td>
        </tr><tr>
            <td><code>secure_required</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, at least one participant requires secure memory.

 When aggregating BufferCollectionConstraints, these values boolean-OR.
</td>
            <td>false</td>
        </tr><tr>
            <td><code>ram_domain_supported</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> By default, participants must ensure the CPU can read or write data to
 the buffer without cache operations. If they support using the RAM
 domain, data must be available in RAM (with CPU cache state such that
 the RAM data won't get corrupted by a dirty CPU cache line writing
 incorrect data to RAM), and a consumer reading using the CPU must
 invalidate CPU cache before reading (the producer doesn't guarantee
 zero stale "clean" cache lines)
</td>
            <td>false</td>
        </tr><tr>
            <td><code>cpu_domain_supported</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>true</td>
        </tr><tr>
            <td><code>inaccessible_domain_supported</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>false</td>
        </tr><tr>
            <td><code>heap_permitted_count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Optional heap constraints. Participants that don't care which heap
 memory is allocated on should leave this field 0.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>heap_permitted</code></td>
            <td>
                <code>[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### BufferMemorySettings {#BufferMemorySettings}
*Defined in [fuchsia.sysmem/constraints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/constraints.fidl#232)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>size_bytes</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>is_physically_contiguous</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>is_secure</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>coherency_domain</code></td>
            <td>
                <code><a class='link' href='#CoherencyDomain'>CoherencyDomain</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>heap</code></td>
            <td>
                <code><a class='link' href='#HeapType'>HeapType</a></code>
            </td>
            <td> The specific heap from which buffers are allocated.
 See above in this file for heap identifier values.
</td>
            <td>No default</td>
        </tr>
</table>

### ImageFormatConstraints {#ImageFormatConstraints}
*Defined in [fuchsia.sysmem/constraints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/constraints.fidl#244)*



 Describes constraints on layout of image data in buffers.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>pixel_format</code></td>
            <td>
                <code><a class='link' href='#PixelFormat'>PixelFormat</a></code>
            </td>
            <td> The PixelFormat for which the following constraints apply.  A
 participant may have more than one PixelFormat that's supported, in
 which case that participant can use a list of ImageFormatConstraints
 with an entry per PixelFormat.  It's not uncommon for the other fields
 of ImageFormatConstraints to vary by PixelFormat - for example for a
 linear format to support smaller max size than a tiled format.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>color_spaces_count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Empty is an error.  Redundant entries are an error.  Arbitrary ordering
 is not an error.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>color_space</code></td>
            <td>
                <code>[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>min_coded_width</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Minimum permitted width in pixels.

 For example a video decoder participant may set this field to the
 minimum coded_width that might potentially be specified by a stream.  In
 contrast, required_min_coded_width would be set to the current
 coded_width specified by the stream.  While min_coded_width aggregates
 by taking the max, required_min_coded_width aggregates by taking the
 min.

 See also required_min_coded_width.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_coded_width</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Maximum width in pixels.  For example Scenic may set this field
 (directly or via sub-participants) to the maximum width that can be
 composited.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>min_coded_height</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Minimum height in pixels.  For example a video decoder participant may
 set this field to the coded_height specified by a stream.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_coded_height</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Maximum height in pixels.  For example Scenic may set this field
 (directly or via sub-participants) to the maximum height that can be
 composited.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>min_bytes_per_row</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Must be >= the value implied by min_coded_width for plane 0.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_bytes_per_row</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Must be >= the value implied by max_coded_width for plane 0.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_coded_width_times_coded_height</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The max image area in pixels is limited indirectly via
 BufferSettings.size_bytes, and can also be enforced directly via this
 field.
</td>
            <td>4294967295</td>
        </tr><tr>
            <td><code>layers</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Number of layers within a multi-layered image.
 Defaults to 1 if not specified.
</td>
            <td>1</td>
        </tr><tr>
            <td><code>coded_width_divisor</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> coded_width % width_divisor must be 0.
</td>
            <td>1</td>
        </tr><tr>
            <td><code>coded_height_divisor</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> coded_height % height_divisor must be 0.
</td>
            <td>1</td>
        </tr><tr>
            <td><code>bytes_per_row_divisor</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> bytes_per_row % bytes_per_row_divisor must be 0.
</td>
            <td>1</td>
        </tr><tr>
            <td><code>start_offset_divisor</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> vmo_usable_start % start_offset_divisor must be 0.
</td>
            <td>1</td>
        </tr><tr>
            <td><code>display_width_divisor</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> display_width % display_width_divisor must be 0.
</td>
            <td>1</td>
        </tr><tr>
            <td><code>display_height_divisor</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> display_height % display_height_divisor must be 0.
</td>
            <td>1</td>
        </tr><tr>
            <td><code>required_min_coded_width</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> required_ dimension bounds.

 In contrast to the corresponding fields without "required_" at the
 start, these fields (when set to non-zero values) express a requirement
 that the resulting aggregated non-required_ fields specify a space that
 fully contain the space expressed by each participant's required_
 fields.

 For example, a producer video decoder is perfectly happy for the
 consumer to be willing to accept anything, and the video decoder doesn't
 really want to constrain the potential space of dimensions that might be
 seen in a stream and may be acceptable to the consumer, but the video
 decoder needs to ensure that the resulting dimension ranges contain
 at least the current dimensions decoded from the stream.

 Similarly, an initiator with a particular dynamic-dimension scenario in
 mind may wish to require up front that participants agree to handle at
 least the range of dimensions expected by the initiator in that
 scenario (else fail earlier rather than later, maybe trying again with
 smaller required_ space).

 It's much more common for a producer or initiator to set these fields
 than for a consumer to set these fields.

 While the non-required_ fields aggregate by taking the intersection, the
 required_ fields aggregate by taking the union.

 If set, the required_max_coded_width and required_max_coded_height will
 cause the allocated buffers to be large enough to hold an image that is
 required_max_coded_width * required_max_coded_height.

 TODO(dustingreen): Make it easier to allocate buffers of minimal size
 that can (optionally) also handle 90 degree rotated version of the max
 dimensions / alternate required bounds for another main aspect ratio.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>required_max_coded_width</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>required_min_coded_height</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>required_max_coded_height</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>required_min_bytes_per_row</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>required_max_bytes_per_row</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ImageFormat_2 {#ImageFormat_2}
*Defined in [fuchsia.sysmem/constraints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/constraints.fidl#358)*



 Describes how an image is represented.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>pixel_format</code></td>
            <td>
                <code><a class='link' href='#PixelFormat'>PixelFormat</a></code>
            </td>
            <td> Pixel format.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>coded_width</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Row width in pixels that exist in the buffer.  Must be >= display_width.
 Can be < the width implied by stride_bytes.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>coded_height</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Number of rows.  Must be >= display_height.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>bytes_per_row</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>display_width</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Row width in pixels that are to be displayed.  This can be <=
 coded_width.  Any cropping occurs on the right of the image (not left).
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>display_height</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Number of rows to be displayed.  This can be <= coded_height, with any
 cropping on the bottom (not top).
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>layers</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Number of layers within a multi-layered image.
</td>
            <td>1</td>
        </tr><tr>
            <td><code>color_space</code></td>
            <td>
                <code><a class='link' href='#ColorSpace'>ColorSpace</a></code>
            </td>
            <td> Color space.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>has_pixel_aspect_ratio</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> The pixel_aspect_ratio_width : pixel_aspect_ratio_height is the
 pixel aspect ratio (AKA sample aspect ratio aka SAR) for the luma
 (AKA Y) samples. A pixel_aspect_ratio of 1:1 mean square pixels. A
 pixel_aspect_ratio of 2:1 would mean pixels that are displayed twice
 as wide as they are tall. Codec implementation should ensure these
 two values are relatively prime by reducing the fraction (dividing
 both by GCF) if necessary.

 When has_pixel_aspect_ratio == false, pixel_aspect_ratio_width and
 pixel_aspect_ratio_height will both be 1, but in that case the
 pixel_aspect_ratio_width : pixel_aspect_ratio_height of 1:1 is just
 a very weak suggestion re. reasonable-ish handling, not in any way
 authoritative. In this case (or in any case really) the receiver of
 this message may have other OOB means to determine the actual
 pixel_aspect_ratio.
</td>
            <td>false</td>
        </tr><tr>
            <td><code>pixel_aspect_ratio_width</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>1</td>
        </tr><tr>
            <td><code>pixel_aspect_ratio_height</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>1</td>
        </tr>
</table>

### FormatModifier {#FormatModifier}
*Defined in [fuchsia.sysmem/format_modifier.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The upper 8 bits are a vendor code as allocated in FormatModifierVendor
 enum.  The lower 56 bits are vendor-defined.

 This field and the values that go in this field are defined this way for
 compatibility reasons.
</td>
            <td>No default</td>
        </tr>
</table>

### BufferFormat {#BufferFormat}
*Defined in [fuchsia.sysmem/formats_deprecated.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/formats_deprecated.fidl#9)*



 Describes how the contents of buffers are represented.
 Buffers of each type are described by their own tables.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>tag</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Since this struct used to be a single member union, we kept the tag
 to avoid any wire format changes. The tag must be set to `0`,
 no other value is correct.
</td>
            <td>0</td>
        </tr><tr>
            <td><code>image</code></td>
            <td>
                <code><a class='link' href='#ImageFormat'>ImageFormat</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### PixelFormat {#PixelFormat}
*Defined in [fuchsia.sysmem/image_formats.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/image_formats.fidl#11)*



 Describes how the pixels within an image are represented.
 Simple formats need only a type.
 Parametric pixel formats may require additional properties.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#PixelFormatType'>PixelFormatType</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>has_format_modifier</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> This bool effectively makes format_modifier optional, to satisfy
 'Layout = "Simple"', to satisify "FIDL Simple C Bindings".
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>format_modifier</code></td>
            <td>
                <code><a class='link' href='#FormatModifier'>FormatModifier</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ColorSpace {#ColorSpace}
*Defined in [fuchsia.sysmem/image_formats.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/image_formats.fidl#77)*



 Describes how the pixels within an image are meant to be presented.
 Simple color spaces need only a type.
 Parametric color spaces may require additional properties.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#ColorSpaceType'>ColorSpaceType</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ImageFormat {#ImageFormat}
*Defined in [fuchsia.sysmem/image_formats_deprecated.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/image_formats_deprecated.fidl#9)*



 Describes how an image is represented.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>width</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Row width in pixels.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Number of rows.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>layers</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Number of layers within a multi-layered image.
 Defaults to 1 if not specified.
</td>
            <td>1</td>
        </tr><tr>
            <td><code>pixel_format</code></td>
            <td>
                <code><a class='link' href='#PixelFormat'>PixelFormat</a></code>
            </td>
            <td> Pixel format.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>color_space</code></td>
            <td>
                <code><a class='link' href='#ColorSpace'>ColorSpace</a></code>
            </td>
            <td> Color space.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>planes</code></td>
            <td>
                <code>[4]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ImagePlane {#ImagePlane}
*Defined in [fuchsia.sysmem/image_formats_deprecated.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/image_formats_deprecated.fidl#29)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>byte_offset</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Byte offset of the start of the plane from the beginning of the image.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>bytes_per_row</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Stride in bytes per row.
 Only meaningful for linear buffer formats.
</td>
            <td>No default</td>
        </tr>
</table>

### ImageSpec {#ImageSpec}
*Defined in [fuchsia.sysmem/image_formats_deprecated.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/image_formats_deprecated.fidl#40)*



 Describes constraints for allocating images of some desired form.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>min_width</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Minimum width in pixels.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>min_height</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Minimum height in pixels.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>layers</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Number of layers within a multi-layered image.
 Defaults to 1 if not specified.
</td>
            <td>1</td>
        </tr><tr>
            <td><code>pixel_format</code></td>
            <td>
                <code><a class='link' href='#PixelFormat'>PixelFormat</a></code>
            </td>
            <td> Pixel format.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>color_space</code></td>
            <td>
                <code><a class='link' href='#ColorSpace'>ColorSpace</a></code>
            </td>
            <td> Color space.
</td>
            <td>No default</td>
        </tr>
</table>

### SecureMem_GetPhysicalSecureHeaps_Response {#SecureMem_GetPhysicalSecureHeaps_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>heaps</code></td>
            <td>
                <code><a class='link' href='#PhysicalSecureHeaps'>PhysicalSecureHeaps</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SecureMem_SetPhysicalSecureHeaps_Response {#SecureMem_SetPhysicalSecureHeaps_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### PhysicalSecureHeap {#PhysicalSecureHeap}
*Defined in [fuchsia.sysmem/secure_mem.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/secure_mem.fidl#92)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>heap</code></td>
            <td>
                <code><a class='link' href='#HeapType'>HeapType</a></code>
            </td>
            <td> This must be a HeapType that is secure/protected.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>physical_address</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Must be at least PAGE_SIZE aligned.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>size_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Must be at least PAGE_SIZE aligned.
</td>
            <td>No default</td>
        </tr>
</table>

### PhysicalSecureHeaps {#PhysicalSecureHeaps}
*Defined in [fuchsia.sysmem/secure_mem.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/secure_mem.fidl#108)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>heaps_count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Must be <= MAX_HEAPS_COUNT.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>heaps</code></td>
            <td>
                <code>[32]</code>
            </td>
            <td> Only the first heaps_count are meaningful.  The rest are ignored.
</td>
            <td>No default</td>
        </tr>
</table>

### BufferUsage {#BufferUsage}
*Defined in [fuchsia.sysmem/usages.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#9)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>none</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>cpu</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vulkan</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>display</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>video</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### HeapType {#HeapType}
Type: <code>uint64</code>

*Defined in [fuchsia.sysmem/constraints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/constraints.fidl#178)*

 Known heap types.
 Device specific types should have bit 60 set. Top order bit is reserved
 and should not be set.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SYSTEM_RAM</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>AMLOGIC_SECURE</code></td>
            <td><code>1152921504606912512</code></td>
            <td> Heap used for amlogic protected memory.
</td>
        </tr><tr>
            <td><code>AMLOGIC_SECURE_VDEC</code></td>
            <td><code>1152921504606912513</code></td>
            <td> Heap used for amlogic protected memory between decrypt and video decode.
</td>
        </tr><tr>
            <td><code>GOLDFISH_DEVICE_LOCAL</code></td>
            <td><code>1152921504606978048</code></td>
            <td> Heap used by goldfish vulkan for device-local memory.
</td>
        </tr></table>

### CoherencyDomain {#CoherencyDomain}
Type: <code>uint32</code>

*Defined in [fuchsia.sysmem/constraints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/constraints.fidl#226)*

 Inaccessible is only for cases where there is no CPU-based access to the
 buffers.  A secure_required buffer can still have CoherencyDomain Cpu or
 Ram even if the secure_required buffer can only be accessed by the CPU when
 the CPU is running in secure mode (or similar).  In contrast, device-local
 memory that isn't reachable from the CPU is CoherencyDomain Inaccessible,
 even if it's possible to cause a device (physical or virtual) to copy the
 data from the Inaccessible buffers to buffers that are visible to the CPU.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>CPU</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>RAM</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>INACCESSIBLE</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### PixelFormatType {#PixelFormatType}
Type: <code>uint32</code>

*Defined in [fuchsia.sysmem/image_formats.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/image_formats.fidl#28)*

 The ordering of the channels in the format name reflects how
 the actual layout of the channel.

 Each of these values is opinionated re. the color spaces that can be
 contained within (in contrast with Vulkan).


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INVALID</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>R8G8B8A8</code></td>
            <td><code>1</code></td>
            <td> RGB only, 8 bits per each of R/G/B/A sample
</td>
        </tr><tr>
            <td><code>BGRA32</code></td>
            <td><code>101</code></td>
            <td> 32bpp BGRA, 1 plane.  RGB only, 8 bits per each of B/G/R/A sample.
</td>
        </tr><tr>
            <td><code>I420</code></td>
            <td><code>102</code></td>
            <td> YUV only, 8 bits per Y sample
</td>
        </tr><tr>
            <td><code>M420</code></td>
            <td><code>103</code></td>
            <td> YUV only, 8 bits per Y sample
</td>
        </tr><tr>
            <td><code>NV12</code></td>
            <td><code>104</code></td>
            <td> YUV only, 8 bits per Y sample
</td>
        </tr><tr>
            <td><code>YUY2</code></td>
            <td><code>105</code></td>
            <td> YUV only, 8 bits per Y sample
</td>
        </tr><tr>
            <td><code>MJPEG</code></td>
            <td><code>106</code></td>
            <td></td>
        </tr><tr>
            <td><code>YV12</code></td>
            <td><code>107</code></td>
            <td> YUV only, 8 bits per Y sample
</td>
        </tr><tr>
            <td><code>BGR24</code></td>
            <td><code>108</code></td>
            <td> 24bpp BGR, 1 plane. RGB only, 8 bits per each of B/G/R sample
</td>
        </tr><tr>
            <td><code>RGB565</code></td>
            <td><code>109</code></td>
            <td> 16bpp RGB, 1 plane. 5 bits R, 6 bits G, 5 bits B
</td>
        </tr><tr>
            <td><code>RGB332</code></td>
            <td><code>110</code></td>
            <td> 8bpp RGB, 1 plane. 3 bits R, 3 bits G, 2 bits B
</td>
        </tr><tr>
            <td><code>RGB2220</code></td>
            <td><code>111</code></td>
            <td> 8bpp RGB, 1 plane. 2 bits R, 2 bits G, 2 bits B
</td>
        </tr><tr>
            <td><code>L8</code></td>
            <td><code>112</code></td>
            <td> 8bpp, Luminance-only.
</td>
        </tr></table>

### ColorSpaceType {#ColorSpaceType}
Type: <code>uint32</code>

*Defined in [fuchsia.sysmem/image_formats.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/image_formats.fidl#107)*

 This list has a separate entry for each variant of a color space standard.

 For this reason, should we ever add support for the RGB variant of 709, for
 example, we'd add a separate entry to this list for that variant.  Similarly
 for the RGB variants of 2020 or 2100.  Similarly for the YcCbcCrc variant of
 2020.  Similarly for the ICtCp variant of 2100.

 A given ColorSpaceType may permit usage with a PixelFormatType(s) that
 provides a bits-per-sample that's compatible with the ColorSpaceType's
 official spec.  Not all spec-valid combinations are necessarily supported.
 See ImageFormatIsSupportedColorSpaceForPixelFormat() for the best-case degree
 of support, but a "true" from that function doesn't guarantee that any given
 combination of participants will all support the desired combination of
 ColorSpaceType and PixelFormatType.

 The sysmem service helps find a mutually supported combination and allocate
 suitable buffers.

 A ColorSpaceType's spec is not implicitly extended to support
 outside-the-standard bits-per-sample (R, G, B, or Y sample).  For example,
 for 2020 and 2100, 8 bits-per-Y-sample is not supported (by sysmem), because
 8 bits-per-Y-sample is not in the spec for 2020 or 2100.  A sysmem
 participant that attempts to advertise support for a PixelFormat + ColorSpace
 that's non-standard will cause sysmem to reject the combo and fail to
 allocate (intentionally, to strongly discourage specifying
 insufficiently-defined combos).


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INVALID</code></td>
            <td><code>0</code></td>
            <td> Not a valid color space type.
</td>
        </tr><tr>
            <td><code>SRGB</code></td>
            <td><code>1</code></td>
            <td> sRGB
</td>
        </tr><tr>
            <td><code>REC601_NTSC</code></td>
            <td><code>2</code></td>
            <td> 601 NTSC ("525 line") YCbCr primaries, narrow
</td>
        </tr><tr>
            <td><code>REC601_NTSC_FULL_RANGE</code></td>
            <td><code>3</code></td>
            <td> 601 NTSC ("525 line") YCbCr primaries, wide
</td>
        </tr><tr>
            <td><code>REC601_PAL</code></td>
            <td><code>4</code></td>
            <td> 601 PAL ("625 line") YCbCr primaries, narrow
</td>
        </tr><tr>
            <td><code>REC601_PAL_FULL_RANGE</code></td>
            <td><code>5</code></td>
            <td> 601 PAL ("625 line") YCbCr primaries, wide
</td>
        </tr><tr>
            <td><code>REC709</code></td>
            <td><code>6</code></td>
            <td> 709 YCbCr (not RGB)
</td>
        </tr><tr>
            <td><code>REC2020</code></td>
            <td><code>7</code></td>
            <td> 2020 YCbCr (not RGB, not YcCbcCrc)
</td>
        </tr><tr>
            <td><code>REC2100</code></td>
            <td><code>8</code></td>
            <td> 2100 YCbCr (not RGB, not ICtCp)
</td>
        </tr></table>





## **UNIONS**

### SecureMem_GetPhysicalSecureHeaps_Result {#SecureMem_GetPhysicalSecureHeaps_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#SecureMem_GetPhysicalSecureHeaps_Response'>SecureMem_GetPhysicalSecureHeaps_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### SecureMem_SetPhysicalSecureHeaps_Result {#SecureMem_SetPhysicalSecureHeaps_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#SecureMem_SetPhysicalSecureHeaps_Response'>SecureMem_SetPhysicalSecureHeaps_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#16">FORMAT_MODIFIER_NONE</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#18">FORMAT_MODIFIER_VENDOR_NONE</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#19">FORMAT_MODIFIER_VENDOR_INTEL</a></td>
            <td>
                    <code>72057594037927936</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#20">FORMAT_MODIFIER_VENDOR_AMD</a></td>
            <td>
                    <code>144115188075855872</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#21">FORMAT_MODIFIER_VENDOR_NVIDIA</a></td>
            <td>
                    <code>216172782113783808</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#22">FORMAT_MODIFIER_VENDOR_SAMSUNG</a></td>
            <td>
                    <code>288230376151711744</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#23">FORMAT_MODIFIER_VENDOR_QCOM</a></td>
            <td>
                    <code>360287970189639680</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#24">FORMAT_MODIFIER_VENDOR_VIVANTE</a></td>
            <td>
                    <code>432345564227567616</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#25">FORMAT_MODIFIER_VENDOR_BROADCOM</a></td>
            <td>
                    <code>504403158265495552</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#26">FORMAT_MODIFIER_VENDOR_ARM</a></td>
            <td>
                    <code>576460752303423488</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#28">FORMAT_MODIFIER_VALUE_RESERVED</a></td>
            <td>
                    <code>72057594037927935</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#30">FORMAT_MODIFIER_INVALID</a></td>
            <td>
                    <code><a class='link' href='#FORMAT_MODIFIER_VALUE_RESERVED'>FORMAT_MODIFIER_VALUE_RESERVED</a></code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#32">FORMAT_MODIFIER_LINEAR</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#39">FORMAT_MODIFIER_INTEL_I915_X_TILED</a></td>
            <td>
                    <code>72057594037927937</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#40">FORMAT_MODIFIER_INTEL_I915_Y_TILED</a></td>
            <td>
                    <code>72057594037927938</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#41">FORMAT_MODIFIER_INTEL_I915_YF_TILED</a></td>
            <td>
                    <code>72057594037927939</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#56">FORMAT_MODIFIER_ARM_AFBC_16x16</a></td>
            <td>
                    <code>576460752303423489</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#57">FORMAT_MODIFIER_ARM_AFBC_32x8</a></td>
            <td>
                    <code>576460752303423490</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/secure_mem.fidl#105">MAX_HEAPS_COUNT</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#21">noneUsage</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#25">cpuUsageRead</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#26">cpuUsageReadOften</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#27">cpuUsageWrite</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#28">cpuUsageWriteOften</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#32">vulkanUsageTransferSrc</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#33">vulkanUsageTransferDst</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#34">vulkanUsageSampled</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#35">vulkanUsageStorage</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#36">vulkanUsageColorAttachment</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#37">vulkanUsageStencilAttachment</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#38">vulkanUsageTransientAttachment</a></td>
            <td>
                    <code>64</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#39">vulkanUsageInputAttachment</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#42">displayUsageLayer</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#43">displayUsageCursor</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#47">videoUsageHwDecoder</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#48">videoUsageHwEncoder</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#51">videoUsageHwProtected</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#52">videoUsageCapture</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#65">videoUsageDecryptorOutput</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    
</table>

