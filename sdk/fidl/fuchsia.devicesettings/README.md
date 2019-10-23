[TOC]

# fuchsia.devicesettings


## **PROTOCOLS**

## DeviceSettingsManager {#DeviceSettingsManager}
*Defined in [fuchsia.devicesettings/devicesettings.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.devicesettings/devicesettings.fidl#22)*

 Manager interface used to manage settings

### GetInteger {#GetInteger}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>val</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>s</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>

### GetString {#GetString}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>val</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>s</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>

### SetInteger {#SetInteger}

 Returns false on database error and true on success.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>val</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

### SetString {#SetString}

 Returns false on database error and true on success.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>val</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

### Watch {#Watch}

 Register a watcher to be called when a setting changes
 Returns Status::ok, Status::errInvalidSetting or Status::errUnknown

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#DeviceSettingsWatcher'>DeviceSettingsWatcher</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>

## DeviceSettingsWatcher {#DeviceSettingsWatcher}
*Defined in [fuchsia.devicesettings/devicesettings.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.devicesettings/devicesettings.fidl#39)*

 A watcher for device settings changes

### OnChangeSettings {#OnChangeSettings}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#ValueType'>ValueType</a></code>
            </td>
        </tr></table>







## **ENUMS**

### Status {#Status}
Type: <code>uint8</code>

*Defined in [fuchsia.devicesettings/devicesettings.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.devicesettings/devicesettings.fidl#6)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ok</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>errNotSet</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>errInvalidSetting</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>errRead</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>errIncorrectType</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>errUnknown</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr></table>

### ValueType {#ValueType}
Type: <code>uint8</code>

*Defined in [fuchsia.devicesettings/devicesettings.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.devicesettings/devicesettings.fidl#15)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>number</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>text</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>











