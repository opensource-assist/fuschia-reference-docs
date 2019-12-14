[TOC]

# fuchsia.test.hub


## **PROTOCOLS**

## HubReport {#HubReport}
*Defined in [fuchsia.test.hub/hub.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/component_manager/tests/fidl/hub.fidl#16)*

<p>A protocol used in testing by a component instance to propagate its view of
hub directory to the integration test.</p>

### ListDirectory {#ListDirectory}

<p>Returns a list of the entiries within the directories specified by the
provided path.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>path</code></td>
            <td>
                <code>string[4096]</code>
            </td>
        </tr><tr>
            <td><code>entries</code></td>
            <td>
                <code>vector&lt;string&gt;[100]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### ReportFileContent {#ReportFileContent}

<p>Returns the content of the file specified by the provided path.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>path</code></td>
            <td>
                <code>string[4096]</code>
            </td>
        </tr><tr>
            <td><code>content</code></td>
            <td>
                <code>string[8192]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>















## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="MAX_NUM_ENTRIES">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/component_manager/tests/fidl/hub.fidl#11">MAX_NUM_ENTRIES</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint64</code></td>
            <td><p>The maximum number of entries to report within a directory in tests.
This capacity is currently set somewhat arbitrarily.</p>
</td>
        </tr>
    
</table>



