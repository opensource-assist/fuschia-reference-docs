[TOC]

# fuchsia.ui.scenic


## **PROTOCOLS**

## PointerCaptureListener {#PointerCaptureListener}
*Defined in [fuchsia.ui.scenic/pointer_capture.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/pointer_capture.fidl#11)*

<p>A method of obtaining global pointer events, regardless of view focus.</p>

### OnPointerEvent {#OnPointerEvent}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>event</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.input/'>fuchsia.ui.input</a>/<a class='link' href='../fuchsia.ui.input/#PointerEvent'>PointerEvent</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## PointerCaptureListenerRegistry {#PointerCaptureListenerRegistry}
*Defined in [fuchsia.ui.scenic/pointer_capture.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/pointer_capture.fidl#17)*

<p>Injects a listener protocol, along with a ViewRef that defines the coordinate space of the captured pointer events.</p>

### RegisterListener {#RegisterListener}

<p>This protocol will be subsumed by gesture disambiguation.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='#PointerCaptureListener'>PointerCaptureListener</a></code>
            </td>
        </tr><tr>
            <td><code>view_ref</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/#ViewRef'>ViewRef</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>success</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

## Scenic {#Scenic}
*Defined in [fuchsia.ui.scenic/scenic.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/scenic.fidl#19)*


### CreateSession {#CreateSession}

<p>Create a new Session, which is the primary way to interact with Scenic.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>session</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Session'>Session</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='#SessionListener'>SessionListener</a>?</code>
            </td>
        </tr></table>



### CreateSession2 {#CreateSession2}

<p>Create a new Session, which is the primary way to interact with Scenic.</p>
<p>In this variant, the caller may register a request for focus management.
The |view_focuser|'s client is coupled to the requested |session|, and
this coupling acts as a security boundary: the ViewRef used as the basis
for authority by |view_focuser| must come from |session|.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>session</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Session'>Session</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='#SessionListener'>SessionListener</a>?</code>
            </td>
        </tr><tr>
            <td><code>view_focuser</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.ui.views/'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/#Focuser'>Focuser</a>&gt;?</code>
            </td>
        </tr></table>



### GetDisplayInfo {#GetDisplayInfo}

<p>Get information about the Scenic's primary display.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/'>fuchsia.ui.gfx</a>/<a class='link' href='../fuchsia.ui.gfx/#DisplayInfo'>DisplayInfo</a></code>
            </td>
        </tr></table>

### GetDisplayOwnershipEvent {#GetDisplayOwnershipEvent}

<p>Gets an event signaled with displayOwnedSignal or displayNotOwnedSignal
when display ownership changes.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ownership_event</code></td>
            <td>
                <code>handle&lt;event&gt;</code>
            </td>
        </tr></table>

### TakeScreenshot {#TakeScreenshot}

<p>Take a screenshot and return the data in <code>img_data</code>. <code>img_data</code> will
not contain BGRA data if <code>success</code> is false.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>img_data</code></td>
            <td>
                <code><a class='link' href='#ScreenshotData'>ScreenshotData</a></code>
            </td>
        </tr><tr>
            <td><code>success</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

## Session {#Session}
*Defined in [fuchsia.ui.scenic/session.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/session.fidl#53)*

<p>Client use Sessions to interact with a Scenic instance by enqueuing commands
that create or modify resources.</p>

### Enqueue {#Enqueue}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>cmds</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Command'>Command</a>&gt;</code>
            </td>
        </tr></table>



### Present {#Present}

<p>Present all previously enqueued operations.  In order to pipeline the
preparation of the resources required to render the scene, two lists of
fences (implemented as events) are passed.</p>
<p>SCHEDULING PRESENTATION</p>
<p><code>presentation_time</code> specifies the time on or after which the
client would like the enqueued operations should take visible effect
(light up pixels on the screen), expressed in nanoseconds in the
<code>CLOCK_MONOTONIC</code> timebase.  Desired presentation times must be
monotonically non-decreasing.</p>
<p>Using a desired presentation time in the present or past (such as 0)
schedules enqueued operations to take visible effect as soon as possible
(during the next frame to be prepared).</p>
<p>Using a desired presentation time in the future schedules the enqueued
operations to take visible effect as closely as possible to or after
the stated time (but no earlier).</p>
<p>Each rendered frame has a target presentation time.  Before rendering
a frame, the scene manager applies all enqueued operations associated
with all prior calls to <code>Present()</code> whose desired presentation time
is on or before the frame's target presentation time.</p>
<p>The <code>Present()</code> method does not return until the scene manager begins
preparing the first frame which includes its presented content.
Upon return, the <code>PresentationInfo</code> provides timing information for the
frame which includes the presented content.</p>
<p>To present new content on each successive frame, wait for <code>Present()</code>
to return before calling <code>Present()</code> again with content for the next
frame.</p>
<p>It is also possible to enqueue and present successive frames of content
all at once with increasing desired presentation times, incrementing by
<code>PresentationInfo.presentation_interval</code> for each one.</p>
<p>Animation updates are also coordinated in terms of presentation time.</p>
<p>SYNCHRONIZATION</p>
<p><code>acquire_fences</code> are used by Scenic to wait until all of the session's
resources are ready to render (or to allow downstream components, such as
the Vulkan driver, to wait for these resources).</p>
<p>For example, Fuchsia's Vulkan driver allows an zx::event to be obtained
from a VkSemaphore.  This allows a Scenic client to submit a Vulkan command
buffer to generate images/meshes/etc., and instructing Vulkan to signal a
VkSemaphore when it is done.  By inserting the zx::event corresponding to
this semaphore into <code>acquire_fences</code>, the client allows Scenic to submit work
to the Vulkan driver without waiting on the CPU for the event to be
signalled.</p>
<p><code>release_fences</code> is a list of events that will be signalled by Scenic when
the updated session state has been fully committed: future frames will be
rendered using this state, and all frames generated using previous session
states have been fully-rendered and presented to the display.</p>
<p>Together, <code>acquire_fences</code> and <code>release_fences</code> are intended to allow clients
to implement strategies such as double-buffering.  For example, a client
might do the following in the Scenic subsystem:</p>
<ol>
<li>create two Image with resource IDs #1 and #2.</li>
<li>create two Materials with resource IDs #3 and #4, which respectively
use Images #1 and #2 as their texture.</li>
<li>create a tree of Nodes and attach them to the scene.</li>
<li>set one of the nodes above, say #5, to use Material #3.</li>
<li>submit a Vulkan command-buffer which renders into Image #1, and
will signal a VkSemaphore.</li>
<li>call Present() with one acquire-fence (obtained from the VkSemaphore
above) and one newly-created release-fence.</li>
</ol>
<p>After the steps above, Scenic will use the committed session state to render
frames whenever necessary.  When the client wants to display something
different than Image #1, it would do something similar to steps 4) to 6):
7) set Node #5 to use Material #4.
8) submit a Vulkan command-buffer which renders into Image #1, and
will signal a VkSemaphore.
9) call Present() with one acquire-fence (obtained from the VkSemaphore
above) and one newly-created release-fence.</p>
<p>Finally, to continually draw new content, the client could repeat steps
4) to 9), with one important difference: step 5) must wait on the event
signalled by step 9).  Otherwise, it might render into Image #1 while that
image is still being used by Scenic to render a frame.  Similarly, step 8)
must wait on the event signalled by step 6).</p>
<p>The scenario described above uses one acquire-fence and one release-fence,
but it is easy to imagine cases that require more.  For example, in addition
to using Vulkan to render into Images #1 and #2, the client might also
upload other resources to Vulkan on a different VkQueue, which would
would signal a separate semaphore, and therefore require an additional
acquire-fence.</p>
<p>Note: <code>acquire_fences</code> and <code>release_fences</code> are only necessary to synchronize
access to memory (and other external resources).  Any modification to
resources made via the Session API are automatically synchronized.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>presentation_time</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>acquire_fences</code></td>
            <td>
                <code>vector&lt;event&gt;</code>
            </td>
        </tr><tr>
            <td><code>release_fences</code></td>
            <td>
                <code>vector&lt;event&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>presentation_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.images/'>fuchsia.images</a>/<a class='link' href='../fuchsia.images/#PresentationInfo'>PresentationInfo</a></code>
            </td>
        </tr></table>

### Present2 {#Present2}

<p>Present all previously enqueued operations. In order to pipeline the
preparation of the resources required to render the scene, two lists of
fences, implemented as events, are passed.</p>
<p>When a client calls Present2, they receive an immediate callback
consisting of the same information they would get as if they had called
|RequestPresentationTimes| with the equivalent
|requested_prediction_span|. See its documentation below for more
information, as Present2's functionality is a superset of it.</p>
<p>Then, when the commands flushed by Present2 make it to display, an
|OnFramePresented| event is fired. This event includes information
pertaining to all Present2s that had content that were part of that
frame.</p>
<p>Clients may only use one of Present/Present2 per Session.
Switching between both is an error that will result in the Session being
closed.</p>
<p>See |Present2Args| documentation above for more detailed information on
what arguments are passed in and their role.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>args</code></td>
            <td>
                <code><a class='link' href='#Present2Args'>Present2Args</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request_presentation_times_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.scenic.scheduling/'>fuchsia.scenic.scheduling</a>/<a class='link' href='../fuchsia.scenic.scheduling/#FuturePresentationTimes'>FuturePresentationTimes</a></code>
            </td>
        </tr></table>

### OnFramePresented {#OnFramePresented}

<p>This event is fired whenever a set of one or more Present2s are
presented simultaenously, and are therefore no longer in flight.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>frame_presented_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.scenic.scheduling/'>fuchsia.scenic.scheduling</a>/<a class='link' href='../fuchsia.scenic.scheduling/#FramePresentedInfo'>FramePresentedInfo</a></code>
            </td>
        </tr></table>

### RequestPresentationTimes {#RequestPresentationTimes}

<p>Returns information about future presentation times, and their
respective latch points. Clients can use the returned information to
make informed scheduling decisions: if a client wants their frame to be
displayed at a given |presentation_time|, they should aim to have all
|acquire_fences| fired before the associated |latch_point|.</p>
<p>Scenic will attempt to return predictions that span a duration equal to
|requested_prediction_span|, up to a limit.</p>
<p>A value of 0 is guaranteed to give at least one future presentation info.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>requested_prediction_span</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#duration'>duration</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request_presentation_times_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.scenic.scheduling/'>fuchsia.scenic.scheduling</a>/<a class='link' href='../fuchsia.scenic.scheduling/#FuturePresentationTimes'>FuturePresentationTimes</a></code>
            </td>
        </tr></table>

### SetDebugName {#SetDebugName}

<p>Set an optional debug name for the session. The debug name will be
output in things such as logging and trace events.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>debug_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



## SessionListener {#SessionListener}
*Defined in [fuchsia.ui.scenic/session.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/session.fidl#216)*

<p>Listens for events which occur within the session.</p>

### OnScenicError {#OnScenicError}

<p>Called when an error has occurred and the session will be torn down.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### OnScenicEvent {#OnScenicEvent}

<p>Called to deliver a batch of one or more events to the listener.
Use <code>SetEventMaskCmd</code> to enable event delivery for a resource.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>events</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Event'>Event</a>&gt;</code>
            </td>
        </tr></table>



## Snapshot {#Snapshot}
*Defined in [fuchsia.ui.scenic/snapshot.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/snapshot.fidl#9)*

<p>Defines an interface to take view snapshots.</p>



## **STRUCTS**

### ScreenshotData {#ScreenshotData}
*Defined in [fuchsia.ui.scenic/scenic.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/scenic.fidl#13)*



<p>Scenic.TakeScreenshot() returns a raw BGRA formatted image in this struct.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.images/'>fuchsia.images</a>/<a class='link' href='../fuchsia.images/#ImageInfo'>ImageInfo</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>





## **TABLES**

### Present2Args {#Present2Args}


*Defined in [fuchsia.ui.scenic/session.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/session.fidl#12)*

<p>Arguments passed into Present2(). Note that every argument is mandatory.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>requested_presentation_time</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#time'>time</a></code>
            </td>
            <td><p>|requested_presentation_time| specifies the time on or after which the
client would like the enqueued operations to take visible effect
(light up pixels on the screen), expressed in nanoseconds in the
<code>CLOCK_MONOTONIC</code> timebase.</p>
<p>Using a |requested_presentation_time| in the present or past (such as 0)
schedules enqueued operations to take visible effect as soon as
possible, during the next frame to be prepared. Requested presentation
times must be monotonically increasing.</p>
<p>Using a |requested_presentation_time| in the future schedules the enqueued
operations to take visible effect as closely as possible to or after
the stated time, but no earlier.</p>
<p>Each rendered frame has a target presentation time. This is when Scenic
aims to have the frame presented to the user. Before rendering a frame,
the scene manager applies all enqueued operations associated with all
prior calls to Present2 whose |requested_presentation_time| is on or
before the frame's target presentation time.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>acquire_fences</code></td>
            <td>
                <code>vector&lt;event&gt;</code>
            </td>
            <td><p>Scenic will wait until all of a session's |acquire_fences| are ready
before it will execute the presented commands.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>release_fences</code></td>
            <td>
                <code>vector&lt;event&gt;</code>
            </td>
            <td><p>|release_fences| is the list of events that will be signalled by Scenic when
the following Present2 call's |acquire_fences| has been signalled, and
the updated session state has been fully committed: future frames will be
rendered using this state, and all frames generated using previous session
states have been fully-rendered and presented to the display.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>requested_prediction_span</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#duration'>duration</a></code>
            </td>
            <td><p>|requested_prediction_span| is the amount of time into the future Scenic
will provide predictions for. A span of 0 is guaranteed to provide at
least one future time.</p>
</td>
        </tr></table>



## **UNIONS**

### Command {#Command}
*Defined in [fuchsia.ui.scenic/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/commands.fidl#12)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>gfx</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/'>fuchsia.ui.gfx</a>/<a class='link' href='../fuchsia.ui.gfx/#Command'>Command</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>vectorial</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.vectorial/'>fuchsia.ui.vectorial</a>/<a class='link' href='../fuchsia.ui.vectorial/#Command'>Command</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>views</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/#Command'>Command</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>input</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.input/'>fuchsia.ui.input</a>/<a class='link' href='../fuchsia.ui.input/#Command'>Command</a></code>
            </td>
            <td></td>
        </tr></table>

### Event {#Event}
*Defined in [fuchsia.ui.scenic/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/events.fidl#10)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>gfx</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/'>fuchsia.ui.gfx</a>/<a class='link' href='../fuchsia.ui.gfx/#Event'>Event</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>input</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.input/'>fuchsia.ui.input</a>/<a class='link' href='../fuchsia.ui.input/#InputEvent'>InputEvent</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>unhandled</code></td>
            <td>
                <code><a class='link' href='#Command'>Command</a></code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="displayOwnedSignal">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/scenic.fidl#48">displayOwnedSignal</a></td>
            <td>
                    <code>33554432</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="displayNotOwnedSignal">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/scenic.fidl#49">displayNotOwnedSignal</a></td>
            <td>
                    <code>16777216</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    
</table>



