[TOC]

# fuchsia.update.installer


## **PROTOCOLS**

## Installer {#Installer}
*Defined in [fuchsia.update.installer/installer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update.installer/installer.fidl#14)*

<p>Updates the system.</p>
<p>This protocol is intended to be consumed by a component capable of
discovering when to update and what version of the system to install.</p>

### GetLastUpdateResult {#GetLastUpdateResult}

<p>Get the status of the last update attempt. If this device hasn't
attempted an update since the last factory reset, every field in the
result will be absent.</p>
<ul>
<li>response <code>info</code> the status of the last update attempt, if available.</li>
</ul>

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
                <code><a class='link' href='#UpdateResult'>UpdateResult</a></code>
            </td>
        </tr></table>

### GetUpdateResult {#GetUpdateResult}

<p>Get the status of the given update attempt, if it exists. If this device
hasn't attempted an update with the given <code>attempt_id</code> or forgotten about
that attempt, every field in the result will be absent.</p>
<ul>
<li>request <code>attempt_id</code> UUID identifying the requested update attempt.</li>
</ul>
<ul>
<li>response <code>info</code> the status of the last update attempt, if available.</li>
</ul>

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
                <code><a class='link' href='#UpdateResult'>UpdateResult</a></code>
            </td>
        </tr></table>

### StartUpdate {#StartUpdate}

<p>Start an update if one is not running, or attach to a pending update
attempt. Attach the provided monitor to the update attempt.</p>
<ul>
<li>request <code>url</code> The fuchsia-pkg URL of the update package to update to.</li>
<li>request <code>options</code> Configuration options for this update attempt. Ignored or merged
with the existing <code>options</code> if an update attempt is already in progress.</li>
<li>request <code>monitor</code> A protocol on which to receive progress updates.</li>
<li>request <code>monitor_options</code> Configuration options to control the behavior of the
given <a class='link' href='#Monitor'>Monitor</a>.</li>
</ul>
<ul>
<li>response <code>attempt_id</code> UUID identifying this update attempt. For
updates that require a reboot, components may use this identifier to
disambiguate the completion of this update attempt from new update
attempts that start post-reboot.</li>
</ul>

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
                <code><a class='link' href='#Options'>Options</a></code>
            </td>
        </tr><tr>
            <td><code>monitor</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Monitor'>Monitor</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>monitor_options</code></td>
            <td>
                <code><a class='link' href='#MonitorOptions'>MonitorOptions</a></code>
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

### MonitorUpdate {#MonitorUpdate}

<p>Attempt to monitor a specific update attempt, if it exists. This API
will not start an update if one is not already running.</p>
<ul>
<li>request <code>attempt_id</code> UUID identifying the requested update attempt. If
not given, monitor any active update attempt.</li>
<li>request <code>monitor</code> A protocol on which to receive progress updates.</li>
<li>request <code>monitor_options</code> Configuration options to control the behavior of the
given <a class='link' href='#Monitor'>Monitor</a>.</li>
</ul>
<ul>
<li>response <code>attached</code> Whether or not the provided monitor was attached
to an in-progress update attempt. If false, monitor will be closed
by the server.</li>
</ul>

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
                <code>request&lt;<a class='link' href='#Monitor'>Monitor</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>monitor_options</code></td>
            <td>
                <code><a class='link' href='#MonitorOptions'>MonitorOptions</a></code>
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

### MonitorAllUpdates {#MonitorAllUpdates}

<p>Monitor all update attempts as they start, as well as an in-progress
attempt, if there is one.</p>
<ul>
<li>request <code>attempts_monitor</code> A protocol on which to receive <a class='link' href='#Monitor'>Monitor</a>
instances as update attempts start.</li>
<li>request <code>monitor_options</code> Configuration options to control the behavior of the
given <a class='link' href='#Monitor'>Monitor</a>.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>attempts_monitor</code></td>
            <td>
                <code>request&lt;<a class='link' href='#AttemptsMonitor'>AttemptsMonitor</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>monitor_options</code></td>
            <td>
                <code><a class='link' href='#MonitorOptions'>MonitorOptions</a></code>
            </td>
        </tr></table>



## AttemptsMonitor {#AttemptsMonitor}
*Defined in [fuchsia.update.installer/progress.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update.installer/progress.fidl#8)*

<p>Monitors update attempts as they start.</p>

### OnStart {#OnStart}

<p>Emitted when a new update attempt has started.</p>
<ul>
<li>request <code>attempt_id</code> UUID identifying this update attempt.</li>
<li>request <code>monitor</code> A protocol on which to receive progress updates.</li>
</ul>



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
                <code><a class='link' href='#Monitor'>Monitor</a></code>
            </td>
        </tr></table>

## Monitor {#Monitor}
*Defined in [fuchsia.update.installer/progress.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update.installer/progress.fidl#23)*

<p>Monitors an update attempt.</p>
<p>When a Monitor is attached to an update attempt with
<a class='link' href='#MonitorOptions.should_notify'>MonitorOptions.should_notify</a> set to true, the server will emit events on
the protocol that the client must consume. Clients that attach to an attempt
will be sent any events they may have missed (by attaching to an update
attempt after it has started, for example).</p>

### OnStateEnter {#OnStateEnter}

<p>Emitted when transitioning from one state to another.</p>
<ul>
<li>response <code>state</code> The new state.</li>
</ul>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#State'>State</a></code>
            </td>
        </tr></table>

### GetNextProgress {#GetNextProgress}

<p>Retrieve the latest progress of this update attempt, blocking until
newer progress is available if this client has already seen the
currently available progress. If this update attempt has completed (or
failed), this API immediately returns the final progress.</p>
<ul>
<li>response <code>progress</code> The latest progress of this update attempt.</li>
</ul>

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
                <code><a class='link' href='#Progress'>Progress</a></code>
            </td>
        </tr></table>





## **ENUMS**

### Initiator {#Initiator}
Type: <code>uint32</code>

*Defined in [fuchsia.update.installer/installer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update.installer/installer.fidl#116)*

<p>Who or what initiated the update check.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>USER</code></td>
            <td><code>0</code></td>
            <td><p>The update check was initiated by an interactive user, or the user is
otherwise blocked and waiting for the result of this update check.</p>
</td>
        </tr><tr>
            <td><code>SERVICE</code></td>
            <td><code>1</code></td>
            <td><p>The update check was initiated by a service, in the background.</p>
</td>
        </tr></table>

### State {#State}
Type: <code>uint32</code>

*Defined in [fuchsia.update.installer/progress.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update.installer/progress.fidl#40)*

<p>States that an update attempt may transition through. An update attempt
always starts in <a class='link' href='#State.PREPARE'>State.PREPARE</a>. See each state for more details.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>PREPARE</code></td>
            <td><code>0</code></td>
            <td><p>Fetching required metadata to begin the update. This state will also
compute and expose an estimate of the required download size.</p>
<h2>Next States</h2>
<ul>
<li><a class='link' href='#State.DOWNLOAD'>State.DOWNLOAD</a> on success.</li>
<li><a class='link' href='#State.FAIL'>State.FAIL</a> on error.</li>
</ul>
</td>
        </tr><tr>
            <td><code>DOWNLOAD</code></td>
            <td><code>1</code></td>
            <td><p>Downloading packages and kernel images.</p>
<h2>Next States</h2>
<ul>
<li><a class='link' href='#State.STAGE'>State.STAGE</a> on success.</li>
<li><a class='link' href='#State.FAIL'>State.FAIL</a> on error.</li>
</ul>
</td>
        </tr><tr>
            <td><code>STAGE</code></td>
            <td><code>2</code></td>
            <td><p>Writing kernel images and preparing to switch over to the new system.</p>
<h2>Next States</h2>
<ul>
<li><a class='link' href='#State.REBOOT'>State.REBOOT</a> if a reboot is required to complete the update.</li>
<li><a class='link' href='#State.FINALIZE'>State.FINALIZE</a> if a reboot is not required to complete the update.</li>
<li><a class='link' href='#State.FAIL'>State.FAIL</a> on error.</li>
</ul>
</td>
        </tr><tr>
            <td><code>REBOOT</code></td>
            <td><code>3</code></td>
            <td><p>Waiting to reboot.</p>
<h2>Next States</h2>
<ul>
<li><a class='link' href='#State.FINALIZE'>State.FINALIZE</a> if a reboot is not required to complete the update.</li>
<li><a class='link' href='#State.FAIL'>State.FAIL</a> on error.</li>
</ul>
</td>
        </tr><tr>
            <td><code>FINALIZE</code></td>
            <td><code>4</code></td>
            <td><p>Running final tasks post-reboot.</p>
<h2>Next States</h2>
<ul>
<li><a class='link' href='#State.COMPLETE'>State.COMPLETE</a> on success.</li>
<li><a class='link' href='#State.FAIL'>State.FAIL</a> on error.</li>
</ul>
</td>
        </tr><tr>
            <td><code>COMPLETE</code></td>
            <td><code>5</code></td>
            <td><p>Terminal states. An update attempt will eventually end up in one of
these and will not transition out of them.</p>
<h2>Next States</h2>
<p>none</p>
</td>
        </tr><tr>
            <td><code>FAIL</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### UpdateResult {#UpdateResult}


*Defined in [fuchsia.update.installer/installer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update.installer/installer.fidl#80)*

<p>Metadata about a prior update attempt.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>attempt_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>UUID for this specific update attempt. Always present.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source_version</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>Source version of this update attempt. Always present.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>target_version</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>Target version of this update attempt, if known.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#Options'>Options</a></code>
            </td>
            <td><p>Configuration options for this update attempt. Always present.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#State'>State</a></code>
            </td>
            <td><p>Terminal state of this update attempt. Always present.</p>
</td>
        </tr><tr>
            <td>6</td>
            <td><code>when</code></td>
            <td>
                <code>int64</code>
            </td>
            <td><p>When this update attempt started. Always present.</p>
</td>
        </tr></table>

### Options {#Options}


*Defined in [fuchsia.update.installer/installer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update.installer/installer.fidl#103)*

<p>Configuration options for an update attempt.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>initiator</code></td>
            <td>
                <code><a class='link' href='#Initiator'>Initiator</a></code>
            </td>
            <td><p>What initiated this update attempt. Required.</p>
</td>
        </tr></table>

### MonitorOptions {#MonitorOptions}


*Defined in [fuchsia.update.installer/installer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update.installer/installer.fidl#109)*

<p>Configuration options for the <a class='link' href='#Monitor'>Monitor</a> protocol.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>should_notify</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>True if events should be sent over the <a class='link' href='#Monitor'>Monitor</a> protocol. Assumed to
be false if absent.</p>
</td>
        </tr></table>

### Progress {#Progress}


*Defined in [fuchsia.update.installer/progress.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update.installer/progress.fidl#91)*

<p>State of an update attempt.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#State'>State</a></code>
            </td>
            <td><p>The current state of the update. Always present.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>percent_complete</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td><p>When not present, progress is not yet known. When present, must be less
than or equal to <a class='link' href='#PERCENT_MAX'>PERCENT_MAX</a>.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>download_size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The number of bytes that must be downloaded to apply this update.
Populated during <a class='link' href='#State.PREPARE'>State.PREPARE</a>.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>bytes_downloaded</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The number of bytes downloaded during this update attempt. Less than or
equal to <a class='link' href='#download_size'>download_size</a>.</p>
</td>
        </tr></table>









## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update.installer/progress.fidl#88">PERCENT_MAX</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint8</code></td>
            <td><p>Fixed precision decimal representing 100%.</p>
</td>
        </tr>
    
</table>

