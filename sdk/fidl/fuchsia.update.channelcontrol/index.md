Project: /_project.yaml
Book: /_book.yaml

# fuchsia.update.channelcontrol


## **PROTOCOLS**

## ChannelControl {:#ChannelControl}
*Defined in [fuchsia.update.channelcontrol/channelcontrol.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update.channelcontrol/channelcontrol.fidl#11)*

 Control the target update channel, this is the channel we will use on the next update check.

### GetCurrent {:#GetCurrent}

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

### GetTargetList {:#GetTargetList}

 Get the list of well-known target channels that can be passed to SetTarget().
 There may be other, unlisted channels.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>channels</code></td>
            <td>
                <code>vector&lt;string&gt;[100]</code>
            </td>
        </tr></table>















