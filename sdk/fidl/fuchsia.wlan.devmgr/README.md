[TOC]

# fuchsia.wlan.devmgr


## **PROTOCOLS**

## IsolatedDevmgr {#IsolatedDevmgr}
*Defined in [fuchsia.wlan.devmgr/devmgr.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/wlan/testing/wlan-devmgr/fidl/devmgr.fidl#15)*

 Provides an isolated devfs.

 IsolatedDevmgr is a wrapper around a fuchsia.io.Directory node that is provided by
 an isolated devmgr component instance (//src/lib/isolated_devmgr). If injected into a test
 components, it represents the devfs (/dev) served by devmgr, in a real environment.

### Clone {#Clone}

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
 It is invalid to pass any of the `OPEN_RIGHT_*` flags together with
 `CLONE_FLAG_SAME_RIGHTS`.

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

### Describe {#Describe}

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
                <code><a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#NodeInfo'>NodeInfo</a></code>
            </td>
        </tr></table>

### OnOpen {#OnOpen}

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
                <code><a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#NodeInfo'>NodeInfo</a>?</code>
            </td>
        </tr></table>

### Sync {#Sync}

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

### GetAttr {#GetAttr}

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
                <code><a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#NodeAttributes'>NodeAttributes</a></code>
            </td>
        </tr></table>

### SetAttr {#SetAttr}

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

 Acquires the `Directory.Open` rights and flags used to access this file.

 This method does not require any rights.
 This method has the same functionality as GetFlags for File and is
 meant as an in-progress replacement.

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

 Changes the `Directory.Open` flags used to access the file.
 Supported flags which can be turned on / off:
 - `OPEN_FLAG_APPEND`

 This method does not require any rights.
 This method has the same functionality as SetFlags for File and is
 meant as an in-progress replacement.

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

 Opens a new object relative to this directory object.

 `path` may contain multiple segments, separated by "/" characters,
 and should never be empty; i.e., "" is an invalid path.

 `flags` may be any of the `OPEN_FLAG_*` and `OPEN_RIGHT_*` values, bitwise ORed together.
 The `OPEN_FLAG_DESCRIBE` flag may cause an `OnOpen` event to be transmitted
 on the `object` handle, indicating the type of object opened.

 If an unknown value is sent for either flags or mode, the connection should
 be closed.

 `OPEN_RIGHT_*` flags provided in `flags` will restrict access rights on
 the `object` channel which will be connected to the opened entity.

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
                <code>request&lt;<a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#Node'>Node</a>&gt;</code>
            </td>
        </tr></table>



### Unlink {#Unlink}

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

### ReadDirents {#ReadDirents}

 Reads a collection of variably sized dirents into a buffer.
 The number of dirents in a directory may be very large: akin to
 calling read multiple times on a file, directories have a seek
 offset which is updated on subsequent calls to ReadDirents.

 These dirents are of the form:
 ```
 struct dirent {
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
 ```

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

### Rewind {#Rewind}

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

### GetToken {#GetToken}

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

### Rename {#Rename}

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

### Link {#Link}

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

### Watch {#Watch}

 Watches a directory, receiving events of added messages on the
 watcher request channel.

 The `watcher` handle will send messages of the form:
 ```
 struct {
   uint8 event;
   uint8 len;
   char name[];
 };
 ```
 Where names are NOT null-terminated.

 This API is unstable; in the future, watcher will be a `DirectoryWatcher` client.

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















