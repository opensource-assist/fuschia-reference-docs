[TOC]

# fuchsia.io


## **PROTOCOLS**

## Node {#Node}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#164)*

<p>Node defines the minimal interface for entities which can be accessed in a filesystem.</p>

### Clone {#Clone}

<p>Create another connection to the same remote object.</p>
<p><code>flags</code> may be any of:</p>
<ul>
<li><code>OPEN_RIGHT_*</code></li>
<li><code>OPEN_FLAG_APPEND</code></li>
<li><code>OPEN_FLAG_NO_REMOTE</code></li>
<li><code>OPEN_FLAG_DESCRIBE</code></li>
<li><code>CLONE_FLAG_SAME_RIGHTS</code></li>
</ul>
<p>All other flags are ignored.</p>
<p>The <code>OPEN_RIGHT_*</code> bits in <code>flags</code> request corresponding rights over the resulting
cloned object.
The cloned object must have rights less than or equal to the original object.
Alternatively, pass <code>CLONE_FLAG_SAME_RIGHTS</code> to inherit the rights on the source connection.
It is invalid to pass any of the <code>OPEN_RIGHT_*</code> flags together with
<code>CLONE_FLAG_SAME_RIGHTS</code>.</p>

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



### Close {#Close}

<p>Terminates connection with object.</p>
<p>This method does not require any rights.</p>

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

### Describe {#Describe}

<p>Returns extra information about the type of the object.
If the <code>Describe</code> operation fails, the connection is closed.</p>
<p>This method does not require any rights.</p>

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

### OnOpen {#OnOpen}

<p>An event produced eagerly by a FIDL server if requested by <code>OPEN_FLAG_DESCRIBE</code>.</p>
<p>Indicates the success or failure of the open operation, and optionally describes the
object. If the status is <code>ZX_OK</code>, <code>info</code> contains descriptive information about the object
(the same as would be returned by <code>Describe</code>).</p>



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

### Sync {#Sync}

<p>Synchronizes updates to the node to the underlying media, if it exists.</p>
<p>This method does not require any rights.</p>

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

### GetAttr {#GetAttr}

<p>Acquires information about the node.</p>
<p>This method does not require any rights.</p>

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

### SetAttr {#SetAttr}

<p>Updates information about the node.
<code>flags</code> may be any of <code>NODE_ATTRIBUTE_FLAG_*</code>.</p>
<p>This method requires following rights: <code>OPEN_RIGHT_WRITABLE</code>.</p>

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

### NodeGetFlags {#NodeGetFlags}

<p>Acquires the <code>Directory.Open</code> rights and flags used to access this file.</p>
<p>This method does not require any rights.
This method has the same functionality as GetFlags for File and is
meant as an in-progress replacement.</p>

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

### NodeSetFlags {#NodeSetFlags}

<p>Changes the <code>Directory.Open</code> flags used to access the file.
Supported flags which can be turned on / off:</p>
<ul>
<li><code>OPEN_FLAG_APPEND</code></li>
</ul>
<p>This method does not require any rights.
This method has the same functionality as SetFlags for File and is
meant as an in-progress replacement.</p>

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

## File {#File}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#317)*

<p>File defines the interface of a node which contains a flat layout of data.</p>

### Clone {#Clone}

<p>Create another connection to the same remote object.</p>
<p><code>flags</code> may be any of:</p>
<ul>
<li><code>OPEN_RIGHT_*</code></li>
<li><code>OPEN_FLAG_APPEND</code></li>
<li><code>OPEN_FLAG_NO_REMOTE</code></li>
<li><code>OPEN_FLAG_DESCRIBE</code></li>
<li><code>CLONE_FLAG_SAME_RIGHTS</code></li>
</ul>
<p>All other flags are ignored.</p>
<p>The <code>OPEN_RIGHT_*</code> bits in <code>flags</code> request corresponding rights over the resulting
cloned object.
The cloned object must have rights less than or equal to the original object.
Alternatively, pass <code>CLONE_FLAG_SAME_RIGHTS</code> to inherit the rights on the source connection.
It is invalid to pass any of the <code>OPEN_RIGHT_*</code> flags together with
<code>CLONE_FLAG_SAME_RIGHTS</code>.</p>

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



### Close {#Close}

<p>Terminates connection with object.</p>
<p>This method does not require any rights.</p>

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

### Describe {#Describe}

<p>Returns extra information about the type of the object.
If the <code>Describe</code> operation fails, the connection is closed.</p>
<p>This method does not require any rights.</p>

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

### OnOpen {#OnOpen}

<p>An event produced eagerly by a FIDL server if requested by <code>OPEN_FLAG_DESCRIBE</code>.</p>
<p>Indicates the success or failure of the open operation, and optionally describes the
object. If the status is <code>ZX_OK</code>, <code>info</code> contains descriptive information about the object
(the same as would be returned by <code>Describe</code>).</p>



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

### Sync {#Sync}

<p>Synchronizes updates to the node to the underlying media, if it exists.</p>
<p>This method does not require any rights.</p>

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

### GetAttr {#GetAttr}

<p>Acquires information about the node.</p>
<p>This method does not require any rights.</p>

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

### SetAttr {#SetAttr}

<p>Updates information about the node.
<code>flags</code> may be any of <code>NODE_ATTRIBUTE_FLAG_*</code>.</p>
<p>This method requires following rights: <code>OPEN_RIGHT_WRITABLE</code>.</p>

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

### NodeGetFlags {#NodeGetFlags}

<p>Acquires the <code>Directory.Open</code> rights and flags used to access this file.</p>
<p>This method does not require any rights.
This method has the same functionality as GetFlags for File and is
meant as an in-progress replacement.</p>

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

### NodeSetFlags {#NodeSetFlags}

<p>Changes the <code>Directory.Open</code> flags used to access the file.
Supported flags which can be turned on / off:</p>
<ul>
<li><code>OPEN_FLAG_APPEND</code></li>
</ul>
<p>This method does not require any rights.
This method has the same functionality as SetFlags for File and is
meant as an in-progress replacement.</p>

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

### Read {#Read}

<p>Reads <code>count</code> bytes at the seek offset.
The seek offset is moved forward by the number of bytes read.</p>
<p>This method requires following rights: <code>OPEN_RIGHT_READABLE</code>.</p>

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

### ReadAt {#ReadAt}

<p>Reads <code>count</code> bytes at the provided offset.
Does not affect the seek offset.</p>
<p>This method requires following rights: <code>OPEN_RIGHT_READABLE</code>.</p>

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

### Write {#Write}

<p>Writes data at the seek offset.
The seek offset is moved forward by the number of bytes written.</p>
<p>This method requires following rights: <code>OPEN_RIGHT_WRITABLE</code>.</p>

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

### WriteAt {#WriteAt}

<p>Writes data to the provided offset.
Does not affect the seek offset.</p>
<p>This method requires following rights: <code>OPEN_RIGHT_WRITABLE</code>.</p>

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

### Seek {#Seek}

<p>Moves the offset at which the next invocation of <code>Read()</code> or <code>Write()</code> will
occur.</p>
<p>This method does not require any rights.</p>

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

### Truncate {#Truncate}

<p>Shrinks the file size to 'length' bytes.</p>
<p>This method requires following rights: <code>OPEN_RIGHT_WRITABLE</code>.</p>

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

### GetFlags {#GetFlags}

<p>Acquires the <code>Directory.Open</code> rights and flags used to access this file.</p>
<p>This method does not require any rights.</p>

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

### SetFlags {#SetFlags}

<p>Changes the <code>Directory.Open</code> flags used to access the file.
Supported flags which can be turned on / off:</p>
<ul>
<li><code>OPEN_FLAG_APPEND</code></li>
</ul>
<p>This method does not require any rights.</p>

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

### GetBuffer {#GetBuffer}

<p>Acquires a buffer representing this file, if there is one, with the
requested access rights.</p>
<p><code>flags</code> may be any of <code>VMO_FLAG_*</code>.</p>
<p>This method requires following rights:</p>
<ul>
<li><code>OPEN_RIGHT_WRITABLE</code> if <code>flags</code> includes <code>VMO_FLAG_WRITE</code>.</li>
<li><code>OPEN_RIGHT_READABLE</code> if <code>flags</code> includes <code>VMO_FLAG_READ</code> or <code>VMO_FLAG_EXEC</code>.</li>
</ul>

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
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a>?</code>
            </td>
        </tr></table>

## DirectoryWatcher {#DirectoryWatcher}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#437)*

<p>DirectoryWatcher transmits messages from a filesystem server
about events happening in the filesystem. Clients can register
new watchers using the <code>Directory.Watch</code> method, where they can
filter which events they want to receive notifications for.</p>

### OnEvent {#OnEvent}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>events</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>



## Directory {#Directory}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#444)*

<p>Directory defines a node which is capable of containing other Objects.</p>

### Clone {#Clone}

<p>Create another connection to the same remote object.</p>
<p><code>flags</code> may be any of:</p>
<ul>
<li><code>OPEN_RIGHT_*</code></li>
<li><code>OPEN_FLAG_APPEND</code></li>
<li><code>OPEN_FLAG_NO_REMOTE</code></li>
<li><code>OPEN_FLAG_DESCRIBE</code></li>
<li><code>CLONE_FLAG_SAME_RIGHTS</code></li>
</ul>
<p>All other flags are ignored.</p>
<p>The <code>OPEN_RIGHT_*</code> bits in <code>flags</code> request corresponding rights over the resulting
cloned object.
The cloned object must have rights less than or equal to the original object.
Alternatively, pass <code>CLONE_FLAG_SAME_RIGHTS</code> to inherit the rights on the source connection.
It is invalid to pass any of the <code>OPEN_RIGHT_*</code> flags together with
<code>CLONE_FLAG_SAME_RIGHTS</code>.</p>

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



### Close {#Close}

<p>Terminates connection with object.</p>
<p>This method does not require any rights.</p>

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

### Describe {#Describe}

<p>Returns extra information about the type of the object.
If the <code>Describe</code> operation fails, the connection is closed.</p>
<p>This method does not require any rights.</p>

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

### OnOpen {#OnOpen}

<p>An event produced eagerly by a FIDL server if requested by <code>OPEN_FLAG_DESCRIBE</code>.</p>
<p>Indicates the success or failure of the open operation, and optionally describes the
object. If the status is <code>ZX_OK</code>, <code>info</code> contains descriptive information about the object
(the same as would be returned by <code>Describe</code>).</p>



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

### Sync {#Sync}

<p>Synchronizes updates to the node to the underlying media, if it exists.</p>
<p>This method does not require any rights.</p>

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

### GetAttr {#GetAttr}

<p>Acquires information about the node.</p>
<p>This method does not require any rights.</p>

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

### SetAttr {#SetAttr}

<p>Updates information about the node.
<code>flags</code> may be any of <code>NODE_ATTRIBUTE_FLAG_*</code>.</p>
<p>This method requires following rights: <code>OPEN_RIGHT_WRITABLE</code>.</p>

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

### NodeGetFlags {#NodeGetFlags}

<p>Acquires the <code>Directory.Open</code> rights and flags used to access this file.</p>
<p>This method does not require any rights.
This method has the same functionality as GetFlags for File and is
meant as an in-progress replacement.</p>

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

### NodeSetFlags {#NodeSetFlags}

<p>Changes the <code>Directory.Open</code> flags used to access the file.
Supported flags which can be turned on / off:</p>
<ul>
<li><code>OPEN_FLAG_APPEND</code></li>
</ul>
<p>This method does not require any rights.
This method has the same functionality as SetFlags for File and is
meant as an in-progress replacement.</p>

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

### Open {#Open}

<p>Opens a new object relative to this directory object.</p>
<p><code>path</code> may contain multiple segments, separated by &quot;/&quot; characters,
and should never be empty; i.e., &quot;&quot; is an invalid path.</p>
<p><code>flags</code> may be any of the <code>OPEN_FLAG_*</code> and <code>OPEN_RIGHT_*</code> values, bitwise ORed together.
The <code>OPEN_FLAG_DESCRIBE</code> flag may cause an <code>OnOpen</code> event to be transmitted
on the <code>object</code> handle, indicating the type of object opened.</p>
<p>If an unknown value is sent for either flags or mode, the connection should
be closed.</p>
<p><code>OPEN_RIGHT_*</code> flags provided in <code>flags</code> will restrict access rights on
the <code>object</code> channel which will be connected to the opened entity.</p>
<p>Rights are never increased. When you open a nested entity within a directory, you may only
request the same rights as what the directory connection already has, or a subset of those.
Exceeding those rights causes an access denied error to be transmitted in the
<code>OnOpen</code> event if applicable, and the <code>object</code> connection closed.</p>
<p>The caller must specify either one or more of the <code>OPEN_RIGHT_*</code> flags, or
the <code>OPEN_FLAG_NODE_REFERENCE</code> flag.</p>

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



### Unlink {#Unlink}

<p>Detaches an object from this directory object.</p>
<p>The underlying object may or may not be deleted after this method
completes: although the link will be removed from the containing directory,
objects with multiple references (such as files which are still open)
will not actually be destroyed until all references are removed.</p>
<p>If a directory is unlinked while it still has an open reference,
it must become read-only, preventing new entries from being created
until all references close and the directory is destroyed.</p>
<p><code>path</code> identifies the file which should be detached.
If <code>path</code> contains multiple segments, separated by &quot;/&quot; characters,
then the directory is traversed, one segment at a time, relative to the
originally accessed Directory.</p>
<p>Returns:
<code>ZX_ERR_ACCESS_DENIED</code> if the connection (or the underlying filesystem) does not
allow writable access.
<code>ZX_ERR_INVALID_ARGS</code> if <code>path</code> contains &quot;..&quot; segments.
<code>ZX_ERR_NOT_EMPTY</code> if <code>path</code> refers to a non-empty directory.
<code>ZX_ERR_UNAVAILABLE</code> if <code>path</code> refers to a mount point, containing a remote channel.
<code>ZX_ERR_UNAVAILABLE</code> if <code>path</code> is &quot;.&quot;.</p>
<p>Other errors may be returned for filesystem-specific reasons.</p>
<p>This method requires following rights: <code>OPEN_RIGHT_WRITABLE</code>.</p>

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

### ReadDirents {#ReadDirents}

<p>Reads a collection of variably sized dirents into a buffer.
The number of dirents in a directory may be very large: akin to
calling read multiple times on a file, directories have a seek
offset which is updated on subsequent calls to ReadDirents.</p>
<p>These dirents are of the form:</p>
<pre><code>struct dirent {
  // Describes the inode of the entry.
  uint64 ino;
  // Describes the length of the dirent name in bytes.
  uint8 size;
  // Describes the type of the entry. Aligned with the
  // POSIX d_type values. Use `DIRENT_TYPE_*` constants.
  uint8 type;
  // Unterminated name of entry.
  char name[0];
}
</code></pre>
<p>This method does not require any rights, since one could always probe for
directory contents by triggering name conflicts during file creation.</p>

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

### Rewind {#Rewind}

<p>Resets the directory seek offset.</p>
<p>This method does not require any rights, similar to ReadDirents.</p>

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

### GetToken {#GetToken}

<p>Acquires a token to a Directory which can be used to identify
access to it at a later point in time.</p>
<p>This method requires following rights: <code>OPEN_RIGHT_WRITABLE</code>.</p>

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

### Rename {#Rename}

<p>Renames an object named src to the name dst, in a directory represented by token.</p>
<p><code>src/dst</code> must be resolved object names. Including &quot;/&quot; in any position
other than the end of the string will return <code>ZX_ERR_INVALID_ARGS</code>.
Returning &quot;/&quot; at the end of either string implies that it must be a
directory, or else <code>ZX_ERR_NOT_DIR</code> should be returned.</p>
<p>This method requires following rights: <code>OPEN_RIGHT_WRITABLE</code>.</p>

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

### Link {#Link}

<p>Creates a link to an object named src by the name dst, within a directory represented by
token.</p>
<p><code>src</code> must be a resolved object name. Including &quot;/&quot; in the string will
return <code>ZX_ERR_INVALID_ARGS</code>.</p>
<p><code>dst</code> must be a resolved object name. Including &quot;/&quot; in the string will
return <code>ZX_ERR_INVALID_ARGS</code>.</p>
<p>This method requires following rights: <code>OPEN_RIGHT_WRITABLE</code>.</p>

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

### Watch {#Watch}

<p>Watches a directory, receiving events of added messages on the
watcher request channel.</p>
<p>The <code>watcher</code> handle will send messages of the form:</p>
<pre><code>struct {
  uint8 event;
  uint8 len;
  char name[];
};
</code></pre>
<p>Where names are NOT null-terminated.</p>
<p>This API is unstable; in the future, watcher will be a <code>DirectoryWatcher</code> client.</p>
<p>Mask specifies a bitmask of events to observe.
Options must be zero; it is reserved.</p>
<p>This method does not require any rights, similar to ReadDirents.</p>

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

## DirectoryAdmin {#DirectoryAdmin}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#620)*

<p>DirectoryAdmin defines a directory which is capable of handling
administrator tasks within the filesystem.</p>

### Clone {#Clone}

<p>Create another connection to the same remote object.</p>
<p><code>flags</code> may be any of:</p>
<ul>
<li><code>OPEN_RIGHT_*</code></li>
<li><code>OPEN_FLAG_APPEND</code></li>
<li><code>OPEN_FLAG_NO_REMOTE</code></li>
<li><code>OPEN_FLAG_DESCRIBE</code></li>
<li><code>CLONE_FLAG_SAME_RIGHTS</code></li>
</ul>
<p>All other flags are ignored.</p>
<p>The <code>OPEN_RIGHT_*</code> bits in <code>flags</code> request corresponding rights over the resulting
cloned object.
The cloned object must have rights less than or equal to the original object.
Alternatively, pass <code>CLONE_FLAG_SAME_RIGHTS</code> to inherit the rights on the source connection.
It is invalid to pass any of the <code>OPEN_RIGHT_*</code> flags together with
<code>CLONE_FLAG_SAME_RIGHTS</code>.</p>

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



### Close {#Close}

<p>Terminates connection with object.</p>
<p>This method does not require any rights.</p>

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

### Describe {#Describe}

<p>Returns extra information about the type of the object.
If the <code>Describe</code> operation fails, the connection is closed.</p>
<p>This method does not require any rights.</p>

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

### OnOpen {#OnOpen}

<p>An event produced eagerly by a FIDL server if requested by <code>OPEN_FLAG_DESCRIBE</code>.</p>
<p>Indicates the success or failure of the open operation, and optionally describes the
object. If the status is <code>ZX_OK</code>, <code>info</code> contains descriptive information about the object
(the same as would be returned by <code>Describe</code>).</p>



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

### Sync {#Sync}

<p>Synchronizes updates to the node to the underlying media, if it exists.</p>
<p>This method does not require any rights.</p>

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

### GetAttr {#GetAttr}

<p>Acquires information about the node.</p>
<p>This method does not require any rights.</p>

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

### SetAttr {#SetAttr}

<p>Updates information about the node.
<code>flags</code> may be any of <code>NODE_ATTRIBUTE_FLAG_*</code>.</p>
<p>This method requires following rights: <code>OPEN_RIGHT_WRITABLE</code>.</p>

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

### NodeGetFlags {#NodeGetFlags}

<p>Acquires the <code>Directory.Open</code> rights and flags used to access this file.</p>
<p>This method does not require any rights.
This method has the same functionality as GetFlags for File and is
meant as an in-progress replacement.</p>

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

### NodeSetFlags {#NodeSetFlags}

<p>Changes the <code>Directory.Open</code> flags used to access the file.
Supported flags which can be turned on / off:</p>
<ul>
<li><code>OPEN_FLAG_APPEND</code></li>
</ul>
<p>This method does not require any rights.
This method has the same functionality as SetFlags for File and is
meant as an in-progress replacement.</p>

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

### Open {#Open}

<p>Opens a new object relative to this directory object.</p>
<p><code>path</code> may contain multiple segments, separated by &quot;/&quot; characters,
and should never be empty; i.e., &quot;&quot; is an invalid path.</p>
<p><code>flags</code> may be any of the <code>OPEN_FLAG_*</code> and <code>OPEN_RIGHT_*</code> values, bitwise ORed together.
The <code>OPEN_FLAG_DESCRIBE</code> flag may cause an <code>OnOpen</code> event to be transmitted
on the <code>object</code> handle, indicating the type of object opened.</p>
<p>If an unknown value is sent for either flags or mode, the connection should
be closed.</p>
<p><code>OPEN_RIGHT_*</code> flags provided in <code>flags</code> will restrict access rights on
the <code>object</code> channel which will be connected to the opened entity.</p>
<p>Rights are never increased. When you open a nested entity within a directory, you may only
request the same rights as what the directory connection already has, or a subset of those.
Exceeding those rights causes an access denied error to be transmitted in the
<code>OnOpen</code> event if applicable, and the <code>object</code> connection closed.</p>
<p>The caller must specify either one or more of the <code>OPEN_RIGHT_*</code> flags, or
the <code>OPEN_FLAG_NODE_REFERENCE</code> flag.</p>

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



### Unlink {#Unlink}

<p>Detaches an object from this directory object.</p>
<p>The underlying object may or may not be deleted after this method
completes: although the link will be removed from the containing directory,
objects with multiple references (such as files which are still open)
will not actually be destroyed until all references are removed.</p>
<p>If a directory is unlinked while it still has an open reference,
it must become read-only, preventing new entries from being created
until all references close and the directory is destroyed.</p>
<p><code>path</code> identifies the file which should be detached.
If <code>path</code> contains multiple segments, separated by &quot;/&quot; characters,
then the directory is traversed, one segment at a time, relative to the
originally accessed Directory.</p>
<p>Returns:
<code>ZX_ERR_ACCESS_DENIED</code> if the connection (or the underlying filesystem) does not
allow writable access.
<code>ZX_ERR_INVALID_ARGS</code> if <code>path</code> contains &quot;..&quot; segments.
<code>ZX_ERR_NOT_EMPTY</code> if <code>path</code> refers to a non-empty directory.
<code>ZX_ERR_UNAVAILABLE</code> if <code>path</code> refers to a mount point, containing a remote channel.
<code>ZX_ERR_UNAVAILABLE</code> if <code>path</code> is &quot;.&quot;.</p>
<p>Other errors may be returned for filesystem-specific reasons.</p>
<p>This method requires following rights: <code>OPEN_RIGHT_WRITABLE</code>.</p>

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

### ReadDirents {#ReadDirents}

<p>Reads a collection of variably sized dirents into a buffer.
The number of dirents in a directory may be very large: akin to
calling read multiple times on a file, directories have a seek
offset which is updated on subsequent calls to ReadDirents.</p>
<p>These dirents are of the form:</p>
<pre><code>struct dirent {
  // Describes the inode of the entry.
  uint64 ino;
  // Describes the length of the dirent name in bytes.
  uint8 size;
  // Describes the type of the entry. Aligned with the
  // POSIX d_type values. Use `DIRENT_TYPE_*` constants.
  uint8 type;
  // Unterminated name of entry.
  char name[0];
}
</code></pre>
<p>This method does not require any rights, since one could always probe for
directory contents by triggering name conflicts during file creation.</p>

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

### Rewind {#Rewind}

<p>Resets the directory seek offset.</p>
<p>This method does not require any rights, similar to ReadDirents.</p>

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

### GetToken {#GetToken}

<p>Acquires a token to a Directory which can be used to identify
access to it at a later point in time.</p>
<p>This method requires following rights: <code>OPEN_RIGHT_WRITABLE</code>.</p>

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

### Rename {#Rename}

<p>Renames an object named src to the name dst, in a directory represented by token.</p>
<p><code>src/dst</code> must be resolved object names. Including &quot;/&quot; in any position
other than the end of the string will return <code>ZX_ERR_INVALID_ARGS</code>.
Returning &quot;/&quot; at the end of either string implies that it must be a
directory, or else <code>ZX_ERR_NOT_DIR</code> should be returned.</p>
<p>This method requires following rights: <code>OPEN_RIGHT_WRITABLE</code>.</p>

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

### Link {#Link}

<p>Creates a link to an object named src by the name dst, within a directory represented by
token.</p>
<p><code>src</code> must be a resolved object name. Including &quot;/&quot; in the string will
return <code>ZX_ERR_INVALID_ARGS</code>.</p>
<p><code>dst</code> must be a resolved object name. Including &quot;/&quot; in the string will
return <code>ZX_ERR_INVALID_ARGS</code>.</p>
<p>This method requires following rights: <code>OPEN_RIGHT_WRITABLE</code>.</p>

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

### Watch {#Watch}

<p>Watches a directory, receiving events of added messages on the
watcher request channel.</p>
<p>The <code>watcher</code> handle will send messages of the form:</p>
<pre><code>struct {
  uint8 event;
  uint8 len;
  char name[];
};
</code></pre>
<p>Where names are NOT null-terminated.</p>
<p>This API is unstable; in the future, watcher will be a <code>DirectoryWatcher</code> client.</p>
<p>Mask specifies a bitmask of events to observe.
Options must be zero; it is reserved.</p>
<p>This method does not require any rights, similar to ReadDirents.</p>

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

### Mount {#Mount}

<p>Mount a channel representing a remote filesystem onto this directory.
All future requests to this node will be forwarded to the remote filesystem.
To re-open a node without forwarding to the remote target, the node
should be opened with <code>OPEN_FLAG_NO_REMOTE</code>.</p>

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

### MountAndCreate {#MountAndCreate}

<p>Atomically create a directory with a provided path, and mount the
remote handle to the newly created directory.</p>

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

### Unmount {#Unmount}

<p>Unmount this filesystem. After this function returns successfully,
all connections to the filesystem will be terminated.</p>

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

### UnmountNode {#UnmountNode}

<p>Detach a node which was previously attached to this directory
with Mount.</p>

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

### QueryFilesystem {#QueryFilesystem}

<p>Query the filesystem for filesystem-specific information.</p>

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

### GetDevicePath {#GetDevicePath}

<p>Acquire the path to the device backing this filesystem, if there is one.</p>

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

### Service {#Service}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#27)*



<p>The default protocol, interface information must be acquired some
other way.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### FileObject {#FileObject}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#36)*



<p>The object may be cast to interface 'File'.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>event</code></td>
            <td>
                <code>handle&lt;event&gt;?</code>
            </td>
            <td><p>An optional event which transmits information about an object's readability
or writability. This event relays information about the underlying object, not
the capability granted to client: this event may be signalled &quot;readable&quot; on a
connection that does not have the capability to read.</p>
<p>The &quot;<code>FILE_SIGNAL_</code>&quot; values may be observed on this event.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### DirectoryObject {#DirectoryObject}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#47)*



<p>The object may be cast to interface 'Directory'.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Pipe {#Pipe}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#51)*



<p>The object is accompanied by a pipe.</p>


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

### Socket {#Socket}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#56)*



<p>The object is accompanied by a socket.</p>


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

### Vmofile {#Vmofile}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#64)*



<p>The object is a file which is represented as an immutable VMO.
Although a VMO is returned as a part of this structure, this underlying object
may represent multiple Vmofiles. To identify the logical portion of the VMO
that represents the single file, an offset and length parameter are also supplied.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
            <td><p>The VMO which backs this file.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>offset</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The index into <code>vmo</code> which represents the first byte of the file.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>length</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The number of bytes, starting at <code>offset</code>, which may be used to represent this file.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### Device {#Device}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#85)*



<p>The object may be cast to interface 'Device'.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>event</code></td>
            <td>
                <code>handle&lt;eventpair&gt;?</code>
            </td>
            <td><p>An optional event which transmits information about a device's state.</p>
<p>The &quot;<code>DEVICE_SIGNAL_</code>&quot; values may be observed on this event.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### Tty {#Tty}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#93)*



<p>The object may be cast to interface 'Tty'</p>


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

### NodeAttributes {#NodeAttributes}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#254)*



<p>NodeAttributes defines generic information about a filesystem node.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>mode</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Protection bits and node type information describe in 'mode'.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>A filesystem-unique ID.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>content_size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Node size, in bytes.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>storage_size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Space needed to store node (possibly larger than size), in bytes.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>link_count</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Hard link count.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>creation_time</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Time of creation (may be updated manually after creation) in ns since Unix epoch, UTC.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>modification_time</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Time of last modification in ns since Unix epoch, UTC.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### WatchedEvent {#WatchedEvent}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#425)*



<p>WatchedEvent describes events returned from a DirectoryWatcher.</p>


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

### FilesystemInfo {#FilesystemInfo}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#589)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>total_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The number of data bytes which may be stored in a filesystem.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>used_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The number of data bytes which are in use by the filesystem.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>total_nodes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The number of nodes which may be stored in the filesystem.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>used_nodes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The number of nodes used by the filesystem.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>free_shared_pool_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The amount of space which may be allocated from the underlying
volume manager. If unsupported, this will be zero.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>fs_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>A unique identifier for this filesystem instance. Will not be preserved
across reboots.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>block_size</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>The size of a single filesystem block.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_filename_size</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>The maximum length of a filesystem name.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>fs_type</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>A unique identifier for the type of the underlying filesystem.</p>
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

### SeekOrigin {#SeekOrigin}
Type: <code>uint32</code>

*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#287)*

<p>Update the Seek offset.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>START</code></td>
            <td><code>0</code></td>
            <td><p>Seek from the start of the file.</p>
</td>
        </tr><tr>
            <td><code>CURRENT</code></td>
            <td><code>1</code></td>
            <td><p>Seek from the current position in the file.</p>
</td>
        </tr><tr>
            <td><code>END</code></td>
            <td><code>2</code></td>
            <td><p>Seek from the end of the file.</p>
</td>
        </tr></table>





## **UNIONS**

### NodeInfo {#NodeInfo}
*Defined in [fuchsia.io/io.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#14)*

<p>Describes how the connection to an should be handled, as well as
how to interpret the optional handle.</p>
<p>Refer to <code>Node.Describe()</code> and <code>Node.OnOpen()</code> for usage.</p>

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
            <td><p>Indicates the file is ready for reading.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#33">FILE_SIGNAL_WRITABLE</a></td>
            <td>
                    <code>33554432</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Indicates the file is ready for writing.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#74">DEVICE_SIGNAL_READABLE</a></td>
            <td>
                    <code>16777216</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Indicates the device is ready for reading.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#76">DEVICE_SIGNAL_OOB</a></td>
            <td>
                    <code>33554432</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Indicates an out-of-band state transition has occurred.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#78">DEVICE_SIGNAL_WRITABLE</a></td>
            <td>
                    <code>67108864</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Indicates the device is ready for writing.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#80">DEVICE_SIGNAL_ERROR</a></td>
            <td>
                    <code>134217728</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Indicates the device has encountered an error state.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#82">DEVICE_SIGNAL_HANGUP</a></td>
            <td>
                    <code>268435456</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Indicates the device has hung up on the current connection.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#98">OPEN_RIGHT_READABLE</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Can read from target object.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#100">OPEN_RIGHT_WRITABLE</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Can write to target object.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#102">OPEN_RIGHT_ADMIN</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Connection can mount/umount filesystem.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#104">OPEN_RIGHT_EXECUTABLE</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Connection can map target object executable.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#107">OPEN_FLAG_CREATE</a></td>
            <td>
                    <code>65536</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Create the object if it doesn't exist.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#109">OPEN_FLAG_CREATE_IF_ABSENT</a></td>
            <td>
                    <code>131072</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>(with Create) Fail if the object already exists.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#111">OPEN_FLAG_TRUNCATE</a></td>
            <td>
                    <code>262144</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Truncate the object before usage.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#114">OPEN_FLAG_DIRECTORY</a></td>
            <td>
                    <code>524288</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Assert that the object to be opened is a directory.
Return an error if the target object is not a directory.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#116">OPEN_FLAG_APPEND</a></td>
            <td>
                    <code>1048576</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Seek to the end of the object before all writes.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#118">OPEN_FLAG_NO_REMOTE</a></td>
            <td>
                    <code>2097152</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>If the object is a mount point, open the local directory.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#129">OPEN_FLAG_NODE_REFERENCE</a></td>
            <td>
                    <code>4194304</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Open a reference to the object, not the object itself.
It is ONLY valid to pass the following flags together with <code>OPEN_FLAG_NODE_REFERENCE</code>:</p>
<ul>
<li><code>OPEN_FLAG_DIRECTORY</code></li>
<li><code>OPEN_FLAG_NOT_DIRECTORY</code></li>
<li><code>OPEN_FLAG_DESCRIBE</code>
otherwise an error is returned.
If an object is opened or cloned using this method, the resulting connection does not carry
any permission flags.
The resulting node allows a limited set of operations: <code>GetAttr</code>, <code>Clone</code>, <code>Close</code>, <code>Describe</code>,
and, if the node is a file, these extra operations: <code>GetFlags</code>, <code>SetFlags</code>.</li>
</ul>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#132">OPEN_FLAGS_ALLOWED_WITH_NODE_REFERENCE</a></td>
            <td>
                    <code>46661632</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Binary OR of <code>OPEN_FLAG_DIRECTORY</code>, OPEN_FLAG_NOT_DIRECTORY, OPEN_FLAG_DESCRIBE, and
<code>OPEN_FLAG_NODE_REFERENCE</code>. Flags used when opening a node reference must fall within this mask.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#135">OPEN_FLAG_DESCRIBE</a></td>
            <td>
                    <code>8388608</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Requests that an &quot;OnOpen&quot; event is sent to the interface request.
The event will contain a non-null NodeInfo if the open/clone is successful.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#153">OPEN_FLAG_POSIX</a></td>
            <td>
                    <code>16777216</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Specify this flag to request POSIX-compatibility. Currently, it affects permission handling.
During Open:</p>
<ul>
<li>If the target path is a directory, the rights on the new connection expand to include
<code>OPEN_RIGHT_WRITABLE</code> if and only if the current connection and all intermediate mount points
are writable, and to include <code>OPEN_RIGHT_EXECUTABLE</code> if and only if the current connection and
all intermediate mount points are executable.</li>
<li>Otherwise, this flag is ignored. It is an access denied error to request more rights
than those on the current connection, or any intermediate mount points.</li>
</ul>
<p>If the posix compatibility flag is not specified, opening always uses the requested rights,
failing the operation with access denied error if requested rights exceeds the rights attached
to the current connection.</p>
<p>If the requesting connection is read-only and the requested rights are read-only, the flag
may be ignored by the server, and is not forwarded downstream. This is an implementation detail,
necessary to enforce hierarchical permissions across mount points, and should have no effect
on the expected behavior for clients.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#156">OPEN_FLAG_NOT_DIRECTORY</a></td>
            <td>
                    <code>33554432</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Assert that the object to be opened is not a directory.
Return an error if the target object is a directory.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#160">CLONE_FLAG_SAME_RIGHTS</a></td>
            <td>
                    <code>67108864</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>When used during clone, the new connection inherits the rights on the source connection,
regardless if it is a file or directory. Otherwise, clone attempts to use the requested rights.
It is invalid to pass any of the <code>OPEN_RIGHT_*</code> flags together with <code>CLONE_FLAG_SAME_RIGHTS</code>.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#242">MODE_PROTECTION_MASK</a></td>
            <td>
                    <code>4095</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Bits reserved for posix protections. Native fuchsia filesystems
are not required to set bits contained within <code>MODE_PROTECTION_MASK</code>,
but filesystems that wish to do so may refer to sys/stat.h for their
definitions.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#246">MODE_TYPE_MASK</a></td>
            <td>
                    <code>1044480</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Bits indicating node type. The canonical mechanism to check
for a node type is to take 'mode', bitwise AND it with the
<code>MODE_TYPE_MASK</code>, and check exact equality against a mode type.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#247">MODE_TYPE_DIRECTORY</a></td>
            <td>
                    <code>16384</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#248">MODE_TYPE_BLOCK_DEVICE</a></td>
            <td>
                    <code>24576</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#249">MODE_TYPE_FILE</a></td>
            <td>
                    <code>32768</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#250">MODE_TYPE_SOCKET</a></td>
            <td>
                    <code>49152</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#251">MODE_TYPE_SERVICE</a></td>
            <td>
                    <code>65536</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#273">MAX_BUF</a></td>
            <td>
                    <code>8192</code>
                </td>
                <td><code>uint64</code></td>
            <td><p>The maximal buffer size which can be transmitted for buffered operations.
This capacity is currently set somewhat arbitrarily.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#277">MAX_PATH</a></td>
            <td>
                    <code>4096</code>
                </td>
                <td><code>uint64</code></td>
            <td><p>The maximum length, in bytes, of a filesystem string.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#279">MAX_FILENAME</a></td>
            <td>
                    <code>255</code>
                </td>
                <td><code>uint64</code></td>
            <td><p>The maximum length, in bytes, of a single filesystem component.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#283">NODE_ATTRIBUTE_FLAG_CREATION_TIME</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The fields of 'attributes' which are used to update the Node are indicated
by the 'flags' argument.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#284">NODE_ATTRIBUTE_FLAG_MODIFICATION_TIME</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#297">VMO_FLAG_READ</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Requests that the VMO be readable.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#300">VMO_FLAG_WRITE</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Requests that the VMO be writable.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#303">VMO_FLAG_EXEC</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Requests that the VMO be executable.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#308">VMO_FLAG_PRIVATE</a></td>
            <td>
                    <code>65536</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Require a copy-on-write clone of the underlying VMO.
The request should fail if the VMO is not cloned.
May not be supplied with fuchsia_io_<code>VMO_FLAG_EXACT</code>.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#313">VMO_FLAG_EXACT</a></td>
            <td>
                    <code>131072</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Require an exact (non-cloned) handle to the underlying VMO.
The request should fail if a handle to the exact VMO is not returned.
May not be supplied with <code>VMO_FLAG_PRIVATE</code>.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#383">DIRENT_TYPE_UNKNOWN</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint8</code></td>
            <td><p>A dirent with an unknown type.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#385">DIRENT_TYPE_DIRECTORY</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint8</code></td>
            <td><p>A dirent representing a directory object.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#387">DIRENT_TYPE_BLOCK_DEVICE</a></td>
            <td>
                    <code>6</code>
                </td>
                <td><code>uint8</code></td>
            <td><p>A dirent representing a block device object.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#389">DIRENT_TYPE_FILE</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint8</code></td>
            <td><p>A dirent representing a file object.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#391">DIRENT_TYPE_SOCKET</a></td>
            <td>
                    <code>12</code>
                </td>
                <td><code>uint8</code></td>
            <td><p>A dirent representing a socket object.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#393">DIRENT_TYPE_SERVICE</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint8</code></td>
            <td><p>A dirent representing a service object.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#397">INO_UNKNOWN</a></td>
            <td>
                    <code>18446744073709551615</code>
                </td>
                <td><code>uint64</code></td>
            <td><p>Nodes which do not have ino values should return this value
from Readdir and GetAttr.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#400">WATCH_EVENT_DELETED</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint8</code></td>
            <td><p>Indicates the directory being watched has been deleted.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#402">WATCH_EVENT_ADDED</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint8</code></td>
            <td><p>Indicates a node has been created (either new or moved) into a directory.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#404">WATCH_EVENT_REMOVED</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint8</code></td>
            <td><p>Identifies a node has been removed (either deleted or moved) from the directory.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#406">WATCH_EVENT_EXISTING</a></td>
            <td>
                    <code>3</code>
                </td>
                <td><code>uint8</code></td>
            <td><p>Identifies a node already existed in the directory when watching started.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#408">WATCH_EVENT_IDLE</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint8</code></td>
            <td><p>Identifies that no more <code>WATCH_EVENT_EXISTING</code> events will be sent.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#411">WATCH_MASK_DELETED</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Used by <code>Directory.Watch</code>. Requests transmission of <code>WATCH_EVENT_DELETED</code>.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#413">WATCH_MASK_ADDED</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Used by <code>Directory.Watch</code>. Requests transmission of <code>WATCH_EVENT_ADDED</code>.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#415">WATCH_MASK_REMOVED</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Used by <code>Directory.Watch</code>. Requests transmission of <code>WATCH_EVENT_REMOVED</code>.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#417">WATCH_MASK_EXISTING</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Used by <code>Directory.Watch</code>. Requests transmission of <code>WATCH_EVENT_EXISTING</code>.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#419">WATCH_MASK_IDLE</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Used by <code>Directory.Watch</code>. Requests transmission of <code>WATCH_EVENT_IDLE</code>.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#421">WATCH_MASK_ALL</a></td>
            <td>
                    <code>31</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Used by <code>Directory.Watch</code>. Requests transmission of all watcher events.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#585">MOUNT_CREATE_FLAG_REPLACE</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io/io.fidl#587">MAX_FS_NAME_BUFFER</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    
</table>



