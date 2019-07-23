Project: /_project.yaml
Book: /_book.yaml

# fuchsia.examples.intl.manager


## **PROTOCOLS**

## PropertyManager {:#PropertyManager}
*Defined in [fuchsia.examples.intl.manager/manager.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/examples/intl/manager/fidl/manager.test.fidl#17)*

 For toy examples, defines the setter counterpart to the getter in
 `fuchsia.intl.PropertyProvider`, allowing the internationalization `Profile` to be set via FIDL,
 and hence passed on to additional recipients.

 Note that in production scenarios, a `fuchsia.intl.PropertyProvider` would like be reading the
 user's internationalization preferences from a preferences service and generating a `Profile`,
 rather than allowing a `Profile` to be set directly.

### SetProfile {:#SetProfile}

 Set the internationalization profile that is served by this provider.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>intl_profile</code></td>
            <td>
                <code><a class='link' href='../fuchsia.intl/index.html'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/index.html#Profile'>Profile</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>















