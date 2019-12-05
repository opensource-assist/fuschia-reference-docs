[TOC]

# fuchsia.update


## **PROTOCOLS**

## Manager {#Manager}
*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#8)*


### CheckNow {#CheckNow}

<p>Immediately check for an update.
<code>options</code>:  Did a user initiate this request? (<code>USER_INITIATED</code>) This changes
some parameters about aggressiveness of retries and throttling.
<code>monitor</code>:  An interface on which to receive the status events for this update check.
It's only valid for a single update check, after that it won't receive any
more events.</p>
<p>-&gt; Was the update check successfully started (state machine in a proper state
to do so).</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#Options'>Options</a></code>
            </td>
        </tr><tr>
            <td><code>monitor</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Monitor'>Monitor</a>&gt;?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#CheckStartedResult'>CheckStartedResult</a></code>
            </td>
        </tr></table>

### GetState {#GetState}

<p>Get the current state of the Manager (is an update available, is it currently
checking for an update, etc).</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#State'>State</a></code>
            </td>
        </tr></table>

### AddMonitor {#AddMonitor}

<p>Get all status events, for all update checks (interactive and background).</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>monitor</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Monitor'>Monitor</a>&gt;</code>
            </td>
        </tr></table>



## Monitor {#Monitor}
*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#31)*

<p>Receiver of updates for either an individual update check, or to continuously
receive updates for all checks.</p>

### OnState {#OnState}

<p>Receive the current state as it changes.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#State'>State</a></code>
            </td>
        </tr></table>





## **ENUMS**

### Initiator {#Initiator}
Type: <code>uint32</code>

*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#46)*

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

### ManagerState {#ManagerState}
Type: <code>uint32</code>

*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#82)*

<pre><code>The various states that the manager can be in.

    +----------------------+
---&gt;|         IDLE         |&lt;--------------------------------+
|   +----------------------+                                 |
|              |               +----------------------+      |
|              |&lt;--------------|   UPDATE_AVAILABLE   |      |
|              |               +----------------------+      |
|              v                       ^                     |
|   +----------------------+           |                     |
|&lt;--| CHECKING_FOR_UPDATES |-----------------+               |
|   +----------------------+                 |               |
|              v                             |               |
|   +----------------------+                 |               |
|   |  PERFORMING_UPDATE   |----------------&gt;|               |
|   +----------------------+                 |               |
|              v                             |               |
|   +----------------------+                 |               |
|   |  WAITING_FOR_REBOOT  |----------------&gt;|               |
|   +----------------------+                 |               |
|              v                             v               |
|   +----------------------+     +----------------------+    |
+---|  FINALIZING_UPDATE   |----&gt;|  ENCOUNTERED_ERROR   |----+
    +----------------------+     +----------------------+

</code></pre>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>IDLE</code></td>
            <td><code>0</code></td>
            <td><p>The Manager is currently idle (in between updates).</p>
<p>Next states:</p>
<ul>
<li><code>CHECKING_FOR_UPDATES</code></li>
</ul>
</td>
        </tr><tr>
            <td><code>CHECKING_FOR_UPDATES</code></td>
            <td><code>1</code></td>
            <td><p>The Manager is currently checking for an update.</p>
<p>Next states:</p>
<ul>
<li><code>IDLE</code> update is not available</li>
<li><code>UPDATE_AVAILABLE</code> update is available but not allowed by policy</li>
<li><code>PERFORMING_UPDATE</code> update is available and allowed by policy</li>
<li><code>ENCOUNTERED_ERROR</code> on error</li>
</ul>
</td>
        </tr><tr>
            <td><code>UPDATE_AVAILABLE</code></td>
            <td><code>2</code></td>
            <td><p>The Manager has found an available update but is not allowed to update
due to policy.</p>
<p>Next states:</p>
<ul>
<li><code>CHECKING_FOR_UPDATES</code> when CheckNow() is called or a background update starts</li>
</ul>
</td>
        </tr><tr>
            <td><code>PERFORMING_UPDATE</code></td>
            <td><code>3</code></td>
            <td><p>The Manager has started the available update.</p>
<p>Next states:</p>
<ul>
<li><code>WAITING_FOR_REBOOT</code> on success</li>
<li><code>ENCOUNTERED_ERROR</code> on error</li>
</ul>
</td>
        </tr><tr>
            <td><code>WAITING_FOR_REBOOT</code></td>
            <td><code>4</code></td>
            <td><p>The update has been performed, and the device is waiting to be rebooted.</p>
<p>Next states:</p>
<ul>
<li><code>FINALIZING_UPDATE</code> after device reboot</li>
<li><code>ENCOUNTERED_ERROR</code> on error</li>
</ul>
</td>
        </tr><tr>
            <td><code>FINALIZING_UPDATE</code></td>
            <td><code>5</code></td>
            <td><p>The update is being finalized after reboot.</p>
<p>Next states:</p>
<ul>
<li><code>IDLE</code> on success</li>
<li><code>ENCOUNTERED_ERROR</code> on error</li>
</ul>
</td>
        </tr><tr>
            <td><code>ENCOUNTERED_ERROR</code></td>
            <td><code>6</code></td>
            <td><p>The Manager is reporting to Omaha that an error has occurred during the
update.</p>
<p>Next states:</p>
<ul>
<li><code>IDLE</code></li>
</ul>
</td>
        </tr></table>

### CheckStartedResult {#CheckStartedResult}
Type: <code>uint32</code>

*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#128)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>STARTED</code></td>
            <td><code>0</code></td>
            <td><p>The update check has been started.</p>
</td>
        </tr><tr>
            <td><code>IN_PROGRESS</code></td>
            <td><code>1</code></td>
            <td><p>The update check was not started, as an update is already in progress, <code>monitor</code> is
attached to that update and will immediately get a OnState() call on current state.</p>
</td>
        </tr><tr>
            <td><code>THROTTLED</code></td>
            <td><code>2</code></td>
            <td><p>The update check was not started, because too many requests to check have
been made in a short period of time.</p>
</td>
        </tr></table>



## **TABLES**

### Options {#Options}


*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#40)*

<p>Configuration options for an update attempt (this is common with the Fuchsia
OTA Interface v2)</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>initiator</code></td>
            <td>
                <code><a class='link' href='#Initiator'>Initiator</a></code>
            </td>
            <td><p>What initiated this update attempt.</p>
</td>
        </tr></table>

### State {#State}


*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#139)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#ManagerState'>ManagerState</a></code>
            </td>
            <td><p>The current state of the Manager. Always present.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>version_available</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The version available from Omaha. Will be present in <code>UPDATE_AVAILABLE</code> or starting
from <code>PERFORMING_UPDATE</code>.</p>
</td>
        </tr></table>











