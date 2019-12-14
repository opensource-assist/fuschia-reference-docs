[TOC]

# fuchsia.scenic.snapshot


## **PROTOCOLS**

## Loader {#Loader}
*Defined in [fuchsia.scenic.snapshot/loader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.scenic.snapshot/loader.fidl#12)*

<p>Snapshot loader exported by <code>ViewProvider</code> to load snapshots into views
created from it.</p>

### Load {#Load}

<p>Load the snapshot from the Vmo buffer payload.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>payload</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
        </tr></table>



















