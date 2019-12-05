[TOC]

# fuchsia.scenic.scheduling




## **STRUCTS**

### FuturePresentationTimes {#FuturePresentationTimes}
*Defined in [fuchsia.scenic.scheduling/prediction_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.scenic.scheduling/prediction_info.fidl#37)*



<p>The data type returned in |fuchsia.ui.scenic::RequestPresentationTimes|. See
that method description for more information.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>future_presentations</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#PresentationInfo'>PresentationInfo</a>&gt;[8]</code>
            </td>
            <td><p>The future estimated presentation times. They represent the times Scenic
intends to let the client's work be presented over the next few frames.
These values may change after they are queried.</p>
<p>Clients who wish to minimize latency should use these values to schedule
their work accordingly.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>remaining_presents_in_flight_allowed</code></td>
            <td>
                <code>int64</code>
            </td>
            <td><p>The amount of Present() calls the client is currently allowed. If the
client calls Present() when this number is zero, the session will be
shut down.</p>
<p>This value is decremented every Present() call, and is incremented every
OnFramePresented() event.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### FramePresentedInfo {#FramePresentedInfo}
*Defined in [fuchsia.scenic.scheduling/prediction_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.scenic.scheduling/prediction_info.fidl#55)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>actual_presentation_time</code></td>
            <td>
                <code>int64</code>
            </td>
            <td><p>The time the frame was presented to the user. This value was captured
after the fact, differentiating it from the |presentation_time|s
included in |FuturePresentationTimes|.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>presentation_infos</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#PresentReceivedInfo'>PresentReceivedInfo</a>&gt;[32]</code>
            </td>
            <td><p>The presentation informations for each Present2() that comprised the
content of this frame. These are ordered by present submission order.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>num_presents_allowed</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The number of times remaining that the client can call |Present2|.</p>
</td>
            <td>No default</td>
        </tr>
</table>





## **TABLES**

### PresentationInfo {#PresentationInfo}


*Defined in [fuchsia.scenic.scheduling/prediction_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.scenic.scheduling/prediction_info.fidl#11)*

<p>The times we predict for a future presentation, expressed in nanoseconds in
the |CLOCK_MONOTONIC| timebase.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>latch_point</code></td>
            <td>
                <code>int64</code>
            </td>
            <td><p>The time where Scenic processes all pending updates to its scene graph
and render a new frame. Clients should aim to have all  commands sent
and acquire fences reached in order to have their  content be
presented at the corresponding |presentation_time|. The |latch_point|
is guaranteed to be less than |presentation_time|.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>presentation_time</code></td>
            <td>
                <code>int64</code>
            </td>
            <td><p>The time in which the enqueued operations submitted before |latch_point|
take visible effect. This time is usually but not necessarily vsync.</p>
</td>
        </tr></table>

### PresentReceivedInfo {#PresentReceivedInfo}


*Defined in [fuchsia.scenic.scheduling/prediction_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.scenic.scheduling/prediction_info.fidl#26)*

<p>The times we record for each Present2, expressed in nanoseconds in the
|CLOCK_MONOTONIC| timebase.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>present_received_time</code></td>
            <td>
                <code>int64</code>
            </td>
            <td><p>The time Scenic receives the Present2 call.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>latched_time</code></td>
            <td>
                <code>int64</code>
            </td>
            <td><p>The time Scenic latched the Present2 call to. This is guaranteed to be
greater than the |present_received_time|.</p>
</td>
        </tr></table>











