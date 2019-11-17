[TOC]

# fuchsia.update.channel


## **PROTOCOLS**

## Provider {#Provider}
*Defined in [fuchsia.update.channel/channel.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update.channel/channel.fidl#9)*

<p>Information about the state of the update system.</p>

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















