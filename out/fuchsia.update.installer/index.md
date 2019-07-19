Project: /_project.yaml
Book: /_book.yaml

# fuchsia.update.installer


## **PROTOCOLS**

## Installer {:#Installer}
*Defined in [fuchsia.update.installer/installer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update.installer/installer.fidl#14)*

 Updates the system.

 This protocol is intended to be consumed by a component capable of
 discovering when to update and what version of the system to install.

### GetLastUpdateResult {:#GetLastUpdateResult}

 Get the status of the last update attempt. If this device hasn't
 attempted an update since the last factory reset, every field in the
 result will be absent.

 - response `info` the status of the last update attempt, if available.

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
                <code><a class='link' href='../fuchsia.update.installer/index.html#UpdateResult'>UpdateResult</a></code>
            </td>
        </tr></table>

### GetUpdateResult {:#GetUpdateResult}

 Get the status of the given update attempt, if it exists. If this device
 hasn't attempted an update with the given `attempt_id` or forgotten about
 that attempt, every field in the result will be absent.

 + request `attempt_id` UUID identifying the requested update attempt.
 - response `info` the status of the last update attempt, if available.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>attempt_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.update.installer/index.html#UpdateResult'>UpdateResult</a></code>
            </td>
        </tr></table>

### StartUpdate {:#StartUpdate}

 Start an update if one is not running, or attach to a pending update
 attempt. Attach the provided monitor to the update attempt.

 + request `url` The fuchsia-pkg URL of the update package to update to.
 + request `options` Configuration options for this update attempt. Ignored or merged
     with the existing `options` if an update attempt is already in progress.
 + request `monitor` A protocol on which to receive progress updates.
 + request `monitor_options` Configuration options to control the behavior of the
     given <a class='link' href='../fuchsia.update.installer/index.html#Monitor'>Monitor</a>.

 - response `attempt_id` UUID identifying this update attempt. For
     updates that require a reboot, components may use this identifier to
     disambiguate the completion of this update attempt from new update
     attempts that start post-reboot.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>url</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='../fuchsia.update.installer/index.html#Options'>Options</a></code>
            </td>
        </tr><tr>
            <td><code>monitor</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.update.installer/index.html#Monitor'>Monitor</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>monitor_options</code></td>
            <td>
                <code><a class='link' href='../fuchsia.update.installer/index.html#MonitorOptions'>MonitorOptions</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>attempt_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

### MonitorUpdate {:#MonitorUpdate}

 Attempt to monitor a specific update attempt, if it exists. This API
 will not start an update if one is not already running.

 + request `attempt_id` UUID identifying the requested update attempt. If
     not given, monitor any active update attempt.
 + request `monitor` A protocol on which to receive progress updates.
 + request `monitor_options` Configuration options to control the behavior of the
     given <a class='link' href='../fuchsia.update.installer/index.html#Monitor'>Monitor</a>.

 - response `attached` Whether or not the provided monitor was attached
     to an in-progress update attempt. If false, monitor will be closed
     by the server.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>attempt_id</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr><tr>
            <td><code>monitor</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.update.installer/index.html#Monitor'>Monitor</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>monitor_options</code></td>
            <td>
                <code><a class='link' href='../fuchsia.update.installer/index.html#MonitorOptions'>MonitorOptions</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>attached</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

### MonitorAllUpdates {:#MonitorAllUpdates}

 Monitor all update attempts as they start, as well as an in-progress
 attempt, if there is one.

 + request `attempts_monitor` A protocol on which to receive <a class='link' href='../fuchsia.update.installer/index.html#Monitor'>Monitor</a>
     instances as update attempts start.
 + request `monitor_options` Configuration options to control the behavior of the
     given <a class='link' href='../fuchsia.update.installer/index.html#Monitor'>Monitor</a>.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>attempts_monitor</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.update.installer/index.html#AttemptsMonitor'>AttemptsMonitor</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>monitor_options</code></td>
            <td>
                <code><a class='link' href='../fuchsia.update.installer/index.html#MonitorOptions'>MonitorOptions</a></code>
            </td>
        </tr></table>



## AttemptsMonitor {:#AttemptsMonitor}
*Defined in [fuchsia.update.installer/progress.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update.installer/progress.fidl#8)*

 Monitors update attempts as they start.

### OnStart {:#OnStart}

 Emitted when a new update attempt has started.

 + request `attempt_id` UUID identifying this update attempt.
 + request `monitor` A protocol on which to receive progress updates.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>attempt_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>monitor</code></td>
            <td>
                <code><a class='link' href='../fuchsia.update.installer/index.html#Monitor'>Monitor</a></code>
            </td>
        </tr></table>

## Monitor {:#Monitor}
*Defined in [fuchsia.update.installer/progress.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update.installer/progress.fidl#23)*

 Monitors an update attempt.

 When a Monitor is attached to an update attempt with
 <a class='link' href='../fuchsia.update.installer/index.html#MonitorOptions.should_notify'>MonitorOptions.should_notify</a> set to true, the server will emit events on
 the protocol that the client must consume. Clients that attach to an attempt
 will be sent any events they may have missed (by attaching to an update
 attempt after it has started, for example).

### OnStateEnter {:#OnStateEnter}

 Emitted when transitioning from one state to another.

 - response `state` The new state.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.update.installer/index.html#State'>State</a></code>
            </td>
        </tr></table>

### GetNextProgress {:#GetNextProgress}

 Retrieve the latest progress of this update attempt, blocking until
 newer progress is available if this client has already seen the
 currently available progress. If this update attempt has completed (or
 failed), this API immediately returns the final progress.

 - response `progress` The latest progress of this update attempt.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>progress</code></td>
            <td>
                <code><a class='link' href='../fuchsia.update.installer/index.html#Progress'>Progress</a></code>
            </td>
        </tr></table>





## **ENUMS**

### Initiator {:#Initiator}
Type: <code>uint32</code>

*Defined in [fuchsia.update.installer/installer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update.installer/installer.fidl#116)*

 Who or what initiated the update check.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>USER</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>SERVICE</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### State {:#State}
Type: <code>uint32</code>

*Defined in [fuchsia.update.installer/progress.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update.installer/progress.fidl#40)*

 States that an update attempt may transition through. An update attempt
 always starts in <a class='link' href='../fuchsia.update.installer/index.html#State.PREPARE'>State.PREPARE</a>. See each state for more details.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>PREPARE</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>DOWNLOAD</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>STAGE</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>REBOOT</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>FINALIZE</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>COMPLETE</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>FAIL</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### UpdateResult {:#UpdateResult}


*Defined in [fuchsia.update.installer/installer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update.installer/installer.fidl#80)*

 Metadata about a prior update attempt.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>attempt_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td> UUID for this specific update attempt. Always present.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source_version</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Source version of this update attempt. Always present.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>target_version</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Target version of this update attempt, if known.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='../fuchsia.update.installer/index.html#Options'>Options</a></code>
            </td>
            <td> Configuration options for this update attempt. Always present.
</td>
        </tr><tr>
            <td>5</td>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.update.installer/index.html#State'>State</a></code>
            </td>
            <td> Terminal state of this update attempt. Always present.
</td>
        </tr><tr>
            <td>6</td>
            <td><code>when</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> When this update attempt started. Always present.
</td>
        </tr></table>

### Options {:#Options}


*Defined in [fuchsia.update.installer/installer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update.installer/installer.fidl#103)*

 Configuration options for an update attempt.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>initiator</code></td>
            <td>
                <code><a class='link' href='../fuchsia.update.installer/index.html#Initiator'>Initiator</a></code>
            </td>
            <td> What initiated this update attempt. Required.
</td>
        </tr></table>

### MonitorOptions {:#MonitorOptions}


*Defined in [fuchsia.update.installer/installer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update.installer/installer.fidl#109)*

 Configuration options for the <a class='link' href='../fuchsia.update.installer/index.html#Monitor'>Monitor</a> protocol.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>should_notify</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> True if events should be sent over the <a class='link' href='../fuchsia.update.installer/index.html#Monitor'>Monitor</a> protocol. Assumed to
 be false if absent.
</td>
        </tr></table>

### Progress {:#Progress}


*Defined in [fuchsia.update.installer/progress.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update.installer/progress.fidl#91)*

 State of an update attempt.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.update.installer/index.html#State'>State</a></code>
            </td>
            <td> The current state of the update. Always present.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>percent_complete</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td> When not present, progress is not yet known. When present, must be less
 than or equal to <a class='link' href='../fuchsia.update.installer/index.html#PERCENT_MAX'>PERCENT_MAX</a>.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>download_size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The number of bytes that must be downloaded to apply this update.
 Populated during <a class='link' href='../fuchsia.update.installer/index.html#State.PREPARE'>State.PREPARE</a>.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>bytes_downloaded</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The number of bytes downloaded during this update attempt. Less than or
 equal to <a class='link' href='../fuchsia.update.installer/index.html#download_size'>download_size</a>.
</td>
        </tr></table>









## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update.installer/progress.fidl#88">PERCENT_MAX</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint8</code></td>
        </tr>
    
</table>

