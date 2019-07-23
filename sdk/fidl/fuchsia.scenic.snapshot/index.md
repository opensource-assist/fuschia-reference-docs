Project: /_project.yaml
Book: /_book.yaml

# fuchsia.scenic.snapshot


## **PROTOCOLS**

## Loader {:#Loader}
*Defined in [fuchsia.scenic.snapshot/loader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.scenic.snapshot/loader.fidl#12)*

 Snapshot loader exported by `ViewProvider` to load snapshots into views
 created from it.

### Load {:#Load}

 Load the snapshot from the Vmo buffer payload.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>payload</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
        </tr></table>

















