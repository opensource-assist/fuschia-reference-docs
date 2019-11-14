[TOC]

# fuchsia.space


## **PROTOCOLS**

## Manager {#Manager}
*Defined in [fuchsia.space/space.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.space/space.fidl#12)*


### Gc {#Gc}

<p>Trigger a garbage collection.</p>

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
                <code><a class='link' href='#Manager_Gc_Result'>Manager_Gc_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Manager_Gc_Response {#Manager_Gc_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>



## **ENUMS**

### ErrorCode {#ErrorCode}
Type: <code>uint32</code>

*Defined in [fuchsia.space/space.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.space/space.fidl#7)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INTERNAL</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>





## **UNIONS**

### Manager_Gc_Result {#Manager_Gc_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Manager_Gc_Response'>Manager_Gc_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ErrorCode'>ErrorCode</a></code>
            </td>
            <td></td>
        </tr></table>







