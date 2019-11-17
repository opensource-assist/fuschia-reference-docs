[TOC]

# test.component.mockrunner


## **PROTOCOLS**

## MockComponent {#MockComponent}
*Defined in [test.component.mockrunner/runner.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/appmgr/integration_tests/fidl/runner.fidl#15)*


### Kill {#Kill}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>errorcode</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### ConnectToService {#ConnectToService}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>channel</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



### SetServiceDirectory {#SetServiceDirectory}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>channel</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



### PublishService {#PublishService}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### GetProgramMetadata {#GetProgramMetadata}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>metadata</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.sys/'>fuchsia.sys</a>/<a class='link' href='../fuchsia.sys/#ProgramMetadata'>ProgramMetadata</a>&gt;[20]</code>
            </td>
        </tr></table>

## MockRunner {#MockRunner}
*Defined in [test.component.mockrunner/runner.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/appmgr/integration_tests/fidl/runner.fidl#31)*


### Crash {#Crash}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### ConnectToComponent {#ConnectToComponent}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>req</code></td>
            <td>
                <code>request&lt;<a class='link' href='#MockComponent'>MockComponent</a>&gt;</code>
            </td>
        </tr></table>



### OnComponentCreated {#OnComponentCreated}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#ComponentInfo'>ComponentInfo</a></code>
            </td>
        </tr></table>

### OnComponentKilled {#OnComponentKilled}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

## MockRunnerRegistry {#MockRunnerRegistry}
*Defined in [test.component.mockrunner/runner.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/appmgr/integration_tests/fidl/runner.fidl#44)*


### Register {#Register}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>runner</code></td>
            <td>
                <code><a class='link' href='#MockRunner'>MockRunner</a></code>
            </td>
        </tr></table>





## **STRUCTS**

### ComponentInfo {#ComponentInfo}
*Defined in [test.component.mockrunner/runner.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/appmgr/integration_tests/fidl/runner.fidl#9)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>unique_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>url</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>













