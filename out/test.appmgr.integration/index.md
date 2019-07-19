Project: /_project.yaml
Book: /_book.yaml

# test.appmgr.integration


## **PROTOCOLS**

## DataFileReaderWriter {:#DataFileReaderWriter}
*Defined in [test.appmgr.integration/data_file_reader_writer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/bin/appmgr/integration_tests/util/data_file_reader_writer.fidl#12)*


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
                <code>string?</code>
            </td>
        </tr></table>

### WriteFile {:#WriteFile}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>path</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>contents</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>















