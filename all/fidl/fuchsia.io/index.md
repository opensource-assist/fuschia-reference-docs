Project: /_project.yaml
Book: /_book.yaml

# fuchsia.io


## **PROTOCOLS**

## Node {:#Node}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#161)*

 Node defines the minimal interface for entities which can be accessed in a filesystem.

### Clone {:#Clone}

 Create another connection to the same remote object.

 `flags` may be any of:
 - `OPEN_RIGHT_*`
 - `OPEN_FLAG_APPEND`
 - `OPEN_FLAG_NO_REMOTE`
 - `OPEN_FLAG_DESCRIBE`
 - `CLONE_FLAG_SAME_RIGHTS`

 All other flags are ignored.

 The `OPEN_RIGHT_*` bits in `flags` request corresponding rights over the resulting
 cloned object.
 The cloned object must have rights less than or equal to the original object.
 Alternatively, pass `CLONE_FLAG_SAME_RIGHTS` to inherit the rights on the source connection.
 It is invalid to pass any of the `OPEN_RIGHT_*` flags together with `CLONE_FLAG_SAME_RIGHTS`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>object</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Node'>Node</a>&gt;</code>
            </td>
        </tr></table>



### Close {:#Close}

 Terminates connection with object.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Describe {:#Describe}

 Returns extra information about the type of the object.
 If the `Describe` operation fails, the connection is closed.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#NodeInfo'>NodeInfo</a></code>
            </td>
        </tr></table>

### OnOpen {:#OnOpen}

 An event produced eagerly by a FIDL server if requested by `OPEN_FLAG_DESCRIBE`.

 Indicates the success or failure of the open operation, and optionally describes the
 object. If the status is `ZX_OK`, `info` contains descriptive information about the object
 (the same as would be returned by `Describe`).



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#NodeInfo'>NodeInfo</a>?</code>
            </td>
        </tr></table>

### Sync {:#Sync}

 Synchronizes updates to the node to the underlying media, if it exists.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### GetAttr {:#GetAttr}

 Acquires information about the node.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='#NodeAttributes'>NodeAttributes</a></code>
            </td>
        </tr></table>

### SetAttr {:#SetAttr}

 Updates information about the node.
 `flags` may be any of `NODE_ATTRIBUTE_FLAG_*`.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='#NodeAttributes'>NodeAttributes</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Ioctl {:#Ioctl}

 Deprecated. Only for use with compatibility with devhost.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>opcode</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>max_out</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>handles</code></td>
            <td>
                <code>vector&lt;handle&gt;[2]</code>
            </td>
        </tr><tr>
            <td><code>in</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>handles</code></td>
            <td>
                <code>vector&lt;handle&gt;[2]</code>
            </td>
        </tr><tr>
            <td><code>out</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>

## File {:#File}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#301)*

 File defines the interface of a node which contains a flat layout of data.

### Clone {:#Clone}

 Create another connection to the same remote object.

 `flags` may be any of:
 - `OPEN_RIGHT_*`
 - `OPEN_FLAG_APPEND`
 - `OPEN_FLAG_NO_REMOTE`
 - `OPEN_FLAG_DESCRIBE`
 - `CLONE_FLAG_SAME_RIGHTS`

 All other flags are ignored.

 The `OPEN_RIGHT_*` bits in `flags` request corresponding rights over the resulting
 cloned object.
 The cloned object must have rights less than or equal to the original object.
 Alternatively, pass `CLONE_FLAG_SAME_RIGHTS` to inherit the rights on the source connection.
 It is invalid to pass any of the `OPEN_RIGHT_*` flags together with `CLONE_FLAG_SAME_RIGHTS`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>object</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Node'>Node</a>&gt;</code>
            </td>
        </tr></table>



### Close {:#Close}

 Terminates connection with object.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Describe {:#Describe}

 Returns extra information about the type of the object.
 If the `Describe` operation fails, the connection is closed.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#NodeInfo'>NodeInfo</a></code>
            </td>
        </tr></table>

### OnOpen {:#OnOpen}

 An event produced eagerly by a FIDL server if requested by `OPEN_FLAG_DESCRIBE`.

 Indicates the success or failure of the open operation, and optionally describes the
 object. If the status is `ZX_OK`, `info` contains descriptive information about the object
 (the same as would be returned by `Describe`).



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#NodeInfo'>NodeInfo</a>?</code>
            </td>
        </tr></table>

### Sync {:#Sync}

 Synchronizes updates to the node to the underlying media, if it exists.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### GetAttr {:#GetAttr}

 Acquires information about the node.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='#NodeAttributes'>NodeAttributes</a></code>
            </td>
        </tr></table>

### SetAttr {:#SetAttr}

 Updates information about the node.
 `flags` may be any of `NODE_ATTRIBUTE_FLAG_*`.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='#NodeAttributes'>NodeAttributes</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Ioctl {:#Ioctl}

 Deprecated. Only for use with compatibility with devhost.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>opcode</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>max_out</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>handles</code></td>
            <td>
                <code>vector&lt;handle&gt;[2]</code>
            </td>
        </tr><tr>
            <td><code>in</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>handles</code></td>
            <td>
                <code>vector&lt;handle&gt;[2]</code>
            </td>
        </tr><tr>
            <td><code>out</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>

### Read {:#Read}

 Reads 'count' bytes at the seek offset.
 The seek offset is moved forward by the number of bytes read.

 This method requires following rights: `OPEN_RIGHT_READABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>count</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>

### ReadAt {:#ReadAt}

 Reads 'count' bytes at the provided offset.
 Does not affect the seek offset.

 This method requires following rights: `OPEN_RIGHT_READABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>count</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>offset</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>

### Write {:#Write}

 Writes data at the seek offset.
 The seek offset is moved forward by the number of bytes written.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>actual</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### WriteAt {:#WriteAt}

 Writes data to the provided offset.
 Does not affect the seek offset.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr><tr>
            <td><code>offset</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>actual</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### Seek {:#Seek}

 Moves the offset at which the next invocation of `Read()` or `Write()` will
 occur.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>offset</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>start</code></td>
            <td>
                <code><a class='link' href='#SeekOrigin'>SeekOrigin</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>offset</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### Truncate {:#Truncate}

 Shrinks the file size to 'length' bytes.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>length</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### GetFlags {:#GetFlags}

 Acquires the Directory::Open rights and flags used to access this file.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### SetFlags {:#SetFlags}

 Changes the Directory::Open flags used to access the file.
 Supported flags which can be turned on / off:
 - `OPEN_FLAG_APPEND`

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### GetBuffer {:#GetBuffer}

 Acquires a buffer representing this file, if there is one, with the
 requested access rights.

 `flags` may be any of `VMO_FLAG_*`.

 This method requires following rights:
 - `OPEN_RIGHT_WRITABLE` if `flags` includes `VMO_FLAG_WRITE`.
 - `OPEN_RIGHT_READABLE` if `flags` includes `VMO_FLAG_READ` or `VMO_FLAG_EXEC`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a>?</code>
            </td>
        </tr></table>

## DirectoryWatcher {:#DirectoryWatcher}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#420)*

 DirectoryWatcher transmits messages from a filesystem server
 about events happening in the filesystem. Clients can register
 new watchers using the Directory "Watch" method, where they can
 filter which events they want to receive notifications for.

### OnEvent {:#OnEvent}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>events</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>



## Directory {:#Directory}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#427)*

 Directory defines a node which is capable of containing other Objects.

### Clone {:#Clone}

 Create another connection to the same remote object.

 `flags` may be any of:
 - `OPEN_RIGHT_*`
 - `OPEN_FLAG_APPEND`
 - `OPEN_FLAG_NO_REMOTE`
 - `OPEN_FLAG_DESCRIBE`
 - `CLONE_FLAG_SAME_RIGHTS`

 All other flags are ignored.

 The `OPEN_RIGHT_*` bits in `flags` request corresponding rights over the resulting
 cloned object.
 The cloned object must have rights less than or equal to the original object.
 Alternatively, pass `CLONE_FLAG_SAME_RIGHTS` to inherit the rights on the source connection.
 It is invalid to pass any of the `OPEN_RIGHT_*` flags together with `CLONE_FLAG_SAME_RIGHTS`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>object</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Node'>Node</a>&gt;</code>
            </td>
        </tr></table>



### Close {:#Close}

 Terminates connection with object.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Describe {:#Describe}

 Returns extra information about the type of the object.
 If the `Describe` operation fails, the connection is closed.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#NodeInfo'>NodeInfo</a></code>
            </td>
        </tr></table>

### OnOpen {:#OnOpen}

 An event produced eagerly by a FIDL server if requested by `OPEN_FLAG_DESCRIBE`.

 Indicates the success or failure of the open operation, and optionally describes the
 object. If the status is `ZX_OK`, `info` contains descriptive information about the object
 (the same as would be returned by `Describe`).



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#NodeInfo'>NodeInfo</a>?</code>
            </td>
        </tr></table>

### Sync {:#Sync}

 Synchronizes updates to the node to the underlying media, if it exists.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### GetAttr {:#GetAttr}

 Acquires information about the node.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='#NodeAttributes'>NodeAttributes</a></code>
            </td>
        </tr></table>

### SetAttr {:#SetAttr}

 Updates information about the node.
 `flags` may be any of `NODE_ATTRIBUTE_FLAG_*`.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='#NodeAttributes'>NodeAttributes</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Ioctl {:#Ioctl}

 Deprecated. Only for use with compatibility with devhost.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>opcode</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>max_out</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>handles</code></td>
            <td>
                <code>vector&lt;handle&gt;[2]</code>
            </td>
        </tr><tr>
            <td><code>in</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>handles</code></td>
            <td>
                <code>vector&lt;handle&gt;[2]</code>
            </td>
        </tr><tr>
            <td><code>out</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>

### Open {:#Open}

 Opens a new object relative to this directory object.

 `path` may contain multiple segments, separated by "/" characters,
 and should never be empty i.e. "" is an invalid path.

 `flags` may be any of the `OPEN_FLAG_*` and `OPEN_RIGHT_*` values, bitwise ORed together.
 The `OPEN_FLAG_DESCRIBE` flag may cause an `OnOpen` event to be transmitted
 on the `object` handle, indicating the type of object opened.

 If an unknown value is sent for either flags or mode, the connection should
 be closed.

 `OPEN_RIGHTS_*` flags provided in `flags` will restrict access rights on the `object` channel
 which will be connected to the opened entity.

 Rights are never increased. When you open a nested entity within a directory, you may only
 request the same rights as what the directory connection already has, or a subset of those.
 Exceeding those rights causes an access denied error to be transmitted in the
 `OnOpen` event if applicable, and the `object` connection closed.

 The caller must specify either one or more of the `OPEN_RIGHT_*` flags, or
 the `OPEN_FLAG_NODE_REFERENCE` flag.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>mode</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>path</code></td>
            <td>
                <code>string[4096]</code>
            </td>
        </tr><tr>
            <td><code>object</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Node'>Node</a>&gt;</code>
            </td>
        </tr></table>



### Unlink {:#Unlink}

 Detaches an object from this directory object.

 The underlying object may or may not be deleted after this method
 completes: although the link will be removed from the containing directory,
 objects with multiple references (such as files which are still open)
 will not actually be destroyed until all references are removed.

 If a directory is unlinked while it still has an open reference,
 it must become read-only, preventing new entries from being created
 until all references close and the directory is destroyed.

 `path` identifies the file which should be detached.
 If `path` contains multiple segments, separated by "/" characters,
 then the directory is traversed, one segment at a time, relative to the
 originally accessed Directory.

 Returns:
   `ZX_ERR_ACCESS_DENIED` if the connection (or the underlying filesystem) does not
     allow writable access.
   `ZX_ERR_INVALID_ARGS` if `path` contains ".." segments.
   `ZX_ERR_NOT_EMPTY` if `path` refers to a non-empty directory.
   `ZX_ERR_UNAVAILABLE` if `path` refers to a mount point, containing a remote channel.
   `ZX_ERR_UNAVAILABLE` if `path` is ".".

 Other errors may be returned for filesystem-specific reasons.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>path</code></td>
            <td>
                <code>string[4096]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### ReadDirents {:#ReadDirents}

 Reads a collection of variably sized dirents into a buffer.
 The number of dirents in a directory may be very large: akin to
 calling read multiple times on a file, directories have a seek
 offset which is updated on subsequent calls to ReadDirents.

 These dirents are of the form:
 struct dirent {
   // Describes the inode of the entry.
   uint64 ino;
   // Describes the length of the dirent name.
   uint8 size;
   // Describes the type of the entry. Aligned with the
   /// POSIX d_type values. Use `DIRENT_TYPE_*` constants.
   uint8 type;
   // Unterminated name of entry.
   char name[0];
 }

 This method does not require any rights, since one could always probe for
 directory contents by triggering name conflicts during file creation.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>max_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>dirents</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>

### Rewind {:#Rewind}

 Resets the directory seek offset.

 This method does not require any rights, similar to ReadDirents.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### GetToken {:#GetToken}

 Acquires a token to a Directory which can be used to identify
 access to it at a later point in time.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>token</code></td>
            <td>
                <code>handle&lt;handle&gt;?</code>
            </td>
        </tr></table>

### Rename {:#Rename}

 Renames an object named src to the name dst, in a directory represented by token.

 `src/dst` must be resolved object names. Including "/" in any position
 other than the end of the string will return `ZX_ERR_INVALID_ARGS`.
 Returning "/" at the end of either string implies that it must be a
 directory, or else `ZX_ERR_NOT_DIR` should be returned.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>src</code></td>
            <td>
                <code>string[4096]</code>
            </td>
        </tr><tr>
            <td><code>dst_parent_token</code></td>
            <td>
                <code>handle&lt;handle&gt;</code>
            </td>
        </tr><tr>
            <td><code>dst</code></td>
            <td>
                <code>string[4096]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Link {:#Link}

 Creates a link to an object named src by the name dst, within a directory represented by
 token.

 `src` must be a resolved object name. Including "/" in the string will
 return `ZX_ERR_INVALID_ARGS`.

 `dst` must be a resolved object name. Including "/" in the string will
 return `ZX_ERR_INVALID_ARGS`.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>src</code></td>
            <td>
                <code>string[4096]</code>
            </td>
        </tr><tr>
            <td><code>dst_parent_token</code></td>
            <td>
                <code>handle&lt;handle&gt;</code>
            </td>
        </tr><tr>
            <td><code>dst</code></td>
            <td>
                <code>string[4096]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Watch {:#Watch}

 Watches a directory, receiving events of added messages on the
 watcher request channel.

 The "watcher" handle will send messages of the form:
 struct {
   uint8 event;
   uint8 len;
   char name[];
 };
 Where names are NOT null-terminated.

 This API is unstable"; in the future, watcher will be a "DirectoryWatcher" client.

 Mask specifies a bitmask of events to observe.
 Options must be zero; it is reserved.

 This method does not require any rights, similar to ReadDirents.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>mask</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>options</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>watcher</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

## DirectoryAdmin {:#DirectoryAdmin}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#599)*

 DirectoryAdmin defines a directory which is capable of handling
 administrator tasks within the filesystem.

### Clone {:#Clone}

 Create another connection to the same remote object.

 `flags` may be any of:
 - `OPEN_RIGHT_*`
 - `OPEN_FLAG_APPEND`
 - `OPEN_FLAG_NO_REMOTE`
 - `OPEN_FLAG_DESCRIBE`
 - `CLONE_FLAG_SAME_RIGHTS`

 All other flags are ignored.

 The `OPEN_RIGHT_*` bits in `flags` request corresponding rights over the resulting
 cloned object.
 The cloned object must have rights less than or equal to the original object.
 Alternatively, pass `CLONE_FLAG_SAME_RIGHTS` to inherit the rights on the source connection.
 It is invalid to pass any of the `OPEN_RIGHT_*` flags together with `CLONE_FLAG_SAME_RIGHTS`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>object</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Node'>Node</a>&gt;</code>
            </td>
        </tr></table>



### Close {:#Close}

 Terminates connection with object.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Describe {:#Describe}

 Returns extra information about the type of the object.
 If the `Describe` operation fails, the connection is closed.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#NodeInfo'>NodeInfo</a></code>
            </td>
        </tr></table>

### OnOpen {:#OnOpen}

 An event produced eagerly by a FIDL server if requested by `OPEN_FLAG_DESCRIBE`.

 Indicates the success or failure of the open operation, and optionally describes the
 object. If the status is `ZX_OK`, `info` contains descriptive information about the object
 (the same as would be returned by `Describe`).



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#NodeInfo'>NodeInfo</a>?</code>
            </td>
        </tr></table>

### Sync {:#Sync}

 Synchronizes updates to the node to the underlying media, if it exists.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### GetAttr {:#GetAttr}

 Acquires information about the node.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='#NodeAttributes'>NodeAttributes</a></code>
            </td>
        </tr></table>

### SetAttr {:#SetAttr}

 Updates information about the node.
 `flags` may be any of `NODE_ATTRIBUTE_FLAG_*`.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='#NodeAttributes'>NodeAttributes</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Ioctl {:#Ioctl}

 Deprecated. Only for use with compatibility with devhost.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>opcode</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>max_out</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>handles</code></td>
            <td>
                <code>vector&lt;handle&gt;[2]</code>
            </td>
        </tr><tr>
            <td><code>in</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>handles</code></td>
            <td>
                <code>vector&lt;handle&gt;[2]</code>
            </td>
        </tr><tr>
            <td><code>out</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>

### Open {:#Open}

 Opens a new object relative to this directory object.

 `path` may contain multiple segments, separated by "/" characters,
 and should never be empty i.e. "" is an invalid path.

 `flags` may be any of the `OPEN_FLAG_*` and `OPEN_RIGHT_*` values, bitwise ORed together.
 The `OPEN_FLAG_DESCRIBE` flag may cause an `OnOpen` event to be transmitted
 on the `object` handle, indicating the type of object opened.

 If an unknown value is sent for either flags or mode, the connection should
 be closed.

 `OPEN_RIGHTS_*` flags provided in `flags` will restrict access rights on the `object` channel
 which will be connected to the opened entity.

 Rights are never increased. When you open a nested entity within a directory, you may only
 request the same rights as what the directory connection already has, or a subset of those.
 Exceeding those rights causes an access denied error to be transmitted in the
 `OnOpen` event if applicable, and the `object` connection closed.

 The caller must specify either one or more of the `OPEN_RIGHT_*` flags, or
 the `OPEN_FLAG_NODE_REFERENCE` flag.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>mode</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>path</code></td>
            <td>
                <code>string[4096]</code>
            </td>
        </tr><tr>
            <td><code>object</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Node'>Node</a>&gt;</code>
            </td>
        </tr></table>



### Unlink {:#Unlink}

 Detaches an object from this directory object.

 The underlying object may or may not be deleted after this method
 completes: although the link will be removed from the containing directory,
 objects with multiple references (such as files which are still open)
 will not actually be destroyed until all references are removed.

 If a directory is unlinked while it still has an open reference,
 it must become read-only, preventing new entries from being created
 until all references close and the directory is destroyed.

 `path` identifies the file which should be detached.
 If `path` contains multiple segments, separated by "/" characters,
 then the directory is traversed, one segment at a time, relative to the
 originally accessed Directory.

 Returns:
   `ZX_ERR_ACCESS_DENIED` if the connection (or the underlying filesystem) does not
     allow writable access.
   `ZX_ERR_INVALID_ARGS` if `path` contains ".." segments.
   `ZX_ERR_NOT_EMPTY` if `path` refers to a non-empty directory.
   `ZX_ERR_UNAVAILABLE` if `path` refers to a mount point, containing a remote channel.
   `ZX_ERR_UNAVAILABLE` if `path` is ".".

 Other errors may be returned for filesystem-specific reasons.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>path</code></td>
            <td>
                <code>string[4096]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### ReadDirents {:#ReadDirents}

 Reads a collection of variably sized dirents into a buffer.
 The number of dirents in a directory may be very large: akin to
 calling read multiple times on a file, directories have a seek
 offset which is updated on subsequent calls to ReadDirents.

 These dirents are of the form:
 struct dirent {
   // Describes the inode of the entry.
   uint64 ino;
   // Describes the length of the dirent name.
   uint8 size;
   // Describes the type of the entry. Aligned with the
   /// POSIX d_type values. Use `DIRENT_TYPE_*` constants.
   uint8 type;
   // Unterminated name of entry.
   char name[0];
 }

 This method does not require any rights, since one could always probe for
 directory contents by triggering name conflicts during file creation.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>max_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>dirents</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>

### Rewind {:#Rewind}

 Resets the directory seek offset.

 This method does not require any rights, similar to ReadDirents.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### GetToken {:#GetToken}

 Acquires a token to a Directory which can be used to identify
 access to it at a later point in time.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>token</code></td>
            <td>
                <code>handle&lt;handle&gt;?</code>
            </td>
        </tr></table>

### Rename {:#Rename}

 Renames an object named src to the name dst, in a directory represented by token.

 `src/dst` must be resolved object names. Including "/" in any position
 other than the end of the string will return `ZX_ERR_INVALID_ARGS`.
 Returning "/" at the end of either string implies that it must be a
 directory, or else `ZX_ERR_NOT_DIR` should be returned.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>src</code></td>
            <td>
                <code>string[4096]</code>
            </td>
        </tr><tr>
            <td><code>dst_parent_token</code></td>
            <td>
                <code>handle&lt;handle&gt;</code>
            </td>
        </tr><tr>
            <td><code>dst</code></td>
            <td>
                <code>string[4096]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Link {:#Link}

 Creates a link to an object named src by the name dst, within a directory represented by
 token.

 `src` must be a resolved object name. Including "/" in the string will
 return `ZX_ERR_INVALID_ARGS`.

 `dst` must be a resolved object name. Including "/" in the string will
 return `ZX_ERR_INVALID_ARGS`.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>src</code></td>
            <td>
                <code>string[4096]</code>
            </td>
        </tr><tr>
            <td><code>dst_parent_token</code></td>
            <td>
                <code>handle&lt;handle&gt;</code>
            </td>
        </tr><tr>
            <td><code>dst</code></td>
            <td>
                <code>string[4096]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Watch {:#Watch}

 Watches a directory, receiving events of added messages on the
 watcher request channel.

 The "watcher" handle will send messages of the form:
 struct {
   uint8 event;
   uint8 len;
   char name[];
 };
 Where names are NOT null-terminated.

 This API is unstable"; in the future, watcher will be a "DirectoryWatcher" client.

 Mask specifies a bitmask of events to observe.
 Options must be zero; it is reserved.

 This method does not require any rights, similar to ReadDirents.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>mask</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>options</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>watcher</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Mount {:#Mount}

 Mount a channel representing a remote filesystem onto this directory.
 All future requests to this node will be forwarded to the remote filesystem.
 To re-open a node without forwarding to the remote target, the node
 should be opened with `OPEN_FLAG_NO_REMOTE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>remote</code></td>
            <td>
                <code><a class='link' href='#Directory'>Directory</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### MountAndCreate {:#MountAndCreate}

 Atomically create a directory with a provided path, and mount the
 remote handle to the newly created directory.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>remote</code></td>
            <td>
                <code><a class='link' href='#Directory'>Directory</a></code>
            </td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[255]</code>
            </td>
        </tr><tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Unmount {:#Unmount}

 Unmount this filesystem. After this function returns successfully,
 all connections to the filesystem will be terminated.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### UnmountNode {:#UnmountNode}

 Detach a node which was previously attached to this directory
 with Mount.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>remote</code></td>
            <td>
                <code><a class='link' href='#Directory'>Directory</a>?</code>
            </td>
        </tr></table>

### QueryFilesystem {:#QueryFilesystem}

 Query the filesystem for filesystem-specific information.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#FilesystemInfo'>FilesystemInfo</a>?</code>
            </td>
        </tr></table>

### GetDevicePath {:#GetDevicePath}

 Acquire the path to the device backing this filesystem, if there is one.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>path</code></td>
            <td>
                <code>string[4096]?</code>
            </td>
        </tr></table>

## Node {:#Node}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#161)*

 Node defines the minimal interface for entities which can be accessed in a filesystem.

### Clone {:#Clone}

 Create another connection to the same remote object.

 `flags` may be any of:
 - `OPEN_RIGHT_*`
 - `OPEN_FLAG_APPEND`
 - `OPEN_FLAG_NO_REMOTE`
 - `OPEN_FLAG_DESCRIBE`
 - `CLONE_FLAG_SAME_RIGHTS`

 All other flags are ignored.

 The `OPEN_RIGHT_*` bits in `flags` request corresponding rights over the resulting
 cloned object.
 The cloned object must have rights less than or equal to the original object.
 Alternatively, pass `CLONE_FLAG_SAME_RIGHTS` to inherit the rights on the source connection.
 It is invalid to pass any of the `OPEN_RIGHT_*` flags together with `CLONE_FLAG_SAME_RIGHTS`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>object</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Node'>Node</a>&gt;</code>
            </td>
        </tr></table>



### Close {:#Close}

 Terminates connection with object.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Describe {:#Describe}

 Returns extra information about the type of the object.
 If the `Describe` operation fails, the connection is closed.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#NodeInfo'>NodeInfo</a></code>
            </td>
        </tr></table>

### OnOpen {:#OnOpen}

 An event produced eagerly by a FIDL server if requested by `OPEN_FLAG_DESCRIBE`.

 Indicates the success or failure of the open operation, and optionally describes the
 object. If the status is `ZX_OK`, `info` contains descriptive information about the object
 (the same as would be returned by `Describe`).



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#NodeInfo'>NodeInfo</a>?</code>
            </td>
        </tr></table>

### Sync {:#Sync}

 Synchronizes updates to the node to the underlying media, if it exists.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### GetAttr {:#GetAttr}

 Acquires information about the node.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='#NodeAttributes'>NodeAttributes</a></code>
            </td>
        </tr></table>

### SetAttr {:#SetAttr}

 Updates information about the node.
 `flags` may be any of `NODE_ATTRIBUTE_FLAG_*`.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='#NodeAttributes'>NodeAttributes</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Ioctl {:#Ioctl}

 Deprecated. Only for use with compatibility with devhost.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>opcode</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>max_out</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>handles</code></td>
            <td>
                <code>vector&lt;handle&gt;[2]</code>
            </td>
        </tr><tr>
            <td><code>in</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>handles</code></td>
            <td>
                <code>vector&lt;handle&gt;[2]</code>
            </td>
        </tr><tr>
            <td><code>out</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>

## File {:#File}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#301)*

 File defines the interface of a node which contains a flat layout of data.

### Clone {:#Clone}

 Create another connection to the same remote object.

 `flags` may be any of:
 - `OPEN_RIGHT_*`
 - `OPEN_FLAG_APPEND`
 - `OPEN_FLAG_NO_REMOTE`
 - `OPEN_FLAG_DESCRIBE`
 - `CLONE_FLAG_SAME_RIGHTS`

 All other flags are ignored.

 The `OPEN_RIGHT_*` bits in `flags` request corresponding rights over the resulting
 cloned object.
 The cloned object must have rights less than or equal to the original object.
 Alternatively, pass `CLONE_FLAG_SAME_RIGHTS` to inherit the rights on the source connection.
 It is invalid to pass any of the `OPEN_RIGHT_*` flags together with `CLONE_FLAG_SAME_RIGHTS`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>object</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Node'>Node</a>&gt;</code>
            </td>
        </tr></table>



### Close {:#Close}

 Terminates connection with object.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Describe {:#Describe}

 Returns extra information about the type of the object.
 If the `Describe` operation fails, the connection is closed.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#NodeInfo'>NodeInfo</a></code>
            </td>
        </tr></table>

### OnOpen {:#OnOpen}

 An event produced eagerly by a FIDL server if requested by `OPEN_FLAG_DESCRIBE`.

 Indicates the success or failure of the open operation, and optionally describes the
 object. If the status is `ZX_OK`, `info` contains descriptive information about the object
 (the same as would be returned by `Describe`).



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#NodeInfo'>NodeInfo</a>?</code>
            </td>
        </tr></table>

### Sync {:#Sync}

 Synchronizes updates to the node to the underlying media, if it exists.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### GetAttr {:#GetAttr}

 Acquires information about the node.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='#NodeAttributes'>NodeAttributes</a></code>
            </td>
        </tr></table>

### SetAttr {:#SetAttr}

 Updates information about the node.
 `flags` may be any of `NODE_ATTRIBUTE_FLAG_*`.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='#NodeAttributes'>NodeAttributes</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Ioctl {:#Ioctl}

 Deprecated. Only for use with compatibility with devhost.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>opcode</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>max_out</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>handles</code></td>
            <td>
                <code>vector&lt;handle&gt;[2]</code>
            </td>
        </tr><tr>
            <td><code>in</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>handles</code></td>
            <td>
                <code>vector&lt;handle&gt;[2]</code>
            </td>
        </tr><tr>
            <td><code>out</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>

### Read {:#Read}

 Reads 'count' bytes at the seek offset.
 The seek offset is moved forward by the number of bytes read.

 This method requires following rights: `OPEN_RIGHT_READABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>count</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>

### ReadAt {:#ReadAt}

 Reads 'count' bytes at the provided offset.
 Does not affect the seek offset.

 This method requires following rights: `OPEN_RIGHT_READABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>count</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>offset</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>

### Write {:#Write}

 Writes data at the seek offset.
 The seek offset is moved forward by the number of bytes written.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>actual</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### WriteAt {:#WriteAt}

 Writes data to the provided offset.
 Does not affect the seek offset.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr><tr>
            <td><code>offset</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>actual</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### Seek {:#Seek}

 Moves the offset at which the next invocation of `Read()` or `Write()` will
 occur.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>offset</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>start</code></td>
            <td>
                <code><a class='link' href='#SeekOrigin'>SeekOrigin</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>offset</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### Truncate {:#Truncate}

 Shrinks the file size to 'length' bytes.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>length</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### GetFlags {:#GetFlags}

 Acquires the Directory::Open rights and flags used to access this file.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### SetFlags {:#SetFlags}

 Changes the Directory::Open flags used to access the file.
 Supported flags which can be turned on / off:
 - `OPEN_FLAG_APPEND`

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### GetBuffer {:#GetBuffer}

 Acquires a buffer representing this file, if there is one, with the
 requested access rights.

 `flags` may be any of `VMO_FLAG_*`.

 This method requires following rights:
 - `OPEN_RIGHT_WRITABLE` if `flags` includes `VMO_FLAG_WRITE`.
 - `OPEN_RIGHT_READABLE` if `flags` includes `VMO_FLAG_READ` or `VMO_FLAG_EXEC`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a>?</code>
            </td>
        </tr></table>

## DirectoryWatcher {:#DirectoryWatcher}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#420)*

 DirectoryWatcher transmits messages from a filesystem server
 about events happening in the filesystem. Clients can register
 new watchers using the Directory "Watch" method, where they can
 filter which events they want to receive notifications for.

### OnEvent {:#OnEvent}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>events</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>



## Directory {:#Directory}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#427)*

 Directory defines a node which is capable of containing other Objects.

### Clone {:#Clone}

 Create another connection to the same remote object.

 `flags` may be any of:
 - `OPEN_RIGHT_*`
 - `OPEN_FLAG_APPEND`
 - `OPEN_FLAG_NO_REMOTE`
 - `OPEN_FLAG_DESCRIBE`
 - `CLONE_FLAG_SAME_RIGHTS`

 All other flags are ignored.

 The `OPEN_RIGHT_*` bits in `flags` request corresponding rights over the resulting
 cloned object.
 The cloned object must have rights less than or equal to the original object.
 Alternatively, pass `CLONE_FLAG_SAME_RIGHTS` to inherit the rights on the source connection.
 It is invalid to pass any of the `OPEN_RIGHT_*` flags together with `CLONE_FLAG_SAME_RIGHTS`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>object</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Node'>Node</a>&gt;</code>
            </td>
        </tr></table>



### Close {:#Close}

 Terminates connection with object.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Describe {:#Describe}

 Returns extra information about the type of the object.
 If the `Describe` operation fails, the connection is closed.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#NodeInfo'>NodeInfo</a></code>
            </td>
        </tr></table>

### OnOpen {:#OnOpen}

 An event produced eagerly by a FIDL server if requested by `OPEN_FLAG_DESCRIBE`.

 Indicates the success or failure of the open operation, and optionally describes the
 object. If the status is `ZX_OK`, `info` contains descriptive information about the object
 (the same as would be returned by `Describe`).



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#NodeInfo'>NodeInfo</a>?</code>
            </td>
        </tr></table>

### Sync {:#Sync}

 Synchronizes updates to the node to the underlying media, if it exists.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### GetAttr {:#GetAttr}

 Acquires information about the node.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='#NodeAttributes'>NodeAttributes</a></code>
            </td>
        </tr></table>

### SetAttr {:#SetAttr}

 Updates information about the node.
 `flags` may be any of `NODE_ATTRIBUTE_FLAG_*`.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='#NodeAttributes'>NodeAttributes</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Ioctl {:#Ioctl}

 Deprecated. Only for use with compatibility with devhost.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>opcode</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>max_out</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>handles</code></td>
            <td>
                <code>vector&lt;handle&gt;[2]</code>
            </td>
        </tr><tr>
            <td><code>in</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>handles</code></td>
            <td>
                <code>vector&lt;handle&gt;[2]</code>
            </td>
        </tr><tr>
            <td><code>out</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>

### Open {:#Open}

 Opens a new object relative to this directory object.

 `path` may contain multiple segments, separated by "/" characters,
 and should never be empty i.e. "" is an invalid path.

 `flags` may be any of the `OPEN_FLAG_*` and `OPEN_RIGHT_*` values, bitwise ORed together.
 The `OPEN_FLAG_DESCRIBE` flag may cause an `OnOpen` event to be transmitted
 on the `object` handle, indicating the type of object opened.

 If an unknown value is sent for either flags or mode, the connection should
 be closed.

 `OPEN_RIGHTS_*` flags provided in `flags` will restrict access rights on the `object` channel
 which will be connected to the opened entity.

 Rights are never increased. When you open a nested entity within a directory, you may only
 request the same rights as what the directory connection already has, or a subset of those.
 Exceeding those rights causes an access denied error to be transmitted in the
 `OnOpen` event if applicable, and the `object` connection closed.

 The caller must specify either one or more of the `OPEN_RIGHT_*` flags, or
 the `OPEN_FLAG_NODE_REFERENCE` flag.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>mode</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>path</code></td>
            <td>
                <code>string[4096]</code>
            </td>
        </tr><tr>
            <td><code>object</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Node'>Node</a>&gt;</code>
            </td>
        </tr></table>



### Unlink {:#Unlink}

 Detaches an object from this directory object.

 The underlying object may or may not be deleted after this method
 completes: although the link will be removed from the containing directory,
 objects with multiple references (such as files which are still open)
 will not actually be destroyed until all references are removed.

 If a directory is unlinked while it still has an open reference,
 it must become read-only, preventing new entries from being created
 until all references close and the directory is destroyed.

 `path` identifies the file which should be detached.
 If `path` contains multiple segments, separated by "/" characters,
 then the directory is traversed, one segment at a time, relative to the
 originally accessed Directory.

 Returns:
   `ZX_ERR_ACCESS_DENIED` if the connection (or the underlying filesystem) does not
     allow writable access.
   `ZX_ERR_INVALID_ARGS` if `path` contains ".." segments.
   `ZX_ERR_NOT_EMPTY` if `path` refers to a non-empty directory.
   `ZX_ERR_UNAVAILABLE` if `path` refers to a mount point, containing a remote channel.
   `ZX_ERR_UNAVAILABLE` if `path` is ".".

 Other errors may be returned for filesystem-specific reasons.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>path</code></td>
            <td>
                <code>string[4096]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### ReadDirents {:#ReadDirents}

 Reads a collection of variably sized dirents into a buffer.
 The number of dirents in a directory may be very large: akin to
 calling read multiple times on a file, directories have a seek
 offset which is updated on subsequent calls to ReadDirents.

 These dirents are of the form:
 struct dirent {
   // Describes the inode of the entry.
   uint64 ino;
   // Describes the length of the dirent name.
   uint8 size;
   // Describes the type of the entry. Aligned with the
   /// POSIX d_type values. Use `DIRENT_TYPE_*` constants.
   uint8 type;
   // Unterminated name of entry.
   char name[0];
 }

 This method does not require any rights, since one could always probe for
 directory contents by triggering name conflicts during file creation.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>max_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>dirents</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>

### Rewind {:#Rewind}

 Resets the directory seek offset.

 This method does not require any rights, similar to ReadDirents.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### GetToken {:#GetToken}

 Acquires a token to a Directory which can be used to identify
 access to it at a later point in time.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>token</code></td>
            <td>
                <code>handle&lt;handle&gt;?</code>
            </td>
        </tr></table>

### Rename {:#Rename}

 Renames an object named src to the name dst, in a directory represented by token.

 `src/dst` must be resolved object names. Including "/" in any position
 other than the end of the string will return `ZX_ERR_INVALID_ARGS`.
 Returning "/" at the end of either string implies that it must be a
 directory, or else `ZX_ERR_NOT_DIR` should be returned.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>src</code></td>
            <td>
                <code>string[4096]</code>
            </td>
        </tr><tr>
            <td><code>dst_parent_token</code></td>
            <td>
                <code>handle&lt;handle&gt;</code>
            </td>
        </tr><tr>
            <td><code>dst</code></td>
            <td>
                <code>string[4096]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Link {:#Link}

 Creates a link to an object named src by the name dst, within a directory represented by
 token.

 `src` must be a resolved object name. Including "/" in the string will
 return `ZX_ERR_INVALID_ARGS`.

 `dst` must be a resolved object name. Including "/" in the string will
 return `ZX_ERR_INVALID_ARGS`.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>src</code></td>
            <td>
                <code>string[4096]</code>
            </td>
        </tr><tr>
            <td><code>dst_parent_token</code></td>
            <td>
                <code>handle&lt;handle&gt;</code>
            </td>
        </tr><tr>
            <td><code>dst</code></td>
            <td>
                <code>string[4096]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Watch {:#Watch}

 Watches a directory, receiving events of added messages on the
 watcher request channel.

 The "watcher" handle will send messages of the form:
 struct {
   uint8 event;
   uint8 len;
   char name[];
 };
 Where names are NOT null-terminated.

 This API is unstable"; in the future, watcher will be a "DirectoryWatcher" client.

 Mask specifies a bitmask of events to observe.
 Options must be zero; it is reserved.

 This method does not require any rights, similar to ReadDirents.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>mask</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>options</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>watcher</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

## DirectoryAdmin {:#DirectoryAdmin}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#599)*

 DirectoryAdmin defines a directory which is capable of handling
 administrator tasks within the filesystem.

### Clone {:#Clone}

 Create another connection to the same remote object.

 `flags` may be any of:
 - `OPEN_RIGHT_*`
 - `OPEN_FLAG_APPEND`
 - `OPEN_FLAG_NO_REMOTE`
 - `OPEN_FLAG_DESCRIBE`
 - `CLONE_FLAG_SAME_RIGHTS`

 All other flags are ignored.

 The `OPEN_RIGHT_*` bits in `flags` request corresponding rights over the resulting
 cloned object.
 The cloned object must have rights less than or equal to the original object.
 Alternatively, pass `CLONE_FLAG_SAME_RIGHTS` to inherit the rights on the source connection.
 It is invalid to pass any of the `OPEN_RIGHT_*` flags together with `CLONE_FLAG_SAME_RIGHTS`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>object</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Node'>Node</a>&gt;</code>
            </td>
        </tr></table>



### Close {:#Close}

 Terminates connection with object.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Describe {:#Describe}

 Returns extra information about the type of the object.
 If the `Describe` operation fails, the connection is closed.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#NodeInfo'>NodeInfo</a></code>
            </td>
        </tr></table>

### OnOpen {:#OnOpen}

 An event produced eagerly by a FIDL server if requested by `OPEN_FLAG_DESCRIBE`.

 Indicates the success or failure of the open operation, and optionally describes the
 object. If the status is `ZX_OK`, `info` contains descriptive information about the object
 (the same as would be returned by `Describe`).



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#NodeInfo'>NodeInfo</a>?</code>
            </td>
        </tr></table>

### Sync {:#Sync}

 Synchronizes updates to the node to the underlying media, if it exists.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### GetAttr {:#GetAttr}

 Acquires information about the node.

 This method does not require any rights.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='#NodeAttributes'>NodeAttributes</a></code>
            </td>
        </tr></table>

### SetAttr {:#SetAttr}

 Updates information about the node.
 `flags` may be any of `NODE_ATTRIBUTE_FLAG_*`.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='#NodeAttributes'>NodeAttributes</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Ioctl {:#Ioctl}

 Deprecated. Only for use with compatibility with devhost.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>opcode</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>max_out</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>handles</code></td>
            <td>
                <code>vector&lt;handle&gt;[2]</code>
            </td>
        </tr><tr>
            <td><code>in</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>handles</code></td>
            <td>
                <code>vector&lt;handle&gt;[2]</code>
            </td>
        </tr><tr>
            <td><code>out</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>

### Open {:#Open}

 Opens a new object relative to this directory object.

 `path` may contain multiple segments, separated by "/" characters,
 and should never be empty i.e. "" is an invalid path.

 `flags` may be any of the `OPEN_FLAG_*` and `OPEN_RIGHT_*` values, bitwise ORed together.
 The `OPEN_FLAG_DESCRIBE` flag may cause an `OnOpen` event to be transmitted
 on the `object` handle, indicating the type of object opened.

 If an unknown value is sent for either flags or mode, the connection should
 be closed.

 `OPEN_RIGHTS_*` flags provided in `flags` will restrict access rights on the `object` channel
 which will be connected to the opened entity.

 Rights are never increased. When you open a nested entity within a directory, you may only
 request the same rights as what the directory connection already has, or a subset of those.
 Exceeding those rights causes an access denied error to be transmitted in the
 `OnOpen` event if applicable, and the `object` connection closed.

 The caller must specify either one or more of the `OPEN_RIGHT_*` flags, or
 the `OPEN_FLAG_NODE_REFERENCE` flag.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>mode</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>path</code></td>
            <td>
                <code>string[4096]</code>
            </td>
        </tr><tr>
            <td><code>object</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Node'>Node</a>&gt;</code>
            </td>
        </tr></table>



### Unlink {:#Unlink}

 Detaches an object from this directory object.

 The underlying object may or may not be deleted after this method
 completes: although the link will be removed from the containing directory,
 objects with multiple references (such as files which are still open)
 will not actually be destroyed until all references are removed.

 If a directory is unlinked while it still has an open reference,
 it must become read-only, preventing new entries from being created
 until all references close and the directory is destroyed.

 `path` identifies the file which should be detached.
 If `path` contains multiple segments, separated by "/" characters,
 then the directory is traversed, one segment at a time, relative to the
 originally accessed Directory.

 Returns:
   `ZX_ERR_ACCESS_DENIED` if the connection (or the underlying filesystem) does not
     allow writable access.
   `ZX_ERR_INVALID_ARGS` if `path` contains ".." segments.
   `ZX_ERR_NOT_EMPTY` if `path` refers to a non-empty directory.
   `ZX_ERR_UNAVAILABLE` if `path` refers to a mount point, containing a remote channel.
   `ZX_ERR_UNAVAILABLE` if `path` is ".".

 Other errors may be returned for filesystem-specific reasons.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>path</code></td>
            <td>
                <code>string[4096]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### ReadDirents {:#ReadDirents}

 Reads a collection of variably sized dirents into a buffer.
 The number of dirents in a directory may be very large: akin to
 calling read multiple times on a file, directories have a seek
 offset which is updated on subsequent calls to ReadDirents.

 These dirents are of the form:
 struct dirent {
   // Describes the inode of the entry.
   uint64 ino;
   // Describes the length of the dirent name.
   uint8 size;
   // Describes the type of the entry. Aligned with the
   /// POSIX d_type values. Use `DIRENT_TYPE_*` constants.
   uint8 type;
   // Unterminated name of entry.
   char name[0];
 }

 This method does not require any rights, since one could always probe for
 directory contents by triggering name conflicts during file creation.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>max_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>dirents</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>

### Rewind {:#Rewind}

 Resets the directory seek offset.

 This method does not require any rights, similar to ReadDirents.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### GetToken {:#GetToken}

 Acquires a token to a Directory which can be used to identify
 access to it at a later point in time.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>token</code></td>
            <td>
                <code>handle&lt;handle&gt;?</code>
            </td>
        </tr></table>

### Rename {:#Rename}

 Renames an object named src to the name dst, in a directory represented by token.

 `src/dst` must be resolved object names. Including "/" in any position
 other than the end of the string will return `ZX_ERR_INVALID_ARGS`.
 Returning "/" at the end of either string implies that it must be a
 directory, or else `ZX_ERR_NOT_DIR` should be returned.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>src</code></td>
            <td>
                <code>string[4096]</code>
            </td>
        </tr><tr>
            <td><code>dst_parent_token</code></td>
            <td>
                <code>handle&lt;handle&gt;</code>
            </td>
        </tr><tr>
            <td><code>dst</code></td>
            <td>
                <code>string[4096]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Link {:#Link}

 Creates a link to an object named src by the name dst, within a directory represented by
 token.

 `src` must be a resolved object name. Including "/" in the string will
 return `ZX_ERR_INVALID_ARGS`.

 `dst` must be a resolved object name. Including "/" in the string will
 return `ZX_ERR_INVALID_ARGS`.

 This method requires following rights: `OPEN_RIGHT_WRITABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>src</code></td>
            <td>
                <code>string[4096]</code>
            </td>
        </tr><tr>
            <td><code>dst_parent_token</code></td>
            <td>
                <code>handle&lt;handle&gt;</code>
            </td>
        </tr><tr>
            <td><code>dst</code></td>
            <td>
                <code>string[4096]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Watch {:#Watch}

 Watches a directory, receiving events of added messages on the
 watcher request channel.

 The "watcher" handle will send messages of the form:
 struct {
   uint8 event;
   uint8 len;
   char name[];
 };
 Where names are NOT null-terminated.

 This API is unstable"; in the future, watcher will be a "DirectoryWatcher" client.

 Mask specifies a bitmask of events to observe.
 Options must be zero; it is reserved.

 This method does not require any rights, similar to ReadDirents.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>mask</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>options</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>watcher</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Mount {:#Mount}

 Mount a channel representing a remote filesystem onto this directory.
 All future requests to this node will be forwarded to the remote filesystem.
 To re-open a node without forwarding to the remote target, the node
 should be opened with `OPEN_FLAG_NO_REMOTE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>remote</code></td>
            <td>
                <code><a class='link' href='#Directory'>Directory</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### MountAndCreate {:#MountAndCreate}

 Atomically create a directory with a provided path, and mount the
 remote handle to the newly created directory.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>remote</code></td>
            <td>
                <code><a class='link' href='#Directory'>Directory</a></code>
            </td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[255]</code>
            </td>
        </tr><tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Unmount {:#Unmount}

 Unmount this filesystem. After this function returns successfully,
 all connections to the filesystem will be terminated.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### UnmountNode {:#UnmountNode}

 Detach a node which was previously attached to this directory
 with Mount.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>remote</code></td>
            <td>
                <code><a class='link' href='#Directory'>Directory</a>?</code>
            </td>
        </tr></table>

### QueryFilesystem {:#QueryFilesystem}

 Query the filesystem for filesystem-specific information.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#FilesystemInfo'>FilesystemInfo</a>?</code>
            </td>
        </tr></table>

### GetDevicePath {:#GetDevicePath}

 Acquire the path to the device backing this filesystem, if there is one.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>path</code></td>
            <td>
                <code>string[4096]?</code>
            </td>
        </tr></table>



## **STRUCTS**

### Service {:#Service}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#27)*



 The default protocol, interface information must be acquired some
 other way.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### FileObject {:#FileObject}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#36)*



 The object may be cast to interface 'File'.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>event</code></td>
            <td>
                <code>handle&lt;event&gt;?</code>
            </td>
            <td> An optional event which transmits information about an object's readability
 or writability. This event relays information about the underlying object, not
 the capability granted to client: this event may be signalled "readable" on a
 connection that does not have the capability to read.

 The "`FILE_SIGNAL_`" values may be observed on this event.
</td>
            <td>No default</td>
        </tr>
</table>

### DirectoryObject {:#DirectoryObject}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#47)*



 The object may be cast to interface 'Directory'.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Pipe {:#Pipe}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#51)*



 The object is accompanied by a pipe.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>socket</code></td>
            <td>
                <code>handle&lt;socket&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Socket {:#Socket}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#56)*



 The object is accompanied by a socket.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>socket</code></td>
            <td>
                <code>handle&lt;socket&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Vmofile {:#Vmofile}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#64)*



 The object is a file which is represented as an immutable VMO.
 Although a VMO is returned as a part of this structure, this underlying object
 may represent multiple Vmofiles. To identify the logical portion of the VMO
 that represents the single file, an offset and length parameter are also supplied.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
            <td> The VMO which backs this file.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>offset</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The index into `vmo` which represents the first byte of the file.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>length</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The number of bytes, starting at `offset`, which may be used to represent this file.
</td>
            <td>No default</td>
        </tr>
</table>

### Device {:#Device}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#85)*



 The object may be cast to interface 'Device'.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>event</code></td>
            <td>
                <code>handle&lt;eventpair&gt;?</code>
            </td>
            <td> An optional event which transmits information about a device's state.

 The "`DEVICE_SIGNAL_`" values may be observed on this event.
</td>
            <td>No default</td>
        </tr>
</table>

### Tty {:#Tty}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#93)*



 The object may be cast to interface 'Tty'


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>event</code></td>
            <td>
                <code>handle&lt;eventpair&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### NodeAttributes {:#NodeAttributes}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#236)*



 NodeAttributes defines generic information about a filesystem node.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>mode</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Protection bits and node type information describe in 'mode'.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> A filesystem-unique ID.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>content_size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Node size, in bytes.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>storage_size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Space needed to store node (possibly larger than size), in bytes.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>link_count</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Hard link count.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>creation_time</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Time of creation (may be updated manually after creation) in ns since Unix epoch, UTC.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>modification_time</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Time of last modification in ns since Unix epoch, UTC.
</td>
            <td>No default</td>
        </tr>
</table>

### WatchedEvent {:#WatchedEvent}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#408)*



 WatchedEvent describes events returned from a DirectoryWatcher.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>event</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>len</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>vector&lt;uint8&gt;[255]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FilesystemInfo {:#FilesystemInfo}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#568)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>total_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The number of data bytes which may be stored in a filesystem.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>used_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The number of data bytes which are in use by the filesystem.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>total_nodes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The number of nodes which may be stored in the filesystem.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>used_nodes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The number of nodes used by the filesystem.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>free_shared_pool_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The amount of space which may be allocated from the underlying
 volume manager. If unsupported, this will be zero.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>fs_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> A unique identifier for this filesystem instance. Will not be preserved
 across reboots.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>block_size</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The size of a single filesystem block.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_filename_size</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The maximum length of a filesystem name.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>fs_type</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> A unique identifier for the type of the underlying filesystem.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>padding</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>int8[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Service {:#Service}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#27)*



 The default protocol, interface information must be acquired some
 other way.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### FileObject {:#FileObject}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#36)*



 The object may be cast to interface 'File'.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>event</code></td>
            <td>
                <code>handle&lt;event&gt;?</code>
            </td>
            <td> An optional event which transmits information about an object's readability
 or writability. This event relays information about the underlying object, not
 the capability granted to client: this event may be signalled "readable" on a
 connection that does not have the capability to read.

 The "`FILE_SIGNAL_`" values may be observed on this event.
</td>
            <td>No default</td>
        </tr>
</table>

### DirectoryObject {:#DirectoryObject}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#47)*



 The object may be cast to interface 'Directory'.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Pipe {:#Pipe}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#51)*



 The object is accompanied by a pipe.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>socket</code></td>
            <td>
                <code>handle&lt;socket&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Socket {:#Socket}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#56)*



 The object is accompanied by a socket.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>socket</code></td>
            <td>
                <code>handle&lt;socket&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Vmofile {:#Vmofile}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#64)*



 The object is a file which is represented as an immutable VMO.
 Although a VMO is returned as a part of this structure, this underlying object
 may represent multiple Vmofiles. To identify the logical portion of the VMO
 that represents the single file, an offset and length parameter are also supplied.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
            <td> The VMO which backs this file.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>offset</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The index into `vmo` which represents the first byte of the file.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>length</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The number of bytes, starting at `offset`, which may be used to represent this file.
</td>
            <td>No default</td>
        </tr>
</table>

### Device {:#Device}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#85)*



 The object may be cast to interface 'Device'.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>event</code></td>
            <td>
                <code>handle&lt;eventpair&gt;?</code>
            </td>
            <td> An optional event which transmits information about a device's state.

 The "`DEVICE_SIGNAL_`" values may be observed on this event.
</td>
            <td>No default</td>
        </tr>
</table>

### Tty {:#Tty}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#93)*



 The object may be cast to interface 'Tty'


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>event</code></td>
            <td>
                <code>handle&lt;eventpair&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### NodeAttributes {:#NodeAttributes}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#236)*



 NodeAttributes defines generic information about a filesystem node.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>mode</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Protection bits and node type information describe in 'mode'.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> A filesystem-unique ID.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>content_size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Node size, in bytes.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>storage_size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Space needed to store node (possibly larger than size), in bytes.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>link_count</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Hard link count.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>creation_time</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Time of creation (may be updated manually after creation) in ns since Unix epoch, UTC.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>modification_time</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Time of last modification in ns since Unix epoch, UTC.
</td>
            <td>No default</td>
        </tr>
</table>

### WatchedEvent {:#WatchedEvent}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#408)*



 WatchedEvent describes events returned from a DirectoryWatcher.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>event</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>len</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>vector&lt;uint8&gt;[255]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FilesystemInfo {:#FilesystemInfo}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#568)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>total_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The number of data bytes which may be stored in a filesystem.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>used_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The number of data bytes which are in use by the filesystem.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>total_nodes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The number of nodes which may be stored in the filesystem.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>used_nodes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The number of nodes used by the filesystem.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>free_shared_pool_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The amount of space which may be allocated from the underlying
 volume manager. If unsupported, this will be zero.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>fs_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> A unique identifier for this filesystem instance. Will not be preserved
 across reboots.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>block_size</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The size of a single filesystem block.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_filename_size</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The maximum length of a filesystem name.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>fs_type</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> A unique identifier for the type of the underlying filesystem.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>padding</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>int8[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### SeekOrigin {:#SeekOrigin}
Type: <code>uint32</code>

*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#271)*

 Update the Seek offset.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>START</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>CURRENT</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>END</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### SeekOrigin {:#SeekOrigin}
Type: <code>uint32</code>

*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#271)*

 Update the Seek offset.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>START</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>CURRENT</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>END</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>





## **UNIONS**

### NodeInfo {:#NodeInfo}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#14)*

 Describes how the connection to an should be handled, as well as
 how to interpret the optional handle.

 Refer to `Node::Describe()` and `Node::OnOpen()` for usage.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>service</code></td>
            <td>
                <code><a class='link' href='#Service'>Service</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>file</code></td>
            <td>
                <code><a class='link' href='#FileObject'>FileObject</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>directory</code></td>
            <td>
                <code><a class='link' href='#DirectoryObject'>DirectoryObject</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>pipe</code></td>
            <td>
                <code><a class='link' href='#Pipe'>Pipe</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>vmofile</code></td>
            <td>
                <code><a class='link' href='#Vmofile'>Vmofile</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>device</code></td>
            <td>
                <code><a class='link' href='#Device'>Device</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>tty</code></td>
            <td>
                <code><a class='link' href='#Tty'>Tty</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>socket</code></td>
            <td>
                <code><a class='link' href='#Socket'>Socket</a></code>
            </td>
            <td></td>
        </tr></table>

### NodeInfo {:#NodeInfo}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#14)*

 Describes how the connection to an should be handled, as well as
 how to interpret the optional handle.

 Refer to `Node::Describe()` and `Node::OnOpen()` for usage.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>service</code></td>
            <td>
                <code><a class='link' href='#Service'>Service</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>file</code></td>
            <td>
                <code><a class='link' href='#FileObject'>FileObject</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>directory</code></td>
            <td>
                <code><a class='link' href='#DirectoryObject'>DirectoryObject</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>pipe</code></td>
            <td>
                <code><a class='link' href='#Pipe'>Pipe</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>vmofile</code></td>
            <td>
                <code><a class='link' href='#Vmofile'>Vmofile</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>device</code></td>
            <td>
                <code><a class='link' href='#Device'>Device</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>tty</code></td>
            <td>
                <code><a class='link' href='#Tty'>Tty</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>socket</code></td>
            <td>
                <code><a class='link' href='#Socket'>Socket</a></code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#31">FILE_SIGNAL_READABLE</a></td>
            <td>
                    <code>16777216</code>
                </td>
                <td><code>uint32</code></td>
            <td> Indicates the file is ready for reading.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#33">FILE_SIGNAL_WRITABLE</a></td>
            <td>
                    <code>33554432</code>
                </td>
                <td><code>uint32</code></td>
            <td> Indicates the file is ready for writing.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#74">DEVICE_SIGNAL_READABLE</a></td>
            <td>
                    <code>16777216</code>
                </td>
                <td><code>uint32</code></td>
            <td> Indicates the device is ready for reading.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#76">DEVICE_SIGNAL_OOB</a></td>
            <td>
                    <code>33554432</code>
                </td>
                <td><code>uint32</code></td>
            <td> Indicates an out-of-band state transition has occurred.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#78">DEVICE_SIGNAL_WRITABLE</a></td>
            <td>
                    <code>67108864</code>
                </td>
                <td><code>uint32</code></td>
            <td> Indicates the device is ready for writing.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#80">DEVICE_SIGNAL_ERROR</a></td>
            <td>
                    <code>134217728</code>
                </td>
                <td><code>uint32</code></td>
            <td> Indicates the device has encountered an error state.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#82">DEVICE_SIGNAL_HANGUP</a></td>
            <td>
                    <code>268435456</code>
                </td>
                <td><code>uint32</code></td>
            <td> Indicates the device has hung up on the current connection.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#98">OPEN_RIGHT_READABLE</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td> Can read from target object.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#100">OPEN_RIGHT_WRITABLE</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td> Can write to target object.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#102">OPEN_RIGHT_ADMIN</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
            <td> Connection can mount/umount filesystem.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#105">OPEN_FLAG_CREATE</a></td>
            <td>
                    <code>65536</code>
                </td>
                <td><code>uint32</code></td>
            <td> Create the object if it doesn't exist.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#107">OPEN_FLAG_CREATE_IF_ABSENT</a></td>
            <td>
                    <code>131072</code>
                </td>
                <td><code>uint32</code></td>
            <td> (with Create) Fail if the object already exists.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#109">OPEN_FLAG_TRUNCATE</a></td>
            <td>
                    <code>262144</code>
                </td>
                <td><code>uint32</code></td>
            <td> Truncate the object before usage.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#112">OPEN_FLAG_DIRECTORY</a></td>
            <td>
                    <code>524288</code>
                </td>
                <td><code>uint32</code></td>
            <td> Assert that the object to be opened is a directory.
 Return an error if the target object is not a directory.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#114">OPEN_FLAG_APPEND</a></td>
            <td>
                    <code>1048576</code>
                </td>
                <td><code>uint32</code></td>
            <td> Seek to the end of the object before all writes.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#116">OPEN_FLAG_NO_REMOTE</a></td>
            <td>
                    <code>2097152</code>
                </td>
                <td><code>uint32</code></td>
            <td> If the object is a mount point, open the local directory.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#127">OPEN_FLAG_NODE_REFERENCE</a></td>
            <td>
                    <code>4194304</code>
                </td>
                <td><code>uint32</code></td>
            <td> Open a reference to the object, not the object itself.
 It is ONLY valid to pass the following flags together with `OPEN_FLAG_NODE_REFERENCE`:
 - `OPEN_FLAG_DIRECTORY`
 - `OPEN_FLAG_NOT_DIRECTORY`
 - `OPEN_FLAG_DESCRIBE`
 otherwise an error is returned.
 If an object is opened or cloned using this method, the resulting connection does not carry
 any permission flags.
 The resulting node allows a limited set of operations: `GetAttr`, `Clone`, `Close`, `Describe`,
 and, if the node is a file, these extra operations: `GetFlags`, `SetFlags`.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#130">OPEN_FLAGS_ALLOWED_WITH_NODE_REFERENCE</a></td>
            <td>
                    <code>46661632</code>
                </td>
                <td><code>uint32</code></td>
            <td> Binary OR of `OPEN_FLAG_DIRECTORY`, OPEN_FLAG_NOT_DIRECTORY, OPEN_FLAG_DESCRIBE, and
 `OPEN_FLAG_NODE_REFERENCE`. Flags used when opening a node reference must fall within this mask.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#133">OPEN_FLAG_DESCRIBE</a></td>
            <td>
                    <code>8388608</code>
                </td>
                <td><code>uint32</code></td>
            <td> Requests that an "OnOpen" event is sent to the interface request.
 The event will contain a non-null NodeInfo if the open/clone is successful.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#150">OPEN_FLAG_POSIX</a></td>
            <td>
                    <code>16777216</code>
                </td>
                <td><code>uint32</code></td>
            <td> Specify this flag to request POSIX-compatibility. Currently, it affects permission handling.
 During Open:
 - If the target path is a directory, the rights on the new connection expands to include
   `OPEN_RIGHT_WRITABLE` if and only if the current connection and all intermediate mount points
   are writable.
 - Otherwise, this flag is ignored. It is an access denied error to request more rights
   than those on the current connection, or any intermediate mount points.

 If the posix compatibility flag is not specified, opening always uses the requested rights,
 failing the operation with access denied error if requested rights exceeds the rights attached
 to the current connection.

 If the requesting connection is read-only and the requested rights are read-only, the flag
 may be ignored by the server, and is not forwarded downstream. This is an implementation detail,
 necessary to enforce hierarchical permissions across mount points, and should have no effect
 on the expected behavior for clients.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#153">OPEN_FLAG_NOT_DIRECTORY</a></td>
            <td>
                    <code>33554432</code>
                </td>
                <td><code>uint32</code></td>
            <td> Assert that the object to be opened is not a directory.
 Return an error if the target object is a directory.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#157">CLONE_FLAG_SAME_RIGHTS</a></td>
            <td>
                    <code>67108864</code>
                </td>
                <td><code>uint32</code></td>
            <td> When used during clone, the new connection inherits the rights on the source connection,
 regardless if it is a file or directory. Otherwise, clone attempts to use the requested rights.
 It is invalid to pass any of the `OPEN_RIGHT_*` flags together with `CLONE_FLAG_SAME_RIGHTS`.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#224">MODE_PROTECTION_MASK</a></td>
            <td>
                    <code>4095</code>
                </td>
                <td><code>uint32</code></td>
            <td> Bits reserved for posix protections. Native fuchsia filesystems
 are not required to set bits contained within `MODE_PROTECTION_MASK`,
 but filesystems that wish to do so may refer to sys/stat.h for their
 definitions.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#228">MODE_TYPE_MASK</a></td>
            <td>
                    <code>1044480</code>
                </td>
                <td><code>uint32</code></td>
            <td> Bits indicating node type. The canonical mechanism to check
 for a node type is to take 'mode', bitwise AND it with the
 `MODE_TYPE_MASK`, and check exact equality against a mode type.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#229">MODE_TYPE_DIRECTORY</a></td>
            <td>
                    <code>16384</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#230">MODE_TYPE_BLOCK_DEVICE</a></td>
            <td>
                    <code>24576</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#231">MODE_TYPE_FILE</a></td>
            <td>
                    <code>32768</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#232">MODE_TYPE_SOCKET</a></td>
            <td>
                    <code>49152</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#233">MODE_TYPE_SERVICE</a></td>
            <td>
                    <code>65536</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#253">MAX_IOCTL_HANDLES</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#257">MAX_BUF</a></td>
            <td>
                    <code>8192</code>
                </td>
                <td><code>uint64</code></td>
            <td> The maximal buffer size which can be transmitted for buffered operations.
 This capacity is currently set somewhat arbitrarily.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#261">MAX_PATH</a></td>
            <td>
                    <code>4096</code>
                </td>
                <td><code>uint64</code></td>
            <td> The maximum length, in bytes, of a filesystem string.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#263">MAX_FILENAME</a></td>
            <td>
                    <code>255</code>
                </td>
                <td><code>uint64</code></td>
            <td> The maximum length, in bytes, of a single filesystem component.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#267">NODE_ATTRIBUTE_FLAG_CREATION_TIME</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td> The fields of 'attributes' which are used to update the Node are indicated
 by the 'flags' argument.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#268">NODE_ATTRIBUTE_FLAG_MODIFICATION_TIME</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#281">VMO_FLAG_READ</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td> Requests that the VMO be readable.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#284">VMO_FLAG_WRITE</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td> Requests that the VMO be writable.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#287">VMO_FLAG_EXEC</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
            <td> Requests that the VMO be executable.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#292">VMO_FLAG_PRIVATE</a></td>
            <td>
                    <code>65536</code>
                </td>
                <td><code>uint32</code></td>
            <td> Require a copy-on-write clone of the underlying VMO.
 The request should fail if the VMO is not cloned.
 May not be supplied with fuchsia_io_`VMO_FLAG_EXACT`.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#297">VMO_FLAG_EXACT</a></td>
            <td>
                    <code>131072</code>
                </td>
                <td><code>uint32</code></td>
            <td> Require an exact (non-cloned) handle to the underlying VMO.
 The request should fail if a handle to the exact VMO is not returned.
 May not be supplied with `VMO_FLAG_PRIVATE`.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#366">DIRENT_TYPE_UNKNOWN</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint8</code></td>
            <td> A dirent with an unknown type.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#368">DIRENT_TYPE_DIRECTORY</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint8</code></td>
            <td> A dirent representing a directory object.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#370">DIRENT_TYPE_BLOCK_DEVICE</a></td>
            <td>
                    <code>6</code>
                </td>
                <td><code>uint8</code></td>
            <td> A dirent representing a block device object.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#372">DIRENT_TYPE_FILE</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint8</code></td>
            <td> A dirent representing a file object.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#374">DIRENT_TYPE_SOCKET</a></td>
            <td>
                    <code>12</code>
                </td>
                <td><code>uint8</code></td>
            <td> A dirent representing a socket object.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#376">DIRENT_TYPE_SERVICE</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint8</code></td>
            <td> A dirent representing a service object.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#380">INO_UNKNOWN</a></td>
            <td>
                    <code>18446744073709551615</code>
                </td>
                <td><code>uint64</code></td>
            <td> Nodes which do not have ino values should return this value
 from Readdir and GetAttr.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#383">WATCH_EVENT_DELETED</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint8</code></td>
            <td> Indicates the directory being watched has been deleted.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#385">WATCH_EVENT_ADDED</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint8</code></td>
            <td> Indicates a node has been created (either new or moved) into a directory.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#387">WATCH_EVENT_REMOVED</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint8</code></td>
            <td> Identifies a node has been removed (either deleted or moved) from the directory.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#389">WATCH_EVENT_EXISTING</a></td>
            <td>
                    <code>3</code>
                </td>
                <td><code>uint8</code></td>
            <td> Identifies a node already existed in the directory when watching started.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#391">WATCH_EVENT_IDLE</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint8</code></td>
            <td> Identifies that no more `WATCH_EVENT_EXISTING` events will be sent.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#394">WATCH_MASK_DELETED</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td> Used by Directory::Watch. Requests transmission of `WATCH_EVENT_DELETED`.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#396">WATCH_MASK_ADDED</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td> Used by Directory::Watch. Requests transmission of `WATCH_EVENT_ADDED`.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#398">WATCH_MASK_REMOVED</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
            <td> Used by Directory::Watch. Requests transmission of `WATCH_EVENT_REMOVED`.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#400">WATCH_MASK_EXISTING</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint32</code></td>
            <td> Used by Directory::Watch. Requests transmission of `WATCH_EVENT_EXISTING`.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#402">WATCH_MASK_IDLE</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
            <td> Used by Directory::Watch. Requests transmission of `WATCH_EVENT_IDLE`.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#404">WATCH_MASK_ALL</a></td>
            <td>
                    <code>31</code>
                </td>
                <td><code>uint32</code></td>
            <td> Used by Directory::Watch. Requests transmission of all watcher events.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#564">MOUNT_CREATE_FLAG_REPLACE</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#566">MAX_FS_NAME_BUFFER</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#31">FILE_SIGNAL_READABLE</a></td>
            <td>
                    <code>16777216</code>
                </td>
                <td><code>uint32</code></td>
            <td> Indicates the file is ready for reading.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#33">FILE_SIGNAL_WRITABLE</a></td>
            <td>
                    <code>33554432</code>
                </td>
                <td><code>uint32</code></td>
            <td> Indicates the file is ready for writing.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#74">DEVICE_SIGNAL_READABLE</a></td>
            <td>
                    <code>16777216</code>
                </td>
                <td><code>uint32</code></td>
            <td> Indicates the device is ready for reading.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#76">DEVICE_SIGNAL_OOB</a></td>
            <td>
                    <code>33554432</code>
                </td>
                <td><code>uint32</code></td>
            <td> Indicates an out-of-band state transition has occurred.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#78">DEVICE_SIGNAL_WRITABLE</a></td>
            <td>
                    <code>67108864</code>
                </td>
                <td><code>uint32</code></td>
            <td> Indicates the device is ready for writing.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#80">DEVICE_SIGNAL_ERROR</a></td>
            <td>
                    <code>134217728</code>
                </td>
                <td><code>uint32</code></td>
            <td> Indicates the device has encountered an error state.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#82">DEVICE_SIGNAL_HANGUP</a></td>
            <td>
                    <code>268435456</code>
                </td>
                <td><code>uint32</code></td>
            <td> Indicates the device has hung up on the current connection.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#98">OPEN_RIGHT_READABLE</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td> Can read from target object.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#100">OPEN_RIGHT_WRITABLE</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td> Can write to target object.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#102">OPEN_RIGHT_ADMIN</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
            <td> Connection can mount/umount filesystem.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#105">OPEN_FLAG_CREATE</a></td>
            <td>
                    <code>65536</code>
                </td>
                <td><code>uint32</code></td>
            <td> Create the object if it doesn't exist.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#107">OPEN_FLAG_CREATE_IF_ABSENT</a></td>
            <td>
                    <code>131072</code>
                </td>
                <td><code>uint32</code></td>
            <td> (with Create) Fail if the object already exists.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#109">OPEN_FLAG_TRUNCATE</a></td>
            <td>
                    <code>262144</code>
                </td>
                <td><code>uint32</code></td>
            <td> Truncate the object before usage.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#112">OPEN_FLAG_DIRECTORY</a></td>
            <td>
                    <code>524288</code>
                </td>
                <td><code>uint32</code></td>
            <td> Assert that the object to be opened is a directory.
 Return an error if the target object is not a directory.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#114">OPEN_FLAG_APPEND</a></td>
            <td>
                    <code>1048576</code>
                </td>
                <td><code>uint32</code></td>
            <td> Seek to the end of the object before all writes.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#116">OPEN_FLAG_NO_REMOTE</a></td>
            <td>
                    <code>2097152</code>
                </td>
                <td><code>uint32</code></td>
            <td> If the object is a mount point, open the local directory.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#127">OPEN_FLAG_NODE_REFERENCE</a></td>
            <td>
                    <code>4194304</code>
                </td>
                <td><code>uint32</code></td>
            <td> Open a reference to the object, not the object itself.
 It is ONLY valid to pass the following flags together with `OPEN_FLAG_NODE_REFERENCE`:
 - `OPEN_FLAG_DIRECTORY`
 - `OPEN_FLAG_NOT_DIRECTORY`
 - `OPEN_FLAG_DESCRIBE`
 otherwise an error is returned.
 If an object is opened or cloned using this method, the resulting connection does not carry
 any permission flags.
 The resulting node allows a limited set of operations: `GetAttr`, `Clone`, `Close`, `Describe`,
 and, if the node is a file, these extra operations: `GetFlags`, `SetFlags`.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#130">OPEN_FLAGS_ALLOWED_WITH_NODE_REFERENCE</a></td>
            <td>
                    <code>46661632</code>
                </td>
                <td><code>uint32</code></td>
            <td> Binary OR of `OPEN_FLAG_DIRECTORY`, OPEN_FLAG_NOT_DIRECTORY, OPEN_FLAG_DESCRIBE, and
 `OPEN_FLAG_NODE_REFERENCE`. Flags used when opening a node reference must fall within this mask.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#133">OPEN_FLAG_DESCRIBE</a></td>
            <td>
                    <code>8388608</code>
                </td>
                <td><code>uint32</code></td>
            <td> Requests that an "OnOpen" event is sent to the interface request.
 The event will contain a non-null NodeInfo if the open/clone is successful.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#150">OPEN_FLAG_POSIX</a></td>
            <td>
                    <code>16777216</code>
                </td>
                <td><code>uint32</code></td>
            <td> Specify this flag to request POSIX-compatibility. Currently, it affects permission handling.
 During Open:
 - If the target path is a directory, the rights on the new connection expands to include
   `OPEN_RIGHT_WRITABLE` if and only if the current connection and all intermediate mount points
   are writable.
 - Otherwise, this flag is ignored. It is an access denied error to request more rights
   than those on the current connection, or any intermediate mount points.

 If the posix compatibility flag is not specified, opening always uses the requested rights,
 failing the operation with access denied error if requested rights exceeds the rights attached
 to the current connection.

 If the requesting connection is read-only and the requested rights are read-only, the flag
 may be ignored by the server, and is not forwarded downstream. This is an implementation detail,
 necessary to enforce hierarchical permissions across mount points, and should have no effect
 on the expected behavior for clients.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#153">OPEN_FLAG_NOT_DIRECTORY</a></td>
            <td>
                    <code>33554432</code>
                </td>
                <td><code>uint32</code></td>
            <td> Assert that the object to be opened is not a directory.
 Return an error if the target object is a directory.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#157">CLONE_FLAG_SAME_RIGHTS</a></td>
            <td>
                    <code>67108864</code>
                </td>
                <td><code>uint32</code></td>
            <td> When used during clone, the new connection inherits the rights on the source connection,
 regardless if it is a file or directory. Otherwise, clone attempts to use the requested rights.
 It is invalid to pass any of the `OPEN_RIGHT_*` flags together with `CLONE_FLAG_SAME_RIGHTS`.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#224">MODE_PROTECTION_MASK</a></td>
            <td>
                    <code>4095</code>
                </td>
                <td><code>uint32</code></td>
            <td> Bits reserved for posix protections. Native fuchsia filesystems
 are not required to set bits contained within `MODE_PROTECTION_MASK`,
 but filesystems that wish to do so may refer to sys/stat.h for their
 definitions.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#228">MODE_TYPE_MASK</a></td>
            <td>
                    <code>1044480</code>
                </td>
                <td><code>uint32</code></td>
            <td> Bits indicating node type. The canonical mechanism to check
 for a node type is to take 'mode', bitwise AND it with the
 `MODE_TYPE_MASK`, and check exact equality against a mode type.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#229">MODE_TYPE_DIRECTORY</a></td>
            <td>
                    <code>16384</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#230">MODE_TYPE_BLOCK_DEVICE</a></td>
            <td>
                    <code>24576</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#231">MODE_TYPE_FILE</a></td>
            <td>
                    <code>32768</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#232">MODE_TYPE_SOCKET</a></td>
            <td>
                    <code>49152</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#233">MODE_TYPE_SERVICE</a></td>
            <td>
                    <code>65536</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#253">MAX_IOCTL_HANDLES</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#257">MAX_BUF</a></td>
            <td>
                    <code>8192</code>
                </td>
                <td><code>uint64</code></td>
            <td> The maximal buffer size which can be transmitted for buffered operations.
 This capacity is currently set somewhat arbitrarily.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#261">MAX_PATH</a></td>
            <td>
                    <code>4096</code>
                </td>
                <td><code>uint64</code></td>
            <td> The maximum length, in bytes, of a filesystem string.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#263">MAX_FILENAME</a></td>
            <td>
                    <code>255</code>
                </td>
                <td><code>uint64</code></td>
            <td> The maximum length, in bytes, of a single filesystem component.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#267">NODE_ATTRIBUTE_FLAG_CREATION_TIME</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td> The fields of 'attributes' which are used to update the Node are indicated
 by the 'flags' argument.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#268">NODE_ATTRIBUTE_FLAG_MODIFICATION_TIME</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#281">VMO_FLAG_READ</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td> Requests that the VMO be readable.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#284">VMO_FLAG_WRITE</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td> Requests that the VMO be writable.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#287">VMO_FLAG_EXEC</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
            <td> Requests that the VMO be executable.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#292">VMO_FLAG_PRIVATE</a></td>
            <td>
                    <code>65536</code>
                </td>
                <td><code>uint32</code></td>
            <td> Require a copy-on-write clone of the underlying VMO.
 The request should fail if the VMO is not cloned.
 May not be supplied with fuchsia_io_`VMO_FLAG_EXACT`.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#297">VMO_FLAG_EXACT</a></td>
            <td>
                    <code>131072</code>
                </td>
                <td><code>uint32</code></td>
            <td> Require an exact (non-cloned) handle to the underlying VMO.
 The request should fail if a handle to the exact VMO is not returned.
 May not be supplied with `VMO_FLAG_PRIVATE`.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#366">DIRENT_TYPE_UNKNOWN</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint8</code></td>
            <td> A dirent with an unknown type.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#368">DIRENT_TYPE_DIRECTORY</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint8</code></td>
            <td> A dirent representing a directory object.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#370">DIRENT_TYPE_BLOCK_DEVICE</a></td>
            <td>
                    <code>6</code>
                </td>
                <td><code>uint8</code></td>
            <td> A dirent representing a block device object.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#372">DIRENT_TYPE_FILE</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint8</code></td>
            <td> A dirent representing a file object.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#374">DIRENT_TYPE_SOCKET</a></td>
            <td>
                    <code>12</code>
                </td>
                <td><code>uint8</code></td>
            <td> A dirent representing a socket object.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#376">DIRENT_TYPE_SERVICE</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint8</code></td>
            <td> A dirent representing a service object.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#380">INO_UNKNOWN</a></td>
            <td>
                    <code>18446744073709551615</code>
                </td>
                <td><code>uint64</code></td>
            <td> Nodes which do not have ino values should return this value
 from Readdir and GetAttr.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#383">WATCH_EVENT_DELETED</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint8</code></td>
            <td> Indicates the directory being watched has been deleted.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#385">WATCH_EVENT_ADDED</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint8</code></td>
            <td> Indicates a node has been created (either new or moved) into a directory.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#387">WATCH_EVENT_REMOVED</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint8</code></td>
            <td> Identifies a node has been removed (either deleted or moved) from the directory.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#389">WATCH_EVENT_EXISTING</a></td>
            <td>
                    <code>3</code>
                </td>
                <td><code>uint8</code></td>
            <td> Identifies a node already existed in the directory when watching started.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#391">WATCH_EVENT_IDLE</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint8</code></td>
            <td> Identifies that no more `WATCH_EVENT_EXISTING` events will be sent.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#394">WATCH_MASK_DELETED</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td> Used by Directory::Watch. Requests transmission of `WATCH_EVENT_DELETED`.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#396">WATCH_MASK_ADDED</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td> Used by Directory::Watch. Requests transmission of `WATCH_EVENT_ADDED`.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#398">WATCH_MASK_REMOVED</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
            <td> Used by Directory::Watch. Requests transmission of `WATCH_EVENT_REMOVED`.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#400">WATCH_MASK_EXISTING</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint32</code></td>
            <td> Used by Directory::Watch. Requests transmission of `WATCH_EVENT_EXISTING`.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#402">WATCH_MASK_IDLE</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
            <td> Used by Directory::Watch. Requests transmission of `WATCH_EVENT_IDLE`.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#404">WATCH_MASK_ALL</a></td>
            <td>
                    <code>31</code>
                </td>
                <td><code>uint32</code></td>
            <td> Used by Directory::Watch. Requests transmission of all watcher events.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#564">MOUNT_CREATE_FLAG_REPLACE</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#566">MAX_FS_NAME_BUFFER</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    
</table>

