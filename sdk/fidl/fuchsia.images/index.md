Project: /_project.yaml
Book: /_book.yaml

# fuchsia.images


## **PROTOCOLS**

## ImagePipe {:#ImagePipe}
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

### AddImage {:#AddImage}

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



### RemoveImage {:#RemoveImage}

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



### PresentImage {:#PresentImage}

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



## **STRUCTS**

### EncodedImage {:#EncodedImage}
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

### ImageInfo {:#ImageInfo}
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

### PresentationInfo {:#PresentationInfo}
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

### PixelFormat {:#PixelFormat}
Type: <code>uint32</code>

*Defined in [fuchsia.images/image_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.images/image_info.fidl#8)*

 Specifies how pixels are represented in the image buffer.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>BGRA_8</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>YUY2</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>NV12</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>YV12</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### ColorSpace {:#ColorSpace}
Type: <code>uint32</code>

*Defined in [fuchsia.images/image_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.images/image_info.fidl#74)*

 Specifies how pixel color information should be interpreted.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SRGB</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr></table>

### Tiling {:#Tiling}
Type: <code>uint32</code>

*Defined in [fuchsia.images/image_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.images/image_info.fidl#79)*

 Specifies how pixels are arranged in memory.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>LINEAR</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>GPU_OPTIMAL</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### AlphaFormat {:#AlphaFormat}
Type: <code>uint32</code>

*Defined in [fuchsia.images/image_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.images/image_info.fidl#90)*

 Specifies how alpha information should be interpreted.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OPAQUE</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>PREMULTIPLIED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>NON_PREMULTIPLIED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### Transform {:#Transform}
Type: <code>uint32</code>

*Defined in [fuchsia.images/image_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.images/image_info.fidl#102)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NORMAL</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>FLIP_HORIZONTAL</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>FLIP_VERTICAL</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>FLIP_VERTICAL_AND_HORIZONTAL</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### MemoryType {:#MemoryType}
Type: <code>uint32</code>

*Defined in [fuchsia.images/memory_type.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.images/memory_type.fidl#8)*

 Specifies the type of VMO's memory.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>HOST_MEMORY</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>VK_DEVICE_MEMORY</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>











