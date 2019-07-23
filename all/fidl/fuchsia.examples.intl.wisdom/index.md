Project: /_project.yaml
Book: /_book.yaml

# fuchsia.examples.intl.wisdom


## **PROTOCOLS**

## IntlWisdomServer {:#IntlWisdomServer}
*Defined in [fuchsia.examples.intl.wisdom/intl_wisdom.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/examples/intl/wisdom/fidl/intl_wisdom.fidl#12)*

 Interface for a service that, given a `fuchsia.intl.Profile` and some basic parameters, can
 provide pithy strings of wisdom to demonstrate the use of `Profile`.

### AskForWisdom {:#AskForWisdom}

 Asks for a wisdom string.

 Params:
   intl_profile: Provides the i18n context for the request
   timestamp_ms: Timestamp in milliseconds since the epoch. Used as an input for the wisdom
   text.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>intl_profile</code></td>
            <td>
                <code><a class='link' href='../fuchsia.intl/index.html'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/index.html#Profile'>Profile</a></code>
            </td>
        </tr><tr>
            <td><code>timestamp_ms</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>response</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr></table>















