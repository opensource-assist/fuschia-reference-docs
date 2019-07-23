Project: /_project.yaml
Book: /_book.yaml

# fuchsia.hardware.mediacodec


## **PROTOCOLS**

## Device {:#Device}
*Defined in [fuchsia.hardware.mediacodec/mediacodec.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-mediacodec/mediacodec.fidl#8)*


### GetCodecFactory {:#GetCodecFactory}

 This method connects the caller with a fuchsia.mediacodec.CodecFactory.
 Ideally, we wouldn't have the intermediary, but it is necessary with the current
 DDK APIs.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>

















