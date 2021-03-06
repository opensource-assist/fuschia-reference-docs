[TOC]

# fuchsia.deprecatedtimezone


## **PROTOCOLS**

## TimeService {#TimeService}
*Defined in [fuchsia.deprecatedtimezone/deprecated_time_service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.deprecatedtimezone/deprecated_time_service.fidl#9)*

<p>Interface to allow manual updates of the system time.</p>

### Update {#Update}

<p>Requests an immediate update of the time from network.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>num_retries</code></td>
            <td>
                <code>uint8</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>successful</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

## Timezone {#Timezone}
*Defined in [fuchsia.deprecatedtimezone/deprecated_time_zone.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.deprecatedtimezone/deprecated_time_zone.fidl#18)*


### GetTimezoneOffsetMinutes {#GetTimezoneOffsetMinutes}

<p>Returns local timezone offset (in minutes from UTC. Can be negative) for
the supplied number of milliseconds since the Unix epoch. Returns a
non-zero DST offset when appropriate.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>milliseconds_since_epoch</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>local_offset_minutes</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>dst_offset_minutes</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### SetTimezone {#SetTimezone}

<p>Sets the timezone for the machine based on an ICU ID.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>timezone_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

### GetTimezoneId {#GetTimezoneId}

<p>Gets the timezone ID string.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>timezone_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

### Watch {#Watch}

<p>Watches for updates to the timezone ID.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#TimezoneWatcher'>TimezoneWatcher</a></code>
            </td>
        </tr></table>



## TimezoneWatcher {#TimezoneWatcher}
*Defined in [fuchsia.deprecatedtimezone/deprecated_time_zone.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.deprecatedtimezone/deprecated_time_zone.fidl#35)*


### OnTimezoneOffsetChange {#OnTimezoneOffsetChange}

<p>When the timezone changes, returns the new timezone ID.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>timezone_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



















