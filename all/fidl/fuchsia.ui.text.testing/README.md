[TOC]

# fuchsia.ui.text.testing


## **PROTOCOLS**

## TextFieldTestSuite {#TextFieldTestSuite}
*Defined in [fuchsia.ui.text.testing/testing.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.text.testing/testing.fidl#13)*

<p>This interface runs the standard suite of tests on an implementation of TextField.
If you maintain a TextField implementation, you should ensure to spin up the
text_test_suite package and call RunTest in your integration tests. Each call to
RunTest should contain a fresh TextField handle that points to an empty text field.</p>

### RunTest {#RunTest}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>field</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.text/'>fuchsia.ui.text</a>/<a class='link' href='../fuchsia.ui.text/#TextField'>TextField</a></code>
            </td>
        </tr><tr>
            <td><code>test_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>passed</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>message</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

### ListTests {#ListTests}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>results</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#TestInfo'>TestInfo</a>&gt;</code>
            </td>
        </tr></table>



## **STRUCTS**

### TestInfo {#TestInfo}
*Defined in [fuchsia.ui.text.testing/testing.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.text.testing/testing.fidl#20)*



<p>Indicates if the tests passed, and a human-readable message indicating test failures
if not.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>















