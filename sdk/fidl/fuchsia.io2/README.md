[TOC]

# fuchsia.io2

<h1>Library Overview</h1>

## **PROTOCOLS**

## Debuglog {#Debuglog}
*Defined in [fuchsia.io2/debuglog.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/debuglog.fidl#10)*

<p>A node for interacting with the kernel debug log.
It may be manipulated via the debuglog object returned from
the <code>DebuglogInfo</code> member in <a class='link' href='#Representation'>Representation</a>.</p>

### Reopen {#Reopen}

<p>Creates another connection to the same node.</p>
<ul>
<li><code>options</code> options applicable to both <code>Open</code> and <code>Reopen</code>,
including negotiating protocol and restricting rights.
See <a class='link' href='#ConnectionOptions'>ConnectionOptions</a>.</li>
<li><code>object_request</code> is the server end of a channel created for the new
connection. The caller may proceed to send messages on the
corresponding client end right away.</li>
</ul>
<p>For files, the cloned connection and the original connection have
independent seek offsets.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#ConnectionOptions'>ConnectionOptions</a></code>
            </td>
        </tr><tr>
            <td><code>object_request</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



### Close {#Close}

<p>Terminates the connection to the node.</p>
<p>After calling <code>Close</code>, the client must not send any other requests.
The result of <code>Close</code> arrives as an epitaph, where the channel is closed
by the server upon processing this operation.</p>
<p>Closing the client end of the channel should be semantically equivalent
to calling <code>Close</code> without monitoring the status epitaph.</p>
<p>This method does not require any rights.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Describe {#Describe}

<p>Returns extra connection information and auxiliary handles.</p>
<ul>
<li><code>query</code> specifies the fields in <code>ConnectionInfo</code> that the caller is
interested in.</li>
</ul>
<ul>
<li><code>info</code> see <a class='link' href='#ConnectionInfo'>ConnectionInfo</a> for details on the fields.</li>
</ul>
<p>When all known bits in <code>query</code> are set, the return value matches
the one from <a class='link' href='#OnConnectionInfo'>OnConnectionInfo</a>, as if the caller requested that event
using <a class='link' href='#ConnectionFlags.GET_CONNECTION_INFO'>ConnectionFlags.GET_CONNECTION_INFO</a>.</p>
<p>If the <code>Describe</code> operation fails, the connection is closed with the
associated error.</p>
<p>This method does not require any rights.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>query</code></td>
            <td>
                <code><a class='link' href='#ConnectionInfoQuery'>ConnectionInfoQuery</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#ConnectionInfo'>ConnectionInfo</a></code>
            </td>
        </tr></table>

### OnConnectionInfo {#OnConnectionInfo}

<p>An event produced eagerly by the server if requested by
<a class='link' href='#ConnectionFlags.GET_CONNECTION_INFO'>ConnectionFlags.GET_CONNECTION_INFO</a>. This event will be the
first message from the server, and is sent exactly once.</p>
<ul>
<li><code>info</code> See <a class='link' href='#ConnectionInfo'>ConnectionInfo</a> for details on the fields.
All members should be present.</li>
</ul>
<p>Different from <a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#OnOpen'>OnOpen</a>, an error during open/reopen is
always manifested as an epitaph.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#ConnectionInfo'>ConnectionInfo</a></code>
            </td>
        </tr></table>

### GetToken {#GetToken}

<p>Acquires a token which can be used to identify this connection at
a later point in time.</p>
<p>This method does not require any rights. Note that the token identifies
the connection, hence carries the rights information on this connection.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Node_GetToken_Result'>Node_GetToken_Result</a></code>
            </td>
        </tr></table>

### GetAttributes {#GetAttributes}

<p>Acquires information about the node.</p>
<p>The attributes of a node should be stable, independent of the
specific protocol used to access it.</p>
<ul>
<li><code>query</code> a bit-mask specifying which attributes to fetch. The server
should not return more than necessary.</li>
</ul>
<ul>
<li><code>attributes</code> the returned attributes.</li>
</ul>
<p>This method requires the <a class='link' href='#Rights.GET_ATTRIBUTES'>Rights.GET_ATTRIBUTES</a> right.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>query</code></td>
            <td>
                <code><a class='link' href='#NodeAttributesQuery'>NodeAttributesQuery</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Node_GetAttributes_Result'>Node_GetAttributes_Result</a></code>
            </td>
        </tr></table>

### UpdateAttributes {#UpdateAttributes}

<p>Updates information about the node.</p>
<ul>
<li><code>attributes</code> the presence of a table field in <code>attributes</code> indicates
the intent to update the corresponding attribute.</li>
</ul>
<p>This method requires the <a class='link' href='#Rights.UPDATE_ATTRIBUTES'>Rights.UPDATE_ATTRIBUTES</a> right.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='#NodeAttributes'>NodeAttributes</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Node_UpdateAttributes_Result'>Node_UpdateAttributes_Result</a></code>
            </td>
        </tr></table>

### Sync {#Sync}

<p>Synchronizes updates to the node to the underlying media, if it exists.</p>
<p>This method will return when the filesystem server has flushed the
relevant updates to the underlying media, but does not guarantee the
underlying media has persisted the information, nor that any information
is committed to hardware. Clients may use <code>Sync</code> to ensure ordering
between operations.</p>
<p>This method does not require any rights.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Node_Sync_Result'>Node_Sync_Result</a></code>
            </td>
        </tr></table>

## DirectoryIterator {#DirectoryIterator}
*Defined in [fuchsia.io2/directory-iterator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/directory-iterator.fidl#9)*


### GetNext {#GetNext}

<p>Reads a collection of variably sized directory entries into a buffer.</p>
<p>The number of entries in a directory may be very large: akin to
calling read multiple times on a file, directories have a seek
offset which is updated on subsequent calls to <code>Enumerate</code>.
The caller should always use a receiving buffer size as large as the
maximum channel limit.</p>
<p>When the end of iteration is reached, the returned <code>entries</code> vector
will be empty.</p>
<p>This method does not require any rights, as the rights are checked
in the <a class='link' href='#Directory.Enumerate'>Directory.Enumerate</a> call.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#DirectoryIterator_GetNext_Result'>DirectoryIterator_GetNext_Result</a></code>
            </td>
        </tr></table>

## DirectoryWatcher {#DirectoryWatcher}
*Defined in [fuchsia.io2/directory-watcher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/directory-watcher.fidl#11)*

<p>DirectoryWatcher transmits messages from a filesystem server about
events happening in the filesystem. Clients can register new watchers
using the <a class='link' href='#Directory.Watch'>Directory.Watch</a> method, where they can
filter which events they want to receive notifications for.</p>

### GetNext {#GetNext}

<p>A hanging get to obtain the next batch of events.</p>
<p>The caller should always use a receiving buffer size as large as the
maximum channel limit.</p>
<p>Clients should attempt to maintain one in-flight <code>GetNext</code> call as much
as possible. If <code>GetNext</code> is not constantly polled, the filesystem
server might hit an upper limit on the number of buffered events,
resulting in dropping. Should this happen, the connection will be closed
with a <code>ZX_ERR_IO_OVERRUN</code> epitaph.</p>
<p>When the watched directory is deleted, this connection will be closed
with a <code>ZX_ERR_UNAVAILABLE</code> epitaph.
When the filesystem server is dying, this connection will be closed
with a <code>ZX_ERR_PEER_CLOSED</code> epitaph.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>events</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#DirectoryWatchedEvent'>DirectoryWatchedEvent</a>&gt;[8192]</code>
            </td>
        </tr></table>

## Directory {#Directory}
*Defined in [fuchsia.io2/directory.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/directory.fidl#10)*

<p>A <a class='link' href='#Node'>Node</a> that is capable of containing other nodes.</p>

### Reopen {#Reopen}

<p>Creates another connection to the same node.</p>
<ul>
<li><code>options</code> options applicable to both <code>Open</code> and <code>Reopen</code>,
including negotiating protocol and restricting rights.
See <a class='link' href='#ConnectionOptions'>ConnectionOptions</a>.</li>
<li><code>object_request</code> is the server end of a channel created for the new
connection. The caller may proceed to send messages on the
corresponding client end right away.</li>
</ul>
<p>For files, the cloned connection and the original connection have
independent seek offsets.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#ConnectionOptions'>ConnectionOptions</a></code>
            </td>
        </tr><tr>
            <td><code>object_request</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



### Close {#Close}

<p>Terminates the connection to the node.</p>
<p>After calling <code>Close</code>, the client must not send any other requests.
The result of <code>Close</code> arrives as an epitaph, where the channel is closed
by the server upon processing this operation.</p>
<p>Closing the client end of the channel should be semantically equivalent
to calling <code>Close</code> without monitoring the status epitaph.</p>
<p>This method does not require any rights.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Describe {#Describe}

<p>Returns extra connection information and auxiliary handles.</p>
<ul>
<li><code>query</code> specifies the fields in <code>ConnectionInfo</code> that the caller is
interested in.</li>
</ul>
<ul>
<li><code>info</code> see <a class='link' href='#ConnectionInfo'>ConnectionInfo</a> for details on the fields.</li>
</ul>
<p>When all known bits in <code>query</code> are set, the return value matches
the one from <a class='link' href='#OnConnectionInfo'>OnConnectionInfo</a>, as if the caller requested that event
using <a class='link' href='#ConnectionFlags.GET_CONNECTION_INFO'>ConnectionFlags.GET_CONNECTION_INFO</a>.</p>
<p>If the <code>Describe</code> operation fails, the connection is closed with the
associated error.</p>
<p>This method does not require any rights.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>query</code></td>
            <td>
                <code><a class='link' href='#ConnectionInfoQuery'>ConnectionInfoQuery</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#ConnectionInfo'>ConnectionInfo</a></code>
            </td>
        </tr></table>

### OnConnectionInfo {#OnConnectionInfo}

<p>An event produced eagerly by the server if requested by
<a class='link' href='#ConnectionFlags.GET_CONNECTION_INFO'>ConnectionFlags.GET_CONNECTION_INFO</a>. This event will be the
first message from the server, and is sent exactly once.</p>
<ul>
<li><code>info</code> See <a class='link' href='#ConnectionInfo'>ConnectionInfo</a> for details on the fields.
All members should be present.</li>
</ul>
<p>Different from <a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#OnOpen'>OnOpen</a>, an error during open/reopen is
always manifested as an epitaph.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#ConnectionInfo'>ConnectionInfo</a></code>
            </td>
        </tr></table>

### GetToken {#GetToken}

<p>Acquires a token which can be used to identify this connection at
a later point in time.</p>
<p>This method does not require any rights. Note that the token identifies
the connection, hence carries the rights information on this connection.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Node_GetToken_Result'>Node_GetToken_Result</a></code>
            </td>
        </tr></table>

### GetAttributes {#GetAttributes}

<p>Acquires information about the node.</p>
<p>The attributes of a node should be stable, independent of the
specific protocol used to access it.</p>
<ul>
<li><code>query</code> a bit-mask specifying which attributes to fetch. The server
should not return more than necessary.</li>
</ul>
<ul>
<li><code>attributes</code> the returned attributes.</li>
</ul>
<p>This method requires the <a class='link' href='#Rights.GET_ATTRIBUTES'>Rights.GET_ATTRIBUTES</a> right.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>query</code></td>
            <td>
                <code><a class='link' href='#NodeAttributesQuery'>NodeAttributesQuery</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Node_GetAttributes_Result'>Node_GetAttributes_Result</a></code>
            </td>
        </tr></table>

### UpdateAttributes {#UpdateAttributes}

<p>Updates information about the node.</p>
<ul>
<li><code>attributes</code> the presence of a table field in <code>attributes</code> indicates
the intent to update the corresponding attribute.</li>
</ul>
<p>This method requires the <a class='link' href='#Rights.UPDATE_ATTRIBUTES'>Rights.UPDATE_ATTRIBUTES</a> right.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='#NodeAttributes'>NodeAttributes</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Node_UpdateAttributes_Result'>Node_UpdateAttributes_Result</a></code>
            </td>
        </tr></table>

### Sync {#Sync}

<p>Synchronizes updates to the node to the underlying media, if it exists.</p>
<p>This method will return when the filesystem server has flushed the
relevant updates to the underlying media, but does not guarantee the
underlying media has persisted the information, nor that any information
is committed to hardware. Clients may use <code>Sync</code> to ensure ordering
between operations.</p>
<p>This method does not require any rights.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Node_Sync_Result'>Node_Sync_Result</a></code>
            </td>
        </tr></table>

### Open {#Open}

<p>Opens or creates a new node relative to this directory node.</p>
<ul>
<li><code>path</code> identifies the node to open.
If <code>path</code> contains multiple segments, then the directory is traversed,
one segment at a time, relative to the directory represented by this
connection.
See <a class='link' href='#Path'>Path</a> for what constitutes a valid path.
To open another connection to the current directory, use
<a class='link' href='#Node.Reopen'>Node.Reopen</a> instead.</li>
<li><code>mode</code> controls whether to open existing/create new etc.</li>
<li><code>options</code> additional options applicable to both <code>Open</code> and <code>Reopen</code>,
including negotiating protocol and restricting rights.
See <a class='link' href='#ConnectionOptions'>ConnectionOptions</a>.</li>
<li><code>object_request</code> is the server end of a channel created for the new
connection. The caller may proceed to send messages on the
corresponding client end right away.</li>
</ul>
<p>This method requires the following rights on the current connection:</p>
<ul>
<li><a class='link' href='#Rights.ENUMERATE'>Rights.ENUMERATE</a></li>
<li><a class='link' href='#Rights.TRAVERSE'>Rights.TRAVERSE</a></li>
</ul>
<p>Errors are presented as an epitaph on the <code>object_request</code> channel.</p>
<ul>
<li>error <code>ZX_ERR_ACCESS_DENIED</code> if the requested rights exceeds
what is allowed.</li>
<li>error <code>ZX_ERR_BAD_PATH</code> if <code>path</code> is invalid.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>path</code></td>
            <td>
                <code><a class='link' href='#Path'>Path</a></code>
            </td>
        </tr><tr>
            <td><code>mode</code></td>
            <td>
                <code><a class='link' href='#OpenMode'>OpenMode</a></code>
            </td>
        </tr><tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#ConnectionOptions'>ConnectionOptions</a></code>
            </td>
        </tr><tr>
            <td><code>object_request</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



### Unlink {#Unlink}

<p>Removes a child node from the this directory's list of entries.</p>
<p>Note: this does not guarantee that the underlying object is destroyed.
Although the link will be removed from the containing directory,
objects with multiple references (such as files which are still open)
will not actually be destroyed until all references are closed.</p>
<ul>
<li><code>path</code> identifies the node to be detached.
If <code>path</code> contains multiple segments, then the directory is traversed,
one segment at a time, relative to the directory represented by this
connection.</li>
</ul>
<ul>
<li>error <code>ZX_ERR_ACCESS_DENIED</code> if the connection does not have
<a class='link' href='#Rights.WRITE_BYTES'>Rights.WRITE_BYTES</a>.</li>
<li>error <code>ZX_ERR_NOT_SUPPORTED</code> if the underlying filesystem does not
support writing.</li>
<li>error <code>ZX_ERR_BAD_PATH</code> if <code>path</code> is invalid.</li>
<li>error <code>ZX_ERR_NOT_EMPTY</code> if <code>path</code> refers to a non-empty directory.</li>
<li>error <code>ZX_ERR_UNAVAILABLE</code> if <code>path</code> refers to a mount point,
containing a remote channel.</li>
</ul>
<p>Other errors may be returned for filesystem-specific reasons.</p>
<p>This method requires the following rights:</p>
<ul>
<li><a class='link' href='#Rights.ENUMERATE'>Rights.ENUMERATE</a></li>
<li><a class='link' href='#Rights.MODIFY_DIRECTORY'>Rights.MODIFY_DIRECTORY</a></li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>path</code></td>
            <td>
                <code><a class='link' href='#Path'>Path</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Directory_Unlink_Result'>Directory_Unlink_Result</a></code>
            </td>
        </tr></table>

### Enumerate {#Enumerate}

<p>Initiates a directory listing operation over the input channel,
starting at seek offset 0.</p>
<p>This method requires the <a class='link' href='#Rights.ENUMERATE'>Rights.ENUMERATE</a> right. If this right is
absent, <code>iterator</code> will be closed with a <code>ZX_ERR_ACCESS_DENIED</code> epitaph.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>iterator</code></td>
            <td>
                <code>request&lt;<a class='link' href='#DirectoryIterator'>DirectoryIterator</a>&gt;</code>
            </td>
        </tr></table>



### Rename {#Rename}

<p>Renames a node named <code>src</code> to the name <code>dst</code>, in a directory represented
by <code>dst_parent_token</code>.</p>
<p><code>src</code> and <code>dst</code> must be valid node names.
See <a class='link' href='#Name'>Name</a> for what constitutes a valid name.</p>
<p>This method requires the following rights on both the current
connection, and the connection identified by <code>dst_parent_token</code>:</p>
<ul>
<li>
<p><a class='link' href='#Rights.ENUMERATE'>Rights.ENUMERATE</a></p>
</li>
<li>
<p><a class='link' href='#Rights.MODIFY_DIRECTORY'>Rights.MODIFY_DIRECTORY</a></p>
</li>
<li>
<p>error <code>ZX_ERR_INVALID_ARGS</code> if <code>src</code> or <code>dst</code> is invalid.</p>
</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>src</code></td>
            <td>
                <code><a class='link' href='#Name'>Name</a></code>
            </td>
        </tr><tr>
            <td><code>dst_parent_token</code></td>
            <td>
                <code><a class='link' href='#Token'>Token</a></code>
            </td>
        </tr><tr>
            <td><code>dst</code></td>
            <td>
                <code><a class='link' href='#Name'>Name</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Directory_Rename_Result'>Directory_Rename_Result</a></code>
            </td>
        </tr></table>

### Link {#Link}

<p>Creates a link to a node named <code>src</code> by the name <code>dst</code>,
in a directory represented by <code>dst_parent_token</code>.</p>
<p>Directories cannot be linked, to prevent reference cycles.</p>
<p><code>src</code> and <code>dst</code> must be valid node names.
See <a class='link' href='#Name'>Name</a> for what constitutes a valid name.</p>
<p>This method requires the following rights on both the current
connection, and the connection identified by <code>dst_parent_token</code>:</p>
<ul>
<li>
<p><a class='link' href='#Rights.ENUMERATE'>Rights.ENUMERATE</a></p>
</li>
<li>
<p><a class='link' href='#Rights.MODIFY_DIRECTORY'>Rights.MODIFY_DIRECTORY</a></p>
</li>
<li>
<p>error <code>ZX_ERR_INVALID_ARGS</code> if <code>src</code> or <code>dst</code> is invalid.</p>
</li>
<li>
<p>error <code>ZX_ERR_INVALID_ARGS</code> if <code>src</code> is a directory.</p>
</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>src</code></td>
            <td>
                <code><a class='link' href='#Name'>Name</a></code>
            </td>
        </tr><tr>
            <td><code>dst_parent_token</code></td>
            <td>
                <code><a class='link' href='#Token'>Token</a></code>
            </td>
        </tr><tr>
            <td><code>dst</code></td>
            <td>
                <code><a class='link' href='#Name'>Name</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Directory_Link_Result'>Directory_Link_Result</a></code>
            </td>
        </tr></table>

### Watch {#Watch}

<p>Watches a directory, monitoring events for children being added or
removed on the server end of the <code>watcher</code> channel.</p>
<p>Mask specifies a bit mask of events to observe.</p>
<p>This method requires the <a class='link' href='#Rights.ENUMERATE'>Rights.ENUMERATE</a> right. If this right is
absent, <code>watcher</code> will be closed with a <code>ZX_ERR_ACCESS_DENIED</code> epitaph.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>mask</code></td>
            <td>
                <code><a class='link' href='#DirectoryWatchMask'>DirectoryWatchMask</a></code>
            </td>
        </tr><tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#DirectoryWatchOptions'>DirectoryWatchOptions</a></code>
            </td>
        </tr><tr>
            <td><code>watcher</code></td>
            <td>
                <code>request&lt;<a class='link' href='#DirectoryWatcher'>DirectoryWatcher</a>&gt;</code>
            </td>
        </tr></table>



## File {#File}
*Defined in [fuchsia.io2/file.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/file.fidl#21)*

<p>A <a class='link' href='#Node'>Node</a> which contains a sequence of bytes of definite
length.</p>

### Reopen {#Reopen}

<p>Creates another connection to the same node.</p>
<ul>
<li><code>options</code> options applicable to both <code>Open</code> and <code>Reopen</code>,
including negotiating protocol and restricting rights.
See <a class='link' href='#ConnectionOptions'>ConnectionOptions</a>.</li>
<li><code>object_request</code> is the server end of a channel created for the new
connection. The caller may proceed to send messages on the
corresponding client end right away.</li>
</ul>
<p>For files, the cloned connection and the original connection have
independent seek offsets.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#ConnectionOptions'>ConnectionOptions</a></code>
            </td>
        </tr><tr>
            <td><code>object_request</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



### Close {#Close}

<p>Terminates the connection to the node.</p>
<p>After calling <code>Close</code>, the client must not send any other requests.
The result of <code>Close</code> arrives as an epitaph, where the channel is closed
by the server upon processing this operation.</p>
<p>Closing the client end of the channel should be semantically equivalent
to calling <code>Close</code> without monitoring the status epitaph.</p>
<p>This method does not require any rights.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Describe {#Describe}

<p>Returns extra connection information and auxiliary handles.</p>
<ul>
<li><code>query</code> specifies the fields in <code>ConnectionInfo</code> that the caller is
interested in.</li>
</ul>
<ul>
<li><code>info</code> see <a class='link' href='#ConnectionInfo'>ConnectionInfo</a> for details on the fields.</li>
</ul>
<p>When all known bits in <code>query</code> are set, the return value matches
the one from <a class='link' href='#OnConnectionInfo'>OnConnectionInfo</a>, as if the caller requested that event
using <a class='link' href='#ConnectionFlags.GET_CONNECTION_INFO'>ConnectionFlags.GET_CONNECTION_INFO</a>.</p>
<p>If the <code>Describe</code> operation fails, the connection is closed with the
associated error.</p>
<p>This method does not require any rights.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>query</code></td>
            <td>
                <code><a class='link' href='#ConnectionInfoQuery'>ConnectionInfoQuery</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#ConnectionInfo'>ConnectionInfo</a></code>
            </td>
        </tr></table>

### OnConnectionInfo {#OnConnectionInfo}

<p>An event produced eagerly by the server if requested by
<a class='link' href='#ConnectionFlags.GET_CONNECTION_INFO'>ConnectionFlags.GET_CONNECTION_INFO</a>. This event will be the
first message from the server, and is sent exactly once.</p>
<ul>
<li><code>info</code> See <a class='link' href='#ConnectionInfo'>ConnectionInfo</a> for details on the fields.
All members should be present.</li>
</ul>
<p>Different from <a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#OnOpen'>OnOpen</a>, an error during open/reopen is
always manifested as an epitaph.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#ConnectionInfo'>ConnectionInfo</a></code>
            </td>
        </tr></table>

### GetToken {#GetToken}

<p>Acquires a token which can be used to identify this connection at
a later point in time.</p>
<p>This method does not require any rights. Note that the token identifies
the connection, hence carries the rights information on this connection.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Node_GetToken_Result'>Node_GetToken_Result</a></code>
            </td>
        </tr></table>

### GetAttributes {#GetAttributes}

<p>Acquires information about the node.</p>
<p>The attributes of a node should be stable, independent of the
specific protocol used to access it.</p>
<ul>
<li><code>query</code> a bit-mask specifying which attributes to fetch. The server
should not return more than necessary.</li>
</ul>
<ul>
<li><code>attributes</code> the returned attributes.</li>
</ul>
<p>This method requires the <a class='link' href='#Rights.GET_ATTRIBUTES'>Rights.GET_ATTRIBUTES</a> right.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>query</code></td>
            <td>
                <code><a class='link' href='#NodeAttributesQuery'>NodeAttributesQuery</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Node_GetAttributes_Result'>Node_GetAttributes_Result</a></code>
            </td>
        </tr></table>

### UpdateAttributes {#UpdateAttributes}

<p>Updates information about the node.</p>
<ul>
<li><code>attributes</code> the presence of a table field in <code>attributes</code> indicates
the intent to update the corresponding attribute.</li>
</ul>
<p>This method requires the <a class='link' href='#Rights.UPDATE_ATTRIBUTES'>Rights.UPDATE_ATTRIBUTES</a> right.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='#NodeAttributes'>NodeAttributes</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Node_UpdateAttributes_Result'>Node_UpdateAttributes_Result</a></code>
            </td>
        </tr></table>

### Sync {#Sync}

<p>Synchronizes updates to the node to the underlying media, if it exists.</p>
<p>This method will return when the filesystem server has flushed the
relevant updates to the underlying media, but does not guarantee the
underlying media has persisted the information, nor that any information
is committed to hardware. Clients may use <code>Sync</code> to ensure ordering
between operations.</p>
<p>This method does not require any rights.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Node_Sync_Result'>Node_Sync_Result</a></code>
            </td>
        </tr></table>

### Seek {#Seek}

<p>Moves the offset at which the next invocation of <a class='link' href='#Read'>Read</a> or <a class='link' href='#Write'>Write</a>
will occur. The seek offset is specific to each file connection.</p>
<ul>
<li>request <code>origin</code> the reference point where <code>offset</code> will be based on.</li>
<li>request <code>offset</code> the number of bytes to seek.</li>
</ul>
<ul>
<li>response <code>offset_from_start</code> the adjusted seek offset, from the start
of the file.</li>
</ul>
<p>This method does not require any rights.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>origin</code></td>
            <td>
                <code><a class='link' href='#SeekOrigin'>SeekOrigin</a></code>
            </td>
        </tr><tr>
            <td><code>offset</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#File_Seek_Result'>File_Seek_Result</a></code>
            </td>
        </tr></table>

### Read {#Read}

<p>Reads up to 'count' bytes at the seek offset.
The seek offset is moved forward by the number of bytes read.</p>
<h2>Invariants</h2>
<ul>
<li>The returned <code>data.length</code> will never be greater than <code>count</code>.</li>
<li>If <code>data.length</code> is less than <code>count</code>, it means that the seek offset
has reached the end of file as part of this operation.</li>
<li>If <code>data.length</code> is zero while <code>count</code> is not, it means that the
seek offset is already at or beyond the end of file, and no data could
be read.</li>
<li>If <code>count</code> is zero, the server should perform all the checks ensuring
read access without actually read anything, and return an empty
<code>data</code> vector.</li>
</ul>
<p>This method requires the <a class='link' href='#Rights.READ_BYTES'>Rights.READ_BYTES</a> right.</p>

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
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#File_Read_Result'>File_Read_Result</a></code>
            </td>
        </tr></table>

### Write {#Write}

<p>Writes data at the seek offset.
The seek offset is moved forward by the number of bytes written.
If the file is in append mode, the seek offset is first set to the end
of the file, followed by the write, in one atomic step.</p>
<p>The file size may grow if the seek offset plus <code>data.length</code> is beyond
the current end of file.</p>
<ul>
<li>request <code>data</code> the byte buffer to write to the file.</li>
</ul>
<ul>
<li>response <code>actual_count</code> the number of bytes written.</li>
</ul>
<h2>Invariants</h2>
<ul>
<li>The returned <code>actual_count</code> will never be greater than <code>data.length</code>.</li>
<li>If the server is unable to write all the data due to e.g. not enough
space, <code>actual_count</code> may be less than <code>data.length</code>.</li>
<li>If <code>data.length</code> is zero, the server should perform all the checks
ensuring write access without mutating the file. The seek offset
is still updated if in append mode.</li>
</ul>
<p>This method requires the <a class='link' href='#Rights.WRITE_BYTES'>Rights.WRITE_BYTES</a> right.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='#Transfer'>Transfer</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#File_Write_Result'>File_Write_Result</a></code>
            </td>
        </tr></table>

### ReadAt {#ReadAt}

<p>Reads up to 'count' bytes at the provided offset.
Does not affect the seek offset.</p>
<h2>Invariants</h2>
<ul>
<li>The returned <code>data.length</code> will never be greater than <code>count</code>.</li>
<li>If <code>data.length</code> is less than <code>count</code>, it means that <code>ReadAt</code> has hit
the end of file as part of this operation.</li>
<li>If <code>data.length</code> is zero while <code>count</code> is not, it means that <code>offset</code>
is at or past the end of file, and no data can be read.</li>
<li>If <code>count</code> is zero, the server should perform all the checks ensuring
read access without actually reading anything, and return an empty
<code>data</code> vector.</li>
</ul>
<p>This method requires the <a class='link' href='#Rights.READ_BYTES'>Rights.READ_BYTES</a> right.</p>

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
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#File_ReadAt_Result'>File_ReadAt_Result</a></code>
            </td>
        </tr></table>

### WriteAt {#WriteAt}

<p>Writes data at the provided offset.
Does not affect the seek offset.</p>
<p>The file size may grow if <code>offset</code> plus <code>data.length</code> is past the
current end of file.</p>
<ul>
<li>request <code>data</code> the byte buffer to write to the file.</li>
<li>request <code>offset</code> the offset from start of the file to begin writing.</li>
</ul>
<ul>
<li>response <code>actual_count</code> the number of bytes written.</li>
</ul>
<h2>Invariants</h2>
<ul>
<li>The returned <code>actual_count</code> will never be greater than <code>data.length</code>.</li>
<li>If the server is unable to write all the data due to e.g. not enough
space, <code>actual_count</code> may be less than <code>data.length</code>.</li>
<li>If <code>data.length</code> is zero, the server should perform all the checks
ensuring write access without mutating the file.</li>
</ul>
<p>This method requires the <a class='link' href='#Rights.WRITE_BYTES'>Rights.WRITE_BYTES</a> right.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='#Transfer'>Transfer</a></code>
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
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#File_WriteAt_Result'>File_WriteAt_Result</a></code>
            </td>
        </tr></table>

### Resize {#Resize}

<p>Shrinks or grows the file size to 'length' bytes.</p>
<p>If file size is reduced by this operation, the extra trailing data'
is discarded.
If file size is increased by this operation, the extended area appears
as if it was zeroed.</p>
<p>This method requires the <a class='link' href='#Rights.WRITE_BYTES'>Rights.WRITE_BYTES</a> right.</p>

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
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#File_Resize_Result'>File_Resize_Result</a></code>
            </td>
        </tr></table>

### GetMemRange {#GetMemRange}

<p>Acquires a <a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Range'>Range</a> representing this file, if
there is one, with the requested access rights.</p>
<ul>
<li>request <code>flags</code> a <a class='link' href='#VmoFlags'>VmoFlags</a> indicating the desired mode of access.</li>
</ul>
<ul>
<li>response <code>buffer</code> the requested <a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Range'>Range</a>.</li>
</ul>
<ul>
<li>error a <a class='link' href='#zx.status'>zx.status</a> value indicating the failure.</li>
</ul>
<p>This method requires the following rights:</p>
<ul>
<li><a class='link' href='#Rights.READ_BYTES'>Rights.READ_BYTES</a> if <code>flags</code> includes <a class='link' href='#VmoFlags.READ'>VmoFlags.READ</a>.</li>
<li><a class='link' href='#Rights.WRITE_BYTES'>Rights.WRITE_BYTES</a> if <code>flags</code> includes <a class='link' href='#VmoFlags.WRITE'>VmoFlags.WRITE</a>.</li>
<li><a class='link' href='#Rights.EXECUTE'>Rights.EXECUTE</a> if <code>flags</code> includes <a class='link' href='#VmoFlags.EXECUTE'>VmoFlags.EXECUTE</a>.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
            <td>
                <code><a class='link' href='#VmoFlags'>VmoFlags</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#File_GetMemRange_Result'>File_GetMemRange_Result</a></code>
            </td>
        </tr></table>

## Memory {#Memory}
*Defined in [fuchsia.io2/memory.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/memory.fidl#13)*

<p>A file-like node backed by a VMO.
No memory-specific methods are provided by this protocol.
The client should access it via the the <a class='link' href='#MemoryInfo.buffer'>MemoryInfo.buffer</a> object in
<a class='link' href='#Representation'>Representation</a>.</p>

### Reopen {#Reopen}

<p>Creates another connection to the same node.</p>
<ul>
<li><code>options</code> options applicable to both <code>Open</code> and <code>Reopen</code>,
including negotiating protocol and restricting rights.
See <a class='link' href='#ConnectionOptions'>ConnectionOptions</a>.</li>
<li><code>object_request</code> is the server end of a channel created for the new
connection. The caller may proceed to send messages on the
corresponding client end right away.</li>
</ul>
<p>For files, the cloned connection and the original connection have
independent seek offsets.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#ConnectionOptions'>ConnectionOptions</a></code>
            </td>
        </tr><tr>
            <td><code>object_request</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



### Close {#Close}

<p>Terminates the connection to the node.</p>
<p>After calling <code>Close</code>, the client must not send any other requests.
The result of <code>Close</code> arrives as an epitaph, where the channel is closed
by the server upon processing this operation.</p>
<p>Closing the client end of the channel should be semantically equivalent
to calling <code>Close</code> without monitoring the status epitaph.</p>
<p>This method does not require any rights.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Describe {#Describe}

<p>Returns extra connection information and auxiliary handles.</p>
<ul>
<li><code>query</code> specifies the fields in <code>ConnectionInfo</code> that the caller is
interested in.</li>
</ul>
<ul>
<li><code>info</code> see <a class='link' href='#ConnectionInfo'>ConnectionInfo</a> for details on the fields.</li>
</ul>
<p>When all known bits in <code>query</code> are set, the return value matches
the one from <a class='link' href='#OnConnectionInfo'>OnConnectionInfo</a>, as if the caller requested that event
using <a class='link' href='#ConnectionFlags.GET_CONNECTION_INFO'>ConnectionFlags.GET_CONNECTION_INFO</a>.</p>
<p>If the <code>Describe</code> operation fails, the connection is closed with the
associated error.</p>
<p>This method does not require any rights.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>query</code></td>
            <td>
                <code><a class='link' href='#ConnectionInfoQuery'>ConnectionInfoQuery</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#ConnectionInfo'>ConnectionInfo</a></code>
            </td>
        </tr></table>

### OnConnectionInfo {#OnConnectionInfo}

<p>An event produced eagerly by the server if requested by
<a class='link' href='#ConnectionFlags.GET_CONNECTION_INFO'>ConnectionFlags.GET_CONNECTION_INFO</a>. This event will be the
first message from the server, and is sent exactly once.</p>
<ul>
<li><code>info</code> See <a class='link' href='#ConnectionInfo'>ConnectionInfo</a> for details on the fields.
All members should be present.</li>
</ul>
<p>Different from <a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#OnOpen'>OnOpen</a>, an error during open/reopen is
always manifested as an epitaph.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#ConnectionInfo'>ConnectionInfo</a></code>
            </td>
        </tr></table>

### GetToken {#GetToken}

<p>Acquires a token which can be used to identify this connection at
a later point in time.</p>
<p>This method does not require any rights. Note that the token identifies
the connection, hence carries the rights information on this connection.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Node_GetToken_Result'>Node_GetToken_Result</a></code>
            </td>
        </tr></table>

### GetAttributes {#GetAttributes}

<p>Acquires information about the node.</p>
<p>The attributes of a node should be stable, independent of the
specific protocol used to access it.</p>
<ul>
<li><code>query</code> a bit-mask specifying which attributes to fetch. The server
should not return more than necessary.</li>
</ul>
<ul>
<li><code>attributes</code> the returned attributes.</li>
</ul>
<p>This method requires the <a class='link' href='#Rights.GET_ATTRIBUTES'>Rights.GET_ATTRIBUTES</a> right.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>query</code></td>
            <td>
                <code><a class='link' href='#NodeAttributesQuery'>NodeAttributesQuery</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Node_GetAttributes_Result'>Node_GetAttributes_Result</a></code>
            </td>
        </tr></table>

### UpdateAttributes {#UpdateAttributes}

<p>Updates information about the node.</p>
<ul>
<li><code>attributes</code> the presence of a table field in <code>attributes</code> indicates
the intent to update the corresponding attribute.</li>
</ul>
<p>This method requires the <a class='link' href='#Rights.UPDATE_ATTRIBUTES'>Rights.UPDATE_ATTRIBUTES</a> right.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='#NodeAttributes'>NodeAttributes</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Node_UpdateAttributes_Result'>Node_UpdateAttributes_Result</a></code>
            </td>
        </tr></table>

### Sync {#Sync}

<p>Synchronizes updates to the node to the underlying media, if it exists.</p>
<p>This method will return when the filesystem server has flushed the
relevant updates to the underlying media, but does not guarantee the
underlying media has persisted the information, nor that any information
is committed to hardware. Clients may use <code>Sync</code> to ensure ordering
between operations.</p>
<p>This method does not require any rights.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Node_Sync_Result'>Node_Sync_Result</a></code>
            </td>
        </tr></table>

## Node {#Node}
*Defined in [fuchsia.io2/node.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/node.fidl#12)*

<p>Node defines the minimal protocol for entities which can be accessed
in a filesystem.</p>

### Reopen {#Reopen}

<p>Creates another connection to the same node.</p>
<ul>
<li><code>options</code> options applicable to both <code>Open</code> and <code>Reopen</code>,
including negotiating protocol and restricting rights.
See <a class='link' href='#ConnectionOptions'>ConnectionOptions</a>.</li>
<li><code>object_request</code> is the server end of a channel created for the new
connection. The caller may proceed to send messages on the
corresponding client end right away.</li>
</ul>
<p>For files, the cloned connection and the original connection have
independent seek offsets.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#ConnectionOptions'>ConnectionOptions</a></code>
            </td>
        </tr><tr>
            <td><code>object_request</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



### Close {#Close}

<p>Terminates the connection to the node.</p>
<p>After calling <code>Close</code>, the client must not send any other requests.
The result of <code>Close</code> arrives as an epitaph, where the channel is closed
by the server upon processing this operation.</p>
<p>Closing the client end of the channel should be semantically equivalent
to calling <code>Close</code> without monitoring the status epitaph.</p>
<p>This method does not require any rights.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Describe {#Describe}

<p>Returns extra connection information and auxiliary handles.</p>
<ul>
<li><code>query</code> specifies the fields in <code>ConnectionInfo</code> that the caller is
interested in.</li>
</ul>
<ul>
<li><code>info</code> see <a class='link' href='#ConnectionInfo'>ConnectionInfo</a> for details on the fields.</li>
</ul>
<p>When all known bits in <code>query</code> are set, the return value matches
the one from <a class='link' href='#OnConnectionInfo'>OnConnectionInfo</a>, as if the caller requested that event
using <a class='link' href='#ConnectionFlags.GET_CONNECTION_INFO'>ConnectionFlags.GET_CONNECTION_INFO</a>.</p>
<p>If the <code>Describe</code> operation fails, the connection is closed with the
associated error.</p>
<p>This method does not require any rights.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>query</code></td>
            <td>
                <code><a class='link' href='#ConnectionInfoQuery'>ConnectionInfoQuery</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#ConnectionInfo'>ConnectionInfo</a></code>
            </td>
        </tr></table>

### OnConnectionInfo {#OnConnectionInfo}

<p>An event produced eagerly by the server if requested by
<a class='link' href='#ConnectionFlags.GET_CONNECTION_INFO'>ConnectionFlags.GET_CONNECTION_INFO</a>. This event will be the
first message from the server, and is sent exactly once.</p>
<ul>
<li><code>info</code> See <a class='link' href='#ConnectionInfo'>ConnectionInfo</a> for details on the fields.
All members should be present.</li>
</ul>
<p>Different from <a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#OnOpen'>OnOpen</a>, an error during open/reopen is
always manifested as an epitaph.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#ConnectionInfo'>ConnectionInfo</a></code>
            </td>
        </tr></table>

### GetToken {#GetToken}

<p>Acquires a token which can be used to identify this connection at
a later point in time.</p>
<p>This method does not require any rights. Note that the token identifies
the connection, hence carries the rights information on this connection.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Node_GetToken_Result'>Node_GetToken_Result</a></code>
            </td>
        </tr></table>

### GetAttributes {#GetAttributes}

<p>Acquires information about the node.</p>
<p>The attributes of a node should be stable, independent of the
specific protocol used to access it.</p>
<ul>
<li><code>query</code> a bit-mask specifying which attributes to fetch. The server
should not return more than necessary.</li>
</ul>
<ul>
<li><code>attributes</code> the returned attributes.</li>
</ul>
<p>This method requires the <a class='link' href='#Rights.GET_ATTRIBUTES'>Rights.GET_ATTRIBUTES</a> right.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>query</code></td>
            <td>
                <code><a class='link' href='#NodeAttributesQuery'>NodeAttributesQuery</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Node_GetAttributes_Result'>Node_GetAttributes_Result</a></code>
            </td>
        </tr></table>

### UpdateAttributes {#UpdateAttributes}

<p>Updates information about the node.</p>
<ul>
<li><code>attributes</code> the presence of a table field in <code>attributes</code> indicates
the intent to update the corresponding attribute.</li>
</ul>
<p>This method requires the <a class='link' href='#Rights.UPDATE_ATTRIBUTES'>Rights.UPDATE_ATTRIBUTES</a> right.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='#NodeAttributes'>NodeAttributes</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Node_UpdateAttributes_Result'>Node_UpdateAttributes_Result</a></code>
            </td>
        </tr></table>

### Sync {#Sync}

<p>Synchronizes updates to the node to the underlying media, if it exists.</p>
<p>This method will return when the filesystem server has flushed the
relevant updates to the underlying media, but does not guarantee the
underlying media has persisted the information, nor that any information
is committed to hardware. Clients may use <code>Sync</code> to ensure ordering
between operations.</p>
<p>This method does not require any rights.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Node_Sync_Result'>Node_Sync_Result</a></code>
            </td>
        </tr></table>

## Pipe {#Pipe}
*Defined in [fuchsia.io2/pipe.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/pipe.fidl#11)*

<p>A node for streaming unstructured data.
No pipe-specific methods are provided by this protocol. The client should
access the pipe via the socket object returned from the <code>PipeInfo</code> member
in <a class='link' href='#Representation'>Representation</a>.</p>

### Reopen {#Reopen}

<p>Creates another connection to the same node.</p>
<ul>
<li><code>options</code> options applicable to both <code>Open</code> and <code>Reopen</code>,
including negotiating protocol and restricting rights.
See <a class='link' href='#ConnectionOptions'>ConnectionOptions</a>.</li>
<li><code>object_request</code> is the server end of a channel created for the new
connection. The caller may proceed to send messages on the
corresponding client end right away.</li>
</ul>
<p>For files, the cloned connection and the original connection have
independent seek offsets.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#ConnectionOptions'>ConnectionOptions</a></code>
            </td>
        </tr><tr>
            <td><code>object_request</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



### Close {#Close}

<p>Terminates the connection to the node.</p>
<p>After calling <code>Close</code>, the client must not send any other requests.
The result of <code>Close</code> arrives as an epitaph, where the channel is closed
by the server upon processing this operation.</p>
<p>Closing the client end of the channel should be semantically equivalent
to calling <code>Close</code> without monitoring the status epitaph.</p>
<p>This method does not require any rights.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Describe {#Describe}

<p>Returns extra connection information and auxiliary handles.</p>
<ul>
<li><code>query</code> specifies the fields in <code>ConnectionInfo</code> that the caller is
interested in.</li>
</ul>
<ul>
<li><code>info</code> see <a class='link' href='#ConnectionInfo'>ConnectionInfo</a> for details on the fields.</li>
</ul>
<p>When all known bits in <code>query</code> are set, the return value matches
the one from <a class='link' href='#OnConnectionInfo'>OnConnectionInfo</a>, as if the caller requested that event
using <a class='link' href='#ConnectionFlags.GET_CONNECTION_INFO'>ConnectionFlags.GET_CONNECTION_INFO</a>.</p>
<p>If the <code>Describe</code> operation fails, the connection is closed with the
associated error.</p>
<p>This method does not require any rights.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>query</code></td>
            <td>
                <code><a class='link' href='#ConnectionInfoQuery'>ConnectionInfoQuery</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#ConnectionInfo'>ConnectionInfo</a></code>
            </td>
        </tr></table>

### OnConnectionInfo {#OnConnectionInfo}

<p>An event produced eagerly by the server if requested by
<a class='link' href='#ConnectionFlags.GET_CONNECTION_INFO'>ConnectionFlags.GET_CONNECTION_INFO</a>. This event will be the
first message from the server, and is sent exactly once.</p>
<ul>
<li><code>info</code> See <a class='link' href='#ConnectionInfo'>ConnectionInfo</a> for details on the fields.
All members should be present.</li>
</ul>
<p>Different from <a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#OnOpen'>OnOpen</a>, an error during open/reopen is
always manifested as an epitaph.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#ConnectionInfo'>ConnectionInfo</a></code>
            </td>
        </tr></table>

### GetToken {#GetToken}

<p>Acquires a token which can be used to identify this connection at
a later point in time.</p>
<p>This method does not require any rights. Note that the token identifies
the connection, hence carries the rights information on this connection.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Node_GetToken_Result'>Node_GetToken_Result</a></code>
            </td>
        </tr></table>

### GetAttributes {#GetAttributes}

<p>Acquires information about the node.</p>
<p>The attributes of a node should be stable, independent of the
specific protocol used to access it.</p>
<ul>
<li><code>query</code> a bit-mask specifying which attributes to fetch. The server
should not return more than necessary.</li>
</ul>
<ul>
<li><code>attributes</code> the returned attributes.</li>
</ul>
<p>This method requires the <a class='link' href='#Rights.GET_ATTRIBUTES'>Rights.GET_ATTRIBUTES</a> right.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>query</code></td>
            <td>
                <code><a class='link' href='#NodeAttributesQuery'>NodeAttributesQuery</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Node_GetAttributes_Result'>Node_GetAttributes_Result</a></code>
            </td>
        </tr></table>

### UpdateAttributes {#UpdateAttributes}

<p>Updates information about the node.</p>
<ul>
<li><code>attributes</code> the presence of a table field in <code>attributes</code> indicates
the intent to update the corresponding attribute.</li>
</ul>
<p>This method requires the <a class='link' href='#Rights.UPDATE_ATTRIBUTES'>Rights.UPDATE_ATTRIBUTES</a> right.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='#NodeAttributes'>NodeAttributes</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Node_UpdateAttributes_Result'>Node_UpdateAttributes_Result</a></code>
            </td>
        </tr></table>

### Sync {#Sync}

<p>Synchronizes updates to the node to the underlying media, if it exists.</p>
<p>This method will return when the filesystem server has flushed the
relevant updates to the underlying media, but does not guarantee the
underlying media has persisted the information, nor that any information
is committed to hardware. Clients may use <code>Sync</code> to ensure ordering
between operations.</p>
<p>This method does not require any rights.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Node_Sync_Result'>Node_Sync_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### DirectoryIterator_GetNext_Response {#DirectoryIterator_GetNext_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>entries</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#DirectoryEntry'>DirectoryEntry</a>&gt;[8192]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### IdleEvent {#IdleEvent}
*Defined in [fuchsia.io2/directory-watcher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/directory-watcher.fidl#67)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Directory_Unlink_Response {#Directory_Unlink_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Directory_Rename_Response {#Directory_Rename_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Directory_Link_Response {#Directory_Link_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### File_Seek_Response {#File_Seek_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>offset_from_start</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### File_Read_Response {#File_Read_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='#Transfer'>Transfer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### File_Write_Response {#File_Write_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>actual_count</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### File_ReadAt_Response {#File_ReadAt_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='#Transfer'>Transfer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### File_WriteAt_Response {#File_WriteAt_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>actual_count</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### File_Resize_Response {#File_Resize_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### File_GetMemRange_Response {#File_GetMemRange_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Range'>Range</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Node_GetToken_Response {#Node_GetToken_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>token</code></td>
            <td>
                <code><a class='link' href='#Token'>Token</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Node_GetAttributes_Response {#Node_GetAttributes_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='#NodeAttributes'>NodeAttributes</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Node_UpdateAttributes_Response {#Node_UpdateAttributes_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Node_Sync_Response {#Node_Sync_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>



## **ENUMS**

### OpenMode {#OpenMode}
Type: <code>uint32</code>

*Defined in [fuchsia.io2/directory.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/directory.fidl#131)*

<p>Options related to node creation during <a class='link' href='#Directory.Open'>Directory.Open</a>.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OPEN_EXISTING</code></td>
            <td><code>1</code></td>
            <td><p>Only succeed if the object exists.</p>
</td>
        </tr><tr>
            <td><code>MAYBE_CREATE</code></td>
            <td><code>2</code></td>
            <td><p>Create the object if it does not exist, otherwise open existing.
The check and the creation are performed in one atomic step.</p>
</td>
        </tr><tr>
            <td><code>ALWAYS_CREATE</code></td>
            <td><code>3</code></td>
            <td><p>Assert that the object does not exist, then create it.
The assertion and creation are performed in one atomic step.</p>
</td>
        </tr><tr>
            <td><code>OPEN_MOUNT_POINT</code></td>
            <td><code>268435456</code></td>
            <td><p>If the object is a mount point, open the local directory
instead of forwarding the request. The object must be a directory.</p>
<p>This option implies the behavior of <code>OPEN_EXISTING</code>.</p>
</td>
        </tr></table>

### SeekOrigin {#SeekOrigin}
Type: <code>uint32</code>

*Defined in [fuchsia.io2/file.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/file.fidl#142)*

<p>The reference point for updating the seek offset. See <a class='link' href='#File.Seek'>File.Seek</a>.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>START</code></td>
            <td><code>1</code></td>
            <td><p>Seek from the start of the file.
The seek offset will be set to <code>offset</code> bytes.
The seek offset cannot be negative in this case.</p>
</td>
        </tr><tr>
            <td><code>CURRENT</code></td>
            <td><code>2</code></td>
            <td><p>Seek from the current position in the file.
The seek offset will be the current seek offset plus <code>offset</code> bytes.</p>
</td>
        </tr><tr>
            <td><code>END</code></td>
            <td><code>3</code></td>
            <td><p>Seek from the end of the file.
The seek offset will be the file size plus <code>offset</code> bytes.</p>
</td>
        </tr></table>



## **TABLES**

### ConnectionInfo {#ConnectionInfo}


*Defined in [fuchsia.io2/connection-info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/connection-info.fidl#9)*

<p>Returns run-time information about a node that is specific to the
current connection.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>representation</code></td>
            <td>
                <code><a class='link' href='#Representation'>Representation</a></code>
            </td>
            <td><p>The active variant corresponds to one of the supported protocols
of the node, and represents the result of the connection-time
negotiation. Provides auxiliary handles if applicable.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>rights</code></td>
            <td>
                <code><a class='link' href='#Rights'>Rights</a></code>
            </td>
            <td><p>Information about the rights possessed by the current connection.
Note: <code>rights</code> limits the set of operations allowed on the connection,
but does not guarantee their availability. For example, one may have
the <a class='link' href='#Rights.EXECUTE'>Rights.EXECUTE</a> right on a file connection, but the file itself
does not have the <code>EXECUTE</code> ability, and hence cannot be executed.
See <a class='link' href='#ConnectionOptions.rights'>ConnectionOptions.rights</a>.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>available_operations</code></td>
            <td>
                <code><a class='link' href='#Operations'>Operations</a></code>
            </td>
            <td><p>The set of available operations on this channel. It is always the
intersection between the rights possessed by this connection, and the
abilities of the node. The value may be zero in the case of an empty
intersection.
See <a class='link' href='#ConnectionOptions.rights'>ConnectionOptions.rights</a>.</p>
</td>
        </tr></table>

### ConnectionOptions {#ConnectionOptions}


*Defined in [fuchsia.io2/connection-options.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/connection-options.fidl#8)*

<p>Options for <a class='link' href='#Directory.Open'>Directory.Open</a> and <a class='link' href='#Node.Reopen'>Node.Reopen</a>.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>flags</code></td>
            <td>
                <code><a class='link' href='#ConnectionFlags'>ConnectionFlags</a></code>
            </td>
            <td><p>Flags which can affect the behavior when opening and reopening.
If absent, assumes a default of zero.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>protocols</code></td>
            <td>
                <code><a class='link' href='#NodeProtocolSet'>NodeProtocolSet</a></code>
            </td>
            <td><p>Specifies the set of representations accepted by the client, to support
a form of protocol negotiation on the node being opened.
Refer to the definition of <a class='link' href='#NodeProtocolSet'>NodeProtocolSet</a> for more details.
It cannot be zero.</p>
<p>In addition, clients may assert the type of the object by setting
the protocol corresponding to the expected type:</p>
<ul>
<li>If the caller expected a directory but the node cannot be accessed
as a directory, the error is <code>ZX_ERR_NOT_DIR</code>.</li>
<li>If the caller expected a file but the node cannot be accessed as a
file, the error is <code>ZX_ERR_NOT_FILE</code>.</li>
<li>In other mismatched cases, the error is <code>ZX_ERR_WRONG_TYPE</code>.</li>
</ul>
<p>During <a class='link' href='#Directory.Open'>Directory.Open</a>, if a new object is to be created, <code>protocols</code>
determines the type of object to create; it must be present.
If a valid object type cannot be unambiguously inferred e.g.
both <code>DIRECTORY</code> and <code>FILE</code> were set, the request must fail.</p>
<p>During <a class='link' href='#Node.Reopen'>Node.Reopen</a>, clients may specify a different but compatible
<code>protocols</code> to do a &quot;protocol upgrade&quot;.</p>
<p>If more than one protocol is present in <code>protocols</code>, the resultant
protocol may become any one of them. Clients should specify
<a class='link' href='#ConnectionFlags.GET_CONNECTION_INFO'>ConnectionFlags.GET_CONNECTION_INFO</a> to receive a
<a class='link' href='#Node.OnConnectionInfo'>Node.OnConnectionInfo</a> event, in order to ascertain the protocol.</p>
<p>If absent, indicates that the caller accepts any type of node, and
the resulting protocol is unspecified.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>rights</code></td>
            <td>
                <code><a class='link' href='#Rights'>Rights</a></code>
            </td>
            <td><p>Requests the specified rights on the new connection. If absent, inherits
the same rights as the source connection.</p>
<h2>Rights Hierarchy</h2>
<p>Respecting principles of least privileges, <code>rights</code> must meet the
following restrictions:</p>
<ul>
<li>A connection must have nonzero rights.</li>
<li>Rights must never increase in a derived connection:
<ul>
<li>During <a class='link' href='#Directory.Open'>Directory.Open</a>, you may only request the same rights as
what the directory connection already has, or a subset of those.</li>
<li>During <a class='link' href='#Node.Reopen'>Node.Reopen</a>, similarly, you may only request the same or
a subset of rights possessed by the original connection.</li>
</ul>
</li>
<li>Exceeding those rights causes <code>object_request</code> to be closed with a
<code>ZX_ERR_ACCESS_DENIED</code> epitaph.</li>
</ul>
<p>The proper enforcement of the rights hierarchy is a powerful refinement
over the existing access control facilities offered by directory
sandboxing. The rights manipulation should be implemented mechanically
without knowledge of any specific rights, and servers should propagate
unknown bits members, to gracefully handle future rights extensions.</p>
<h2>Rights Inheritance</h2>
<p>Absent <code>rights</code> field means inheriting the same rights as the source.</p>
<ul>
<li>During <a class='link' href='#Node.Reopen'>Node.Reopen</a>, the new connection would have the same rights
as the connection where the <code>Reopen</code> call is made.</li>
<li>During <a class='link' href='#Directory.Open'>Directory.Open</a>, the connection would have the same
rights as the connection where the <code>Open</code> call is made.</li>
</ul>
<p>Note: <code>rights</code> limits the set of operations allowed on the new
connection, but does not guarantee their availability. For convenience,
clients may query the <a class='link' href='#ConnectionInfo.available_operations'>ConnectionInfo.available_operations</a> field on a
new connection, which is the intersection of the rights and abilities
and indicates the guaranteed set of available operations.</p>
<p>See <a class='link' href='#Rights'>Rights</a> and <a class='link' href='#Abilities'>Abilities</a>.</p>
</td>
        </tr></table>

### ConnectorInfo {#ConnectorInfo}


*Defined in [fuchsia.io2/connector.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/connector.fidl#12)*

<p>Auxiliary data for the connector representation of a node, used for
protocol discovery and connection.</p>
<p>It supports connecting to arbitrary protocols exported by the filesystem
server at a path, including ones that do not compose <a class='link' href='#Node'>Node</a>.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    </table>

### DebuglogInfo {#DebuglogInfo}


*Defined in [fuchsia.io2/debuglog.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/debuglog.fidl#17)*

<p>The debuglog representation of a node.
The selection of this variant in <a class='link' href='#Representation'>Representation</a> implies that the
connection speaks the <a class='link' href='#Debuglog'>Debuglog</a> protocol.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>debuglog</code></td>
            <td>
                <code>handle&lt;debuglog&gt;</code>
            </td>
            <td><p>The backing debuglog kernel object.</p>
</td>
        </tr></table>

### DeviceInfo {#DeviceInfo}


*Defined in [fuchsia.io2/deprecated.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/deprecated.fidl#23)*

<p>The object may be cast to the shared interface of devices.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>event</code></td>
            <td>
                <code>handle&lt;event&gt;</code>
            </td>
            <td><p>An optional event which transmits information about a device's state.</p>
<p>The <a class='link' href='#DeviceSignal'>DeviceSignal</a> values may be observed on this event.</p>
</td>
        </tr></table>

### TtyInfo {#TtyInfo}


*Defined in [fuchsia.io2/deprecated.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/deprecated.fidl#32)*

<p>The object may be cast to a Tty interface.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>event</code></td>
            <td>
                <code>handle&lt;event&gt;</code>
            </td>
            <td><p>An optional event which transmits information about a device's state.</p>
<p>The <a class='link' href='#DeviceSignal'>DeviceSignal</a> values may be observed on this event.</p>
</td>
        </tr></table>

### DirectoryEntry {#DirectoryEntry}


*Defined in [fuchsia.io2/directory-entry.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/directory-entry.fidl#7)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code><a class='link' href='#Name'>Name</a></code>
            </td>
            <td><p>Name of the entry.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>protocols</code></td>
            <td>
                <code><a class='link' href='#NodeProtocolSet'>NodeProtocolSet</a></code>
            </td>
            <td><p>Describes the kinds of representations supported by the entry.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>abilities</code></td>
            <td>
                <code><a class='link' href='#Abilities'>Abilities</a></code>
            </td>
            <td><p>Describes the kinds of operations supported by the entry.</p>
</td>
        </tr></table>

### DirectoryWatchOptions {#DirectoryWatchOptions}


*Defined in [fuchsia.io2/directory-watcher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/directory-watcher.fidl#31)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    </table>

### DirectoryInfo {#DirectoryInfo}


*Defined in [fuchsia.io2/directory.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/directory.fidl#154)*

<p>Auxiliary data for the directory representation of a node.
The selection of this variant in <a class='link' href='#Representation'>Representation</a> implies that the
connection speaks the <a class='link' href='#Directory'>Directory</a> protocol.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    </table>

### FileInfo {#FileInfo}


*Defined in [fuchsia.io2/file.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/file.fidl#182)*

<p>Auxiliary data for the file representation of a node.
The selection of this variant in <a class='link' href='#Representation'>Representation</a> implies that the
connection speaks the <a class='link' href='#File'>File</a> protocol.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>observer</code></td>
            <td>
                <code>handle&lt;event&gt;</code>
            </td>
            <td><p>An optional event which transmits information about an object's
readability or writability. This event relays information about the
underlying object, not the capability granted to client: this event
may be signalled &quot;readable&quot; on a connection that does not have
the capability to read.</p>
<p>This event will be present if the following conditions are met:</p>
<ul>
<li>The <code>available_operations</code> on the file connection is not empty.</li>
<li>The filesystem supports signalling readability/writability events.</li>
</ul>
<p>The <a class='link' href='#FileSignal'>FileSignal</a> values may be observed on this event.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>is_append</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Returns if the file is opened in append mode.
In append mode, the seek offset is moved to the end before every
write, the two steps performed in an atomic manner.</p>
</td>
        </tr></table>

### MemoryInfo {#MemoryInfo}


*Defined in [fuchsia.io2/memory.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/memory.fidl#21)*

<p>Auxiliary data for the memory object representation of a node.
The node is a file which is represented as a VMO.
The selection of this variant in <a class='link' href='#Representation'>Representation</a> implies that the
connection speaks the <a class='link' href='#Memory'>Memory</a> protocol.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Range'>Range</a></code>
            </td>
            <td><p>Although a VMO is returned as a part of this structure, that VMO may
back multiple files. To identify the logical portion of the VMO that
represents the single file, offset and size are also supplied.</p>
<p>If the range covers the entire VMO (i.e. the offset is zero and the
length matches the size of the VMO), then all clients must receive a
VMO with the same koid. This can be a duplicate of the same underlying
page-aligned VMO.</p>
<p>The rights on this VMO should correspond to the rights on the
node connection.</p>
</td>
        </tr></table>

### NodeAttributes {#NodeAttributes}


*Defined in [fuchsia.io2/node-attributes.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/node-attributes.fidl#15)*

<p>Objective information about a filesystem node.
See <a class='link' href='#Node.GetAttributes'>Node.GetAttributes</a> and <a class='link' href='#Node.UpdateAttributes'>Node.UpdateAttributes</a>.</p>
<p>The attributes of a node should be stable, independent of the
specific protocol used to access it.</p>
<p>If a particular attribute is not applicable or not supported,
filesystems should leave the corresponding field absent.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>protocols</code></td>
            <td>
                <code><a class='link' href='#NodeProtocolSet'>NodeProtocolSet</a></code>
            </td>
            <td><p>Describes the kinds of representations supported by the node.
Note: This is not the result of the connection-time negotiation,
which is conveyed via <code>representation</code>.</p>
<p>This attribute is read-only.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>abilities</code></td>
            <td>
                <code><a class='link' href='#Abilities'>Abilities</a></code>
            </td>
            <td><p>Describes the kinds of operations supported by the node.
Note: This is distinct from the rights used at connection time.</p>
<p>This attribute is read-only.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>content_size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Node size, in bytes.</p>
<p>This attribute is read-only.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>storage_size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Space needed to store the node (possibly larger than size), in bytes.</p>
<p>This attribute is read-only.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>link_count</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Number of hard links to the node. It must be at least one.</p>
<p>This attribute is read-only.</p>
</td>
        </tr><tr>
            <td>6</td>
            <td><code>creation_time</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Time of creation in nanoseconds since the Unix epoch, UTC.
It may be updated manually after creation.</p>
</td>
        </tr><tr>
            <td>7</td>
            <td><code>modification_time</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Time of last modification in nanoseconds since the Unix epoch, UTC.</p>
</td>
        </tr></table>

### PipeInfo {#PipeInfo}


*Defined in [fuchsia.io2/pipe.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/pipe.fidl#20)*

<p>The pipe representation of a node.
A pipe is a data streaming interface, commonly used for standard in/out.
There is no universal requirement as to if it is uni- or bi-directional.
The selection of this variant in <a class='link' href='#Representation'>Representation</a> implies that the
connection speaks the <a class='link' href='#Pipe'>Pipe</a> protocol.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>socket</code></td>
            <td>
                <code>handle&lt;socket&gt;</code>
            </td>
            <td><p>The backing socket transport for the pipe.
The rights on this socket should correspond to the rights on the
node connection.</p>
</td>
        </tr></table>

### PosixSocketInfo {#PosixSocketInfo}


*Defined in [fuchsia.io2/posix-socket.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/posix-socket.fidl#10)*

<p>Auxiliary data for the POSIX socket representation of a node.
The selection of this variant in <a class='link' href='#Representation'>Representation</a> implies that the
connection speaks the <a class='link' href='../fuchsia.posix.socket/'>fuchsia.posix.socket</a>/<a class='link' href='../fuchsia.posix.socket/#Control'>Control</a> protocol.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>socket</code></td>
            <td>
                <code>handle&lt;socket&gt;</code>
            </td>
            <td><p>The backing transport for the socket.
The rights on this socket should correspond to the rights on the
node connection.</p>
</td>
        </tr></table>



## **UNIONS**

### DirectoryIterator_GetNext_Result {#DirectoryIterator_GetNext_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#DirectoryIterator_GetNext_Response'>DirectoryIterator_GetNext_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### Directory_Unlink_Result {#Directory_Unlink_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Directory_Unlink_Response'>Directory_Unlink_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### Directory_Rename_Result {#Directory_Rename_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Directory_Rename_Response'>Directory_Rename_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### Directory_Link_Result {#Directory_Link_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Directory_Link_Response'>Directory_Link_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### File_Seek_Result {#File_Seek_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#File_Seek_Response'>File_Seek_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### File_Read_Result {#File_Read_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#File_Read_Response'>File_Read_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### File_Write_Result {#File_Write_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#File_Write_Response'>File_Write_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### File_ReadAt_Result {#File_ReadAt_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#File_ReadAt_Response'>File_ReadAt_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### File_WriteAt_Result {#File_WriteAt_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#File_WriteAt_Response'>File_WriteAt_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### File_Resize_Result {#File_Resize_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#File_Resize_Response'>File_Resize_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### File_GetMemRange_Result {#File_GetMemRange_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#File_GetMemRange_Response'>File_GetMemRange_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### Node_GetToken_Result {#Node_GetToken_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Node_GetToken_Response'>Node_GetToken_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### Node_GetAttributes_Result {#Node_GetAttributes_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Node_GetAttributes_Response'>Node_GetAttributes_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### Node_UpdateAttributes_Result {#Node_UpdateAttributes_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Node_UpdateAttributes_Response'>Node_UpdateAttributes_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### Node_Sync_Result {#Node_Sync_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Node_Sync_Response'>Node_Sync_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>



## **XUNIONS**

### Representation {#Representation}
*Defined in [fuchsia.io2/connection-info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/connection-info.fidl#57)*

<p>Describes how the connection should be handled, and provides auxiliary
handles and information for the connection where applicable.
Refer to <a class='link' href='#Node.Describe'>Node.Describe</a> and <a class='link' href='#Node.OnConnectionInfo'>Node.OnConnectionInfo</a>.</p>
<p>If handles are returned which offer alternative ways of access to the node,
the rights on the handles should correspond to the rights on the connection.</p>
<p>If the client specified more than one protocol in <code>protocols</code> during
<a class='link' href='#Directory.Open'>Directory.Open</a> or <a class='link' href='#Node.Reopen'>Node.Reopen</a>, the <a class='link' href='#Representation'>Representation</a> xunion carries
additionally the result of the connection-time negotiation via its tag.</p>
<p>The elements have one-to-one correspondence with the members of
<a class='link' href='#NodeProtocolSet'>NodeProtocolSet</a>.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>connector</code></td>
            <td>
                <code><a class='link' href='#ConnectorInfo'>ConnectorInfo</a></code>
            </td>
            <td><p>See <a class='link' href='#NodeProtocolSet.CONNECTOR'>NodeProtocolSet.CONNECTOR</a>.</p>
</td>
        </tr><tr>
            <td><code>directory</code></td>
            <td>
                <code><a class='link' href='#DirectoryInfo'>DirectoryInfo</a></code>
            </td>
            <td><p>See <a class='link' href='#NodeProtocolSet.DIRECTORY'>NodeProtocolSet.DIRECTORY</a>.</p>
</td>
        </tr><tr>
            <td><code>file</code></td>
            <td>
                <code><a class='link' href='#FileInfo'>FileInfo</a></code>
            </td>
            <td><p>See <a class='link' href='#NodeProtocolSet.FILE'>NodeProtocolSet.FILE</a>.</p>
</td>
        </tr><tr>
            <td><code>memory</code></td>
            <td>
                <code><a class='link' href='#MemoryInfo'>MemoryInfo</a></code>
            </td>
            <td><p>See <a class='link' href='#NodeProtocolSet.MEMORY'>NodeProtocolSet.MEMORY</a>.</p>
</td>
        </tr><tr>
            <td><code>posix_socket</code></td>
            <td>
                <code><a class='link' href='#PosixSocketInfo'>PosixSocketInfo</a></code>
            </td>
            <td><p>See <a class='link' href='#NodeProtocolSet.POSIX_SOCKET'>NodeProtocolSet.POSIX_SOCKET</a>.</p>
</td>
        </tr><tr>
            <td><code>pipe</code></td>
            <td>
                <code><a class='link' href='#PipeInfo'>PipeInfo</a></code>
            </td>
            <td><p>See <a class='link' href='#NodeProtocolSet.PIPE'>NodeProtocolSet.PIPE</a>.</p>
</td>
        </tr><tr>
            <td><code>debuglog</code></td>
            <td>
                <code><a class='link' href='#DebuglogInfo'>DebuglogInfo</a></code>
            </td>
            <td><p>See <a class='link' href='#NodeProtocolSet.DEBUGLOG'>NodeProtocolSet.DEBUGLOG</a>.</p>
</td>
        </tr><tr>
            <td><code>device</code></td>
            <td>
                <code><a class='link' href='#DeviceInfo'>DeviceInfo</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>tty</code></td>
            <td>
                <code><a class='link' href='#TtyInfo'>TtyInfo</a></code>
            </td>
            <td></td>
        </tr></table>

### DirectoryWatchedEvent {#DirectoryWatchedEvent}
*Defined in [fuchsia.io2/directory-watcher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/directory-watcher.fidl#35)*

<p>Events returned from <a class='link' href='#DirectoryWatcher.GetNext'>DirectoryWatcher.GetNext</a>.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>existing</code></td>
            <td>
                <code><a class='link' href='#DirectoryEntry'>DirectoryEntry</a></code>
            </td>
            <td><p>Indicates a node already existed in the directory when watching started.</p>
</td>
        </tr><tr>
            <td><code>idle</code></td>
            <td>
                <code><a class='link' href='#IdleEvent'>IdleEvent</a></code>
            </td>
            <td><p>Indicates that no more <code>existing</code> events will be sent.</p>
</td>
        </tr><tr>
            <td><code>added</code></td>
            <td>
                <code><a class='link' href='#DirectoryEntry'>DirectoryEntry</a></code>
            </td>
            <td><p>Indicates a node has been created (either new or moved) into a
directory.</p>
</td>
        </tr><tr>
            <td><code>removed</code></td>
            <td>
                <code><a class='link' href='#Name'>Name</a></code>
            </td>
            <td><p>Indicates a node has been removed (either deleted or moved) from the
directory.</p>
</td>
        </tr></table>



## **BITS**

### ConnectionInfoQuery {#ConnectionInfoQuery}
Type: <code>uint64</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>REPRESENTATION</td>
            <td>1</td>
            <td><p>Requests <a class='link' href='#ConnectionInfo.representation'>ConnectionInfo.representation</a>.</p>
</td>
        </tr><tr>
            <td>RIGHTS</td>
            <td>2</td>
            <td><p>Requests <a class='link' href='#ConnectionInfo.rights'>ConnectionInfo.rights</a>.</p>
</td>
        </tr><tr>
            <td>AVAILABLE_OPERATIONS</td>
            <td>4</td>
            <td><p>Requests <a class='link' href='#ConnectionInfo.available_operations'>ConnectionInfo.available_operations</a>.</p>
</td>
        </tr></table>

### NodeProtocolSet {#NodeProtocolSet}
Type: <code>uint64</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>CONNECTOR</td>
            <td>1</td>
            <td><p>The connector representation of a node.
The connection will speak either <a class='link' href='#Node'>Node</a>, or some custom
protocol, depending on the flags used during opening and reopening.</p>
</td>
        </tr><tr>
            <td>DIRECTORY</td>
            <td>2</td>
            <td><p>The directory representation of a node.
The connection will speak the <a class='link' href='#Directory'>Directory</a> protocol.</p>
</td>
        </tr><tr>
            <td>FILE</td>
            <td>4</td>
            <td><p>The file representation of a node.
The connection will speak the <a class='link' href='#File'>File</a> protocol.</p>
</td>
        </tr><tr>
            <td>MEMORY</td>
            <td>8</td>
            <td><p>The memory representation of a node. A memory object is a file whose
contents are explicitly backed by some VMO.
The connection will speak the <a class='link' href='#Memory'>Memory</a> protocol, and
<a class='link' href='#Representation'>Representation</a> would contain a <a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Range'>Range</a> object
representing the contents of the file.</p>
</td>
        </tr><tr>
            <td>POSIX_SOCKET</td>
            <td>16</td>
            <td><p>The POSIX socket representation of a node.
The connection will speak the <a class='link' href='../fuchsia.posix.socket/'>fuchsia.posix.socket</a>/<a class='link' href='../fuchsia.posix.socket/#Control'>Control</a> protocol.</p>
</td>
        </tr><tr>
            <td>PIPE</td>
            <td>32</td>
            <td><p>The pipe representation of a node.
The connection will speak the <a class='link' href='#Pipe'>Pipe</a> protocol.</p>
</td>
        </tr><tr>
            <td>DEBUGLOG</td>
            <td>64</td>
            <td><p>The debuglog representation of a node.
The connection will speak the <a class='link' href='#Debuglog'>Debuglog</a> protocol.</p>
</td>
        </tr><tr>
            <td>DEVICE</td>
            <td>268435456</td>
            <td></td>
        </tr><tr>
            <td>TTY</td>
            <td>536870912</td>
            <td></td>
        </tr></table>

### ConnectionFlags {#ConnectionFlags}
Type: <code>uint64</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>GET_CONNECTION_INFO</td>
            <td>1</td>
            <td><p>Requests that an <a class='link' href='#Node.OnConnectionInfo'>Node.OnConnectionInfo</a> event be sent as the first
message on the protocol request. Requests all fields in the
<a class='link' href='#ConnectionInfo'>ConnectionInfo</a> table. Doing so is more efficient than calling
<a class='link' href='#Node.Describe'>Node.Describe</a> later on the connection.</p>
</td>
        </tr><tr>
            <td>CONNECT</td>
            <td>2</td>
            <td><p>Connects to the exposed protocol if the node is a Connector.
It is an error to use this flag with other types of nodes.</p>
<p>If both <code>GET_CONNECTION_INFO</code> and <code>CONNECT</code> are specified, the channel
will receive exactly one <a class='link' href='#Node.OnConnectionInfo'>Node.OnConnectionInfo</a> event, after which
the protocol switches from <a class='link' href='#Node'>Node</a> to the intended protocol.
Message sent by the client prior to receiving <a class='link' href='#Node.OnConnectionInfo'>Node.OnConnectionInfo</a>
are queued and processed after the protocol switch.</p>
<p><code>CONNECT</code> cannot be supplied together with <code>APPEND</code>.
<code>CONNECT</code> cannot be supplied together with <code>TRUNCATE</code>.</p>
<p>Requires the <a class='link' href='#Rights.CONNECT'>Rights.CONNECT</a> right on the connection.</p>
</td>
        </tr><tr>
            <td>APPEND</td>
            <td>4</td>
            <td><p>Opens the node in append mode, i.e. the connection should seek to the
end of the node before every write.</p>
<p>If the node does not support appending, it should result in a
<code>ZX_ERR_NOT_SUPPORTED</code> epitaph.
Currently, only <a class='link' href='#NodeProtocolSet.FILE'>NodeProtocolSet.FILE</a> connections
may be configured for appending.</p>
</td>
        </tr><tr>
            <td>TRUNCATE</td>
            <td>8</td>
            <td><p>Truncates the object before usage, by setting its length to 0.
Requires the <a class='link' href='#Rights.WRITE_BYTES'>Rights.WRITE_BYTES</a> right on the connection.</p>
<p>If the node does not support truncating, it should result in a
<code>ZX_ERR_NOT_SUPPORTED</code> epitaph.</p>
</td>
        </tr></table>

### DeviceSignal {#DeviceSignal}
Type: <code>uint32</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>READABLE</td>
            <td>16777216</td>
            <td><p>Indicates the device is ready for reading.</p>
</td>
        </tr><tr>
            <td>WRITABLE</td>
            <td>33554432</td>
            <td><p>Indicates the device is ready for writing.</p>
</td>
        </tr><tr>
            <td>ERROR</td>
            <td>67108864</td>
            <td><p>Indicates the device has encountered an error state.</p>
</td>
        </tr><tr>
            <td>HANGUP</td>
            <td>134217728</td>
            <td><p>Indicates the device has hung up on the current connection.</p>
</td>
        </tr><tr>
            <td>OOB</td>
            <td>268435456</td>
            <td><p>Indicates an out-of-band state transition has occurred.</p>
</td>
        </tr></table>

### DirectoryWatchMask {#DirectoryWatchMask}
Type: <code>uint64</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>EXISTING</td>
            <td>1</td>
            <td><p>Requests transmission of <code>existing</code> events.</p>
</td>
        </tr><tr>
            <td>IDLE</td>
            <td>2</td>
            <td><p>Requests transmission of <code>idle</code> events.</p>
</td>
        </tr><tr>
            <td>ADDED</td>
            <td>4</td>
            <td><p>Requests transmission of <code>added</code> events.</p>
</td>
        </tr><tr>
            <td>REMOVED</td>
            <td>8</td>
            <td><p>Requests transmission of <code>removed</code> events.</p>
</td>
        </tr></table>

### VmoFlags {#VmoFlags}
Type: <code>uint64</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>READ</td>
            <td>1</td>
            <td><p>Requests that the VMO be readable.</p>
</td>
        </tr><tr>
            <td>WRITE</td>
            <td>2</td>
            <td><p>Requests that the VMO be writable.</p>
</td>
        </tr><tr>
            <td>EXECUTE</td>
            <td>4</td>
            <td></td>
        </tr><tr>
            <td>PRIVATE_CLONE</td>
            <td>65536</td>
            <td><p>Require a copy-on-write clone of the underlying VMO.
The request should fail if the VMO cannot be cloned.
May not be supplied with <code>SHARED_BUFFER</code>.</p>
</td>
        </tr><tr>
            <td>SHARED_BUFFER</td>
            <td>131072</td>
            <td><p>Require an exact (non-cloned) handle to the underlying VMO.
All clients using this flag would get a VMO with the same koid.
The request should fail if a handle to the exact VMO cannot be returned.
May not be supplied with <code>PRIVATE_CLONE</code>.</p>
</td>
        </tr></table>

### FileSignal {#FileSignal}
Type: <code>uint32</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>READABLE</td>
            <td>16777216</td>
            <td><p>Indicates the file is ready for reading.</p>
</td>
        </tr><tr>
            <td>WRITABLE</td>
            <td>33554432</td>
            <td><p>Indicates the file is ready for writing.</p>
</td>
        </tr></table>

### NodeAttributesQuery {#NodeAttributesQuery}
Type: <code>uint64</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>PROTOCOLS</td>
            <td>1</td>
            <td><p>Requests <a class='link' href='#NodeAttributes.protocols'>NodeAttributes.protocols</a>.</p>
</td>
        </tr><tr>
            <td>ABILITIES</td>
            <td>2</td>
            <td><p>Requests <a class='link' href='#NodeAttributes.abilities'>NodeAttributes.abilities</a>.</p>
</td>
        </tr><tr>
            <td>CONTENT_SIZE</td>
            <td>4</td>
            <td><p>Requests <a class='link' href='#NodeAttributes.content_size'>NodeAttributes.content_size</a>.</p>
</td>
        </tr><tr>
            <td>STORAGE_SIZE</td>
            <td>8</td>
            <td><p>Requests <a class='link' href='#NodeAttributes.storage_size'>NodeAttributes.storage_size</a>.</p>
</td>
        </tr><tr>
            <td>LINK_COUNT</td>
            <td>16</td>
            <td><p>Requests <a class='link' href='#NodeAttributes.link_count'>NodeAttributes.link_count</a>.</p>
</td>
        </tr><tr>
            <td>CREATION_TIME</td>
            <td>32</td>
            <td><p>Requests <a class='link' href='#NodeAttributes.creation_time'>NodeAttributes.creation_time</a>.</p>
</td>
        </tr><tr>
            <td>MODIFICATION_TIME</td>
            <td>64</td>
            <td><p>Requests <a class='link' href='#NodeAttributes.modification_time'>NodeAttributes.modification_time</a>.</p>
</td>
        </tr></table>

### Operations {#Operations}
Type: <code>uint64</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>CONNECT</td>
            <td>1</td>
            <td><p>Connecting to a service.</p>
</td>
        </tr><tr>
            <td>READ_BYTES</td>
            <td>2</td>
            <td><p>Reading from the byte contents of a node.</p>
</td>
        </tr><tr>
            <td>WRITE_BYTES</td>
            <td>4</td>
            <td><p>Writing to the byte contents of a node.</p>
</td>
        </tr><tr>
            <td>EXECUTE</td>
            <td>8</td>
            <td><p>Execute the byte contents of a node.</p>
</td>
        </tr><tr>
            <td>GET_ATTRIBUTES</td>
            <td>16</td>
            <td><p>Reading the attributes of a node.</p>
</td>
        </tr><tr>
            <td>UPDATE_ATTRIBUTES</td>
            <td>32</td>
            <td><p>Updating the attributes of a node.</p>
</td>
        </tr><tr>
            <td>ENUMERATE</td>
            <td>64</td>
            <td><p>Reading the list of entries in a directory.</p>
</td>
        </tr><tr>
            <td>TRAVERSE</td>
            <td>128</td>
            <td><p>Opening a node from a directory.</p>
<p>When used in <code>ConnectionOptions.rights</code>, it must be specified together
with <a class='link' href='#Rights.ENUMERATE'>Rights.ENUMERATE</a>, since one can always probe the directory
contents by opening children.</p>
</td>
        </tr><tr>
            <td>MODIFY_DIRECTORY</td>
            <td>256</td>
            <td><p>Modifying the list of entries in a directory.
For example: node creation, renaming, linking, unlinking, etc.</p>
<p>When used in <code>ConnectionOptions.rights</code>, it must be specified together
with <a class='link' href='#Rights.ENUMERATE'>Rights.ENUMERATE</a>, since one can always probe the directory
contents by triggering name conflicts during node creation.</p>
</td>
        </tr><tr>
            <td>ADMIN</td>
            <td>72057594037927936</td>
            <td></td>
        </tr></table>



## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="MAX_DIRECTORY_BATCH_SIZE">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/directory-entry.fidl#20">MAX_DIRECTORY_BATCH_SIZE</a></td>
            <td>
                    <code>8192</code>
                </td>
                <td><code>uint64</code></td>
            <td><p>The maximum number of directory entires or watcher events returned
in a batch by a hanging-get pattern.</p>
</td>
        </tr>
    <tr id="MAX_TRANSFER_SIZE">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/file.fidl#14">MAX_TRANSFER_SIZE</a></td>
            <td>
                    <code>8192</code>
                </td>
                <td><code>uint64</code></td>
            <td><p>The maximum I/O size that is allowed for read/write operations using
byte vectors.</p>
</td>
        </tr>
    <tr id="MAX_NAME_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/io2.fidl#25">MAX_NAME_LENGTH</a></td>
            <td>
                    <code>255</code>
                </td>
                <td><code>uint64</code></td>
            <td><p>The maximum length, in bytes, of a single filesystem component.</p>
</td>
        </tr>
    <tr id="MAX_PATH_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/io2.fidl#46">MAX_PATH_LENGTH</a></td>
            <td>
                    <code>4095</code>
                </td>
                <td><code>uint64</code></td>
            <td><p>The maximum length, in bytes, of a filesystem path.</p>
</td>
        </tr>
    
</table>



## **TYPE ALIASES**

<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr id="Transfer">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/file.fidl#17">Transfer</a></td>
            <td>
                <code>vector</code>[<code><a class='link' href='#MAX_TRANSFER_SIZE'>MAX_TRANSFER_SIZE</a></code>]</td>
            <td><p>The byte vector type used for read/write operations.</p>
</td>
        </tr><tr id="Name">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/io2.fidl#22">Name</a></td>
            <td>
                <code>string</code>[<code><a class='link' href='#MAX_NAME_LENGTH'>MAX_NAME_LENGTH</a></code>]</td>
            <td><p>The type for the name of a node, i.e. a single path component.
E.g. <code>foo</code></p>
<h2>Invariants</h2>
<p>A valid node name must meet the following criteria:</p>
<ul>
<li>It cannot be longer than <a class='link' href='#MAX_NAME_LENGTH'>MAX_NAME_LENGTH</a>.</li>
<li>It cannot be empty.</li>
<li>It cannot be &quot;..&quot; (dot-dot).</li>
<li>It cannot be &quot;.&quot; (single dot).</li>
<li>It cannot contain &quot;/&quot;.</li>
<li>It cannot contain embedded NUL.</li>
</ul>
</td>
        </tr><tr id="Path">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/io2.fidl#43">Path</a></td>
            <td>
                <code>string</code>[<code><a class='link' href='#MAX_PATH_LENGTH'>MAX_PATH_LENGTH</a></code>]</td>
            <td><p>A path is a string of one or more components, separated by &quot;/&quot;.
E.g. <code>foo/bar/baz</code></p>
<h2>Invariants</h2>
<p>A valid path must meet the following criteria:</p>
<ul>
<li>It cannot be empty.</li>
<li>It cannot be longer than <a class='link' href='#MAX_PATH_LENGTH'>MAX_PATH_LENGTH</a>.</li>
<li>It cannot have a leading &quot;/&quot;.</li>
<li>It cannot have a trailing &quot;/&quot;.</li>
<li>Each component must be a valid <a class='link' href='#Name'>Name</a>.</li>
</ul>
<p>Paths should be transformed into their canonical forms at client side.
For example, a client should convert <code>&quot;foo/bar/.././baz/&quot;</code> to <code>&quot;foo/baz&quot;</code>
before using it as a path.</p>
</td>
        </tr><tr id="Token">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/io2.fidl#50">Token</a></td>
            <td>
                <code>handle</code></td>
            <td><p>The type to identify a connection to a node.
It represents a capability: a reference to a node with associated rights.</p>
</td>
        </tr><tr id="Rights">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/rights-abilities.fidl#74">Rights</a></td>
            <td>
                <code>fuchsia.io2/Operations</code></td>
            <td><p>Rights are properties specific to a connection. They limit which operations
are allowed on a connection.</p>
<p>Invoking an operation without the corresponding right results in a
<code>ZX_ERR_ACCESS_DENIED</code> error.</p>
<p>Right Aliases - Useful constants for commonly used collections of rights.
Currently FIDL doesn't support expressions on assignment so these cannot
be defined. They are left here as documentation.</p>
<p>&quot;r*&quot; a collection of rights to read from a directory.
const Rights R_STAR_DIR = CONNECT | ENUMERATE | TRAVERSE |
READ_BYTES | GET_ATTRIBUTES;</p>
<p>&quot;w*&quot; a collection of rights to write to a directory.
const Rights W_STAR_DIR = CONNECT | ENUMERATE | TRAVERSE |
MODIFY_DIRECTORY | WRITE_BYTES |
UPDATE_ATTRIBUTES;</p>
<p>&quot;x*&quot; a collection of rights to execute from a directory.
const Rights X_STAR_DIR = CONNECT | ENUMERATE | TRAVERSE | EXECUTE;</p>
</td>
        </tr><tr id="Abilities">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-io2/rights-abilities.fidl#83">Abilities</a></td>
            <td>
                <code>fuchsia.io2/Operations</code></td>
            <td><p>Abilities are properties intrinsic to a node. They specify which operations
are supported by it.</p>
<p>Invoking an operation without corresponding support in the node results in a
<code>ZX_ERR_NOT_SUPPORTED</code> error.
Note that if both the access denied and the not supported error conditions
apply, the access denied case takes precedence.</p>
</td>
        </tr></table>

