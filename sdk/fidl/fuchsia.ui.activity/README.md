[TOC]

# fuchsia.ui.activity


## **PROTOCOLS**

## Control {#Control}
*Defined in [fuchsia.ui.activity/control.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.activity/control.fidl#19)*

<p>The Control protocol can be used to override the activity state of the
Activity Service.</p>
<p>State provided through this interface takes precedence over state which
is determined based on activity sent through the Tracker API.</p>
<p>Once a state has been assigned through this protocol, the Activity
Service will no longer determine state based on input to the Tracker
protocol, and instead will only report state transitions occuring through
the Control protocol.</p>

### SetState {#SetState}

<p>Sets the Activity Service's state to |state|.
All listeners registered through the Provider protocol will immediately
be notified of the new state.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#State'>State</a></code>
            </td>
        </tr></table>



## Provider {#Provider}
*Defined in [fuchsia.ui.activity/provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.activity/provider.fidl#12)*

<p>The Provider protocol offers a subscription interface through
which clients can watch for changes in the system's activity state.</p>

### WatchState {#WatchState}

<p>Subscribe to changes in the system's state.
The server will always invoke listener.OnStateChanged at least once with
the initial state, and after that invoke listener.OnStateChanged
whenever the system's state changes.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='#Listener'>Listener</a></code>
            </td>
        </tr></table>



## Listener {#Listener}
*Defined in [fuchsia.ui.activity/provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.activity/provider.fidl#23)*

<p>The Listener protocol subscribes to changes in the system's activity
state. Clients which care about the activity state of the system are
expected to implement this protocol and subscribe via Provider.WatchState.</p>

### OnStateChanged {#OnStateChanged}

<p>Callback that is invoked whenever the system state changes.
The Listener is expected to acknowledge each call explicitly and will
not receive new state until this acknowledgement is done.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#State'>State</a></code>
            </td>
        </tr><tr>
            <td><code>transition_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## Tracker {#Tracker}
*Defined in [fuchsia.ui.activity/tracker.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.activity/tracker.fidl#14)*

<p>The Tracker protocol collects evidence of user activity and uses this
evidence to set the system's activity state.</p>

### ReportDiscreteActivity {#ReportDiscreteActivity}

<p>Reports a discrete activity such as a keystroke.
|event_time| is in nanoseconds in the <code>CLOCK_MONOTONIC</code> time base.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>activity</code></td>
            <td>
                <code><a class='link' href='#DiscreteActivity'>DiscreteActivity</a></code>
            </td>
        </tr><tr>
            <td><code>event_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>



### StartOngoingActivity {#StartOngoingActivity}

<p>Reports the start of an ongoing activity such as media playback.
Returns a unique |activity_id| which is expected to be later passed
to EndOngoingActivity.
|start_time| is in nanoseconds in the <code>CLOCK_MONOTONIC</code> time base.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>activity</code></td>
            <td>
                <code><a class='link' href='#OngoingActivity'>OngoingActivity</a></code>
            </td>
        </tr><tr>
            <td><code>start_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>activity_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### EndOngoingActivity {#EndOngoingActivity}

<p>Reports the end of an ongoing activity such as media playback.
|activity_id| is the nonce which was returned by StartOngoingActivity.
|end_time| is in nanoseconds in the <code>CLOCK_MONOTONIC</code> time base.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>activity_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>end_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>







## **ENUMS**

### LidState {#LidState}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.activity/activity.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.activity/activity.fidl#38)*

<p>LidState is an enumeration of states that a clamshell-like device's lid may
be in.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>OPEN</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>CLOSED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>FLIPPED</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### State {#State}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.activity/state.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.activity/state.fidl#8)*

<p>State is an enumeration of the activity states the system may be in.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>IDLE</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>ACTIVE</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### GenericActivity {#GenericActivity}


*Defined in [fuchsia.ui.activity/activity.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.activity/activity.fidl#24)*

<p>GenericActivity is a user or system activity of unspecified type, e.g.
a keyboard press or an alarm going off.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>label</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>Brief human-readable label for the activity, for logging/debugging.
e.g. &quot;cursor&quot;, &quot;key&quot;, &quot;video&quot;</p>
</td>
        </tr></table>

### LidActivity {#LidActivity}


*Defined in [fuchsia.ui.activity/activity.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.activity/activity.fidl#32)*

<p>LidActivity is an event originating from a change in the state of the lid
of a clamshell-like device.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#LidState'>LidState</a></code>
            </td>
            <td></td>
        </tr></table>





## **XUNIONS**

### DiscreteActivity {#DiscreteActivity}
*Defined in [fuchsia.ui.activity/activity.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.activity/activity.fidl#8)*

<p>DiscreteActivity is an activity which occurs at a point in time.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>generic</code></td>
            <td>
                <code><a class='link' href='#GenericActivity'>GenericActivity</a></code>
            </td>
            <td><p>Activities that require no special handling.</p>
</td>
        </tr><tr>
            <td><code>lid</code></td>
            <td>
                <code><a class='link' href='#LidActivity'>LidActivity</a></code>
            </td>
            <td><p>An activity originating from opening or closing the lid of a
clamshell-format device.</p>
</td>
        </tr></table>

### OngoingActivity {#OngoingActivity}
*Defined in [fuchsia.ui.activity/activity.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.activity/activity.fidl#17)*

<p>OngoingActivity is an activity which has a definite start and end time.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>generic</code></td>
            <td>
                <code><a class='link' href='#GenericActivity'>GenericActivity</a></code>
            </td>
            <td><p>Activities that require no special handling.</p>
</td>
        </tr></table>







## **TYPE ALIASES**

<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.activity/tracker.fidl#9">OngoingActivityId</a></td>
            <td>
                <code>uint32</code></td>
            <td></td>
        </tr></table>

