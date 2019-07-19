Project: /_project.yaml
Book: /_book.yaml

# fuchsia.vulkan.loader


## **PROTOCOLS**

## Loader {:#Loader}
*Defined in [fuchsia.vulkan.loader/loader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.vulkan.loader/loader.fidl#9)*


### Get {:#Get}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string[64]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>lib</code></td>
            <td>
                <code>handle&lt;vmo&gt;?</code>
            </td>
        </tr></table>















