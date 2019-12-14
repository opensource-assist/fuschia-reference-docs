[TOC]

# fuchsia.images


## **PROTOCOLS**

## ImagePipe {#ImagePipe}
*Defined in [fuchsia.images/image_pipe.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.images/image_pipe.fidl#64)*

<p>ImagePipe is a mechanism for streaming shared images between a producer
and a consumer which may be running in different processes.</p>
<p>Conceptually, the image pipe maintains a table of image resources supplied
by the producer into which graphical content may be stored as well as a
presentation queue containing a sequence of images which the producer has
asked the consumer to present.</p>
<p>The presentation queue is initially empty.</p>
<p>Each entry in the presentation queue consists of an image together with a
pair of optional synchronization fences:</p>
<ul>
<li>Acquire fence: signaled by the producer when the image is ready to be consumed</li>
<li>Release fence: signaled by the consumer when the image is free to be freed or
modified by the producer</li>
</ul>
<p>The producer performs the following sequence of steps to present content:</p>
<ul>
<li>Allocate and add some number of images (often 2 or 3) to the image pipe
to establish a pool using <code>AddImage()</code>.</li>
<li>Obtain the next available image from the pool.</li>
<li>Ask the consumer to enqueue an image for presentation and provide fences
using <code>PresentImage()</code>.</li>
<li>Start rendering the image.</li>
<li>Signal the image's acquire fence when rendering is complete.</li>
<li>Loop to present more image, listen for signals on release fences to recycle
images back into the pool.</li>
</ul>
<p>The consumer performs the following sequence of steps for each image which
is enqueued in the presentation queue:</p>
<ul>
<li>Await signals on the image's acquire fence.</li>
<li>If the fence wait cannot be satisfied or if some other error is detected,
close the image pipe.
Otherwise, begin presenting the image's content.</li>
<li>Retire the previously presented image (if any) from the presentation queue
and signal its release fence when no longer needed.</li>
<li>Continue presenting the same image until the next one is ready.  Loop.</li>
</ul>
<p>If the producer wants to close the image pipe, it should:</p>
<ul>
<li>Close its side of the connection.</li>
<li>Wait on all release fences for buffers that it has submitted with
<code>PresentImage()</code>.</li>
<li>Proceed with resource cleanup.</li>
</ul>
<p>When the consumer detects the image pipe has closed, it should:</p>
<ul>
<li>Stop using/presenting any images from the pipe.</li>
<li>Unmap all VMOs associated with the images in the pipe.</li>
<li>Close all handles to the VMOs.</li>
<li>Signal all release fences for presented and queued buffers.</li>
<li>Close all handles to fences.</li>
<li>Close its side of the connection.</li>
</ul>
<p>When either party detects that a fence has been abandoned (remotely closed
without being signaled) it should assume that the associated image is in
an indeterminate state.  This will typically happen when the other party
(or one of its delegates) has crashed.  The safest course of action is to
close the image pipe, release all resources which were shared with the
other party, and re-establish the connection to recover.</p>

### AddImage {#AddImage}

<p>Adds an image resource to image pipe.</p>
<p>The <code>memory</code> is the handle of a memory object which contains the image
data.  It is valid to create multiple images backed by the same memory
object; they may even overlap.  Consumers must detect this and handle
it accordingly.  The <code>offset_bytes</code> indicates the offset within the
memory object at which the image data begins.  The <code>size_bytes</code>
indicates the amount of memory from <code>memory</code> that should be utilized.
The type of memory stored in the VMO is <code>memory_type</code> (e.g. GPU memory,
host memory).</p>
<p>The following errors will cause the connection to be closed:</p>
<ul>
<li><code>image_id</code> is already registered</li>
<li><code>image_info</code> represents a format not supported by the consumer</li>
<li><code>memory</code> is not a handle for a readable VMO</li>
<li>the image data expected at <code>offset_bytes</code> according to the <code>image_info</code>
exceeds the memory object's bounds</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>image_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>image_info</code></td>
            <td>
                <code><a class='link' href='#ImageInfo'>ImageInfo</a></code>
            </td>
        </tr><tr>
            <td><code>memory</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr><tr>
            <td><code>offset_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>size_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>memory_type</code></td>
            <td>
                <code><a class='link' href='#MemoryType'>MemoryType</a></code>
            </td>
        </tr></table>



### RemoveImage {#RemoveImage}

<p>Removes an image resource from the pipe.</p>
<p>The <code>image_id</code> is detached from the image resource and is free to be
reused to add a new image resource.</p>
<p>Removing an image from the image pipe does not affect the presentation
queue or the currently presented image.</p>
<p>The producer must wait for all release fences associated with the image to
be signaled before freeing or modifying the underlying memory object since
the image may still be in use in the presentation queue.</p>
<p>The following errors will cause the connection to be closed:</p>
<ul>
<li><code>image_id</code> does not reference a currently registered image resource</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>image_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### PresentImage {#PresentImage}

<p>Enqueues the specified image for presentation by the consumer.</p>
<p>The <code>acquire_fences</code> are a set of fences which must all be signaled by the
producer before the consumer presents the image.
The <code>release_fences</code> are set of fences which must all be signaled by the
consumer before it is safe for the producer to free or modify the image.
<code>presentation_time</code> specifies the time on or after which the
client would like the enqueued operations should take visible effect
(light up pixels on the screen), expressed in nanoseconds in the
<code>CLOCK_MONOTONIC</code> timebase.  Desired presentation times must be
monotonically non-decreasing.</p>
<p><code>presentation_info</code> returns timing information about the submitted frame
and future frames (see presentation_info.fidl).</p>
<p>The following errors will cause the connection to be closed:</p>
<ul>
<li><code>image_id</code> does not reference a currently registered image resource</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>image_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>presentation_time</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>acquire_fences</code></td>
            <td>
                <code>vector&lt;event&gt;</code>
            </td>
        </tr><tr>
            <td><code>release_fences</code></td>
            <td>
                <code>vector&lt;event&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>presentation_info</code></td>
            <td>
                <code><a class='link' href='#PresentationInfo'>PresentationInfo</a></code>
            </td>
        </tr></table>

## ImagePipe2 {#ImagePipe2}
*Defined in [fuchsia.images/image_pipe2.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.images/image_pipe2.fidl#71)*

<p>ImagePipe is a mechanism for streaming shared images between a producer
and a consumer which may be running in different processes.</p>
<p>Conceptually, the image pipe maintains a table of image resources supplied
by the producer into which graphical content may be stored as well as a
presentation queue containing a sequence of images which the producer has
asked the consumer to present.</p>
<p>The presentation queue is initially empty.</p>
<p>Each entry in the presentation queue consists of an image together with a
pair of optional synchronization fences:</p>
<ul>
<li>Acquire fence: signaled by the producer when the image is ready to be consumed</li>
<li>Release fence: signaled by the consumer when the image is free to be freed or
modified by the producer</li>
</ul>
<p>The producer performs the following sequence of steps to present content:</p>
<ul>
<li>Allocate and add some number of BufferCollections to the image pipe to allow
consumer to set constraints.</li>
<li>Allocate and add some number of images (often 2 or 3) to the image pipe
to establish a pool using <code>AddImage()</code>.</li>
<li>Obtain the next available image from the pool.</li>
<li>Ask the consumer to enqueue an image for presentation and provide fences
using <code>PresentImage()</code>.</li>
<li>Start rendering the image.</li>
<li>Signal the image's acquire fence when rendering is complete.</li>
<li>Loop to present more image, listen for signals on release fences to recycle
images back into the pool.</li>
</ul>
<p>The consumer performs the following sequence of steps for each image which
is enqueued in the presentation queue:</p>
<ul>
<li>Await signals on the image's acquire fence.</li>
<li>If the fence wait cannot be satisfied or if some other error is detected,
close the image pipe.
Otherwise, begin presenting the image's content.</li>
<li>Retire the previously presented image (if any) from the presentation queue
and signal its release fence when no longer needed.</li>
<li>Continue presenting the same image until the next one is ready.  Loop.</li>
</ul>
<p>If the producer wants to close the image pipe, it should:</p>
<ul>
<li>Close its side of the connection.</li>
<li>Wait on all release fences for buffers that it has submitted with
<code>PresentImage()</code>.</li>
<li>Proceed with resource cleanup.</li>
</ul>
<p>When the consumer detects the image pipe has closed, it should:</p>
<ul>
<li>Stop using/presenting any images from the pipe.</li>
<li>Unmap all memory objects associated with the images in the pipe.</li>
<li>Close all BufferCollection resources.</li>
<li>Signal all release fences for presented and queued buffers.</li>
<li>Close all handles to fences.</li>
<li>Close its side of the connection.</li>
</ul>
<p>When either party detects that a fence has been abandoned (remotely closed
without being signaled) it should assume that the associated image is in
an indeterminate state.  This will typically happen when the other party
(or one of its delegates) has crashed.  The safest course of action is to
close the image pipe, release all resources which were shared with the
other party, and re-establish the connection to recover.</p>

### AddBufferCollection {#AddBufferCollection}

<p>Adds a BufferCollection resource to the image pipe.</p>
<p>The producer is expected to set constraints on this resource for images added
via <code>AddImage()</code>. The consumer can set its constraints on
<code>buffer_collection_token</code> before or after. Note that the buffers won’t be
allocated until all BufferCollectionToken instances are used to set
constraints, on both the producer and consumer side. See collection.fidl for
details.</p>
<p>The following errors will cause the connection to be closed:</p>
<ul>
<li><code>buffer_collection_id</code> is already registered</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer_collection_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>buffer_collection_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sysmem/'>fuchsia.sysmem</a>/<a class='link' href='../fuchsia.sysmem/#BufferCollectionToken'>BufferCollectionToken</a></code>
            </td>
        </tr></table>



### AddImage {#AddImage}

<p>Adds an image resource to image pipe.</p>
<p><code>buffer_collection_id</code> refers to the BufferCollectionToken instance that is
registered via <code>AddBufferCollection()</code>. The underlying memory objects allocated
are used to address to the image data. <code>buffer_collection_id</code> refers to the
index of the memory object allocated in BufferCollection.</p>
<p><code>image_format</code> specifiies image properties. <code>coded_width</code> and <code>coded_height</code> are
used to set image dimensions.</p>
<p>It is valid to create multiple images backed by the same memory object; they
may even overlap.  Consumers must detect this and handle it accordingly.</p>
<p>The following errors will cause the connection to be closed:</p>
<ul>
<li><code>image_id</code> is already registered</li>
<li><code>buffer_collection_id</code> refers to an unregistered BufferCollection.</li>
<li><code>buffer_collection_index</code> points to a resource index out of the initialized
BufferCollection bounds</li>
<li>No resource is allocated in the registered BufferCollection.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>image_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>buffer_collection_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>buffer_collection_index</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>image_format</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sysmem/'>fuchsia.sysmem</a>/<a class='link' href='../fuchsia.sysmem/#ImageFormat_2'>ImageFormat_2</a></code>
            </td>
        </tr></table>



### RemoveBufferCollection {#RemoveBufferCollection}

<p>Removes a BufferCollection resource from the pipe.</p>
<p>The <code>buffer_collection_id</code> resource is detached as well as all Images that are
associated with that BufferCollection. Leads to the same results as calling
<code>RemoveImage()</code> on all Images for <code>buffer_collection_id</code>.</p>
<p>The producer must wait for all release fences associated with the Images to
be signaled before freeing or modifying the underlying memory object since
the image may still be in use in the presentation queue.</p>
<p>The following errors will cause the connection to be closed:</p>
<ul>
<li><code>buffer_collection_id</code> does not reference a currently registered BufferCollection</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer_collection_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### RemoveImage {#RemoveImage}

<p>Removes an image resource from the pipe.</p>
<p>The <code>image_id</code> is detached from the image resource and is free to be
reused to add a new image resource.</p>
<p>Removing an image from the image pipe does not affect the presentation
queue or the currently presented image.</p>
<p>The producer must wait for all release fences associated with the image to
be signaled before freeing or modifying the underlying memory object since
the image may still be in use in the presentation queue.</p>
<p>The following errors will cause the connection to be closed:</p>
<ul>
<li><code>image_id</code> does not reference a currently registered image resource</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>image_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### PresentImage {#PresentImage}

<p>Enqueues the specified image for presentation by the consumer.</p>
<p>The <code>acquire_fences</code> are a set of fences which must all be signaled by the
producer before the consumer presents the image.
The <code>release_fences</code> are set of fences which must all be signaled by the
consumer before it is safe for the producer to free or modify the image.
<code>presentation_time</code> specifies the time on or after which the
client would like the enqueued operations should take visible effect
(light up pixels on the screen), expressed in nanoseconds in the
<code>CLOCK_MONOTONIC</code> timebase.  Desired presentation times must be
monotonically non-decreasing.</p>
<p><code>presentation_info</code> returns timing information about the submitted frame
and future frames (see presentation_info.fidl).</p>
<p>The producer may decide not to signal <code>acquire_fences</code> for an image.
In that case, if a later image is enqueued and later image’s
<code>presentation_time</code> is reached, the consumer presents the later image when
later image’s <code>acquire_fences</code> are signaled. The consumer also signals
earlier image’s <code>release_fences</code> and removes it from the presentation queue.
This sequence works as a cancellation mechanism.</p>
<p>The following errors will cause the connection to be closed:</p>
<ul>
<li><code>image_id</code> does not reference a currently registered image resource</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>image_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>presentation_time</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>acquire_fences</code></td>
            <td>
                <code>vector&lt;event&gt;[16]</code>
            </td>
        </tr><tr>
            <td><code>release_fences</code></td>
            <td>
                <code>vector&lt;event&gt;[16]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>presentation_info</code></td>
            <td>
                <code><a class='link' href='#PresentationInfo'>PresentationInfo</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### EncodedImage {#EncodedImage}
*Defined in [fuchsia.images/encoded_image.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.images/encoded_image.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
            <td><p>The vmo.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The size of the image in the vmo in bytes.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### ImageInfo {#ImageInfo}
*Defined in [fuchsia.images/image_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.images/image_info.fidl#117)*



<p>Information about a graphical image (texture) including its format and size.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>transform</code></td>
            <td>
                <code><a class='link' href='#Transform'>Transform</a></code>
            </td>
            <td><p>Specifies if the image should be mirrored before displaying.</p>
</td>
            <td><a class='link' href='#Transform.NORMAL'>Transform.NORMAL</a></td>
        </tr><tr>
            <td><code>width</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>The width and height of the image in pixels.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>stride</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>The number of bytes per row in the image buffer.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>pixel_format</code></td>
            <td>
                <code><a class='link' href='#PixelFormat'>PixelFormat</a></code>
            </td>
            <td><p>The pixel format of the image.</p>
</td>
            <td><a class='link' href='#PixelFormat.BGRA_8'>PixelFormat.BGRA_8</a></td>
        </tr><tr>
            <td><code>color_space</code></td>
            <td>
                <code><a class='link' href='#ColorSpace'>ColorSpace</a></code>
            </td>
            <td><p>The pixel color space.</p>
</td>
            <td><a class='link' href='#ColorSpace.SRGB'>ColorSpace.SRGB</a></td>
        </tr><tr>
            <td><code>tiling</code></td>
            <td>
                <code><a class='link' href='#Tiling'>Tiling</a></code>
            </td>
            <td><p>The pixel arrangement in memory.</p>
</td>
            <td><a class='link' href='#Tiling.LINEAR'>Tiling.LINEAR</a></td>
        </tr><tr>
            <td><code>alpha_format</code></td>
            <td>
                <code><a class='link' href='#AlphaFormat'>AlphaFormat</a></code>
            </td>
            <td><p>Specifies the interpretion of the alpha channel, if one exists.</p>
</td>
            <td><a class='link' href='#AlphaFormat.OPAQUE'>AlphaFormat.OPAQUE</a></td>
        </tr>
</table>

### PresentationInfo {#PresentationInfo}
*Defined in [fuchsia.images/presentation_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.images/presentation_info.fidl#10)*



<p>Information returned by methods such as <code>ImagePipe.PresentImage()</code> and
<code>Session.Present()</code>, when the consumer begins preparing the first frame
which includes the presented content.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>presentation_time</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The actual time at which the enqueued operations are anticipated to take
visible effect, expressed in nanoseconds in the <code>CLOCK_MONOTONIC</code>
timebase.</p>
<p>This value increases monotonically with each new frame, typically in
increments of the <code>presentation_interval</code>.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>presentation_interval</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The nominal amount of time which is anticipated to elapse between
successively presented frames, expressed in nanoseconds.  When rendering
to a display, the interval will typically be derived from the display
refresh rate.</p>
<p>This value is non-zero.  It may vary from time to time, such as when
changing display modes.</p>
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### PixelFormat {#PixelFormat}
Type: <code>uint32</code>

*Defined in [fuchsia.images/image_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.images/image_info.fidl#8)*

<p>Specifies how pixels are represented in the image buffer.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>BGRA_8</code></td>
            <td><code>0</code></td>
            <td><p>BGRA_8</p>
<p>A 32-bit four-component unsigned integer format.
Byte order: B, G, R, A (little-endian ARGB packed 32-bit word).
Equivalent to Skia <code>kBGRA_8888_SkColorType</code> color type.
Equivalent to Zircon <code>ARGB_8888</code> pixel format on little-endian arch.</p>
</td>
        </tr><tr>
            <td><code>YUY2</code></td>
            <td><code>1</code></td>
            <td><p>YUY2</p>
<p>4:2:2 (2x down-sampled UV horizontally; full res UV vertically)</p>
<p>A 32-bit component that contains information for 2 pixels:
Byte order: Y1, U, Y2, V
Unpacks to 2 RGB pixels, where RGB1 = func(Y1, U, V)
and RGB2 = func(Y2, U, V)
Equivalent to YUV422</p>
</td>
        </tr><tr>
            <td><code>NV12</code></td>
            <td><code>2</code></td>
            <td><p>NV12</p>
<p>4:2:0 (2x down-sampled UV in both directions)</p>
<p>Offset 0:
8 bit per pixel Y plane with bytes YYY.
Offset height * stride:
8 bit UV data interleaved bytes as UVUVUV.</p>
<p>Y plane has line stride &gt;= width.</p>
<p>In this context, both width and height are required to be even.</p>
<p>The UV data is separated into &quot;lines&quot;, with each &quot;line&quot; having same byte
width as a line of Y data, and same &quot;line&quot; stride as Y data's line stride.
The UV data has height / 2 &quot;lines&quot;.</p>
<p>In converting to RGB, the UV data gets up-scaled by 2x in both directions
overall.  This comment is intentionally silent on exactly how UV up-scaling
phase/filtering/signal processing works, as it's a complicated topic that
can vary by implementation, typically trading off speed and quality of the
up-scaling.  See comments in relevant conversion code for approach taken
by any given convert path.  The precise relative phase of the UV data is
not presently conveyed.</p>
</td>
        </tr><tr>
            <td><code>YV12</code></td>
            <td><code>3</code></td>
            <td><p>YV12</p>
<p>Like I420, except with V and U swapped.</p>
<p>4:2:0 (2x down-sampled UV in both directions)</p>
<p>Offset 0:
8 bit per pixel Y plane with bytes YYY.
Offset height * stride:
8 bit V data with uv_stride = stride / 2
Offset height * stride + uv_stride * height / 2:
8 bit U data with uv_stride = stride / 2</p>
<p>Y plane has line stride &gt;= width.</p>
<p>Both width and height are required to be even.</p>
</td>
        </tr></table>

### ColorSpace {#ColorSpace}
Type: <code>uint32</code>

*Defined in [fuchsia.images/image_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.images/image_info.fidl#74)*

<p>Specifies how pixel color information should be interpreted.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SRGB</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr></table>

### Tiling {#Tiling}
Type: <code>uint32</code>

*Defined in [fuchsia.images/image_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.images/image_info.fidl#79)*

<p>Specifies how pixels are arranged in memory.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>LINEAR</code></td>
            <td><code>0</code></td>
            <td><p>Pixels are packed linearly.
Equivalent to <code>VK_IMAGE_TILING_LINEAR</code>.</p>
</td>
        </tr><tr>
            <td><code>GPU_OPTIMAL</code></td>
            <td><code>1</code></td>
            <td><p>Pixels are packed in a GPU-dependent optimal format.
Equivalent to <code>VK_IMAGE_TILING_OPTIMAL</code>.</p>
</td>
        </tr></table>

### AlphaFormat {#AlphaFormat}
Type: <code>uint32</code>

*Defined in [fuchsia.images/image_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.images/image_info.fidl#90)*

<p>Specifies how alpha information should be interpreted.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OPAQUE</code></td>
            <td><code>0</code></td>
            <td><p>Image is considered to be opaque.  Alpha channel is ignored.
Blend function is: src.RGB</p>
</td>
        </tr><tr>
            <td><code>PREMULTIPLIED</code></td>
            <td><code>1</code></td>
            <td><p>Color channels have been premultiplied by alpha.
Blend function is: src.RGB + (dest.RGB * (1 - src.A))</p>
</td>
        </tr><tr>
            <td><code>NON_PREMULTIPLIED</code></td>
            <td><code>2</code></td>
            <td><p>Color channels have not been premultiplied by alpha.
Blend function is: (src.RGB * src.A) + (dest.RGB * (1 - src.A))</p>
</td>
        </tr></table>

### Transform {#Transform}
Type: <code>uint32</code>

*Defined in [fuchsia.images/image_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.images/image_info.fidl#102)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NORMAL</code></td>
            <td><code>0</code></td>
            <td><p>Pixels are displayed normally.</p>
</td>
        </tr><tr>
            <td><code>FLIP_HORIZONTAL</code></td>
            <td><code>1</code></td>
            <td><p>Pixels are mirrored left-right.</p>
</td>
        </tr><tr>
            <td><code>FLIP_VERTICAL</code></td>
            <td><code>2</code></td>
            <td><p>Pixels are flipped vertically.</p>
</td>
        </tr><tr>
            <td><code>FLIP_VERTICAL_AND_HORIZONTAL</code></td>
            <td><code>3</code></td>
            <td><p>Pixels are flipped vertically and mirrored left-right.</p>
</td>
        </tr></table>

### MemoryType {#MemoryType}
Type: <code>uint32</code>

*Defined in [fuchsia.images/memory_type.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.images/memory_type.fidl#8)*

<p>Specifies the type of VMO's memory.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>HOST_MEMORY</code></td>
            <td><code>0</code></td>
            <td><p>VMO is regular host CPU memory.</p>
</td>
        </tr><tr>
            <td><code>VK_DEVICE_MEMORY</code></td>
            <td><code>1</code></td>
            <td><p>VMO can be imported as a VkDeviceMemory by calling VkAllocateMemory with a
VkImportMemoryFuchsiaHandleInfoKHR wrapped in a VkMemoryAllocateInfo.</p>
</td>
        </tr></table>











## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="MAX_ACQUIRE_RELEASE_FENCE_COUNT">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.images/image_pipe2.fidl#10">MAX_ACQUIRE_RELEASE_FENCE_COUNT</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>int32</code></td>
            <td></td>
        </tr>
    
</table>



