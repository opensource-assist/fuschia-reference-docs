[TOC]

# fuchsia.examples.intl.manager


## **PROTOCOLS**

## PropertyManager {#PropertyManager}
*Defined in [fuchsia.examples.intl.manager/manager.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/examples/intl/manager/fidl/manager.test.fidl#17)*

<p>For toy examples, defines the setter counterpart to the getter in
<code>fuchsia.intl.PropertyProvider</code>, allowing the internationalization <code>Profile</code> to be set via FIDL,
and hence passed on to additional recipients.</p>
<p>Note that in production scenarios, a <code>fuchsia.intl.PropertyProvider</code> would like be reading the
user's internationalization preferences from a preferences service and generating a <code>Profile</code>,
rather than allowing a <code>Profile</code> to be set directly.</p>

### SetProfile {#SetProfile}

<p>Set the internationalization profile that is served by this provider.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>intl_profile</code></td>
            <td>
                <code><a class='link' href='../fuchsia.intl/'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/#Profile'>Profile</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>















