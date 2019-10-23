[TOC]

# fuchsia.images


## **PROTOCOLS**

## ImagePipe {#ImagePipe}
*Defined in [fuchsia.images/image_pipe.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.images/image_pipe.fidl#64)*

 ImagePipe is a mechanism for streaming shared images between a producer
 and a consumer which may be running in different processes.

 Conceptually, the image pipe maintains a table of image resources supplied
 by the producer into which graphical content may be stored as well as a
 presentation queue containing a sequence of images which the producer has
 asked the consumer to present.

 The presentation queue is initially empty.

 Each entry in the presentation queue consists of an image together with a
 pair of optional synchronization fences:
 - Acquire fence: signaled by the producer when the image is ready to be consumed
 - Release fence: signaled by the consumer when the image is free to be freed or
   modified by the producer

 The producer performs the following sequence of steps to present content:
 - Allocate and add some number of images (often 2 or 3) to the image pipe
   to establish a pool using `AddImage()`.
 - Obtain the next available image from the pool.
 - Ask the consumer to enqueue an image for presentation and provide fences
   using `PresentImage()`.
 - Start rendering the image.
 - Signal the image's acquire fence when rendering is complete.
 - Loop to present more image, listen for signals on release fences to recycle
   images back into the pool.

 The consumer performs the following sequence of steps for each image which
 is enqueued in the presentation queue:
 - Await signals on the image's acquire fence.
 - If the fence wait cannot be satisfied or if some other error is detected,
   close the image pipe.
   Otherwise, begin presenting the image's content.
 - Retire the previously presented image (if any) from the presentation queue
   and signal its release fence when no longer needed.
 - Continue presenting the same image until the next one is ready.  Loop.

 If the producer wants to close the image pipe, it should:
 - Close its side of the connection.
 - Wait on all release fences for buffers that it has submitted with
   `PresentImage()`.
 - Proceed with resource cleanup.

 When the consumer detects the image pipe has closed, it should:
 - Stop using/presenting any images from the pipe.
 - Unmap all VMOs associated with the images in the pipe.
 - Close all handles to the VMOs.
 - Signal all release fences for presented and queued buffers.
 - Close all handles to fences.
 - Close its side of the connection.

 When either party detects that a fence has been abandoned (remotely closed
 without being signaled) it should assume that the associated image is in
 an indeterminate state.  This will typically happen when the other party
 (or one of its delegates) has crashed.  The safest course of action is to
 close the image pipe, release all resources which were shared with the
 other party, and re-establish the connection to recover.

### AddImage {#AddImage}

 Adds an image resource to image pipe.

 The `memory` is the handle of a memory object which contains the image
 data.  It is valid to create multiple images backed by the same memory
 object; they may even overlap.  Consumers must detect this and handle
 it accordingly.  The `offset_bytes` indicates the offset within the
 memory object at which the image data begins.  The `size_bytes`
 indicates the amount of memory from `memory` that should be utilized.
 The type of memory stored in the VMO is `memory_type` (e.g. GPU memory,
 host memory).

 The following errors will cause the connection to be closed:
 - `image_id` is already registered
 - `image_info` represents a format not supported by the consumer
 - `memory` is not a handle for a readable VMO
 - the image data expected at `offset_bytes` according to the `image_info`
   exceeds the memory object's bounds

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

 Removes an image resource from the pipe.

 The `image_id` is detached from the image resource and is free to be
 reused to add a new image resource.

 Removing an image from the image pipe does not affect the presentation
 queue or the currently presented image.

 The producer must wait for all release fences associated with the image to
 be signaled before freeing or modifying the underlying memory object since
 the image may still be in use in the presentation queue.

 The following errors will cause the connection to be closed:
 - `image_id` does not reference a currently registered image resource

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

 Enqueues the specified image for presentation by the consumer.

 The `acquire_fences` are a set of fences which must all be signaled by the
 producer before the consumer presents the image.
 The `release_fences` are set of fences which must all be signaled by the
 consumer before it is safe for the producer to free or modify the image.
 `presentation_time` specifies the time on or after which the
 client would like the enqueued operations should take visible effect
 (light up pixels on the screen), expressed in nanoseconds in the
 `CLOCK_MONOTONIC` timebase.  Desired presentation times must be
 monotonically non-decreasing.

 `presentation_info` returns timing information about the submitted frame
 and future frames (see presentation_info.fidl).

 The following errors will cause the connection to be closed:
 - `image_id` does not reference a currently registered image resource

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

 ImagePipe is a mechanism for streaming shared images between a producer
 and a consumer which may be running in different processes.

 Conceptually, the image pipe maintains a table of image resources supplied
 by the producer into which graphical content may be stored as well as a
 presentation queue containing a sequence of images which the producer has
 asked the consumer to present.

 The presentation queue is initially empty.

 Each entry in the presentation queue consists of an image together with a
 pair of optional synchronization fences:
 - Acquire fence: signaled by the producer when the image is ready to be consumed
 - Release fence: signaled by the consumer when the image is free to be freed or
   modified by the producer

 The producer performs the following sequence of steps to present content:
 - Allocate and add some number of BufferCollections to the image pipe to allow
 consumer to set constraints.
 - Allocate and add some number of images (often 2 or 3) to the image pipe
   to establish a pool using `AddImage()`.
 - Obtain the next available image from the pool.
 - Ask the consumer to enqueue an image for presentation and provide fences
   using `PresentImage()`.
 - Start rendering the image.
 - Signal the image's acquire fence when rendering is complete.
 - Loop to present more image, listen for signals on release fences to recycle
   images back into the pool.

 The consumer performs the following sequence of steps for each image which
 is enqueued in the presentation queue:
 - Await signals on the image's acquire fence.
 - If the fence wait cannot be satisfied or if some other error is detected,
   close the image pipe.
   Otherwise, begin presenting the image's content.
 - Retire the previously presented image (if any) from the presentation queue
   and signal its release fence when no longer needed.
 - Continue presenting the same image until the next one is ready.  Loop.

 If the producer wants to close the image pipe, it should:
 - Close its side of the connection.
 - Wait on all release fences for buffers that it has submitted with
   `PresentImage()`.
 - Proceed with resource cleanup.

 When the consumer detects the image pipe has closed, it should:
 - Stop using/presenting any images from the pipe.
 - Unmap all memory objects associated with the images in the pipe.
 - Close all BufferCollection resources.
 - Signal all release fences for presented and queued buffers.
 - Close all handles to fences.
 - Close its side of the connection.

 When either party detects that a fence has been abandoned (remotely closed
 without being signaled) it should assume that the associated image is in
 an indeterminate state.  This will typically happen when the other party
 (or one of its delegates) has crashed.  The safest course of action is to
 close the image pipe, release all resources which were shared with the
 other party, and re-establish the connection to recover.

### AddBufferCollection {#AddBufferCollection}

 Adds a BufferCollection resource to the image pipe.

 The producer is expected to set constraints on this resource for images added
 via `AddImage()`. The consumer can set its constraints on
 `buffer_collection_token` before or after. Note that the buffers won’t be
 allocated until all BufferCollectionToken instances are used to set
 constraints, on both the producer and consumer side. See collection.fidl for
 details.

 The following errors will cause the connection to be closed:
 - `buffer_collection_id` is already registered

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

 Adds an image resource to image pipe.

 `buffer_collection_id` refers to the BufferCollectionToken instance that is
 registered via `AddBufferCollection()`. The underlying memory objects allocated
 are used to address to the image data. `buffer_collection_id` refers to the
 index of the memory object allocated in BufferCollection.

 `image_format` specifiies image properties. `coded_width` and `coded_height` are
 used to set image dimensions.

 It is valid to create multiple images backed by the same memory object; they
 may even overlap.  Consumers must detect this and handle it accordingly.

 The following errors will cause the connection to be closed:
 - `image_id` is already registered
 - `buffer_collection_id` refers to an unregistered BufferCollection.
 - `buffer_collection_index` points to a resource index out of the initialized
     BufferCollection bounds
 - No resource is allocated in the registered BufferCollection.

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

 Removes a BufferCollection resource from the pipe.

 The `buffer_collection_id` resource is detached as well as all Images that are
 associated with that BufferCollection. Leads to the same results as calling
 `RemoveImage()` on all Images for `buffer_collection_id`.

 The producer must wait for all release fences associated with the Images to
 be signaled before freeing or modifying the underlying memory object since
 the image may still be in use in the presentation queue.

 The following errors will cause the connection to be closed:
 - `buffer_collection_id` does not reference a currently registered BufferCollection

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

 Removes an image resource from the pipe.

 The `image_id` is detached from the image resource and is free to be
 reused to add a new image resource.

 Removing an image from the image pipe does not affect the presentation
 queue or the currently presented image.

 The producer must wait for all release fences associated with the image to
 be signaled before freeing or modifying the underlying memory object since
 the image may still be in use in the presentation queue.

 The following errors will cause the connection to be closed:
 - `image_id` does not reference a currently registered image resource

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

 Enqueues the specified image for presentation by the consumer.

 The `acquire_fences` are a set of fences which must all be signaled by the
 producer before the consumer presents the image.
 The `release_fences` are set of fences which must all be signaled by the
 consumer before it is safe for the producer to free or modify the image.
 `presentation_time` specifies the time on or after which the
 client would like the enqueued operations should take visible effect
 (light up pixels on the screen), expressed in nanoseconds in the
 `CLOCK_MONOTONIC` timebase.  Desired presentation times must be
 monotonically non-decreasing.

 `presentation_info` returns timing information about the submitted frame
 and future frames (see presentation_info.fidl).

 The producer may decide not to signal `acquire_fences` for an image.
 In that case, if a later image is enqueued and later image’s
 `presentation_time` is reached, the consumer presents the later image when
 later image’s `acquire_fences` are signaled. The consumer also signals
 earlier image’s `release_fences` and removes it from the presentation queue.
 This sequence works as a cancellation mechanism.

 The following errors will cause the connection to be closed:
 - `image_id` does not reference a currently registered image resource

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
            <td> The vmo.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The size of the image in the vmo in bytes.
</td>
            <td>No default</td>
        </tr>
</table>

### ImageInfo {#ImageInfo}
*Defined in [fuchsia.images/image_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.images/image_info.fidl#117)*



 Information about a graphical image (texture) including its format and size.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>transform</code></td>
            <td>
                <code><a class='link' href='#Transform'>Transform</a></code>
            </td>
            <td> Specifies if the image should be mirrored before displaying.
</td>
            <td><a class='link' href='#Transform.NORMAL'>Transform.NORMAL</a></td>
        </tr><tr>
            <td><code>width</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The width and height of the image in pixels.
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
            <td> The number of bytes per row in the image buffer.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>pixel_format</code></td>
            <td>
                <code><a class='link' href='#PixelFormat'>PixelFormat</a></code>
            </td>
            <td> The pixel format of the image.
</td>
            <td><a class='link' href='#PixelFormat.BGRA_8'>PixelFormat.BGRA_8</a></td>
        </tr><tr>
            <td><code>color_space</code></td>
            <td>
                <code><a class='link' href='#ColorSpace'>ColorSpace</a></code>
            </td>
            <td> The pixel color space.
</td>
            <td><a class='link' href='#ColorSpace.SRGB'>ColorSpace.SRGB</a></td>
        </tr><tr>
            <td><code>tiling</code></td>
            <td>
                <code><a class='link' href='#Tiling'>Tiling</a></code>
            </td>
            <td> The pixel arrangement in memory.
</td>
            <td><a class='link' href='#Tiling.LINEAR'>Tiling.LINEAR</a></td>
        </tr><tr>
            <td><code>alpha_format</code></td>
            <td>
                <code><a class='link' href='#AlphaFormat'>AlphaFormat</a></code>
            </td>
            <td> Specifies the interpretion of the alpha channel, if one exists.
</td>
            <td><a class='link' href='#AlphaFormat.OPAQUE'>AlphaFormat.OPAQUE</a></td>
        </tr>
</table>

### PresentationInfo {#PresentationInfo}
*Defined in [fuchsia.images/presentation_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.images/presentation_info.fidl#10)*



 Information returned by methods such as `ImagePipe.PresentImage()` and
 `Session.Present()`, when the consumer begins preparing the first frame
 which includes the presented content.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>presentation_time</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The actual time at which the enqueued operations are anticipated to take
 visible effect, expressed in nanoseconds in the `CLOCK_MONOTONIC`
 timebase.

 This value increases monotonically with each new frame, typically in
 increments of the `presentation_interval`.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>presentation_interval</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The nominal amount of time which is anticipated to elapse between
 successively presented frames, expressed in nanoseconds.  When rendering
 to a display, the interval will typically be derived from the display
 refresh rate.

 This value is non-zero.  It may vary from time to time, such as when
 changing display modes.
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### PixelFormat {#PixelFormat}
Type: <code>uint32</code>

*Defined in [fuchsia.images/image_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.images/image_info.fidl#8)*

 Specifies how pixels are represented in the image buffer.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>BGRA_8</code></td>
            <td><code>0</code></td>
            <td> BGRA_8

 A 32-bit four-component unsigned integer format.
 Byte order: B, G, R, A (little-endian ARGB packed 32-bit word).
 Equivalent to Skia `kBGRA_8888_SkColorType` color type.
 Equivalent to Zircon `ARGB_8888` pixel format on little-endian arch.
</td>
        </tr><tr>
            <td><code>YUY2</code></td>
            <td><code>1</code></td>
            <td> YUY2

 4:2:2 (2x down-sampled UV horizontally; full res UV vertically)

 A 32-bit component that contains information for 2 pixels:
 Byte order: Y1, U, Y2, V
 Unpacks to 2 RGB pixels, where RGB1 = func(Y1, U, V)
 and RGB2 = func(Y2, U, V)
 Equivalent to YUV422
</td>
        </tr><tr>
            <td><code>NV12</code></td>
            <td><code>2</code></td>
            <td> NV12

 4:2:0 (2x down-sampled UV in both directions)

 Offset 0:
 8 bit per pixel Y plane with bytes YYY.
 Offset height * stride:
 8 bit UV data interleaved bytes as UVUVUV.

 Y plane has line stride >= width.

 In this context, both width and height are required to be even.

 The UV data is separated into "lines", with each "line" having same byte
 width as a line of Y data, and same "line" stride as Y data's line stride.
 The UV data has height / 2 "lines".

 In converting to RGB, the UV data gets up-scaled by 2x in both directions
 overall.  This comment is intentionally silent on exactly how UV up-scaling
 phase/filtering/signal processing works, as it's a complicated topic that
 can vary by implementation, typically trading off speed and quality of the
 up-scaling.  See comments in relevant conversion code for approach taken
 by any given convert path.  The precise relative phase of the UV data is
 not presently conveyed.
</td>
        </tr><tr>
            <td><code>YV12</code></td>
            <td><code>3</code></td>
            <td> YV12

 Like I420, except with V and U swapped.

 4:2:0 (2x down-sampled UV in both directions)

 Offset 0:
 8 bit per pixel Y plane with bytes YYY.
 Offset height * stride:
 8 bit V data with uv_stride = stride / 2
 Offset height * stride + uv_stride * height / 2:
 8 bit U data with uv_stride = stride / 2

 Y plane has line stride >= width.

 Both width and height are required to be even.
</td>
        </tr></table>

### ColorSpace {#ColorSpace}
Type: <code>uint32</code>

*Defined in [fuchsia.images/image_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.images/image_info.fidl#74)*

 Specifies how pixel color information should be interpreted.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SRGB</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr></table>

### Tiling {#Tiling}
Type: <code>uint32</code>

*Defined in [fuchsia.images/image_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.images/image_info.fidl#79)*

 Specifies how pixels are arranged in memory.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>LINEAR</code></td>
            <td><code>0</code></td>
            <td> Pixels are packed linearly.
 Equivalent to `VK_IMAGE_TILING_LINEAR`.
</td>
        </tr><tr>
            <td><code>GPU_OPTIMAL</code></td>
            <td><code>1</code></td>
            <td> Pixels are packed in a GPU-dependent optimal format.
 Equivalent to `VK_IMAGE_TILING_OPTIMAL`.
</td>
        </tr></table>

### AlphaFormat {#AlphaFormat}
Type: <code>uint32</code>

*Defined in [fuchsia.images/image_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.images/image_info.fidl#90)*

 Specifies how alpha information should be interpreted.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OPAQUE</code></td>
            <td><code>0</code></td>
            <td> Image is considered to be opaque.  Alpha channel is ignored.
 Blend function is: src.RGB
</td>
        </tr><tr>
            <td><code>PREMULTIPLIED</code></td>
            <td><code>1</code></td>
            <td> Color channels have been premultiplied by alpha.
 Blend function is: src.RGB + (dest.RGB * (1 - src.A))
</td>
        </tr><tr>
            <td><code>NON_PREMULTIPLIED</code></td>
            <td><code>2</code></td>
            <td> Color channels have not been premultiplied by alpha.
 Blend function is: (src.RGB * src.A) + (dest.RGB * (1 - src.A))
</td>
        </tr></table>

### Transform {#Transform}
Type: <code>uint32</code>

*Defined in [fuchsia.images/image_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.images/image_info.fidl#102)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NORMAL</code></td>
            <td><code>0</code></td>
            <td> Pixels are displayed normally.
</td>
        </tr><tr>
            <td><code>FLIP_HORIZONTAL</code></td>
            <td><code>1</code></td>
            <td> Pixels are mirrored left-right.
</td>
        </tr><tr>
            <td><code>FLIP_VERTICAL</code></td>
            <td><code>2</code></td>
            <td> Pixels are flipped vertically.
</td>
        </tr><tr>
            <td><code>FLIP_VERTICAL_AND_HORIZONTAL</code></td>
            <td><code>3</code></td>
            <td> Pixels are flipped vertically and mirrored left-right.
</td>
        </tr></table>

### MemoryType {#MemoryType}
Type: <code>uint32</code>

*Defined in [fuchsia.images/memory_type.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.images/memory_type.fidl#8)*

 Specifies the type of VMO's memory.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>HOST_MEMORY</code></td>
            <td><code>0</code></td>
            <td> VMO is regular host CPU memory.
</td>
        </tr><tr>
            <td><code>VK_DEVICE_MEMORY</code></td>
            <td><code>1</code></td>
            <td> VMO can be imported as a VkDeviceMemory by calling VkAllocateMemory with a
 VkImportMemoryFuchsiaHandleInfoKHR wrapped in a VkMemoryAllocateInfo.
</td>
        </tr></table>











## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.images/image_pipe2.fidl#10">MAX_ACQUIRE_RELEASE_FENCE_COUNT</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>int32</code></td>
            <td></td>
        </tr>
    
</table>

