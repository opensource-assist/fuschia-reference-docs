Project: /_project.yaml
Book: /_book.yaml

# fuchsia.mem




## **STRUCTS**

### Buffer {:#Buffer}
*Defined in [fuchsia.mem/buffer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-mem/buffer.fidl#14)*



 A buffer for data whose size is not necessarily a multiple of the page
 size.

 VMO objects have a physical size that is always a multiple of the page
 size. As such, VMO alone cannot serve as a buffer for arbitrarly sized
 data. `fuchsia.mem.Buffer` is a standard struct that aggregate the VMO
 and its size.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
            <td> The vmo that contains the buffer.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The number of bytes in the buffer.

 The content of the buffer begin at the start of the VMO and continue
 for `size` bytes. To specify a range of bytes that do not start at
 the beginning of the VMO, use `Range` rather than buffer.

 This size must not be greater than the physical size of the VMO.
</td>
            <td>No default</td>
        </tr>
</table>

### Range {:#Range}
*Defined in [fuchsia.mem/range.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-mem/range.fidl#8)*



 A range of bytes within a VMO.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
            <td> The vmo that contains the bytes.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>offset</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The offset of the first byte within the range relative to the start of
 the VMO.

 For example, if `offset` is zero, then the first byte in the range is
 the first byte in the VMO.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The number of bytes in the range.

 For example, if the offset is 3 and the size is 2, and the VMO starts
 with "abcdefg...", then the range contains "de".

 The sum of the offset and the size must not be greater than the
 physical size of the VMO.
</td>
            <td>No default</td>
        </tr>
</table>









## **XUNIONS**

### Data {:#Data}
*Defined in [fuchsia.mem/buffer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-mem/buffer.fidl#34)*

 Binary data that might be stored inline or in a VMO.

 Useful for performance-sensitive protocols that sometimes receive small
 amounts of binary data (i.e., which is more efficient to provide using
 `bytes`) but also need to support arbitrary amounts of data (i.e., which
 need to be provided out-of-line in a `Buffer`).

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>bytes</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td> The binary data provided inline in the message.
</td>
        </tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
            <td> The binary data provided out-of-line in a `Buffer`.
</td>
        </tr></table>





