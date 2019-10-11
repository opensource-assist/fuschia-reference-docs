Project: /_project.yaml
Book: /_book.yaml

# fuchsia.castsysteminfo


## **PROTOCOLS**

## Provider {:#Provider}
*Defined in [fuchsia.castsysteminfo/cast_system_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.castsysteminfo/cast_system_info.fidl#32)*

 Exposes Cast system info, as modeled in the SystemInfo table.

### GetSystemInfo {:#GetSystemInfo}

 Retrieves the SystemInfo fields that are generated at first boot and are
 available at startup.

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
                <code><a class='link' href='#Provider_GetSystemInfo_Result'>Provider_GetSystemInfo_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Provider_GetSystemInfo_Response {:#Provider_GetSystemInfo_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>systemInfo</code></td>
            <td>
                <code><a class='link' href='#SystemInfo'>SystemInfo</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### ErrorCode {:#ErrorCode}
Type: <code>uint32</code>

*Defined in [fuchsia.castsysteminfo/cast_system_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.castsysteminfo/cast_system_info.fidl#8)*

 Error codes for the GetSystemInfo operation.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ERR_NO_SYSTEM_INFO</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERR_INTERNAL</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### SystemInfo {:#SystemInfo}


*Defined in [fuchsia.castsysteminfo/cast_system_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.castsysteminfo/cast_system_info.fidl#20)*

 Cast-related device settings

 This table may be extended to include additional cast-specific information.
 The values requested here are generated on first boot of the device and
 don't change unless there is a factory reset.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>local_device_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Local (CastV2) device ID. Identifies the device on a local network.
 Used by the Home app as the device identifier and for MDNS record matching.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>cloud_device_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The device will use this identifier to send/receive CloudCast commands.
 Sending a CloudCast command to the receiver with this ID will ensure that
 the command is accepted and consumed by the device.
</td>
        </tr></table>



## **UNIONS**

### Provider_GetSystemInfo_Result {:#Provider_GetSystemInfo_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Provider_GetSystemInfo_Response'>Provider_GetSystemInfo_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ErrorCode'>ErrorCode</a></code>
            </td>
            <td></td>
        </tr></table>







