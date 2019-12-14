[TOC]

# fuchsia.telephony.manager


## **PROTOCOLS**

## Manager {#Manager}
*Defined in [fuchsia.telephony.manager/manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.telephony.manager/manager.fidl#11)*

<p>Primary Telephony management interface</p>

### IsAvailable {#IsAvailable}

<p>Returns whether or not a modem is currently available on the system.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>available</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

### GetRilHandle {#GetRilHandle}

<p>Get access to a RIL</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ril_iface</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.telephony.ril/'>fuchsia.telephony.ril</a>/<a class='link' href='../fuchsia.telephony.ril/#RadioInterfaceLayer'>RadioInterfaceLayer</a>&gt;</code>
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

















