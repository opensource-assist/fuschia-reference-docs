[TOC]

# fuchsia.component.test


## **PROTOCOLS**

## Counter {#Counter}
*Defined in [fuchsia.component.test/test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/rust/fuchsia-component/blackbox_unit_tests/test.test.fidl#8)*

<p>A 32-bit counter.</p>

### GetAndIncrement {#GetAndIncrement}

<p>Return the current counter value, then increment it.</p>

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
                <code>uint32</code>
            </td>
        </tr></table>

## CounterV2 {#CounterV2}
*Defined in [fuchsia.component.test/test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/rust/fuchsia-component/blackbox_unit_tests/test.test.fidl#14)*

<p>A new, 64-bit counter.</p>

### GetAndIncrement {#GetAndIncrement}

<p>Return the current counter value, then increment it.</p>

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
                <code>uint64</code>
            </td>
        </tr></table>















