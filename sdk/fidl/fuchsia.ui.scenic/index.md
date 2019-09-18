Project: /_project.yaml
Book: /_book.yaml

# fuchsia.ui.scenic


## **PROTOCOLS**

## Scenic {:#Scenic}
*Defined in [fuchsia.ui.scenic/scenic.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/scenic.fidl#18)*


### CreateSession {:#CreateSession}

 Create a new Session, which is the primary way to interact with Scenic.

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



### GetDisplayInfo {:#GetDisplayInfo}

 Get information about the Scenic's primary display.

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
                <code><a class='link' href='../fuchsia.ui.gfx/index.html'>fuchsia.ui.gfx</a>/<a class='link' href='../fuchsia.ui.gfx/index.html#DisplayInfo'>DisplayInfo</a></code>
            </td>
        </tr></table>

### GetDisplayOwnershipEvent {:#GetDisplayOwnershipEvent}

 Gets an event signaled with displayOwnedSignal or displayNotOwnedSignal
 when display ownership changes.

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

### TakeScreenshot {:#TakeScreenshot}

 Take a screenshot and return the data in `img_data`. `img_data` will
 not contain BGRA data if `success` is false.

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

## Session {:#Session}
*Defined in [fuchsia.ui.scenic/session.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/session.fidl#12)*

 Client use Sessions to interact with a Scenic instance by enqueuing commands
 that create or modify resources.

### Enqueue {:#Enqueue}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>cmds</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Command'>Command</a>&gt;</code>
            </td>
        </tr></table>



### Present {:#Present}

 Present all previously enqueued operations.  In order to pipeline the
 preparation of the resources required to render the scene, two lists of
 fences (implemented as events) are passed.

 SCHEDULING PRESENTATION

 `presentation_time` specifies the time on or after which the
 client would like the enqueued operations should take visible effect
 (light up pixels on the screen), expressed in nanoseconds in the
 `CLOCK_MONOTONIC` timebase.  Desired presentation times must be
 monotonically non-decreasing.

 Using a desired presentation time in the present or past (such as 0)
 schedules enqueued operations to take visible effect as soon as possible
 (during the next frame to be prepared).

 Using a desired presentation time in the future schedules the enqueued
 operations to take visible effect as closely as possible to or after
 the stated time (but no earlier).

 Each rendered frame has a target presentation time.  Before rendering
 a frame, the scene manager applies all enqueued operations associated
 with all prior calls to `Present()` whose desired presentation time
 is on or before the frame's target presentation time.

 The `Present()` method does not return until the scene manager begins
 preparing the first frame which includes its presented content.
 Upon return, the `PresentationInfo` provides timing information for the
 frame which includes the presented content.

 To present new content on each successive frame, wait for `Present()`
 to return before calling `Present()` again with content for the next
 frame.

 It is also possible to enqueue and present successive frames of content
 all at once with increasing desired presentation times, incrementing by
 `PresentationInfo.presentation_interval` for each one.

 Animation updates are also coordinated in terms of presentation time.

 SYNCHRONIZATION

 `acquire_fences` are used by Scenic to wait until all of the session's
 resources are ready to render (or to allow downstream components, such as
 the Vulkan driver, to wait for these resources).

 For example, Fuchsia's Vulkan driver allows an zx::event to be obtained
 from a VkSemaphore.  This allows a Scenic client to submit a Vulkan command
 buffer to generate images/meshes/etc., and instructing Vulkan to signal a
 VkSemaphore when it is done.  By inserting the zx::event corresponding to
 this semaphore into `acquire_fences`, the client allows Scenic to submit work
 to the Vulkan driver without waiting on the CPU for the event to be
 signalled.

 `release_fences` is a list of events that will be signalled by Scenic when
 the updated session state has been fully committed: future frames will be
 rendered using this state, and all frames generated using previous session
 states have been fully-rendered and presented to the display.

 Together, `acquire_fences` and `release_fences` are intended to allow clients
 to implement strategies such as double-buffering.  For example, a client
 might do the following in the Scenic subsystem:
   1) create two Image with resource IDs #1 and #2.
   2) create two Materials with resource IDs #3 and #4, which respectively
      use Images #1 and #2 as their texture.
   3) create a tree of Nodes and attach them to the scene.
   4) set one of the nodes above, say #5, to use Material #3.
   5) submit a Vulkan command-buffer which renders into Image #1, and
      will signal a VkSemaphore.
   6) call Present() with one acquire-fence (obtained from the VkSemaphore
      above) and one newly-created release-fence.

 After the steps above, Scenic will use the committed session state to render
 frames whenever necessary.  When the client wants to display something
 different than Image #1, it would do something similar to steps 4) to 6):
   7) set Node #5 to use Material #4.
   8) submit a Vulkan command-buffer which renders into Image #1, and
      will signal a VkSemaphore.
   9) call Present() with one acquire-fence (obtained from the VkSemaphore
      above) and one newly-created release-fence.

 Finally, to continually draw new content, the client could repeat steps
 4) to 9), with one important difference: step 5) must wait on the event
 signalled by step 9).  Otherwise, it might render into Image #1 while that
 image is still being used by Scenic to render a frame.  Similarly, step 8)
 must wait on the event signalled by step 6).

 The scenario described above uses one acquire-fence and one release-fence,
 but it is easy to imagine cases that require more.  For example, in addition
 to using Vulkan to render into Images #1 and #2, the client might also
 upload other resources to Vulkan on a different VkQueue, which would
 would signal a separate semaphore, and therefore require an additional
 acquire-fence.

 Note: `acquire_fences` and `release_fences` are only necessary to synchronize
 access to memory (and other external resources).  Any modification to
 resources made via the Session API are automatically synchronized.

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
                <code><a class='link' href='../fuchsia.images/index.html'>fuchsia.images</a>/<a class='link' href='../fuchsia.images/index.html#PresentationInfo'>PresentationInfo</a></code>
            </td>
        </tr></table>

### RequestPresentationTimes {:#RequestPresentationTimes}

 Returns information about future presentation times, and their
 respective latch points. Clients can use the returned information to
 make informed scheduling decisions: if a client wants their frame to be
 displayed at a given presentation time, they should aim to have all of
 their work finished before that presentation time's associated latch point.

 Scenic will attempt to return predictions that span a duration equal to
 |requested_prediction_span|, up to a limit.

 A value of 0 is guaranteed to give at least one future presentation info.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>requested_prediction_span</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request_presentation_times_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.scenic.scheduling/index.html'>fuchsia.scenic.scheduling</a>/<a class='link' href='../fuchsia.scenic.scheduling/index.html#FuturePresentationTimes'>FuturePresentationTimes</a></code>
            </td>
        </tr></table>

### SetDebugName {:#SetDebugName}

 Set an optional debug name for the session. The debug name will be
 output in things such as logging and trace events.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>debug_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



## SessionListener {:#SessionListener}
*Defined in [fuchsia.ui.scenic/session.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/session.fidl#147)*

 Listens for events which occur within the session.

### OnScenicError {:#OnScenicError}

 Called when an error has occurred and the session will be torn down.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### OnScenicEvent {:#OnScenicEvent}

 Called to deliver a batch of one or more events to the listener.
 Use `SetEventMaskCmd` to enable event delivery for a resource.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>events</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Event'>Event</a>&gt;</code>
            </td>
        </tr></table>



## Snapshot {:#Snapshot}
*Defined in [fuchsia.ui.scenic/snapshot.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/snapshot.fidl#9)*

 Defines an interface to take view snapshots.

## Scenic {:#Scenic}
*Defined in [fuchsia.ui.scenic/scenic.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/scenic.fidl#18)*


### CreateSession {:#CreateSession}

 Create a new Session, which is the primary way to interact with Scenic.

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



### GetDisplayInfo {:#GetDisplayInfo}

 Get information about the Scenic's primary display.

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
                <code><a class='link' href='../fuchsia.ui.gfx/index.html'>fuchsia.ui.gfx</a>/<a class='link' href='../fuchsia.ui.gfx/index.html#DisplayInfo'>DisplayInfo</a></code>
            </td>
        </tr></table>

### GetDisplayOwnershipEvent {:#GetDisplayOwnershipEvent}

 Gets an event signaled with displayOwnedSignal or displayNotOwnedSignal
 when display ownership changes.

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

### TakeScreenshot {:#TakeScreenshot}

 Take a screenshot and return the data in `img_data`. `img_data` will
 not contain BGRA data if `success` is false.

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

## Session {:#Session}
*Defined in [fuchsia.ui.scenic/session.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/session.fidl#12)*

 Client use Sessions to interact with a Scenic instance by enqueuing commands
 that create or modify resources.

### Enqueue {:#Enqueue}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>cmds</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Command'>Command</a>&gt;</code>
            </td>
        </tr></table>



### Present {:#Present}

 Present all previously enqueued operations.  In order to pipeline the
 preparation of the resources required to render the scene, two lists of
 fences (implemented as events) are passed.

 SCHEDULING PRESENTATION

 `presentation_time` specifies the time on or after which the
 client would like the enqueued operations should take visible effect
 (light up pixels on the screen), expressed in nanoseconds in the
 `CLOCK_MONOTONIC` timebase.  Desired presentation times must be
 monotonically non-decreasing.

 Using a desired presentation time in the present or past (such as 0)
 schedules enqueued operations to take visible effect as soon as possible
 (during the next frame to be prepared).

 Using a desired presentation time in the future schedules the enqueued
 operations to take visible effect as closely as possible to or after
 the stated time (but no earlier).

 Each rendered frame has a target presentation time.  Before rendering
 a frame, the scene manager applies all enqueued operations associated
 with all prior calls to `Present()` whose desired presentation time
 is on or before the frame's target presentation time.

 The `Present()` method does not return until the scene manager begins
 preparing the first frame which includes its presented content.
 Upon return, the `PresentationInfo` provides timing information for the
 frame which includes the presented content.

 To present new content on each successive frame, wait for `Present()`
 to return before calling `Present()` again with content for the next
 frame.

 It is also possible to enqueue and present successive frames of content
 all at once with increasing desired presentation times, incrementing by
 `PresentationInfo.presentation_interval` for each one.

 Animation updates are also coordinated in terms of presentation time.

 SYNCHRONIZATION

 `acquire_fences` are used by Scenic to wait until all of the session's
 resources are ready to render (or to allow downstream components, such as
 the Vulkan driver, to wait for these resources).

 For example, Fuchsia's Vulkan driver allows an zx::event to be obtained
 from a VkSemaphore.  This allows a Scenic client to submit a Vulkan command
 buffer to generate images/meshes/etc., and instructing Vulkan to signal a
 VkSemaphore when it is done.  By inserting the zx::event corresponding to
 this semaphore into `acquire_fences`, the client allows Scenic to submit work
 to the Vulkan driver without waiting on the CPU for the event to be
 signalled.

 `release_fences` is a list of events that will be signalled by Scenic when
 the updated session state has been fully committed: future frames will be
 rendered using this state, and all frames generated using previous session
 states have been fully-rendered and presented to the display.

 Together, `acquire_fences` and `release_fences` are intended to allow clients
 to implement strategies such as double-buffering.  For example, a client
 might do the following in the Scenic subsystem:
   1) create two Image with resource IDs #1 and #2.
   2) create two Materials with resource IDs #3 and #4, which respectively
      use Images #1 and #2 as their texture.
   3) create a tree of Nodes and attach them to the scene.
   4) set one of the nodes above, say #5, to use Material #3.
   5) submit a Vulkan command-buffer which renders into Image #1, and
      will signal a VkSemaphore.
   6) call Present() with one acquire-fence (obtained from the VkSemaphore
      above) and one newly-created release-fence.

 After the steps above, Scenic will use the committed session state to render
 frames whenever necessary.  When the client wants to display something
 different than Image #1, it would do something similar to steps 4) to 6):
   7) set Node #5 to use Material #4.
   8) submit a Vulkan command-buffer which renders into Image #1, and
      will signal a VkSemaphore.
   9) call Present() with one acquire-fence (obtained from the VkSemaphore
      above) and one newly-created release-fence.

 Finally, to continually draw new content, the client could repeat steps
 4) to 9), with one important difference: step 5) must wait on the event
 signalled by step 9).  Otherwise, it might render into Image #1 while that
 image is still being used by Scenic to render a frame.  Similarly, step 8)
 must wait on the event signalled by step 6).

 The scenario described above uses one acquire-fence and one release-fence,
 but it is easy to imagine cases that require more.  For example, in addition
 to using Vulkan to render into Images #1 and #2, the client might also
 upload other resources to Vulkan on a different VkQueue, which would
 would signal a separate semaphore, and therefore require an additional
 acquire-fence.

 Note: `acquire_fences` and `release_fences` are only necessary to synchronize
 access to memory (and other external resources).  Any modification to
 resources made via the Session API are automatically synchronized.

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
                <code><a class='link' href='../fuchsia.images/index.html'>fuchsia.images</a>/<a class='link' href='../fuchsia.images/index.html#PresentationInfo'>PresentationInfo</a></code>
            </td>
        </tr></table>

### RequestPresentationTimes {:#RequestPresentationTimes}

 Returns information about future presentation times, and their
 respective latch points. Clients can use the returned information to
 make informed scheduling decisions: if a client wants their frame to be
 displayed at a given presentation time, they should aim to have all of
 their work finished before that presentation time's associated latch point.

 Scenic will attempt to return predictions that span a duration equal to
 |requested_prediction_span|, up to a limit.

 A value of 0 is guaranteed to give at least one future presentation info.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>requested_prediction_span</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request_presentation_times_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.scenic.scheduling/index.html'>fuchsia.scenic.scheduling</a>/<a class='link' href='../fuchsia.scenic.scheduling/index.html#FuturePresentationTimes'>FuturePresentationTimes</a></code>
            </td>
        </tr></table>

### SetDebugName {:#SetDebugName}

 Set an optional debug name for the session. The debug name will be
 output in things such as logging and trace events.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>debug_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



## SessionListener {:#SessionListener}
*Defined in [fuchsia.ui.scenic/session.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/session.fidl#147)*

 Listens for events which occur within the session.

### OnScenicError {:#OnScenicError}

 Called when an error has occurred and the session will be torn down.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### OnScenicEvent {:#OnScenicEvent}

 Called to deliver a batch of one or more events to the listener.
 Use `SetEventMaskCmd` to enable event delivery for a resource.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>events</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Event'>Event</a>&gt;</code>
            </td>
        </tr></table>



## Snapshot {:#Snapshot}
*Defined in [fuchsia.ui.scenic/snapshot.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/snapshot.fidl#9)*

 Defines an interface to take view snapshots.



## **STRUCTS**

### ScreenshotData {:#ScreenshotData}
*Defined in [fuchsia.ui.scenic/scenic.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/scenic.fidl#12)*



 Scenic.TakeScreenshot() returns a raw BGRA formatted image in this struct.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.images/index.html'>fuchsia.images</a>/<a class='link' href='../fuchsia.images/index.html#ImageInfo'>ImageInfo</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ScreenshotData {:#ScreenshotData}
*Defined in [fuchsia.ui.scenic/scenic.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/scenic.fidl#12)*



 Scenic.TakeScreenshot() returns a raw BGRA formatted image in this struct.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.images/index.html'>fuchsia.images</a>/<a class='link' href='../fuchsia.images/index.html#ImageInfo'>ImageInfo</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>







## **UNIONS**

### Command {:#Command}
*Defined in [fuchsia.ui.scenic/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/commands.fidl#12)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>gfx</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html'>fuchsia.ui.gfx</a>/<a class='link' href='../fuchsia.ui.gfx/index.html#Command'>Command</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>vectorial</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.vectorial/index.html'>fuchsia.ui.vectorial</a>/<a class='link' href='../fuchsia.ui.vectorial/index.html#Command'>Command</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>views</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#Command'>Command</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>input</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.input/index.html'>fuchsia.ui.input</a>/<a class='link' href='../fuchsia.ui.input/index.html#Command'>Command</a></code>
            </td>
            <td></td>
        </tr></table>

### Event {:#Event}
*Defined in [fuchsia.ui.scenic/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/events.fidl#10)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>gfx</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html'>fuchsia.ui.gfx</a>/<a class='link' href='../fuchsia.ui.gfx/index.html#Event'>Event</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>input</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.input/index.html'>fuchsia.ui.input</a>/<a class='link' href='../fuchsia.ui.input/index.html#InputEvent'>InputEvent</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>unhandled</code></td>
            <td>
                <code><a class='link' href='#Command'>Command</a></code>
            </td>
            <td></td>
        </tr></table>

### Command {:#Command}
*Defined in [fuchsia.ui.scenic/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/commands.fidl#12)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>gfx</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html'>fuchsia.ui.gfx</a>/<a class='link' href='../fuchsia.ui.gfx/index.html#Command'>Command</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>vectorial</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.vectorial/index.html'>fuchsia.ui.vectorial</a>/<a class='link' href='../fuchsia.ui.vectorial/index.html#Command'>Command</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>views</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#Command'>Command</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>input</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.input/index.html'>fuchsia.ui.input</a>/<a class='link' href='../fuchsia.ui.input/index.html#Command'>Command</a></code>
            </td>
            <td></td>
        </tr></table>

### Event {:#Event}
*Defined in [fuchsia.ui.scenic/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/events.fidl#10)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>gfx</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html'>fuchsia.ui.gfx</a>/<a class='link' href='../fuchsia.ui.gfx/index.html#Event'>Event</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>input</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.input/index.html'>fuchsia.ui.input</a>/<a class='link' href='../fuchsia.ui.input/index.html#InputEvent'>InputEvent</a></code>
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
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/scenic.fidl#37">displayOwnedSignal</a></td>
            <td>
                    <code>33554432</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/scenic.fidl#38">displayNotOwnedSignal</a></td>
            <td>
                    <code>16777216</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/scenic.fidl#37">displayOwnedSignal</a></td>
            <td>
                    <code>33554432</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic/scenic.fidl#38">displayNotOwnedSignal</a></td>
            <td>
                    <code>16777216</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    
</table>

