Project: /_project.yaml
Book: /_book.yaml

# fuchsia.telephony.manager


## **PROTOCOLS**

## Manager {:#Manager}
*Defined in [fuchsia.telephony.manager/manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.telephony.manager/manager.fidl#11)*

 Primary Telephony management interface

### IsAvailable {:#IsAvailable}

 Returns whether or not a modem is currently available on the system.

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

### GetRilHandle {:#GetRilHandle}

 Get access to a RIL

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ril_iface</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.telephony.ril/index.html'>fuchsia.telephony.ril</a>/<a class='link' href='../fuchsia.telephony.ril/index.html#RadioInterfaceLayer'>RadioInterfaceLayer</a>&gt;</code>
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















