[TOC]

# fuchsia.bluetooth.avrcp


## **PROTOCOLS**

## PeerManager {#PeerManager}
*Defined in [fuchsia.bluetooth.avrcp/controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.avrcp/controller.fidl#10)*


### GetControllerForTarget {#GetControllerForTarget}

 Returns a controller client to a remote target (TG) service at the peer specified by
 `peer_id`.
 TODO (BT-305): change peer_id to fuchsia.bluetooth.PeerId type after BrEdr profile service
 switches.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>peer_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>client</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Controller'>Controller</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#PeerManager_GetControllerForTarget_Result'>PeerManager_GetControllerForTarget_Result</a></code>
            </td>
        </tr></table>

### SetAbsoluteVolumeHandler {#SetAbsoluteVolumeHandler}

 Set the absolute volume handler for the peer specified at `peer_id` to handle absolute
 volume commands and notifications received from the peer. Only one handler may be set with
 a peer at at time. If a second handler is registered it will be dropped and an error will
 be returned.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>peer_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>handler</code></td>
            <td>
                <code><a class='link' href='#AbsoluteVolumeHandler'>AbsoluteVolumeHandler</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#PeerManager_SetAbsoluteVolumeHandler_Result'>PeerManager_SetAbsoluteVolumeHandler_Result</a></code>
            </td>
        </tr></table>

## AbsoluteVolumeHandler {#AbsoluteVolumeHandler}
*Defined in [fuchsia.bluetooth.avrcp/controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.avrcp/controller.fidl#92)*

 Handler for absolute volume requests from a remote peer. See AVRCP v 1.6.2 section 6.13.2.
 Absolute volume is represented as a percentage using one byte with the most significant bit
 reserved. 0% is represented as 0x0 and 100% as 0x7f. Volume should scaled between the
 two values.

### SetVolume {#SetVolume}

 Requests that the absolute volume of the player be changed.
 `requested_volume` is the requested volume by the peer.
 Returns the actual volume set locally by the handler.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>requested_volume</code></td>
            <td>
                <code>uint8</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>set_volume</code></td>
            <td>
                <code>uint8</code>
            </td>
        </tr></table>

### OnVolumeChanged {#OnVolumeChanged}

 Returns latest volume of the handler to the AVRCP service. This function should return
 immediately on the first call and if the volume has changed since the last call to this
 function, otherwise it should only return when the volume has been changed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>new_volume</code></td>
            <td>
                <code>uint8</code>
            </td>
        </tr></table>

### GetCurrentVolume {#GetCurrentVolume}

 Returns the current volume immediately.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>volume</code></td>
            <td>
                <code>uint8</code>
            </td>
        </tr></table>

## Controller {#Controller}
*Defined in [fuchsia.bluetooth.avrcp/controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.avrcp/controller.fidl#111)*

 Client wrapper for local controller (CT) -> remote target (TG) AVCTP connections between devices.
 A client is high level construct and does not represent a connection with a device.
 Connections are internally managed and may be shared by multiple clients.
 The actual connection may be opened on-demand after any command here is called.

### GetPlayerApplicationSettings {#GetPlayerApplicationSettings}

 Returns the remote PlayerApplicationSettings.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Controller_GetPlayerApplicationSettings_Result'>Controller_GetPlayerApplicationSettings_Result</a></code>
            </td>
        </tr></table>

### GetMediaAttributes {#GetMediaAttributes}

 Returns the currently playing media attributes.
 May send either the GetElementAttributes or GetItemAttributes command depending on what
 is supported.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Controller_GetMediaAttributes_Result'>Controller_GetMediaAttributes_Result</a></code>
            </td>
        </tr></table>

### SetAbsoluteVolume {#SetAbsoluteVolume}

 Request the absolute volume on the peer be changed. Returns the actual volume set by the
 peer. Values can range from 0x00 to 0x7F (with 100% volume being 0x7F). You may not get a
 volume changed notification event from the remote peer as result of changing this.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>requested_volume</code></td>
            <td>
                <code>uint8</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Controller_SetAbsoluteVolume_Result'>Controller_SetAbsoluteVolume_Result</a></code>
            </td>
        </tr></table>

### InformBatteryStatus {#InformBatteryStatus}

 Inform target of the controller's battery level.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>battery_status</code></td>
            <td>
                <code><a class='link' href='#BatteryStatus'>BatteryStatus</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Controller_InformBatteryStatus_Result'>Controller_InformBatteryStatus_Result</a></code>
            </td>
        </tr></table>

### SetNotificationFilter {#SetNotificationFilter}

 Filters notifications that will be received with <a class='link' href='#OnNotification'>OnNotification</a>. Not all notifications
 are supported by all peers. Resetting the notification filter may trigger all requested
 notification types to post their current value to <a class='link' href='#OnNotification'>OnNotification</a> immediately.

 The `position_change_interval` argument is used to set the interval in seconds that the
 controller client would like to be notified of `TRACK_POS_CHANGED` events.
 `position_change_interval` is ignored if `TRACK_POS` is not set. The position change interval
 is best effort and not a guarantee and events may arrive more frequently or less frequently
 than requested.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>notifications</code></td>
            <td>
                <code><a class='link' href='#Notifications'>Notifications</a></code>
            </td>
        </tr><tr>
            <td><code>position_change_interval</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### OnNotification {#OnNotification}

 Incoming notification events from the target peer. `timestamp` is monotonic wall time
 of when the event was received by the peer.
 You must call <a class='link' href='#NotifyNotificationHandled'>NotifyNotificationHandled</a> after receving a notification event to
 acknowledge delivery. Multiple non-discrete events may be combined into a single
 notification if acknowledged after a new event arrives from a peer.
 Call <a class='link' href='#SetNotificationFilter'>SetNotificationFilter</a> to set the notifications that are requested of the peer.
 All notifications are discrete state changes except volume change and position change
 notifications.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>timestamp</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>notification</code></td>
            <td>
                <code><a class='link' href='#Notification'>Notification</a></code>
            </td>
        </tr></table>

### NotifyNotificationHandled {#NotifyNotificationHandled}

 Call to acknowledge handling of a notification from <a class='link' href='#OnNotification'>OnNotification</a>.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SetAddressedPlayer {#SetAddressedPlayer}

 Changes the addressed `player_id` on the target when multiple are supported.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>player_id</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Controller_SetAddressedPlayer_Result'>Controller_SetAddressedPlayer_Result</a></code>
            </td>
        </tr></table>

### SendCommand {#SendCommand}

 Send an AV\C passthrough key command. Sends both a key down and key up event.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>command</code></td>
            <td>
                <code><a class='link' href='#AvcPanelCommand'>AvcPanelCommand</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Controller_SendCommand_Result'>Controller_SendCommand_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### PeerManager_GetControllerForTarget_Response {#PeerManager_GetControllerForTarget_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### PeerManager_SetAbsoluteVolumeHandler_Response {#PeerManager_SetAbsoluteVolumeHandler_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Controller_GetPlayerApplicationSettings_Response {#Controller_GetPlayerApplicationSettings_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>settings</code></td>
            <td>
                <code><a class='link' href='#PlayerApplicationSettings'>PlayerApplicationSettings</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Controller_GetMediaAttributes_Response {#Controller_GetMediaAttributes_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='#MediaAttributes'>MediaAttributes</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Controller_SetAbsoluteVolume_Response {#Controller_SetAbsoluteVolume_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>set_volume</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Controller_InformBatteryStatus_Response {#Controller_InformBatteryStatus_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Controller_SetAddressedPlayer_Response {#Controller_SetAddressedPlayer_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Controller_SendCommand_Response {#Controller_SendCommand_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### PlayerApplicationSettings {#PlayerApplicationSettings}
*Defined in [fuchsia.bluetooth.avrcp/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.avrcp/types.fidl#101)*



 Defined by AVRCP 1.6.2 Appendix F (player application settings).


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>equalizer</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>repeat_status_mode</code></td>
            <td>
                <code><a class='link' href='#RepeatStatusMode'>RepeatStatusMode</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>shuffle_mode</code></td>
            <td>
                <code><a class='link' href='#ShuffleMode'>ShuffleMode</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>scan_mode</code></td>
            <td>
                <code><a class='link' href='#ScanMode'>ScanMode</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MediaAttributes {#MediaAttributes}
*Defined in [fuchsia.bluetooth.avrcp/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.avrcp/types.fidl#109)*



 Defined by AVRCP 1.6.2 Appendix E (media attributes).


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>title</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>artist_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>album_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>track_number</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>total_number_of_tracks</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>genre</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>playing_time</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### ControllerError {#ControllerError}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.avrcp/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.avrcp/types.fidl#12)*

 Status codes for commands sent as the controller


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKOWN_FAILURE</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>TIMED_OUT</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>REMOTE_NOT_CONNECTED</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>COMMAND_NOT_IMPLEMENTED</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>COMMAND_REJECTED</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>COMMAND_UNEXPECTED</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVALID_ARGUMENTS</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr><tr>
            <td><code>PACKET_ENCODING</code></td>
            <td><code>8</code></td>
            <td></td>
        </tr><tr>
            <td><code>PROTOCOL_ERROR</code></td>
            <td><code>9</code></td>
            <td></td>
        </tr><tr>
            <td><code>CONNECTION_ERROR</code></td>
            <td><code>10</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNEXPECTED_RESPONSE</code></td>
            <td><code>11</code></td>
            <td></td>
        </tr></table>

### TargetEvent {#TargetEvent}
Type: <code>uint8</code>

*Defined in [fuchsia.bluetooth.avrcp/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.avrcp/types.fidl#28)*

 Defined by AVRCP 1.6.2 section 6.7.2 (RegisterNotification) and Appendix H.
 Style note: named exactly as they are in the specification with the "EVENT_" prefix.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>PLAYBACK_STATUS_CHANGED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>TRACK_CHANGED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>TRACK_REACHED_END</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>TRACK_REACHED_START</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>TRACK_POS_CHANGED</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>BATT_STATUS_CHANGED</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>SYSTEM_STATUS_CHANGED</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr><tr>
            <td><code>PLAYER_APPLICATION_SETTINGS_CHANGED</code></td>
            <td><code>8</code></td>
            <td></td>
        </tr><tr>
            <td><code>NOW_PLAYING_CONTENT_CHANGED</code></td>
            <td><code>9</code></td>
            <td></td>
        </tr><tr>
            <td><code>AVAILABLE_PLAYERS_CHANGED</code></td>
            <td><code>10</code></td>
            <td></td>
        </tr><tr>
            <td><code>ADDRESSED_PLAYER_CHANGED</code></td>
            <td><code>11</code></td>
            <td></td>
        </tr><tr>
            <td><code>UIDS_CHANGED</code></td>
            <td><code>12</code></td>
            <td></td>
        </tr><tr>
            <td><code>VOLUME_CHANGED</code></td>
            <td><code>13</code></td>
            <td></td>
        </tr></table>

### SystemStatus {#SystemStatus}
Type: <code>uint8</code>

*Defined in [fuchsia.bluetooth.avrcp/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.avrcp/types.fidl#46)*

 Defined by AVRCP 1.6.2 section 6.7.2 (RegisterNotification).
 Format for `EVENT_SYSTEM_STATUS_CHANGED`.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>POWER_ON</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>POWER_OFF</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNPLUGGED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### PlaybackStatus {#PlaybackStatus}
Type: <code>uint8</code>

*Defined in [fuchsia.bluetooth.avrcp/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.avrcp/types.fidl#54)*

 Defined by AVRCP 1.6.2 section 6.7.2 (RegisterNotification).
 Format for `EVENT_PLAYBACK_STATUS_CHANGED`.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>STOPPED</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>PLAYING</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>PAUSED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>FWD_SEEK</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>REV_SEEK</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERROR</code></td>
            <td><code>255</code></td>
            <td></td>
        </tr></table>

### BatteryStatus {#BatteryStatus}
Type: <code>uint8</code>

*Defined in [fuchsia.bluetooth.avrcp/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.avrcp/types.fidl#66)*

 Defined by AVRCP 1.6.2 section 6.7.2 (RegisterNotification).
 Format for `EVENT_BATT_STATUS_CHANGED`.
 Same encoding also defined by 6.5.8 (InformBatteryStatusOfCT).


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NORMAL</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>WARNING</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>CRITICAL</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>EXTERNAL</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>FULL_CHARGE</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>RESERVED</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr></table>

### RepeatStatusMode {#RepeatStatusMode}
Type: <code>uint8</code>

*Defined in [fuchsia.bluetooth.avrcp/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.avrcp/types.fidl#76)*

 Defined by AVRCP 1.6.2 Appendix F (player application settings).


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OFF</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>SINGLE_TRACK_REPEAT</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>ALL_TRACK_REPEAT</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>GROUP_REPEAT</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>RESERVED</code></td>
            <td><code>255</code></td>
            <td></td>
        </tr></table>

### ShuffleMode {#ShuffleMode}
Type: <code>uint8</code>

*Defined in [fuchsia.bluetooth.avrcp/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.avrcp/types.fidl#85)*

 Defined by AVRCP 1.6.2 Appendix F (player application settings).


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OFF</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>ALL_TRACK_SHUFFLE</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>GROUP_SHUFFLE</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>RESERVED</code></td>
            <td><code>255</code></td>
            <td></td>
        </tr></table>

### ScanMode {#ScanMode}
Type: <code>uint8</code>

*Defined in [fuchsia.bluetooth.avrcp/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.avrcp/types.fidl#93)*

 Defined by AVRCP 1.6.2 Appendix F (player application settings).


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OFF</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>ALL_TRACK_SCAN</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>GROUP_SCAN</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>RESERVED</code></td>
            <td><code>255</code></td>
            <td></td>
        </tr></table>

### AvcPanelCommand {#AvcPanelCommand}
Type: <code>uint8</code>

*Defined in [fuchsia.bluetooth.avrcp/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.avrcp/types.fidl#121)*

 Defined by AV\C Panel specification.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SELECT</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>UP</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>DOWN</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>LEFT</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>RIGHT</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>ROOT_MENU</code></td>
            <td><code>9</code></td>
            <td></td>
        </tr><tr>
            <td><code>CONTENTS_MENU</code></td>
            <td><code>11</code></td>
            <td></td>
        </tr><tr>
            <td><code>FAVORITE_MENU</code></td>
            <td><code>12</code></td>
            <td></td>
        </tr><tr>
            <td><code>EXIT</code></td>
            <td><code>13</code></td>
            <td></td>
        </tr><tr>
            <td><code>ON_DEMAND_MENU</code></td>
            <td><code>14</code></td>
            <td></td>
        </tr><tr>
            <td><code>APPS_MENU</code></td>
            <td><code>15</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEY_0</code></td>
            <td><code>32</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEY_1</code></td>
            <td><code>33</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEY_2</code></td>
            <td><code>34</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEY_3</code></td>
            <td><code>35</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEY_4</code></td>
            <td><code>36</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEY_5</code></td>
            <td><code>37</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEY_6</code></td>
            <td><code>38</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEY_7</code></td>
            <td><code>39</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEY_8</code></td>
            <td><code>40</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEY_9</code></td>
            <td><code>41</code></td>
            <td></td>
        </tr><tr>
            <td><code>DOT</code></td>
            <td><code>42</code></td>
            <td></td>
        </tr><tr>
            <td><code>ENTER</code></td>
            <td><code>43</code></td>
            <td></td>
        </tr><tr>
            <td><code>CHANNEL_UP</code></td>
            <td><code>48</code></td>
            <td></td>
        </tr><tr>
            <td><code>CHANNEL_DOWN</code></td>
            <td><code>49</code></td>
            <td></td>
        </tr><tr>
            <td><code>CHANNEL_PREVIOUS</code></td>
            <td><code>50</code></td>
            <td></td>
        </tr><tr>
            <td><code>INPUT_SELECT</code></td>
            <td><code>52</code></td>
            <td></td>
        </tr><tr>
            <td><code>INFO</code></td>
            <td><code>53</code></td>
            <td></td>
        </tr><tr>
            <td><code>HELP</code></td>
            <td><code>54</code></td>
            <td></td>
        </tr><tr>
            <td><code>PAGE_UP</code></td>
            <td><code>55</code></td>
            <td></td>
        </tr><tr>
            <td><code>PAGE_DOWN</code></td>
            <td><code>56</code></td>
            <td></td>
        </tr><tr>
            <td><code>LOCK</code></td>
            <td><code>58</code></td>
            <td></td>
        </tr><tr>
            <td><code>POWER</code></td>
            <td><code>64</code></td>
            <td></td>
        </tr><tr>
            <td><code>VOLUME_UP</code></td>
            <td><code>65</code></td>
            <td></td>
        </tr><tr>
            <td><code>VOLUME_DOWN</code></td>
            <td><code>66</code></td>
            <td></td>
        </tr><tr>
            <td><code>MUTE</code></td>
            <td><code>67</code></td>
            <td></td>
        </tr><tr>
            <td><code>PLAY</code></td>
            <td><code>68</code></td>
            <td></td>
        </tr><tr>
            <td><code>STOP</code></td>
            <td><code>69</code></td>
            <td></td>
        </tr><tr>
            <td><code>PAUSE</code></td>
            <td><code>70</code></td>
            <td></td>
        </tr><tr>
            <td><code>RECORD</code></td>
            <td><code>71</code></td>
            <td></td>
        </tr><tr>
            <td><code>REWIND</code></td>
            <td><code>72</code></td>
            <td></td>
        </tr><tr>
            <td><code>FAST_FORWARD</code></td>
            <td><code>73</code></td>
            <td></td>
        </tr><tr>
            <td><code>EJECT</code></td>
            <td><code>74</code></td>
            <td></td>
        </tr><tr>
            <td><code>FORWARD</code></td>
            <td><code>75</code></td>
            <td></td>
        </tr><tr>
            <td><code>BACKWARD</code></td>
            <td><code>76</code></td>
            <td></td>
        </tr><tr>
            <td><code>LIST</code></td>
            <td><code>77</code></td>
            <td></td>
        </tr><tr>
            <td><code>F1</code></td>
            <td><code>113</code></td>
            <td></td>
        </tr><tr>
            <td><code>F2</code></td>
            <td><code>114</code></td>
            <td></td>
        </tr><tr>
            <td><code>F3</code></td>
            <td><code>115</code></td>
            <td></td>
        </tr><tr>
            <td><code>F4</code></td>
            <td><code>116</code></td>
            <td></td>
        </tr><tr>
            <td><code>F5</code></td>
            <td><code>117</code></td>
            <td></td>
        </tr><tr>
            <td><code>F6</code></td>
            <td><code>118</code></td>
            <td></td>
        </tr><tr>
            <td><code>F7</code></td>
            <td><code>119</code></td>
            <td></td>
        </tr><tr>
            <td><code>F8</code></td>
            <td><code>120</code></td>
            <td></td>
        </tr><tr>
            <td><code>F9</code></td>
            <td><code>121</code></td>
            <td></td>
        </tr><tr>
            <td><code>RED</code></td>
            <td><code>122</code></td>
            <td></td>
        </tr><tr>
            <td><code>GREEN</code></td>
            <td><code>123</code></td>
            <td></td>
        </tr><tr>
            <td><code>BLUE</code></td>
            <td><code>124</code></td>
            <td></td>
        </tr><tr>
            <td><code>YELLOW</code></td>
            <td><code>125</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### Notification {#Notification}


*Defined in [fuchsia.bluetooth.avrcp/controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.avrcp/controller.fidl#59)*

 Event data from incoming target notifications.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#PlaybackStatus'>PlaybackStatus</a></code>
            </td>
            <td> `EVENT_PLAYBACK_STATUS_CHANGED` event data
</td>
        </tr><tr>
            <td>2</td>
            <td><code>track_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> `EVENT_TRACK_CHANGED` event data
</td>
        </tr><tr>
            <td>3</td>
            <td><code>pos</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> `EVENT_TRACK_POS_CHANGED` event data
</td>
        </tr><tr>
            <td>4</td>
            <td><code>battery_status</code></td>
            <td>
                <code><a class='link' href='#BatteryStatus'>BatteryStatus</a></code>
            </td>
            <td> `EVENT_BATT_STATUS_CHANGED` event data
</td>
        </tr><tr>
            <td>5</td>
            <td><code>system_status</code></td>
            <td>
                <code><a class='link' href='#SystemStatus'>SystemStatus</a></code>
            </td>
            <td> `EVENT_SYSTEM_STATUS_CHANGED` event data
</td>
        </tr><tr>
            <td>6</td>
            <td><code>application_settings</code></td>
            <td>
                <code><a class='link' href='#PlayerApplicationSettings'>PlayerApplicationSettings</a></code>
            </td>
            <td> `EVENT_PLAYER_APPLICATION_SETTINGS_CHANGED` event data
</td>
        </tr><tr>
            <td>7</td>
            <td><code>player_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td> `EVENT_ADDRESSED_PLAYER_CHANGED` event data
</td>
        </tr><tr>
            <td>8</td>
            <td><code>volume</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td> `EVENT_VOLUME_CHANGED` event data
</td>
        </tr><tr>
            <td>9</td>
            <td><code>device_connected</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> `CONNECTION_CHANGE` event data
</td>
        </tr></table>



## **UNIONS**

### PeerManager_GetControllerForTarget_Result {#PeerManager_GetControllerForTarget_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#PeerManager_GetControllerForTarget_Response'>PeerManager_GetControllerForTarget_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### PeerManager_SetAbsoluteVolumeHandler_Result {#PeerManager_SetAbsoluteVolumeHandler_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#PeerManager_SetAbsoluteVolumeHandler_Response'>PeerManager_SetAbsoluteVolumeHandler_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Controller_GetPlayerApplicationSettings_Result {#Controller_GetPlayerApplicationSettings_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Controller_GetPlayerApplicationSettings_Response'>Controller_GetPlayerApplicationSettings_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ControllerError'>ControllerError</a></code>
            </td>
            <td></td>
        </tr></table>

### Controller_GetMediaAttributes_Result {#Controller_GetMediaAttributes_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Controller_GetMediaAttributes_Response'>Controller_GetMediaAttributes_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ControllerError'>ControllerError</a></code>
            </td>
            <td></td>
        </tr></table>

### Controller_SetAbsoluteVolume_Result {#Controller_SetAbsoluteVolume_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Controller_SetAbsoluteVolume_Response'>Controller_SetAbsoluteVolume_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ControllerError'>ControllerError</a></code>
            </td>
            <td></td>
        </tr></table>

### Controller_InformBatteryStatus_Result {#Controller_InformBatteryStatus_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Controller_InformBatteryStatus_Response'>Controller_InformBatteryStatus_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ControllerError'>ControllerError</a></code>
            </td>
            <td></td>
        </tr></table>

### Controller_SetAddressedPlayer_Result {#Controller_SetAddressedPlayer_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Controller_SetAddressedPlayer_Response'>Controller_SetAddressedPlayer_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ControllerError'>ControllerError</a></code>
            </td>
            <td></td>
        </tr></table>

### Controller_SendCommand_Result {#Controller_SendCommand_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Controller_SendCommand_Response'>Controller_SendCommand_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ControllerError'>ControllerError</a></code>
            </td>
            <td></td>
        </tr></table>





## **BITS**

### Notifications {#Notifications}
Type: <code>uint32</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>PLAYBACK_STATUS</td>
            <td>1</td>
            <td> AVRCP `EVENT_PLAYBACK_STATUS_CHANGED` Notification
</td>
        </tr><tr>
            <td>TRACK</td>
            <td>2</td>
            <td> AVRCP `EVENT_TRACK_CHANGED` Notification
</td>
        </tr><tr>
            <td>TRACK_POS</td>
            <td>4</td>
            <td> AVRCP `EVENT_TRACK_POS_CHANGED` Notification
</td>
        </tr><tr>
            <td>BATT_STATUS</td>
            <td>8</td>
            <td> AVRCP `EVENT_BATT_STATUS_CHANGED` Notification
</td>
        </tr><tr>
            <td>SYSTEM_STATUS</td>
            <td>16</td>
            <td> AVRCP `EVENT_SYSTEM_STATUS_CHANGED` Notification
</td>
        </tr><tr>
            <td>PLAYER_APPLICATION_SETTINGS</td>
            <td>32</td>
            <td> AVRCP `EVENT_PLAYER_APPLICATION_SETTINGS_CHANGED` Notification
</td>
        </tr><tr>
            <td>ADDRESSED_PLAYER</td>
            <td>64</td>
            <td> AVRCP `EVENT_ADDRESSED_PLAYER_CHANGED` Notification
</td>
        </tr><tr>
            <td>VOLUME</td>
            <td>128</td>
            <td> AVRCP `EVENT_VOLUME_CHANGED` Notification
</td>
        </tr><tr>
            <td>CONNECTION</td>
            <td>65536</td>
            <td> Internal connection change event.
</td>
        </tr></table>



