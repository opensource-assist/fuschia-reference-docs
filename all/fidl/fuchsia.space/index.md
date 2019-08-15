Project: /_project.yaml
Book: /_book.yaml

# fuchsia.space


## **PROTOCOLS**

## Manager {:#Manager}
*Defined in [fuchsia.space/space.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.space/space.fidl#12)*


### Gc {:#Gc}

 Trigger a garbage collection.

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

### Manager_Gc_Response {:#Manager_Gc_Response}
*Defined in [fuchsia.space/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#2)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>



## **ENUMS**

### ErrorCode {:#ErrorCode}
Type: <code>uint32</code>

*Defined in [fuchsia.space/space.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.space/space.fidl#7)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INTERNAL</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>





## **UNIONS**

### Manager_Gc_Result {:#Manager_Gc_Result}
*Defined in [fuchsia.space/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#5)*


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







