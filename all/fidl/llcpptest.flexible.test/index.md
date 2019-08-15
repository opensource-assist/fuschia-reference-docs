Project: /_project.yaml
Book: /_book.yaml

# llcpptest.flexible.test


## **PROTOCOLS**

## ReceiveFlexibleEnvelope {:#ReceiveFlexibleEnvelope}
*Defined in [llcpptest.flexible.test/flexible.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/llcpp/flexible.test.fidl#21)*

 The server will be implemented manually to purposefully return xunion/tables
 with an unknown ordinal.

### GetUnknownXUnionMoreBytes {:#GetUnknownXUnionMoreBytes}

 Receive a xunion with an unknown ordinal (suppose coming from a newer
 server) which contains more bytes than the current max message size.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>xu</code></td>
            <td>
                <code><a class='link' href='#FlexibleXUnion'>FlexibleXUnion</a></code>
            </td>
        </tr></table>

### GetUnknownXUnionMoreHandles {:#GetUnknownXUnionMoreHandles}

 Receive a xunion with an unknown ordinal (suppose coming from a newer
 server) which contains more handles than the current max message handle
 count.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>xu</code></td>
            <td>
                <code><a class='link' href='#FlexibleXUnion'>FlexibleXUnion</a></code>
            </td>
        </tr></table>

### GetUnknownTableMoreBytes {:#GetUnknownTableMoreBytes}

 Receive a table with an unknown ordinal (suppose coming from a newer
 server) which contains more bytes than the current max message size.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>t</code></td>
            <td>
                <code><a class='link' href='#FlexibleTable'>FlexibleTable</a></code>
            </td>
        </tr></table>

### GetUnknownTableMoreHandles {:#GetUnknownTableMoreHandles}

 Receive a table with an unknown ordinal (suppose coming from a newer
 server) which contains more handles than the current max message handle
 count.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>t</code></td>
            <td>
                <code><a class='link' href='#FlexibleTable'>FlexibleTable</a></code>
            </td>
        </tr></table>

## ReceiveStrictEnvelope {:#ReceiveStrictEnvelope}
*Defined in [llcpptest.flexible.test/flexible.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/llcpp/flexible.test.fidl#54)*

 Test that the response to GetBoundedXUnion could be allocated on the stack,
 while that to GetUnboundedXUnion is allocated on the heap, through
 compile-time assertions.

### GetBoundedXUnion {:#GetBoundedXUnion}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>xu</code></td>
            <td>
                <code><a class='link' href='#StrictBoundedXUnion'>StrictBoundedXUnion</a></code>
            </td>
        </tr></table>

### GetUnboundedXUnion {:#GetUnboundedXUnion}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>xu</code></td>
            <td>
                <code><a class='link' href='#StrictUnboundedXUnion'>StrictUnboundedXUnion</a></code>
            </td>
        </tr></table>







## **TABLES**

### FlexibleTable {:#FlexibleTable}


*Defined in [llcpptest.flexible.test/flexible.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/llcpp/flexible.test.fidl#14)*

 Only one of the fields will be set by the server. This allows
 the transaction to infer which field is present. See flexible_test.cc.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>want_more_than_30_bytes_at_ordinal_3</code></td>
            <td>
                <code>uint8[30]</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>want_more_than_4_handles_at_ordinal_4</code></td>
            <td>
                <code>handle[4]</code>
            </td>
            <td></td>
        </tr></table>





## **XUNIONS**

### FlexibleXUnion {:#FlexibleXUnion}
*Defined in [llcpptest.flexible.test/flexible.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/llcpp/flexible.test.fidl#7)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>want_more_than_30_bytes</code></td>
            <td>
                <code>uint8[30]</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>want_more_than_4_handles</code></td>
            <td>
                <code>handle[4]</code>
            </td>
            <td></td>
        </tr></table>

### StrictBoundedXUnion {:#StrictBoundedXUnion}
*Defined in [llcpptest.flexible.test/flexible.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/llcpp/flexible.test.fidl#41)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>v</code></td>
            <td>
                <code>vector&lt;uint8&gt;[200]</code>
            </td>
            <td></td>
        </tr></table>

### StrictUnboundedXUnion {:#StrictUnboundedXUnion}
*Defined in [llcpptest.flexible.test/flexible.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/llcpp/flexible.test.fidl#45)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>v</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
        </tr></table>





