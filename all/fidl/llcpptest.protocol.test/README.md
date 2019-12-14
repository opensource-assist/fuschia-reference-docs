[TOC]

# llcpptest.protocol.test


## **PROTOCOLS**

## ErrorMethods {#ErrorMethods}
*Defined in [llcpptest.protocol.test/protocol.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/llcpp/protocol.test.fidl#16)*

<p>Protocol for testing methods with error types.
In the implementation, each method is hardcoded to return either the
success or the error case. This should follow the naming of the method,
e.g. ReturnPrimitiveError will always return the error case.</p>

### NoArgsPrimitiveError {#NoArgsPrimitiveError}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>should_error</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#ErrorMethods_NoArgsPrimitiveError_Result'>ErrorMethods_NoArgsPrimitiveError_Result</a></code>
            </td>
        </tr></table>

### ManyArgsCustomError {#ManyArgsCustomError}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>should_error</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#ErrorMethods_ManyArgsCustomError_Result'>ErrorMethods_ManyArgsCustomError_Result</a></code>
            </td>
        </tr></table>

## Frobinator {#Frobinator}
*Defined in [llcpptest.protocol.test/protocol.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/llcpp/protocol.test.fidl#21)*


### Frob {#Frob}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### Grob {#Grob}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

### Hrob {#Hrob}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



## **STRUCTS**

### ErrorMethods_NoArgsPrimitiveError_Response {#ErrorMethods_NoArgsPrimitiveError_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### ErrorMethods_ManyArgsCustomError_Response {#ErrorMethods_ManyArgsCustomError_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>a</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>b</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>c</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### MyError {#MyError}
Type: <code>int32</code>

*Defined in [llcpptest.protocol.test/protocol.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/llcpp/protocol.test.fidl#7)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>BAD_ERROR</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>REALLY_BAD_ERROR</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>





## **UNIONS**

### ErrorMethods_NoArgsPrimitiveError_Result {#ErrorMethods_NoArgsPrimitiveError_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#ErrorMethods_NoArgsPrimitiveError_Response'>ErrorMethods_NoArgsPrimitiveError_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### ErrorMethods_ManyArgsCustomError_Result {#ErrorMethods_ManyArgsCustomError_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#ErrorMethods_ManyArgsCustomError_Response'>ErrorMethods_ManyArgsCustomError_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#MyError'>MyError</a></code>
            </td>
            <td></td>
        </tr></table>









