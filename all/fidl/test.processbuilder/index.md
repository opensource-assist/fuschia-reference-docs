Project: /_project.yaml
Book: /_book.yaml

# test.processbuilder


## **PROTOCOLS**

## Util {:#Util}
*Defined in [test.processbuilder/test_util.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/process_builder/test_util.test.fidl#13)*


### GetArguments {:#GetArguments}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>args</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr></table>

### GetEnvironment {:#GetEnvironment}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>vars</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#EnvVar'>EnvVar</a>&gt;</code>
            </td>
        </tr></table>

### DumpNamespace {:#DumpNamespace}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>contents</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

### ReadFile {:#ReadFile}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>path</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>contents</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



## **STRUCTS**

### EnvVar {:#EnvVar}
*Defined in [test.processbuilder/test_util.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/process_builder/test_util.test.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>













