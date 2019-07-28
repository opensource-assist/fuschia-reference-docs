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

## ChannelWriter {:#ChannelWriter}
*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#46)*

 Read and write A/B channel data, the data is not authenticated or encrypted by this API.
 The format of the data is specific to the caller, and they should be authenticating the
 data themselves and parsing it with extreme care.

### GetChannelData {:#GetChannelData}

 Get the data blob for the currently running slot.

 - response `slot` the currently running slot
 - response `data_blob` the data blob (if it exists) for the current slot.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>slot</code></td>
            <td>
                <code><a class='link' href='#Slot'>Slot</a></code>
            </td>
        </tr><tr>
            <td><code>data_blob</code></td>
            <td>
                <code>vector&lt;uint8&gt;?</code>
            </td>
        </tr></table>

### SetChannelData {:#SetChannelData}

 Set a new data blob for the given slot.

 + request `slot` the slot to set the data for (could be currently running, could be
     the ‘other’ slot on a two-slot device).
 + request `data_blob` the data blob to write for the given slot.  Providing too
     large of a data blob will result in failure.
 * error <a class='link' href='#SetChannelDataError'>SetChannelDataError</a>.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>slot</code></td>
            <td>
                <code><a class='link' href='#Slot'>Slot</a></code>
            </td>
        </tr><tr>
            <td><code>data_blob</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#ChannelWriter_SetChannelData_Result'>ChannelWriter_SetChannelData_Result</a></code>
            </td>
        </tr></table>

## Manager {:#Manager}
*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#74)*


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
*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#97)*

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



## **STRUCTS**

### ChannelWriter_SetChannelData_Response {:#ChannelWriter_SetChannelData_Response}
*Defined in [fuchsia.update/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#10)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>



## **ENUMS**

### Slot {:#Slot}
Type: <code>uint32</code>

*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#64)*

 The list of valid update slots.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>A</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>B</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### SetChannelDataError {:#SetChannelDataError}
Type: <code>uint32</code>

*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#69)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>FAILED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### Initiator {:#Initiator}
Type: <code>uint32</code>

*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#112)*

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

*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#148)*

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

*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#194)*



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


*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#106)*

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


*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#205)*



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



## **UNIONS**

### ChannelWriter_SetChannelData_Result {:#ChannelWriter_SetChannelData_Result}
*Defined in [fuchsia.update/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#13)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#ChannelWriter_SetChannelData_Response'>ChannelWriter_SetChannelData_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#SetChannelDataError'>SetChannelDataError</a></code>
            </td>
            <td></td>
        </tr></table>







