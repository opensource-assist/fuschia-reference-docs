[TOC]

# fuchsia.update.channelcontrol


## **PROTOCOLS**

## ChannelControl {#ChannelControl}
*Defined in [fuchsia.update.channelcontrol/channelcontrol.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update.channelcontrol/channelcontrol.fidl#11)*

<p>Control the target update channel, this is the channel we will use on the next update check.</p>

### GetCurrent {#GetCurrent}

<p>Retrieve the currently active update channel.</p>
<ul>
<li>response <code>channel</code> the currently active update channel.</li>
</ul>

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

### SetTarget {#SetTarget}

<p>Set a new desired target channel.  This tells the updater to attempt to
check for updates using a new channel.  This is tentative, and won't be
persisted unless an update check on that channel is successful.</p>
<p>A response is generated when the new target channel has been verified as
valid.</p>
<ul>
<li>request <code>channel</code> the new target channel name (name used by the updater)</li>
</ul>

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

### GetTarget {#GetTarget}

<p>Get the current tentative target channel for updates.
This returns the channel that the update client is using to perform update
checks.  It's always one of:
- the current channel
- the default channel
- a new target that's different, but hasn't been OTA'd from yet.</p>
<ul>
<li>response <code>channel</code> the current target channel.</li>
</ul>

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

### GetTargetList {#GetTargetList}

<p>Get the list of well-known target channels that can be passed to SetTarget().
There may be other, unlisted channels.</p>

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

















