[TOC]

# fuchsia.hardware.tee


## **PROTOCOLS**

## DeviceConnector {#DeviceConnector}
*Defined in [fuchsia.hardware.tee/device_connector.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-tee/device_connector.fidl#12)*

<p>Protocol used by the TEE Manager to proxy requests for TEE access to the driver.</p>

### ConnectTee {#ConnectTee}

<p>Requests service from the TEE driver while the caller provides a client end to a
Provider server that supports the driver on any RPCs.</p>
<p>The sole caller of this should be the TEE Manager.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service_provider</code></td>
            <td>
                <code><a class='link' href='../fuchsia.tee.manager/'>fuchsia.tee.manager</a>/<a class='link' href='../fuchsia.tee.manager/#Provider'>Provider</a>?</code>
            </td>
        </tr><tr>
            <td><code>tee_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.tee/'>fuchsia.tee</a>/<a class='link' href='../fuchsia.tee/#Device'>Device</a>&gt;</code>
            </td>
        </tr></table>



















