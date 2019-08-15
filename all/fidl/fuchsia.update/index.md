Project: /_project.yaml
Book: /_book.yaml

# fuchsia.update


## **PROTOCOLS**

## Info {:#Info}
*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#9)*

 Information about the state of the update system.

### GetChannel {:#GetChannel}

 Retrieve the currently active update channel.

 - response `channel` the currently active update channel.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>channel</code></td>
            <td>
                <code>string[128]</code>
            </td>
        </tr></table>

## ChannelControl {:#ChannelControl}
*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#18)*

 Control the target update channel, this is the channel we will use on the next update check.

### GetChannel {:#GetChannel}

 Retrieve the currently active update channel.

 - response `channel` the currently active update channel.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>channel</code></td>
            <td>
                <code>string[128]</code>
            </td>
        </tr></table>

### SetTarget {:#SetTarget}

 Set a new desired target channel.  This tells the updater to attempt to
 check for updates using a new channel.  This is tentative, and won't be
 persisted unless an update check on that channel is successful.

 A response is generated when the new target channel has been verified as
 valid.

 + request `channel` the new target channel name (name used by the updater)

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>channel</code></td>
            <td>
                <code>string[128]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### GetTarget {:#GetTarget}

 Get the current tentative target channel for updates.
 This returns the channel that the update client is using to perform update
 checks.  It's always one of:
    - the current channel
    - the default channel
    - a new target that's different, but hasn't been OTA'd from yet.

 - response `channel` the current target channel.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>channel</code></td>
            <td>
                <code>string[128]</code>
            </td>
        </tr></table>

## Manager {:#Manager}
*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#43)*


### CheckNow {:#CheckNow}

 Immediately check for an update.
  `options`:  Did a user initiate this request? (`USER_INITIATED`) This changes
              some parameters about aggressiveness of retries and throttling.
  `monitor`:  An interface on which to receive the status events for this update check.
               It's only valid for a single update check, after that it won't receive any
               more events.

  -> Was the update check successfully started (state machine in a proper state
     to do so).

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

### GetState {:#GetState}

 Get the current state of the Manager (is an update available, is it currently
 checking for an update, etc).

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

### AddMonitor {:#AddMonitor}

 Get all status events, for all update checks (interactive and background).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>monitor</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Monitor'>Monitor</a>&gt;</code>
            </td>
        </tr></table>



## Monitor {:#Monitor}
*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#66)*

 Receiver of updates for either an individual update check, or to continuously
 receive updates for all checks.

### OnState {:#OnState}

 Receive the current state as it changes.



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

### Initiator {:#Initiator}
Type: <code>uint32</code>

*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#81)*

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

### ManagerState {:#ManagerState}
Type: <code>uint32</code>

*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#117)*

 ```
 The various states that the manager can be in.

     +----------------------+
 --->|         IDLE         |<--------------------------------+
 |   +----------------------+                                 |
 |              |               +----------------------+      |
 |              |<--------------|   UPDATE_AVAILABLE   |      |
 |              |               +----------------------+      |
 |              v                       ^                     |
 |   +----------------------+           |                     |
 |<--| CHECKING_FOR_UPDATES |-----------------+               |
 |   +----------------------+                 |               |
 |              v                             |               |
 |   +----------------------+                 |               |
 |   |  PERFORMING_UPDATE   |---------------->|               |
 |   +----------------------+                 |               |
 |              v                             |               |
 |   +----------------------+                 |               |
 |   |  WAITING_FOR_REBOOT  |---------------->|               |
 |   +----------------------+                 |               |
 |              v                             v               |
 |   +----------------------+     +----------------------+    |
 +---|  FINALIZING_UPDATE   |---->|  ENCOUNTERED_ERROR   |----+
     +----------------------+     +----------------------+

 ```


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>IDLE</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>CHECKING_FOR_UPDATES</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>UPDATE_AVAILABLE</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>PERFORMING_UPDATE</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>WAITING_FOR_REBOOT</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>FINALIZING_UPDATE</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>ENCOUNTERED_ERROR</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr></table>

### CheckStartedResult {:#CheckStartedResult}
Type: <code>uint32</code>

*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#163)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>STARTED</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>IN_PROGRESS</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>THROTTLED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### Options {:#Options}


*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#75)*

 Configuration options for an update attempt (this is common with the Fuchsia
  OTA Interface v2)


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>initiator</code></td>
            <td>
                <code><a class='link' href='#Initiator'>Initiator</a></code>
            </td>
            <td> What initiated this update attempt.
</td>
        </tr></table>

### State {:#State}


*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#174)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#ManagerState'>ManagerState</a></code>
            </td>
            <td> The current state of the Manager. Always present.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>version_available</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The version available from Omaha. Will be present in `UPDATE_AVAILABLE` or starting
 from `PERFORMING_UPDATE`.
</td>
        </tr></table>









