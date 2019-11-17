[TOC]

# fidl.test.frobinator


## **PROTOCOLS**

## Frobinator {#Frobinator}
*Defined in [fidl.test.frobinator/frobinator.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/test/frobinator.test.fidl#7)*


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

### Fail {#Fail}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>fail</code></td>
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
                <code><a class='link' href='#Frobinator_Fail_Result'>Frobinator_Fail_Result</a></code>
            </td>
        </tr></table>

### FailHard {#FailHard}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>fail</code></td>
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
                <code><a class='link' href='#Frobinator_FailHard_Result'>Frobinator_FailHard_Result</a></code>
            </td>
        </tr></table>

### FailHardest {#FailHardest}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>fail</code></td>
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
                <code><a class='link' href='#Frobinator_FailHardest_Result'>Frobinator_FailHardest_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Frobinator_Fail_Response {#Frobinator_Fail_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Frobinator_FailHard_Response {#Frobinator_FailHard_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>froyo</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Frobinator_FailHardest_Response {#Frobinator_FailHardest_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>fro</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>yo</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>







## **UNIONS**

### Frobinator_Fail_Result {#Frobinator_Fail_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Frobinator_Fail_Response'>Frobinator_Fail_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr></table>

### Frobinator_FailHard_Result {#Frobinator_FailHard_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Frobinator_FailHard_Response'>Frobinator_FailHard_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr></table>

### Frobinator_FailHardest_Result {#Frobinator_FailHardest_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Frobinator_FailHardest_Response'>Frobinator_FailHardest_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr></table>







