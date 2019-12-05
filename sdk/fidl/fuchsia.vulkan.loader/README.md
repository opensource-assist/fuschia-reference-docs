[TOC]

# fuchsia.vulkan.loader


## **PROTOCOLS**

## Loader {#Loader}
*Defined in [fuchsia.vulkan.loader/loader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.vulkan.loader/loader.fidl#9)*

<p>Service to provide Vulkan libraries to the loader.</p>

### Get {#Get}

<p>Requests a client driver library with the given name from the Vulkan loader
service. Returns a VMO suitable for loading as a dynamic library on
success, a null handle on failure.</p>

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

















