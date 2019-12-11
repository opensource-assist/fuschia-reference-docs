[TOC]

# fuchsia.recovery


## **PROTOCOLS**

## FactoryReset {#FactoryReset}
*Defined in [fuchsia.recovery/factory_reset.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.recovery/factory_reset.fidl#11)*

<p>A protocol for intitiating a factory reset.</p>

### Reset {#Reset}

<p>Request an immediate factory reset. If unsuccessful will return an
error.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

















