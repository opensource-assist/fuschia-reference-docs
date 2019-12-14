[TOC]

# transformerintegration.test


## **PROTOCOLS**

## ReceiveXunionsForUnions {#ReceiveXunionsForUnions}
*Defined in [transformerintegration.test/transformer_integration.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/transformer_integration.test.fidl#11)*

<p>The server will be implemented manually to test receiving xunions as unions
in both clients and servers.</p>

### UnionEvent {#UnionEvent}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>sandwich</code></td>
            <td>
                <code><a class='link' href='../example/'>example</a>/<a class='link' href='../example/#Sandwich4'>Sandwich4</a></code>
            </td>
        </tr></table>

### SendUnion {#SendUnion}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>sandwich</code></td>
            <td>
                <code><a class='link' href='../example/'>example</a>/<a class='link' href='../example/#Sandwich4'>Sandwich4</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>success</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

### ReceiveUnion {#ReceiveUnion}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>sandwich</code></td>
            <td>
                <code><a class='link' href='../example/'>example</a>/<a class='link' href='../example/#Sandwich4'>Sandwich4</a></code>
            </td>
        </tr></table>

## MultiArgReceiveXunions {#MultiArgReceiveXunions}
*Defined in [transformerintegration.test/transformer_integration.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/transformer_integration.test.fidl#24)*

<p>Tests handling differing argument offsets caused by size differences between
unions to xunions.</p>

### TwoUnion {#TwoUnion}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>one</code></td>
            <td>
                <code><a class='link' href='../example/'>example</a>/<a class='link' href='../example/#Sandwich4'>Sandwich4</a></code>
            </td>
        </tr><tr>
            <td><code>two</code></td>
            <td>
                <code><a class='link' href='../example/'>example</a>/<a class='link' href='../example/#Sandwich4'>Sandwich4</a></code>
            </td>
        </tr></table>

















