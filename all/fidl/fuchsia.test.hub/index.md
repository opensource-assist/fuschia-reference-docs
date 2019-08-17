Project: /_project.yaml
Book: /_book.yaml

# fuchsia.test.hub


## **PROTOCOLS**

## HubReport {:#HubReport}
*Defined in [fuchsia.test.hub/fuchsia.test.hub.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/component_manager/tests/fidl/fuchsia.test.hub.fidl#16)*

 A protocol used in testing by a component instance to propagate its view of
 hub directory to the integration test.

### ListDirectory {:#ListDirectory}

 Returns a list of the entiries within the directories specified by the
 provided path.

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



### ReportFileContent {:#ReportFileContent}

 Returns the content of the file specified by the provided path.

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

















## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/component_manager/tests/fidl/fuchsia.test.hub.fidl#11">MAX_NUM_ENTRIES</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint64</code></td>
            <td> The maximum number of entries to report within a directory in tests.
 This capacity is currently set somewhat arbitrarily.
</td>
        </tr>
    
</table>

