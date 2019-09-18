Project: /_project.yaml
Book: /_book.yaml

# fuchsia.scenic.scheduling




## **STRUCTS**

### PresentationInfo {:#PresentationInfo}
*Defined in [fuchsia.scenic.scheduling/prediction_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.scenic.scheduling/prediction_info.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>latch_point</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The |latch_point| is guaranteed to be less than |presentation_time|. The
 latch point is the time where clients should aim to have their updates
 and fences ready in order for the content to be presented at the
 corresponding presentation time.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>presentation_time</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The predicted time in which the enqueued operations are anticipated to take
 visible effect, expressed in nanoseconds in the |CLOCK_MONOTONIC| timebase.
</td>
            <td>No default</td>
        </tr>
</table>

### FuturePresentationTimes {:#FuturePresentationTimes}
*Defined in [fuchsia.scenic.scheduling/prediction_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.scenic.scheduling/prediction_info.fidl#21)*



 The data type returned in |fuchsia.ui.scenic::RequestPresentationTimes|. See
 that method description for more information.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>future_presentations</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#PresentationInfo'>PresentationInfo</a>&gt;[8]</code>
            </td>
            <td> The future estimated presentation times. They represent the times Scenic
 intends to let the client's work be presented over the next few frames.
 These values may change after they are queried.

 Clients who wish to minimize latency should use these values to schedule
 their work accordingly.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>remaining_presents_in_flight_allowed</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> The amount of Present() calls the client is currently allowed. If the
 client calls Present() when this number is zero, the session will be
 shut down.

 This value is decremented every Present() call, and is incremented every
 OnFramePresented() event.
</td>
            <td>No default</td>
        </tr>
</table>

### PresentationInfo {:#PresentationInfo}
*Defined in [fuchsia.scenic.scheduling/prediction_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.scenic.scheduling/prediction_info.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>latch_point</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The |latch_point| is guaranteed to be less than |presentation_time|. The
 latch point is the time where clients should aim to have their updates
 and fences ready in order for the content to be presented at the
 corresponding presentation time.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>presentation_time</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The predicted time in which the enqueued operations are anticipated to take
 visible effect, expressed in nanoseconds in the |CLOCK_MONOTONIC| timebase.
</td>
            <td>No default</td>
        </tr>
</table>

### FuturePresentationTimes {:#FuturePresentationTimes}
*Defined in [fuchsia.scenic.scheduling/prediction_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.scenic.scheduling/prediction_info.fidl#21)*



 The data type returned in |fuchsia.ui.scenic::RequestPresentationTimes|. See
 that method description for more information.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>future_presentations</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#PresentationInfo'>PresentationInfo</a>&gt;[8]</code>
            </td>
            <td> The future estimated presentation times. They represent the times Scenic
 intends to let the client's work be presented over the next few frames.
 These values may change after they are queried.

 Clients who wish to minimize latency should use these values to schedule
 their work accordingly.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>remaining_presents_in_flight_allowed</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> The amount of Present() calls the client is currently allowed. If the
 client calls Present() when this number is zero, the session will be
 shut down.

 This value is decremented every Present() call, and is incremented every
 OnFramePresented() event.
</td>
            <td>No default</td>
        </tr>
</table>













