[TOC]

# fuchsia.tel.devmgr


## **PROTOCOLS**

## IsolatedDevmgr {#IsolatedDevmgr}
*Defined in [fuchsia.tel.devmgr/devmgr.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/telephony/lib/tel-devmgr/fidl/devmgr.fidl#15)*

<p>Provides an isolated devfs.</p>
<p>IsolatedDevmgr is a wrapper around a fuchsia.io.Directory node that is provided by
an isolated devmgr component instance (//src/lib/isolated_devmgr). If injected into a test
components, it represents the devfs (/dev) in IsolatedDevmgr component.</p>

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
                <code>request&lt;<a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#Node'>Node</a>&gt;</code>
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
                <code><a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#NodeInfo'>NodeInfo</a></code>
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
                <code><a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#NodeInfo'>NodeInfo</a>?</code>
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
                <code><a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#NodeAttributes'>NodeAttributes</a></code>
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
                <code><a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#NodeAttributes'>NodeAttributes</a></code>
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
                <code>request&lt;<a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#Node'>Node</a>&gt;</code>
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















