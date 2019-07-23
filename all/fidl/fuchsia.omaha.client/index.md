Project: /_project.yaml
Book: /_book.yaml

# fuchsia.omaha.client


## **PROTOCOLS**

## OmahaClientConfiguration {:#OmahaClientConfiguration}
*Defined in [fuchsia.omaha.client/fuchsia.omaha.client.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/bin/omaha_client/fuchsia.omaha.client.fidl#12)*


### SetChannel {:#SetChannel}

 Set the target update channel that the device should be tracking.
  `channel`: The new channel name
  `allow_factory_reset`: If the next update (on the new channel) results in a downgrade of
      any component, then the mutable system data will be erased if `allow_factory_reset`
      is true, otherwise it will not get an update until the new channel has an update with
      a higher version number than the current system.
   -> `ZX_OK` if the new channel name was successfully persisted, otherwise return the zx
      status omaha client encountered trying to persist new channel.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>channel</code></td>
            <td>
                <code>string[128]</code>
            </td>
        </tr><tr>
            <td><code>allow_factory_reset</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### GetChannel {:#GetChannel}

 Get the target update channel that the device is tracking.

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















## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/garnet/bin/omaha_client/fuchsia.omaha.client.fidl#9">MAX_CHANNEL_NAME_LENGTH</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    
</table>

