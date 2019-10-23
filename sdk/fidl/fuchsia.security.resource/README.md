[TOC]

# fuchsia.security.resource


## **PROTOCOLS**

## Vmex {#Vmex}
*Defined in [fuchsia.security.resource/vmex.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-security-resource/vmex.fidl#10)*

 Protocol for providing a `ZX_RSRC_KIND_VMEX` to programs that should be
 able to mark VMOs as executable.

### Get {#Get}

 Get a VMEX resource handle as |resource|.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>vmex</code></td>
            <td>
                <code>handle&lt;resource&gt;</code>
            </td>
        </tr></table>















