[TOC]

# fuchsia.storage.ext4server


## **PROTOCOLS**

## Ext4Server {#Ext4Server}
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#178)*


### MountVmo {#MountVmo}

<p>Read the VMO content as an Ext4 image and return a channel to the
root of the mounted file system.</p>
<ul>
<li>request <code>source</code> is an Ext4 image to be served over the <code>root</code>
connection.</li>
<li>request <code>flags</code> is the same flags you can pass to
<a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#Directory.Open'>Directory.Open</a> call.  In particular
<a class='link' href='#OPEN_FLAG_DESCRIBE'>OPEN_FLAG_DESCRIBE</a> can be used to report mount errors.
Note that <a class='link' href='#MountVmoError'>MountVmoError</a> will contain a better
description of any error that may occur at the mount
time.</li>
<li>request <code>root</code> is the server end of a connection that will be
serving the root of the mounted image.</li>
</ul>
<ul>
<li>result <code>result</code> In case we could parse the image far enough to
read the root directory <a class='link' href='#MountVmoResult.success'>MountVmoResult.success</a> will be
returned.  Note that you may pipeline requests to the
<code>root</code> connection even before received a response.  In
case of an error one of the other values will be returned
and the <code>root</code> connection will be closed.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
        </tr><tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>root</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#Directory'>Directory</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#MountVmoResult'>MountVmoResult</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Success {#Success}
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#11)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### InvalidSuperBlock {#InvalidSuperBlock}
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#14)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>position</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Byte position in filesystem image.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### InvalidSuperBlockMagic {#InvalidSuperBlockMagic}
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#19)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>Magic number.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### BlockNumberOutOfBounds {#BlockNumberOutOfBounds}
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#24)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>block_number</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Block number.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### BlockSizeInvalid {#BlockSizeInvalid}
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#29)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>block_size</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Block size.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### InvalidBlockGroupDesc {#InvalidBlockGroupDesc}
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#34)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>position</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Byte position in filesystem image.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### InvalidINode {#InvalidINode}
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#39)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>inode_number</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>INode number.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### InvalidExtentHeader {#InvalidExtentHeader}
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#44)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### InvalidExtentHeaderMagic {#InvalidExtentHeaderMagic}
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#48)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>Magic number.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### InvalidExtent {#InvalidExtent}
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#53)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>position</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Byte position in filesystem image.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### ExtentUnexpectedLength {#ExtentUnexpectedLength}
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#58)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Size received.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>expected</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Size expected.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### InvalidDirEntry2 {#InvalidDirEntry2}
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#65)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>position</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Byte position in filesystem image.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### DirEntry2NonUtf8 {#DirEntry2NonUtf8}
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#70)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[255]</code>
            </td>
            <td><p>Data that was unable to be converted into UTF-8.
Limiting to 255 to match with the max filename length.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### InvalidInputPath {#InvalidInputPath}
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#76)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>Not implemented. Will be empty string.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### PathNotFound {#PathNotFound}
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#81)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>Path given.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### BadEntryType {#BadEntryType}
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#87)*



<p>Directory entry has bad type value.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td><p>Type value.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### BannedFeatureIncompat {#BannedFeatureIncompat}
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#93)*



<p>Feature Incompatible flag has banned flags.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Bitwise flags that are banned.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### RequiredFeatureIncompat {#RequiredFeatureIncompat}
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#99)*



<p>Feature Incompatible flag has missing flags.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Bitwise flags that are missing.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### Incompatible {#Incompatible}
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#104)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>msg</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>Message stating what is wrong.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### BadFile {#BadFile}
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#109)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>Path of file.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### BadDirectory {#BadDirectory}
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#114)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>Path of directory.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### ReaderReadError {#ReaderReadError}
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#119)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>position</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Byte position in filesystem image.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### ReaderOutOfBounds {#ReaderOutOfBounds}
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#124)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>position</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Byte position in filesystem image.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Size of image.</p>
</td>
            <td>No default</td>
        </tr>
</table>









## **XUNIONS**

### ParseError {#ParseError}
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#133)*

<p>Sub-result of an <a class='link' href='#Ext4Server.MountVmo'>Ext4Server.MountVmo</a> call denoting the actual error
that occurred in the reader.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>invalid_super_block</code></td>
            <td>
                <code><a class='link' href='#InvalidSuperBlock'>InvalidSuperBlock</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>invalid_super_block_magic</code></td>
            <td>
                <code><a class='link' href='#InvalidSuperBlockMagic'>InvalidSuperBlockMagic</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>block_number_out_of_bounds</code></td>
            <td>
                <code><a class='link' href='#BlockNumberOutOfBounds'>BlockNumberOutOfBounds</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>block_size_invalid</code></td>
            <td>
                <code><a class='link' href='#BlockSizeInvalid'>BlockSizeInvalid</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>invalid_block_group_desc</code></td>
            <td>
                <code><a class='link' href='#InvalidBlockGroupDesc'>InvalidBlockGroupDesc</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>invalid_inode</code></td>
            <td>
                <code><a class='link' href='#InvalidINode'>InvalidINode</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>invalid_extent_header</code></td>
            <td>
                <code><a class='link' href='#InvalidExtentHeader'>InvalidExtentHeader</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>invalid_extent_header_magic</code></td>
            <td>
                <code><a class='link' href='#InvalidExtentHeaderMagic'>InvalidExtentHeaderMagic</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>invalid_extent</code></td>
            <td>
                <code><a class='link' href='#InvalidExtent'>InvalidExtent</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>extent_unexpected_length</code></td>
            <td>
                <code><a class='link' href='#ExtentUnexpectedLength'>ExtentUnexpectedLength</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>invalid_dir_entry_2</code></td>
            <td>
                <code><a class='link' href='#InvalidDirEntry2'>InvalidDirEntry2</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>dir_entry_2_non_utf8</code></td>
            <td>
                <code><a class='link' href='#DirEntry2NonUtf8'>DirEntry2NonUtf8</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>invalid_input_path</code></td>
            <td>
                <code><a class='link' href='#InvalidInputPath'>InvalidInputPath</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>path_not_found</code></td>
            <td>
                <code><a class='link' href='#PathNotFound'>PathNotFound</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>bad_entry_type</code></td>
            <td>
                <code><a class='link' href='#BadEntryType'>BadEntryType</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>incompatible</code></td>
            <td>
                <code><a class='link' href='#Incompatible'>Incompatible</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>bad_file</code></td>
            <td>
                <code><a class='link' href='#BadFile'>BadFile</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>bad_directory</code></td>
            <td>
                <code><a class='link' href='#BadDirectory'>BadDirectory</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>reader_read_error</code></td>
            <td>
                <code><a class='link' href='#ReaderReadError'>ReaderReadError</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>reader_out_of_bounds</code></td>
            <td>
                <code><a class='link' href='#ReaderOutOfBounds'>ReaderOutOfBounds</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>required_feature_incompat</code></td>
            <td>
                <code><a class='link' href='#RequiredFeatureIncompat'>RequiredFeatureIncompat</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>banned_feature_incompat</code></td>
            <td>
                <code><a class='link' href='#BannedFeatureIncompat'>BannedFeatureIncompat</a></code>
            </td>
            <td></td>
        </tr></table>

### MountVmoResult {#MountVmoResult}
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#161)*

<p>Result of an <a class='link' href='#Ext4Server.MountVmo'>Ext4Server.MountVmo</a> call.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>success</code></td>
            <td>
                <code><a class='link' href='#Success'>Success</a></code>
            </td>
            <td><p>The server has managed to read the image far enough to load the
root directory and none of the early validation checks have failed.</p>
</td>
        </tr><tr>
            <td><code>vmo_read_failure</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td><p>Error reading the VMO.</p>
</td>
        </tr><tr>
            <td><code>parse_error</code></td>
            <td>
                <code><a class='link' href='#ParseError'>ParseError</a></code>
            </td>
            <td></td>
        </tr></table>







