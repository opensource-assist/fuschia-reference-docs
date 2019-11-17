[TOC]

# fuchsia.services.examples


## **PROTOCOLS**

## MindReader {#MindReader}
*Defined in [fuchsia.services.examples/mind_reader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/public/dart/fuchsia_services/examples/mind_reader/fidl/mind_reader.fidl#8)*


### ReadMind {#ReadMind}

<p>When this method is called the service will attempt to guess
what the calling process is thinking.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>response</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

## ThoughtLeaker {#ThoughtLeaker}
*Defined in [fuchsia.services.examples/mind_reader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/public/dart/fuchsia_services/examples/mind_reader/fidl/mind_reader.fidl#15)*


### CurrentThought {#CurrentThought}

<p>This service is used to leak the current thought of the process.
If this service is exposed to the [MindReader] it will connect
to it to extract the current thought.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>response</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>















