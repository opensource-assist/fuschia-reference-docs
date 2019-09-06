Project: /_project.yaml
Book: /_book.yaml

# fuchsia.net.dhcp


## **PROTOCOLS**

## Client {:#Client}
*Defined in [fuchsia.net.dhcp/dhcp.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.dhcp/dhcp.fidl#10)*

 Client provides control operations on a DHCP client.

### Start {:#Start}

 Start runs the DHCP client represented by this protocol.

 # Errors

 In the case that the interface this client represents no longer exists,
 the server end of this protocol's channel will be closed.

 Start returns no other errors currently, but callers should check the error
 value in case new errors are returned in the future.

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
                <code><a class='link' href='#Client_Start_Result'>Client_Start_Result</a></code>
            </td>
        </tr></table>

### Stop {:#Stop}

 Stops the DHCP client (if it is running).

 # Errors

 In the case that the interface this client represents no longer exists,
 the server end of this protocol's channel will be closed.

 Stop returns no other errors currently, but callers should check the error
 value in case new errors are returned in the future.

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
                <code><a class='link' href='#Client_Stop_Result'>Client_Stop_Result</a></code>
            </td>
        </tr></table>

## Client {:#Client}
*Defined in [fuchsia.net.dhcp/dhcp.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.dhcp/dhcp.fidl#10)*

 Client provides control operations on a DHCP client.

### Start {:#Start}

 Start runs the DHCP client represented by this protocol.

 # Errors

 In the case that the interface this client represents no longer exists,
 the server end of this protocol's channel will be closed.

 Start returns no other errors currently, but callers should check the error
 value in case new errors are returned in the future.

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
                <code><a class='link' href='#Client_Start_Result'>Client_Start_Result</a></code>
            </td>
        </tr></table>

### Stop {:#Stop}

 Stops the DHCP client (if it is running).

 # Errors

 In the case that the interface this client represents no longer exists,
 the server end of this protocol's channel will be closed.

 Stop returns no other errors currently, but callers should check the error
 value in case new errors are returned in the future.

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
                <code><a class='link' href='#Client_Stop_Result'>Client_Stop_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Client_Start_Response {:#Client_Start_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Client_Stop_Response {:#Client_Stop_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Client_Start_Response {:#Client_Start_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Client_Stop_Response {:#Client_Stop_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>







## **UNIONS**

### Client_Start_Result {:#Client_Start_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Client_Start_Response'>Client_Start_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Client_Stop_Result {:#Client_Stop_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Client_Stop_Response'>Client_Stop_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Client_Start_Result {:#Client_Start_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Client_Start_Response'>Client_Start_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Client_Stop_Result {:#Client_Stop_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Client_Stop_Response'>Client_Stop_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>







