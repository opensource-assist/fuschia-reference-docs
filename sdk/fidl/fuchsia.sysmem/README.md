[TOC]

# fuchsia.sysmem


## **PROTOCOLS**

## Allocator {#Allocator}
*Defined in [fuchsia.sysmem/allocator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/allocator.fidl#11)*

<p>Allocates system memory buffers.</p>

### AllocateNonSharedCollection {#AllocateNonSharedCollection}

<p>Allocates a BufferCollection on behalf of a single client (aka initiator)
who is also the only participant (from the point of view of sysmem).</p>
<p>This call exists mainly for temp/testing purposes.  This call skips the
BufferCollectionToken stage, so there's no way to allow another
participant to specify its constraints.</p>
<p>Real clients are encouraged to use AllocateSharedCollection() instead,
and to let relevant participants directly convey their own constraints to
sysmem.</p>
<p><code>constraints</code> indicates constraints on the buffer collection, such as how
many buffers to allocate, buffer size constraints, etc.</p>
<p><code>collection</code> is the server end of the BufferCollection FIDL channel.  The
client can call SetConstraints() and then WaitForBuffersAllocated() on
the client end of this channel to specify constraints and then determine
success/failure and get the BufferCollectionInfo_2 for the
BufferCollection.  The client should also keep the client end of
this channel open while using the BufferCollection, and should notice
when this channel closes and stop using the BufferCollection ASAP.</p>

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

<p>Creates a logical BufferCollectionToken which can be shared among
participants (using BufferCollectionToken.Duplicate()), and then
converted into a BufferCollection using BindSharedCollection().</p>
<p>Success/failure to populate the BufferCollection with buffers is
determined via the BufferCollection interface.</p>

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

<p>Convert a BufferCollectionToken into a connection to the logical
BufferCollection.  The BufferCollection hasn't yet been populated with
buffers - the participant must first also send SetConstraints() via the
client end of buffer_collection.</p>
<p>All BufferCollectionToken(s) duplicated from a logical
BufferCollectionToken created via AllocateSharedCollection() must be
turned in via BindSharedCollection() before the logical BufferCollection
will be populated with buffers.</p>
<p><code>token</code> the client endpoint of a channel whose server end was sent to
sysmem using AllocateSharedCollection or whose server end was sent to
sysmem using BufferCollectionToken.Duplicate().  The token is being
&quot;exchanged&quot; for a channel to the logical BufferCollection.</p>
<p><code>buffer_collection</code> the server end of a BufferCollection channel.  The
sender retains the client end as usual.  The BufferCollection channel
is a single participant's connection to the logical BufferCollection.
There typically will be other participants with their own
BufferCollection channel to the logical BufferCollection.</p>

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

<p>A BufferCollectionToken is not a BufferCollection, but rather a way to
identify a potential shared BufferCollection prior to the BufferCollection
being allocated.</p>
<p>We use a channel for the BufferCollectionToken instead of a single eventpair
(pair) because this way we can detect error conditions like a participant
dying mid-create.</p>

### Duplicate {#Duplicate}

<p>The initiator or a participant can send Duplicate() as part of creating
another participant-side handle to the same logical
BufferCollectionToken.</p>
<p>This method is used to hand the logical token to all participants so all
participants can provide constraints to sysmem for the overall
BufferCollection to achieve the goal of allocating buffers compatible
with all participants.</p>
<p>The Duplicate() message is intentionally available only on
BufferCollectionToken not BufferCollection.</p>
<p>The token is separate from BufferCollection so that participants contact
sysmem directly, so that participants are only trusting their environment
for who sysmem is (fake token mitigation), not an initiator.  Only after
successful BindSharedCollection does a participant know that the token
was a real sysmem token.  In contrast, if we had Duplicate() directly on
BufferCollection, an initiator could attempt to serve the
BufferCollection channel itself, which would allow for some problematic
possibilities.</p>
<p>All the BufferCollectionToken channels of a logical token must be turned
in via BindSharedCollection() for a BufferCollection to be successfully
created.  Else the BufferCollection channel will close.</p>
<p>When a client calls BindSharedCollection() to turn in a
BufferCollectionToken, the server will process all Duplicate() messages
before closing down the BufferCollectionToken.  This allows the client
to Duplicate() and immediately turn in the BufferCollectionToken using
BindSharedCollection, then later transfer the client end of token_request
to another participant - the server will notice the existence of the
token_request before considering this BufferCollectionToken fully closed.</p>
<p><code>rights_attenuation_mask</code> rights bits that are zero in this mask will be
absent in the buffer VMO rights obtainable via the client end of
token_request.  This allows an initiator or intermediary participant
to attenuate the rights available to a participant.  This may not be the
only mechanism that attenuates rights on the VMO handles obtainable via
the client end of token_request.  This does not allow a participant
to gain rights that the participant doesn't already have.  The value
ZX_RIGHT_SAME_RIGHTS can be used to specify that no attenuation should
be applied.</p>
<p><code>token_request</code> is the server end of a BufferCollectionToken channel.
The client end of this channel acts as another handle to the same logical
BufferCollectionToken.  Typically the sender of Duplicate() will transfer
the client end corresponding to collection_request to a/another
participant running in a separate process, but it's also fine for the
additional logical participant to be in the same process.</p>
<p>After sending one or more Duplicate() messages, and before sending the
created tokens to other participants (or to other Allocator channels),
the client should send a Sync() and wait for its response.  The Sync()
call can be made on the token, or on the BufferCollection obtained by
passing this token to BindSharedCollection().  Either will ensure that
the server knows about the tokens created via Duplicate() before the
other participant sends the token to the server via separate Allocator
channel.  If a client is using FIDL C generated code and doesn't want to
block waiting for a response message, the other option is to notice
arrival of the BufferCollectionEvents::OnBufferCollectionCreated() event
after turning in this token for a BufferCollection.</p>

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

<p>Ensure that previous Duplicate() messages have been received server side,
so that it's safe to send the client end of token_request to another
participant knowing the server will recognize the token when it's sent
into BindSharedCollection by the other participant.</p>
<p>Other options include waiting for each Duplicate() to complete
individually, or calling Sync() on BufferCollection after this token has
been turned in via BindSharedCollection(), or noticing arrival of
BufferCollectionEvents::OnDuplicatedTokensKnownByServer().</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### Close {#Close}

<p>Normally a participant will convert the token into a BufferCollection
view, but a particpant is also free to Close() the token (and then close
the channel immediately or shortly later in response to server closing
its end), which avoids causing LogicalBufferCollection failure.
Normally an unexpected token channel close will cause
LogicalBufferCollection failure.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## BufferCollection {#BufferCollection}
*Defined in [fuchsia.sysmem/collection.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/collection.fidl#134)*

<p>BufferCollection is a connection directly from a participant to sysmem re.
a logical BufferCollection; typically the logical BufferCollection is shared
with other participants.  In other words, an instance of the BufferCollection
interface is a view of a &quot;LogicalBufferCollection&quot;.</p>
<p>This connection exists to facilitate async indication of when the logical
BufferCollection has been populated with buffers.</p>
<p>Also, the channel's closure by the server is an indication to the client
that the client should close all VMO handles that were obtained from the
BufferCollection ASAP.</p>
<p>Also, this interface may in future allow specifying constraints in other
ways, and may allow for back-and-forth negotiation of constraints to some
degree.</p>
<p>This interface may in future allow for more than 64 VMO handles per
BufferCollection, but currently the limit is 64.</p>
<p>This interface may in future allow for allocating/deallocating single
buffers.</p>
<p>Some initiators may wait a short duration until all old logical
BufferCollection VMO handles have closed (or until the short duration times
out) before allocating a new BufferCollection, to help control physical
memory fragmentation and avoid overlap of buffer allocation lifetimes for
the old and new collections. Collections can be large enough that it's worth
avoiding allocation overlap (in time).</p>

### SetEventSink {#SetEventSink}

<p>At least for now, the only way to get events from a BufferCollection is
to set a reverse BufferCollectionEvents channel.  This can be sent up to
once at any point during BufferCollection channel lifetime.  All events
are one-shot events, and will be sent immediately via <code>events</code> if the
one-shot event's condition has already become true (once true will stay
true; only goes from false to true once).</p>
<p><code>events</code> is the client end of a BufferCollectionEvents which will be sent
one-way messages indicating events relevant to this BufferCollection
channel (some may be specific to this BufferCollection channel and some
may be relevant to the overall logical BufferCollection).</p>

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

<p>See comments on BufferCollectionToken::Sync().</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### SetConstraints {#SetConstraints}

<p>Provide BufferCollectionConstraints to the logical BufferCollection.</p>
<p>Participants with read but not write can only call SetConstraints() once.</p>
<p>Participants with write can call SetConstraints() more than once.  The
initial buffer allocation will use the constraints in the first call to
SetConstraints().  Among other things, this allows a decoder to attempt
to allocate a new buffer that's larger to hold an output frame that's
larger.</p>
<p>Sometimes the initiator is a participant only in the sense of wanting to
keep an eye on success/failure to populate with buffers, and zx.status on
failure.  In that case, <code>has_constraints</code> can be false, and <code>constraints</code>
will be ignored.</p>
<p>VMO handles will not be provided to the client that sends null
constraints - that can be intentional for an initiator that doesn't need
VMO handles.  Not having VMO handles doesn't prevent the initator from
adjusting which portion of a buffer is considered valid and similar, but
the initiator can't hold a VMO handle open to prevent the logical
BufferCollection from cleaning up if the logical BufferCollection needs
to go away regardless of the initiator's degree of involvement for
whatever reason.</p>
<p>For population of buffers to be attempted, all holders of a
BufferCollection client channel need to call SetConstraints() before
sysmem will attempt to allocate buffers.</p>
<p><code>has_constraints</code> if false, the constraints are effectively null, and
<code>constraints</code> are ignored.  The sender of null constraints won't get any
VMO handles in BufferCollectionInfo, but can still find out how many
buffers were allocated and can still refer to buffers by their
buffer_index.</p>
<p><code>constraints</code> are constraints on the buffer collection.</p>

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

<p>This request completes when buffers have been allocated, responds with
some failure detail if allocation has been attempted but failed.</p>
<p>The following must occur before buffers will be allocated:</p>
<ul>
<li>All BufferCollectionToken(s) of the logical BufferCollectionToken
must be turned in via BindSharedCollection().</li>
<li>All BufferCollection(s) of the logical BufferCollection must have had
SetConstraints() sent to them.</li>
</ul>
<p>A caller using C generated FIDL code who wishes not to block a thread in
a zx_channel_call() for a potentially fairly long duration on this
message/response can use SetEventSink() and
BufferCollectionEvents.OnBuffersPopulated() instead.</p>
<p>This method is still legal to call despite use of OnBuffersPopulated(),
but in that case the additional BufferCollectionInfo returned here will
include handles that are redundant with other handles in the
BufferCollectionInfo delivered via OnBuffersPopulated() (separate handle
but same underlying VMO objects), so most clients that bother calling
SetEventSink() will prefer to receive BufferCollectionInfo via
OnBuffersPopulated().  This method is mostly here for clients that don't
call SetEventSink().</p>
<p>Returns <code>ZX_OK</code> if successful.
Returns <code>ZX_ERR_NO_MEMORY</code> if the request is valid but cannot be
fulfilled due to resource exhaustion.
Returns <code>ZX_ERR_ACCESS_DENIED</code> if the caller is not permitted to
obtain the buffers it requested.
Returns <code>ZX_ERR_INVALID_ARGS</code> if the request is malformed.
Returns <code>ZX_ERR_NOT_SUPPORTED</code> if request is valid but cannot be
satisfied, perhaps due to hardware limitations.</p>
<p><code>buffer_collection_info</code> has the VMO handles and other related info.</p>

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
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr><tr>
            <td><code>buffer_collection_info</code></td>
            <td>
                <code><a class='link' href='#BufferCollectionInfo_2'>BufferCollectionInfo_2</a></code>
            </td>
        </tr></table>

### CheckBuffersAllocated {#CheckBuffersAllocated}

<p>This returns the same result code as WaitForBuffersAllocated if the
buffer collection has been allocated or failed, or <code>ZX_ERR_UNAVAILABLE</code>
if WaitForBuffersAllocated would block.</p>

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
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

### CloseSingleBuffer {#CloseSingleBuffer}

<p>The CloseBuffer() doesn't immediately force all VMO handles to that
buffer to close, but it does close any handle held by sysmem, and does
notify all participants of the desire to close the buffer at which point
each participant that's listening may close their handle to the buffer.</p>
<p>Only a particpant with write can do this.  Coordination among multiple
participants with write is outside of the scope of this interface.</p>
<p><code>buffer_index</code> indicates which buffer to close.  If the buffer is already
closed this has no effect (idempotent).</p>

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

<p>This allocates a new buffer that is consistent with the most recent call
to SetConstraints(), if possible.  If not possible, this indicates the
failure via OnNewBufferAllocated().</p>
<p>Only a participant with write can do this.  Coordination among multiple
participants with write is outside the scope of this interface.</p>
<p>The participant is (intentionally) never informed of other participant's
constraints.</p>

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

<p>Completes when AllocateBuffer is done.  Callers who wish to avoid
blocking a thread while waiting can use OnAllocateSingleBufferDone()
instead.</p>

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
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr><tr>
            <td><code>buffer_info</code></td>
            <td>
                <code><a class='link' href='#SingleBufferInfo'>SingleBufferInfo</a></code>
            </td>
        </tr></table>

### CheckSingleBufferAllocated {#CheckSingleBufferAllocated}

<p>A participant can use this message to have sysmem verify that this
buffer_index exists.  This message is intentionally ignored by the
server if the buffer_index <em>does</em> exist.  In that case, the client will
see OnAllocateSingleBufferDone() soon with status == <code>ZX_OK</code> (if the
client hasn't already seen that message).  If on the other hand the
buffer_index does not exist, this message causes the server to send
OnAllocateSingleBufferDone() with status == <code>ZX_ERR_NOT_FOUND</code>.  A
particpant will typically use this when the participant receives a new
buffer_index that the participant doesn't yet know about, to ensure that
the participant won't be waiting forever for the
OnAllocateSingleBufferDone() message regarding this buffer_index.</p>

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

<p>The server handles unexpected failure of a BufferCollection by failing
the whole LogicalBufferCollection.  Partly this is to expedite closing
VMO handles.  If a participant would like to cleanly close a
BufferCollection view without causing LogicalBufferCollection failure,
the participant can send Close() before closing the client end of the
BufferCollection channel.  If this is the last BufferCollection view, the
LogicalBufferCollection will still go away.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## BufferCollectionEvents {#BufferCollectionEvents}
*Defined in [fuchsia.sysmem/collection.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/collection.fidl#287)*

<p>This interface intentionally doesn't include any event for
OnOldBufferClosed(), because such an event could arrive at a participant too
soon to be useful.  Instead, such an indication should be made in-band within
FIDL interfaces that deliver packets to downstream participants.</p>

### OnDuplicatedTokensKnownByServer {#OnDuplicatedTokensKnownByServer}

<p>See comments on BufferCollectionToken::Sync().</p>
<p>This message only indicates that the server has reached the point where
it knows about previously created tokens Duplicate()ed from the token
used to create this BufferCollection.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### OnBuffersAllocated {#OnBuffersAllocated}

<p>This event inidicates that buffer allocation is over, whether succesful
or failed.</p>
<p>This event will eventually be sent by the server (unless the
BufferCollection channel closes first).</p>
<p><code>status</code>:
<code>ZX_OK</code> if successful.
<code>ZX_ERR_NO_MEMORY</code> if the request is valid but cannot be fulfilled due to
resource exhaustion.
<code>ZX_ERR_ACCESS_DENIED</code> if the caller is not permitted to obtain the
buffers it requested.
<code>ZX_ERR_INVALID_ARGS</code> if the request is malformed.
<code>ZX_ERR_NOT_SUPPORTED</code> if request is valid but cannot be satisfied,
perhaps due to hardware limitations.</p>
<p><code>buffer_collection_info</code> The buffer information, including VMO handles.
If <code>status</code> is not <code>ZX_OK</code>, <code>buffer_collection_info</code> is default
initialized and contains no meaningful information.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr><tr>
            <td><code>buffer_collection_info</code></td>
            <td>
                <code><a class='link' href='#BufferCollectionInfo_2'>BufferCollectionInfo_2</a></code>
            </td>
        </tr></table>



### OnAllocateSingleBufferDone {#OnAllocateSingleBufferDone}

<p>A participant can learn when a new buffer is allocated via this event.
The only participant that will see a failing status is the participant
that attempted the single buffer allocation.  Other participants will
only see successful single buffer allocations.</p>
<p><code>status</code>:</p>
<p><code>ZX_OK</code> if successful.  This can be seen by any participant (whether
sender of AllocateSingleBuffer() or not.)</p>
<p><code>ZX_ERR_NOT_FOUND</code> if the buffer_index sent via
CheckSingleBufferAllocated() isn't known to the server.  This can be seen
by any participant (whether sender of AllocateSingleBuffer() or not.)</p>
<p>These error codes are only ever seen by the sender of
AllocateSingleBuffer():</p>
<p><code>ZX_ERR_NO_MEMORY</code> if the request is valid but cannot be fulfilled due to
resource exhaustion.
<code>ZX_ERR_ACCESS_DENIED</code> if the caller is not permitted to obtain the
buffers it requested.
<code>ZX_ERR_INVALID_ARGS</code> if the request is malformed.
<code>ZX_ERR_NOT_SUPPORTED</code> if request is valid but cannot be satisfied,
perhaps due to hardware limitations.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr><tr>
            <td><code>buffer_info</code></td>
            <td>
                <code><a class='link' href='#SingleBufferInfo'>SingleBufferInfo</a></code>
            </td>
        </tr></table>



## DriverConnector {#DriverConnector}
*Defined in [fuchsia.sysmem/driver_connector.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/driver_connector.fidl#26)*

<p>Once a channel with this interface is established to a driver (typically in
advance), this interface allows asynchronously sending the server end of an
Allocator channel which will be served by the driver.</p>
<p>For now, the only FIDL interface directly served via normal devhost FIDL
dispatching code by the sysmem driver is this interface.  Other sysmem
interfaces are served by separate dispatching code primarily because we want
to be able to establish channels async by sending the server channel toward
the driver without needing a round-trip open and without managing the channel
as a file descriptor.</p>
<p>A secondary current reason tracked by ZX-3091 is that the current devhost
dispatching code doesn't permit async processing of requests, which we want
for proper functionining of at least the BufferCollection interface since
that interface has requests that don't complete until the devhost has
constraints from other participants.</p>

### Connect {#Connect}

<p>This one-way message sends in the server end of an Allocator channel.</p>
<p><code>allocator_request</code> will be served by the sysmem driver (or the channel
will close).</p>

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

<p>Manages resources on a specific sysmem heap.</p>
<p>Needs Layout = &quot;Simple&quot; because used with &quot;FIDL Simple C Bindings&quot;.</p>

### AllocateVmo {#AllocateVmo}

<p>Request a new memory allocation of <code>size</code> on heap.
For heaps which don't permit CPU access to the buffer data, this
will create a VMO with an official size, but which never has any
physical pages.  For such heaps, the VMO is effectively used as
an opaque buffer identifier.</p>
<p>Heaps should defer allocation of any associated resources until
CreateResource(), because the caller of AllocateVmo() may simply
delete the returned VMO with no further notification to the heap.
In contrast, after CreateResource(), the caller guarantees that
DestroyResource() or heap channel closure will occur.</p>
<p>The caller guarantees that CreateResource() will be called prior
to the returned VMO or any associated child VMO being used.</p>

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
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr><tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;?</code>
            </td>
        </tr></table>

### CreateResource {#CreateResource}

<p>Create resources and associate heap-specific resources with the
passed-in VMO. Resources can be hardware specific and their
lifetime don't have to be tied to <code>vmo</code>. <code>vmo</code> must be a VMO
(or a direct or indirect child of a VMO) acquired through a call
to AllocateVmo method above.  If the passed-in vmo is a child VMO,
its size must match the size of the parent VMO created by
AllocateVmo().  For heaps that permit CPU access, the passed-in
VMO must not have a copy-on-write relationship with the parent
VMO, but rather a pass-through relationship. Successful return
status indicate that Heap has established a mapping between
VMO and hardware specific resources.</p>
<p>The returned id must be passed to DestroyResource() later when
resources associated with VMO are no longer needed, unless the
heap channel closes first.</p>
<p>The heap must not own/keep a handle to VMO, or any derived child
VMO, or any VMAR mapping to VMO, as any of those would keep VMO
alive beyond all sysmem participant usages of the vmo; instead
the heap can get the vmo's koid for the heap's mapping.</p>

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
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### DestroyResource {#DestroyResource}

<p>Destroy previously created resources.</p>

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
*Defined in [fuchsia.sysmem/secure_mem.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/secure_mem.fidl#27)*

<p>SecureMem</p>
<p>The client is sysmem.  The server is securemem driver.</p>
<p>TEE - Trusted Execution Environment.</p>
<p>REE - Rich Execution Environment.</p>
<p>Enables sysmem to call the securemem driver to get any secure heaps
configured via the TEE (or via the securemem driver), and set any physical
secure heaps configured via sysmem.</p>
<p>Presently, dynamically-allocated secure heaps are configured via sysmem, as
it starts quite early during boot and can successfully reserve contiguous
physical memory.  Presently, fixed-location secure heaps are configured via
TEE, as the plumbing goes from the bootloader to the TEE.  However, this
protocol intentionally doesn't care which heaps are dynamically-allocated
and which are fixed-location.</p>

### GetPhysicalSecureHeaps {#GetPhysicalSecureHeaps}

<p>Gets the physical address and length of any secure heap whose physical
range is configured via the TEE.</p>
<p>Presently, these will be fixed physical addresses and lengths, with the
location plumbed via the TEE.</p>
<p>This is preferred over RegisterHeap() when there isn't any special
heap-specific per-VMO setup or teardown required.</p>
<p>The physical range must be secured/protected by the TEE before the
securemem driver responds to this request with success.</p>
<p>Sysmem should only call this once.  Returning zero heaps is not a
failure.</p>
<p>Errors:</p>
<ul>
<li>ZX_ERR_BAD_STATE - called more than once.</li>
<li>ZX_ERR_INTERNAL - generic internal error (such as in communication
with TEE which doesn't generate zx_status_t errors).</li>
<li>other errors are possible, such as from communication failures or
server propagation of zx_status_t failures</li>
</ul>

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

<p>This request from sysmem to the securemem driver lets the TEE know the
physical memory address and length of any secure heap whose location is
configured/established via sysmem.</p>
<p>Only sysmem can call this because only sysmem is handed the client end
of a FIDL channel serving this protocol, via RegisterSecureMem().  The
securemem driver is the server end of this protocol.</p>
<p>Presently, these physical ranges will be dynamically-allocated by sysmem
early during boot.</p>
<p>The heap ID is included in case that's relevant to the securemem driver,
for more informative log messages, and for consistency with
GetPhysicalSecureHeaps().</p>
<p>The securemem driver must configure all the provided ranges as secure
with the TEE before responding to this message with success.</p>
<p>For heaps configured via sysmem, both the HeapType and heap location are
configured via sysmem, and ZX_ERR_INVALID_ARGS will be the result if the
securemem driver determines that the number of heaps or HeapType(s) are
not what's supported by the securemem driver.  Typically these aspects
are essentially fixed for a given device, so this error would typically
imply a configuration or plumbing problem.</p>
<p>Sysmem should only call this once.</p>
<p>Errors:</p>
<ul>
<li>ZX_ERR_BAD_STATE - called more than once</li>
<li>ZX_ERR_INVALID_ARGS - unexpected heap count or unexpected heap</li>
<li>ZX_ERR_INTERNAL - generic internal error (such as in communication
with TEE which doesn't generate zx_status_t errors).</li>
<li>other errors are possible, such as from communication failures or
server propagation of zx_status_t failures</li>
</ul>

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



<p>Information about a buffer collection and its buffers.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>buffer_count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>The number of buffers in the collection.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>format</code></td>
            <td>
                <code><a class='link' href='#BufferFormat'>BufferFormat</a></code>
            </td>
            <td><p>Describes how the contents of buffers are represented.
All buffers within the collection have the same format.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>vmos</code></td>
            <td>
                <code>vmo[64]</code>
            </td>
            <td><p>VMO handles for each buffer in the collection.
The VMOs are only present when the buffers are backed by VMOs.</p>
<p>If present, all the VMOs after <code>buffer_count</code> are invalid handles.
All buffer VMO handles have identical size and access rights.
The VMO access rights are determined based on the usages which the
client specified when allocating the buffer collection.  For example,
a client which expressed a read-only usage will receive VMOs without
write rights.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>vmo_size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The size of each VMO provided.
This property is only present when the buffers are backed by VMOs.</p>
</td>
            <td>0</td>
        </tr>
</table>

### BufferCollectionConstraints {#BufferCollectionConstraints}
*Defined in [fuchsia.sysmem/constraints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/constraints.fidl#16)*



<p>Constraints on BufferCollection parameters.  These constraints can be
specified per-participant.  The sysmem service implements aggregation of
constraints from multiple participants.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>usage</code></td>
            <td>
                <code><a class='link' href='#BufferUsage'>BufferUsage</a></code>
            </td>
            <td><p>The usage is only meant as a hint to help sysmem choose a more optimal
PixelFormat or similar when multiple compatible options exist.</p>
<p>When aggregating BufferCollectionConstraints, these values bitwise-OR.</p>
<p>At least one usage bit must be specified unless the whole
BufferCollectionConstraints is logically null due to !has_constraints.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>min_buffer_count_for_camping</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Per-participant minimum number of buffers that are needed for camping
purposes.  A participant should specify a number for min_buffer_count
that's &gt;= the maximum number of buffers that the participant may
concurrently camp on for any non-transient period of time.</p>
<p>For example, a video decoder would specify (at least) the maximum number
of reference frames + 1 frame currently being decoded into.</p>
<p>A participant must not camp on more buffers than specified here (except
very transiently) else processing may get stuck.</p>
<p>When aggregating BufferCollectionConstraints, these values add.</p>
<p>In testing scenarios, camping on more buffers than this for any
significant duration may (ideally will) be flagged as a failure.  In
testing scenarios, the participant may not be provided with more buffers
than this concurrently.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>min_buffer_count_for_dedicated_slack</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Per-participant minimum number of buffers that are needed for slack
reasons, for better overlap of processing / better performance.</p>
<p>When aggregating BufferCollectionConstraints, these values add.</p>
<p>A participant should typically specify 0 or 1 here - typically 0 is
appropriate if min_buffer_count_for_camping is already enough to keep
the participant busy 100% of the time when the participant is slightly
behind, while 1 can be appropriate if 1 more buffer than strictly needed
for min-camping reasons gives enough slack to stay busy 100% of the time
(when slightly behind, vs. lower % without the extra buffer).</p>
<p>In testing scenarios, this field may be forced to 0, and all
participants are expected to continue to work without getting stuck.  If
a buffer is needed for forward progress reasons, that buffer should be
accounted for in min_buffer_count_for_camping.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>min_buffer_count_for_shared_slack</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Similar to min_buffer_count_for_dedicated_slack, except when aggregating
these values max (instead of add).  The value here is not shared with
any participant's min_buffer_count_for_dedicated_slack.</p>
<p>A participant can specify &gt; 0 here if a participant would like to ensure
there's some slack overall, but doesn't need that slack to be dedicated.</p>
<p>The choice whether to use min_buffer_count_for_dedicated_slack or
min_buffer_count_for_shared_slack (or both) will typically be about the
degree to which the extra slack improves performance.</p>
<p>In testing scenarios, this field may be forced to 0, and all
participants are expected to continue to work without getting stuck.  If
a buffer is needed for forward progress reasons, that buffer should be
accounted for in min_buffer_count_for_camping.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>min_buffer_count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>A particularly-picky participant may unfortunately need to demand a tight
range of buffer_count, or even a specific buffer_count.  This field
should remain 0 unless a participant really must set this field to
constrain the overall BufferCollectionInfo_2.buffer_count.  Any such
participant should still fill out the min_buffer_count_for_* fields
above.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_buffer_count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>0 is treated as 0xFFFFFFFF.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>has_buffer_memory_constraints</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Constraints on BufferCollectionSettings.buffer_settings.</p>
<p>A participant that intends to specify image_format_constraints_count &gt; 1
will typically specify the minimum buffer size implicitly via
image_format_constraints, and possibly specify only the max buffer size
via buffer_memory_constraints.</p>
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
            <td><p>Optional constraints on the image format parameters of an image stored
in a buffer of the BufferCollection.  This includes pixel format and
image layout.  These constraints are per-pixel-format, so more than one
is permitted.</p>
<p>When aggregating, only pixel formats that are specified by all
particpants with non-zero image_format_constraints_count (and non-Null)
BufferCollectionConstraints) are retained.</p>
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
            <td><p>The same VMO can be used by more than one CodecBuffer (only of the same
buffer_lifetime_ordinal), but each vmo_handle must be a separate handle.</p>
<p>The vmo field can be 0 if this is a VmoBuffer in BufferCollectionInfo_2
that's at or beyond BufferCollectionInfo_2.buffer_count.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>vmo_usable_start</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Offset within the VMO of the first usable byte.  Must be &lt; the VMO's size
in bytes, and leave sufficient room for BufferMemorySettings.size_bytes
before the end of the VMO.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### BufferCollectionInfo_2 {#BufferCollectionInfo_2}
*Defined in [fuchsia.sysmem/constraints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/constraints.fidl#127)*



<p>Information about a buffer collection and its buffers.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>buffer_count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>If this is the initial buffer collection allocation, this is the total
number of buffers.  If this is a single buffer allocation, this is zero,
and the rest of the fields only apply to the single buffer.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>settings</code></td>
            <td>
                <code><a class='link' href='#SingleBufferSettings'>SingleBufferSettings</a></code>
            </td>
            <td><p>These settings apply to all the buffers in the inital buffer allocation.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>buffers</code></td>
            <td>
                <code>[64]</code>
            </td>
            <td><p>VMO handles (and vmo_usable_start offset) for each buffer in the
collection.</p>
<p>If present, all the VMOs at or after index <code>buffer_count</code> are invalid (0)
handles.</p>
<p>All buffer VMO handles have identical size and access rights.  The size
is in settings.buffer_settings.size_bytes.</p>
<p>The VMO access rights are determined based on the usages which the
client specified when allocating the buffer collection.  For example,
a client which expressed a read-only usage will receive VMOs without
write rights.  In addition, the rights can be attenuated by the parameter
to BufferCollectionToken.Duplicate() calls.</p>
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



<p>After the initial buffer allocation, it's allowed to close old buffers and
allocate new buffers.  When a new buffer is allocated its settings can differ
from the rest of the buffers in the collection, and the single buffer's
settings are delivered via OnSingleBufferAllocated() using this struct:</p>


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
            <td><p>Buffers holding data that is not uncompressed image data will not have
this field set.  Buffers holding data that is uncompressed image data
<em>may</em> have this field set.</p>
<p>At least for now, changing the PixelFormat requires re-allocating
buffers.</p>
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
            <td><p>0 is treated as 0xFFFFFFFF.</p>
</td>
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
            <td><p>If true, at least one participant requires secure memory.</p>
<p>When aggregating BufferCollectionConstraints, these values boolean-OR.</p>
</td>
            <td>false</td>
        </tr><tr>
            <td><code>ram_domain_supported</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>By default, participants must ensure the CPU can read or write data to
the buffer without cache operations. If they support using the RAM
domain, data must be available in RAM (with CPU cache state such that
the RAM data won't get corrupted by a dirty CPU cache line writing
incorrect data to RAM), and a consumer reading using the CPU must
invalidate CPU cache before reading (the producer doesn't guarantee
zero stale &quot;clean&quot; cache lines)</p>
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
            <td><p>Optional heap constraints. Participants that don't care which heap
memory is allocated on should leave this field 0.</p>
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
*Defined in [fuchsia.sysmem/constraints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/constraints.fidl#233)*





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
            <td><p>The specific heap from which buffers are allocated.
See above in this file for heap identifier values.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### ImageFormatConstraints {#ImageFormatConstraints}
*Defined in [fuchsia.sysmem/constraints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/constraints.fidl#245)*



<p>Describes constraints on layout of image data in buffers.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>pixel_format</code></td>
            <td>
                <code><a class='link' href='#PixelFormat'>PixelFormat</a></code>
            </td>
            <td><p>The PixelFormat for which the following constraints apply.  A
participant may have more than one PixelFormat that's supported, in
which case that participant can use a list of ImageFormatConstraints
with an entry per PixelFormat.  It's not uncommon for the other fields
of ImageFormatConstraints to vary by PixelFormat - for example for a
linear format to support smaller max size than a tiled format.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>color_spaces_count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Empty is an error.  Redundant entries are an error.  Arbitrary ordering
is not an error.</p>
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
            <td><p>Minimum permitted width in pixels.</p>
<p>For example a video decoder participant may set this field to the
minimum coded_width that might potentially be specified by a stream.  In
contrast, required_min_coded_width would be set to the current
coded_width specified by the stream.  While min_coded_width aggregates
by taking the max, required_min_coded_width aggregates by taking the
min.</p>
<p>See also required_min_coded_width.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_coded_width</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Maximum width in pixels.  For example Scenic may set this field
(directly or via sub-participants) to the maximum width that can be
composited.
0 is treated as 0xFFFFFFFF.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>min_coded_height</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Minimum height in pixels.  For example a video decoder participant may
set this field to the coded_height specified by a stream.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_coded_height</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Maximum height in pixels.  For example Scenic may set this field
(directly or via sub-participants) to the maximum height that can be
composited.
0 is treated as 0xFFFFFFFF.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>min_bytes_per_row</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Must be &gt;= the value implied by min_coded_width for plane 0.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_bytes_per_row</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Must be &gt;= the value implied by max_coded_width for plane 0.
0 is treated as 0xFFFFFFFF.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_coded_width_times_coded_height</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>The max image area in pixels is limited indirectly via
BufferSettings.size_bytes, and can also be enforced directly via this
field.
0 is treated as 0xFFFFFFFF.</p>
</td>
            <td>4294967295</td>
        </tr><tr>
            <td><code>layers</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Number of layers within a multi-layered image.
0 is treated as 1.</p>
</td>
            <td>1</td>
        </tr><tr>
            <td><code>coded_width_divisor</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>coded_width % width_divisor must be 0.
0 is treated as 1.</p>
</td>
            <td>1</td>
        </tr><tr>
            <td><code>coded_height_divisor</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>coded_height % height_divisor must be 0.
0 is treated as 1.</p>
</td>
            <td>1</td>
        </tr><tr>
            <td><code>bytes_per_row_divisor</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>bytes_per_row % bytes_per_row_divisor must be 0.
0 is treated as 1.</p>
</td>
            <td>1</td>
        </tr><tr>
            <td><code>start_offset_divisor</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>vmo_usable_start % start_offset_divisor must be 0.
0 is treated as 1.</p>
</td>
            <td>1</td>
        </tr><tr>
            <td><code>display_width_divisor</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>display_width % display_width_divisor must be 0.
0 is treated as 1.</p>
</td>
            <td>1</td>
        </tr><tr>
            <td><code>display_height_divisor</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>display_height % display_height_divisor must be 0.
0 is treated as 1.</p>
</td>
            <td>1</td>
        </tr><tr>
            <td><code>required_min_coded_width</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>required_ dimension bounds.</p>
<p>In contrast to the corresponding fields without &quot;required_&quot; at the
start, these fields (when set to non-zero values) express a requirement
that the resulting aggregated non-required_ fields specify a space that
fully contain the space expressed by each participant's required_
fields.</p>
<p>For example, a producer video decoder is perfectly happy for the
consumer to be willing to accept anything, and the video decoder doesn't
really want to constrain the potential space of dimensions that might be
seen in a stream and may be acceptable to the consumer, but the video
decoder needs to ensure that the resulting dimension ranges contain
at least the current dimensions decoded from the stream.</p>
<p>Similarly, an initiator with a particular dynamic-dimension scenario in
mind may wish to require up front that participants agree to handle at
least the range of dimensions expected by the initiator in that
scenario (else fail earlier rather than later, maybe trying again with
smaller required_ space).</p>
<p>It's much more common for a producer or initiator to set these fields
than for a consumer to set these fields.</p>
<p>While the non-required_ fields aggregate by taking the intersection, the
required_ fields aggregate by taking the union.</p>
<p>If set, the required_max_coded_width and required_max_coded_height will
cause the allocated buffers to be large enough to hold an image that is
required_max_coded_width * required_max_coded_height.</p>
<p>TODO(dustingreen): Make it easier to allocate buffers of minimal size
that can (optionally) also handle 90 degree rotated version of the max
dimensions / alternate required bounds for another main aspect ratio.
0 is treated as 0xFFFFFFFF.</p>
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
            <td><p>0 is treated as 0xFFFFFFFF.</p>
</td>
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
            <td><p>0 is treated as 0xFFFFFFFF.</p>
</td>
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
*Defined in [fuchsia.sysmem/constraints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/constraints.fidl#372)*



<p>Describes how an image is represented.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>pixel_format</code></td>
            <td>
                <code><a class='link' href='#PixelFormat'>PixelFormat</a></code>
            </td>
            <td><p>Pixel format.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>coded_width</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Row width in pixels that exist in the buffer.  Must be &gt;= display_width.
Can be &lt; the width implied by stride_bytes.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>coded_height</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Number of rows.  Must be &gt;= display_height.</p>
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
            <td><p>Row width in pixels that are to be displayed.  This can be &lt;=
coded_width.  Any cropping occurs on the right of the image (not left).</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>display_height</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Number of rows to be displayed.  This can be &lt;= coded_height, with any
cropping on the bottom (not top).</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>layers</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Number of layers within a multi-layered image.</p>
</td>
            <td>1</td>
        </tr><tr>
            <td><code>color_space</code></td>
            <td>
                <code><a class='link' href='#ColorSpace'>ColorSpace</a></code>
            </td>
            <td><p>Color space.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>has_pixel_aspect_ratio</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>The pixel_aspect_ratio_width : pixel_aspect_ratio_height is the
pixel aspect ratio (AKA sample aspect ratio aka SAR) for the luma
(AKA Y) samples. A pixel_aspect_ratio of 1:1 mean square pixels. A
pixel_aspect_ratio of 2:1 would mean pixels that are displayed twice
as wide as they are tall. Codec implementation should ensure these
two values are relatively prime by reducing the fraction (dividing
both by GCF) if necessary.</p>
<p>When has_pixel_aspect_ratio == false, pixel_aspect_ratio_width and
pixel_aspect_ratio_height will both be 1, but in that case the
pixel_aspect_ratio_width : pixel_aspect_ratio_height of 1:1 is just
a very weak suggestion re. reasonable-ish handling, not in any way
authoritative. In this case (or in any case really) the receiver of
this message may have other OOB means to determine the actual
pixel_aspect_ratio.</p>
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
            <td><p>The upper 8 bits are a vendor code as allocated in FormatModifierVendor
enum.  The lower 56 bits are vendor-defined.</p>
<p>This field and the values that go in this field are defined this way for
compatibility reasons.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### BufferFormat {#BufferFormat}
*Defined in [fuchsia.sysmem/formats_deprecated.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/formats_deprecated.fidl#9)*



<p>Describes how the contents of buffers are represented.
Buffers of each type are described by their own tables.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>tag</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Since this struct used to be a single member union, we kept the tag
to avoid any wire format changes. The tag must be set to <code>0</code>,
no other value is correct.</p>
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



<p>Describes how the pixels within an image are represented.
Simple formats need only a type.
Parametric pixel formats may require additional properties.</p>


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
            <td><p>This bool effectively makes format_modifier optional, to satisfy
'Layout = &quot;Simple&quot;', to satisify &quot;FIDL Simple C Bindings&quot;.</p>
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



<p>Describes how the pixels within an image are meant to be presented.
Simple color spaces need only a type.
Parametric color spaces may require additional properties.</p>


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



<p>Describes how an image is represented.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>width</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Row width in pixels.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Number of rows.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>layers</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Number of layers within a multi-layered image.
Defaults to 1 if not specified.</p>
</td>
            <td>1</td>
        </tr><tr>
            <td><code>pixel_format</code></td>
            <td>
                <code><a class='link' href='#PixelFormat'>PixelFormat</a></code>
            </td>
            <td><p>Pixel format.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>color_space</code></td>
            <td>
                <code><a class='link' href='#ColorSpace'>ColorSpace</a></code>
            </td>
            <td><p>Color space.</p>
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
            <td><p>Byte offset of the start of the plane from the beginning of the image.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>bytes_per_row</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Stride in bytes per row.
Only meaningful for linear buffer formats.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### ImageSpec {#ImageSpec}
*Defined in [fuchsia.sysmem/image_formats_deprecated.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/image_formats_deprecated.fidl#40)*



<p>Describes constraints for allocating images of some desired form.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>min_width</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Minimum width in pixels.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>min_height</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Minimum height in pixels.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>layers</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Number of layers within a multi-layered image.
Defaults to 1 if not specified.</p>
</td>
            <td>1</td>
        </tr><tr>
            <td><code>pixel_format</code></td>
            <td>
                <code><a class='link' href='#PixelFormat'>PixelFormat</a></code>
            </td>
            <td><p>Pixel format.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>color_space</code></td>
            <td>
                <code><a class='link' href='#ColorSpace'>ColorSpace</a></code>
            </td>
            <td><p>Color space.</p>
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
*Defined in [fuchsia.sysmem/secure_mem.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/secure_mem.fidl#88)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>heap</code></td>
            <td>
                <code><a class='link' href='#HeapType'>HeapType</a></code>
            </td>
            <td><p>This must be a HeapType that is secure/protected.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>physical_address</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Must be at least PAGE_SIZE aligned.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>size_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Must be at least PAGE_SIZE aligned.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### PhysicalSecureHeaps {#PhysicalSecureHeaps}
*Defined in [fuchsia.sysmem/secure_mem.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/secure_mem.fidl#104)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>heaps_count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Must be &lt;= MAX_HEAPS_COUNT.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>heaps</code></td>
            <td>
                <code>[32]</code>
            </td>
            <td><p>Only the first heaps_count are meaningful.  The rest are ignored.</p>
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

<p>Known heap types.
Device specific types should have bit 60 set. Top order bit is reserved
and should not be set.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SYSTEM_RAM</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>AMLOGIC_SECURE</code></td>
            <td><code>1152921504606912512</code></td>
            <td><p>Heap used for amlogic protected memory.</p>
</td>
        </tr><tr>
            <td><code>AMLOGIC_SECURE_VDEC</code></td>
            <td><code>1152921504606912513</code></td>
            <td><p>Heap used for amlogic protected memory between decrypt and video decode.</p>
</td>
        </tr><tr>
            <td><code>GOLDFISH_DEVICE_LOCAL</code></td>
            <td><code>1152921504606978048</code></td>
            <td><p>Heap used by goldfish vulkan for device-local memory.</p>
</td>
        </tr></table>

### CoherencyDomain {#CoherencyDomain}
Type: <code>uint32</code>

*Defined in [fuchsia.sysmem/constraints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/constraints.fidl#227)*

<p>Inaccessible is only for cases where there is no CPU-based access to the
buffers.  A secure_required buffer can still have CoherencyDomain Cpu or
Ram even if the secure_required buffer can only be accessed by the CPU when
the CPU is running in secure mode (or similar).  In contrast, device-local
memory that isn't reachable from the CPU is CoherencyDomain Inaccessible,
even if it's possible to cause a device (physical or virtual) to copy the
data from the Inaccessible buffers to buffers that are visible to the CPU.</p>


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

<p>The ordering of the channels in the format name reflects how
the actual layout of the channel.</p>
<p>Each of these values is opinionated re. the color spaces that can be
contained within (in contrast with Vulkan).</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INVALID</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>R8G8B8A8</code></td>
            <td><code>1</code></td>
            <td><p>RGB only, 8 bits per each of R/G/B/A sample</p>
</td>
        </tr><tr>
            <td><code>BGRA32</code></td>
            <td><code>101</code></td>
            <td><p>32bpp BGRA, 1 plane.  RGB only, 8 bits per each of B/G/R/A sample.</p>
</td>
        </tr><tr>
            <td><code>I420</code></td>
            <td><code>102</code></td>
            <td><p>YUV only, 8 bits per Y sample</p>
</td>
        </tr><tr>
            <td><code>M420</code></td>
            <td><code>103</code></td>
            <td><p>YUV only, 8 bits per Y sample</p>
</td>
        </tr><tr>
            <td><code>NV12</code></td>
            <td><code>104</code></td>
            <td><p>YUV only, 8 bits per Y sample</p>
</td>
        </tr><tr>
            <td><code>YUY2</code></td>
            <td><code>105</code></td>
            <td><p>YUV only, 8 bits per Y sample</p>
</td>
        </tr><tr>
            <td><code>MJPEG</code></td>
            <td><code>106</code></td>
            <td></td>
        </tr><tr>
            <td><code>YV12</code></td>
            <td><code>107</code></td>
            <td><p>YUV only, 8 bits per Y sample</p>
</td>
        </tr><tr>
            <td><code>BGR24</code></td>
            <td><code>108</code></td>
            <td><p>24bpp BGR, 1 plane. RGB only, 8 bits per each of B/G/R sample</p>
</td>
        </tr><tr>
            <td><code>RGB565</code></td>
            <td><code>109</code></td>
            <td><p>16bpp RGB, 1 plane. 5 bits R, 6 bits G, 5 bits B</p>
</td>
        </tr><tr>
            <td><code>RGB332</code></td>
            <td><code>110</code></td>
            <td><p>8bpp RGB, 1 plane. 3 bits R, 3 bits G, 2 bits B</p>
</td>
        </tr><tr>
            <td><code>RGB2220</code></td>
            <td><code>111</code></td>
            <td><p>8bpp RGB, 1 plane. 2 bits R, 2 bits G, 2 bits B</p>
</td>
        </tr><tr>
            <td><code>L8</code></td>
            <td><code>112</code></td>
            <td><p>8bpp, Luminance-only.</p>
</td>
        </tr></table>

### ColorSpaceType {#ColorSpaceType}
Type: <code>uint32</code>

*Defined in [fuchsia.sysmem/image_formats.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/image_formats.fidl#107)*

<p>This list has a separate entry for each variant of a color space standard.</p>
<p>For this reason, should we ever add support for the RGB variant of 709, for
example, we'd add a separate entry to this list for that variant.  Similarly
for the RGB variants of 2020 or 2100.  Similarly for the YcCbcCrc variant of
2020.  Similarly for the ICtCp variant of 2100.</p>
<p>A given ColorSpaceType may permit usage with a PixelFormatType(s) that
provides a bits-per-sample that's compatible with the ColorSpaceType's
official spec.  Not all spec-valid combinations are necessarily supported.
See ImageFormatIsSupportedColorSpaceForPixelFormat() for the best-case degree
of support, but a &quot;true&quot; from that function doesn't guarantee that any given
combination of participants will all support the desired combination of
ColorSpaceType and PixelFormatType.</p>
<p>The sysmem service helps find a mutually supported combination and allocate
suitable buffers.</p>
<p>A ColorSpaceType's spec is not implicitly extended to support
outside-the-standard bits-per-sample (R, G, B, or Y sample).  For example,
for 2020 and 2100, 8 bits-per-Y-sample is not supported (by sysmem), because
8 bits-per-Y-sample is not in the spec for 2020 or 2100.  A sysmem
participant that attempts to advertise support for a PixelFormat + ColorSpace
that's non-standard will cause sysmem to reject the combo and fail to
allocate (intentionally, to strongly discourage specifying
insufficiently-defined combos).</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INVALID</code></td>
            <td><code>0</code></td>
            <td><p>Not a valid color space type.</p>
</td>
        </tr><tr>
            <td><code>SRGB</code></td>
            <td><code>1</code></td>
            <td><p>sRGB</p>
</td>
        </tr><tr>
            <td><code>REC601_NTSC</code></td>
            <td><code>2</code></td>
            <td><p>601 NTSC (&quot;525 line&quot;) YCbCr primaries, narrow</p>
</td>
        </tr><tr>
            <td><code>REC601_NTSC_FULL_RANGE</code></td>
            <td><code>3</code></td>
            <td><p>601 NTSC (&quot;525 line&quot;) YCbCr primaries, wide</p>
</td>
        </tr><tr>
            <td><code>REC601_PAL</code></td>
            <td><code>4</code></td>
            <td><p>601 PAL (&quot;625 line&quot;) YCbCr primaries, narrow</p>
</td>
        </tr><tr>
            <td><code>REC601_PAL_FULL_RANGE</code></td>
            <td><code>5</code></td>
            <td><p>601 PAL (&quot;625 line&quot;) YCbCr primaries, wide</p>
</td>
        </tr><tr>
            <td><code>REC709</code></td>
            <td><code>6</code></td>
            <td><p>709 YCbCr (not RGB)</p>
</td>
        </tr><tr>
            <td><code>REC2020</code></td>
            <td><code>7</code></td>
            <td><p>2020 YCbCr (not RGB, not YcCbcCrc)</p>
</td>
        </tr><tr>
            <td><code>REC2100</code></td>
            <td><code>8</code></td>
            <td><p>2100 YCbCr (not RGB, not ICtCp)</p>
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
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
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
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="FORMAT_MODIFIER_NONE">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#16">FORMAT_MODIFIER_NONE</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr id="FORMAT_MODIFIER_VENDOR_NONE">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#18">FORMAT_MODIFIER_VENDOR_NONE</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr id="FORMAT_MODIFIER_VENDOR_INTEL">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#19">FORMAT_MODIFIER_VENDOR_INTEL</a></td>
            <td>
                    <code>72057594037927936</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr id="FORMAT_MODIFIER_VENDOR_AMD">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#20">FORMAT_MODIFIER_VENDOR_AMD</a></td>
            <td>
                    <code>144115188075855872</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr id="FORMAT_MODIFIER_VENDOR_NVIDIA">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#21">FORMAT_MODIFIER_VENDOR_NVIDIA</a></td>
            <td>
                    <code>216172782113783808</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr id="FORMAT_MODIFIER_VENDOR_SAMSUNG">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#22">FORMAT_MODIFIER_VENDOR_SAMSUNG</a></td>
            <td>
                    <code>288230376151711744</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr id="FORMAT_MODIFIER_VENDOR_QCOM">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#23">FORMAT_MODIFIER_VENDOR_QCOM</a></td>
            <td>
                    <code>360287970189639680</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr id="FORMAT_MODIFIER_VENDOR_VIVANTE">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#24">FORMAT_MODIFIER_VENDOR_VIVANTE</a></td>
            <td>
                    <code>432345564227567616</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr id="FORMAT_MODIFIER_VENDOR_BROADCOM">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#25">FORMAT_MODIFIER_VENDOR_BROADCOM</a></td>
            <td>
                    <code>504403158265495552</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr id="FORMAT_MODIFIER_VENDOR_ARM">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#26">FORMAT_MODIFIER_VENDOR_ARM</a></td>
            <td>
                    <code>576460752303423488</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr id="FORMAT_MODIFIER_VALUE_RESERVED">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#28">FORMAT_MODIFIER_VALUE_RESERVED</a></td>
            <td>
                    <code>72057594037927935</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr id="FORMAT_MODIFIER_INVALID">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#30">FORMAT_MODIFIER_INVALID</a></td>
            <td>
                    <code><a class='link' href='#FORMAT_MODIFIER_VALUE_RESERVED'>FORMAT_MODIFIER_VALUE_RESERVED</a></code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr id="FORMAT_MODIFIER_LINEAR">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#32">FORMAT_MODIFIER_LINEAR</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr id="FORMAT_MODIFIER_INTEL_I915_X_TILED">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#39">FORMAT_MODIFIER_INTEL_I915_X_TILED</a></td>
            <td>
                    <code>72057594037927937</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr id="FORMAT_MODIFIER_INTEL_I915_Y_TILED">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#40">FORMAT_MODIFIER_INTEL_I915_Y_TILED</a></td>
            <td>
                    <code>72057594037927938</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr id="FORMAT_MODIFIER_INTEL_I915_YF_TILED">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#41">FORMAT_MODIFIER_INTEL_I915_YF_TILED</a></td>
            <td>
                    <code>72057594037927939</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr id="FORMAT_MODIFIER_ARM_AFBC_16x16">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#56">FORMAT_MODIFIER_ARM_AFBC_16x16</a></td>
            <td>
                    <code>576460752303423489</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr id="FORMAT_MODIFIER_ARM_AFBC_32x8">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/format_modifier.fidl#57">FORMAT_MODIFIER_ARM_AFBC_32x8</a></td>
            <td>
                    <code>576460752303423490</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr id="MAX_HEAPS_COUNT">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/secure_mem.fidl#101">MAX_HEAPS_COUNT</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="noneUsage">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#21">noneUsage</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="cpuUsageRead">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#25">cpuUsageRead</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="cpuUsageReadOften">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#26">cpuUsageReadOften</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="cpuUsageWrite">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#27">cpuUsageWrite</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="cpuUsageWriteOften">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#28">cpuUsageWriteOften</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="vulkanUsageTransferSrc">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#32">vulkanUsageTransferSrc</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="vulkanUsageTransferDst">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#33">vulkanUsageTransferDst</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="vulkanUsageSampled">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#34">vulkanUsageSampled</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="vulkanUsageStorage">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#35">vulkanUsageStorage</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="vulkanUsageColorAttachment">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#36">vulkanUsageColorAttachment</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="vulkanUsageStencilAttachment">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#37">vulkanUsageStencilAttachment</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="vulkanUsageTransientAttachment">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#38">vulkanUsageTransientAttachment</a></td>
            <td>
                    <code>64</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="vulkanUsageInputAttachment">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#39">vulkanUsageInputAttachment</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="displayUsageLayer">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#42">displayUsageLayer</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="displayUsageCursor">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#43">displayUsageCursor</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="videoUsageHwDecoder">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#47">videoUsageHwDecoder</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="videoUsageHwEncoder">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#48">videoUsageHwEncoder</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="videoUsageHwProtected">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#51">videoUsageHwProtected</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="videoUsageCapture">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#52">videoUsageCapture</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="videoUsageDecryptorOutput">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#65">videoUsageDecryptorOutput</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="videoUsageHwDecoderInternal">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysmem/usages.fidl#69">videoUsageHwDecoderInternal</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    
</table>



