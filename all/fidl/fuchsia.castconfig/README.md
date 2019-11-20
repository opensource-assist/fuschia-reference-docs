[TOC]

# fuchsia.castconfig


## **PROTOCOLS**

## Provider {#Provider}
*Defined in [fuchsia.castconfig/cast_config.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.castconfig/cast_config.fidl#19)*

<p>Interface that provides cast config data.</p>

### Watch {#Watch}

<p>Requests a buffer containing cast config data.
This call implements the Hanging Get protocol as detailed in
https://fuchsia.dev/fuchsia-src/development/api/fidl.md#delay-responses-using-hanging-gets</p>
<p>All error cases are terminal, clients should not retry on error.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Provider_Watch_Result'>Provider_Watch_Result</a></code>
            </td>
        </tr></table>

### Notify {#Notify}

<p>Notifies the config provider of the config status.</p>
<p><code>processed</code>: <code>true</code> if successfully recieved and processed
<code>retry</code>: If <code>processed</code> is <code>false</code> config provider determines if a retry
is appropriate.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>processed</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>retry</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



## **STRUCTS**

### Provider_Watch_Response {#Provider_Watch_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### ErrorCode {#ErrorCode}
Type: <code>uint32</code>

*Defined in [fuchsia.castconfig/cast_config.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.castconfig/cast_config.fidl#10)*

<p>Error codes for the Watch operation.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NO_CAST_CONFIG</code></td>
            <td><code>1</code></td>
            <td><p>Error when there is no cast config available.</p>
</td>
        </tr><tr>
            <td><code>INTERNAL</code></td>
            <td><code>2</code></td>
            <td><p>Generic error.</p>
</td>
        </tr></table>





## **UNIONS**

### Provider_Watch_Result {#Provider_Watch_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Provider_Watch_Response'>Provider_Watch_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ErrorCode'>ErrorCode</a></code>
            </td>
            <td></td>
        </tr></table>







