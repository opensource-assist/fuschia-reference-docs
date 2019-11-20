[TOC]

# fuchsia.storage.ext4server


## **PROTOCOLS**

## Ext4Server {#Ext4Server}
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#46)*


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
                <code>handle&lt;vmo&gt;</code>
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
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#10)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### ParseFailure {#ParseFailure}
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#14)*



<p>Parsing of the image failed.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>position</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>details</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>









## **XUNIONS**

### MountVmoResult {#MountVmoResult}
*Defined in [fuchsia.storage.ext4server/ext4_server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/storage/ext4/server/fidl/ext4_server.fidl#28)*

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
                <code>int32</code>
            </td>
            <td><p>Error reading the VMO.</p>
</td>
        </tr><tr>
            <td><code>parse_failure</code></td>
            <td>
                <code><a class='link' href='#ParseFailure'>ParseFailure</a></code>
            </td>
            <td><p>Failure during the initial parsing of the image.</p>
</td>
        </tr></table>





