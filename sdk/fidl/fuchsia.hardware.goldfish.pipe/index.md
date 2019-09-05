Project: /_project.yaml
Book: /_book.yaml

# fuchsia.hardware.goldfish.pipe


## **PROTOCOLS**

## Device {:#Device}
*Defined in [fuchsia.hardware.goldfish.pipe/goldfish-pipe.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-goldfish-pipe/goldfish-pipe.fidl#22)*


### OpenPipe {:#OpenPipe}

 Open pipe. A protocol request |pipe_request| provides an interface
 to the pipe. Multiple pipes can be opened for a single device.
 Closing the device connection will also close all pipe connections.
 TODO(DX-1766): Unify `device` and `pipe`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>pipe_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Pipe'>Pipe</a>&gt;</code>
            </td>
        </tr></table>



## Pipe {:#Pipe}
*Defined in [fuchsia.hardware.goldfish.pipe/goldfish-pipe.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-goldfish-pipe/goldfish-pipe.fidl#31)*


### SetBufferSize {:#SetBufferSize}

 Request new IO buffer size. Can fail if out of memory. Discards
 contents of existing buffer on success. Leaves existing buffer
 intact on failure.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>size</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>res</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### SetEvent {:#SetEvent}

 Set event used to signal device state. Discards existing event
 after having transferred device state to the new event.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>event</code></td>
            <td>
                <code>handle&lt;event&gt;</code>
            </td>
        </tr></table>



### GetBuffer {:#GetBuffer}

 Acquire VMO for IO buffer. Can be called multiple times. Each call
 returns a new handle to the VMO.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>res</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;?</code>
            </td>
        </tr></table>

### Read {:#Read}

 Attempt to read up to count bytes into IO buffer at specified offset.
 Returns `ZX_ERR_SHOULD_WAIT` if pipe device is not readable.

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
            <td><code>res</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>actual</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### Write {:#Write}

 Writes up to count bytes from the IO buffer at specified offset.
 Returns `ZX_ERR_SHOULD_WAIT` if pipe device is not writable.

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
            <td><code>res</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>actual</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### Call {:#Call}

 Writes count bytes from the IO buffer at specified write
 offset. Blocks if pipe device is not writable. Subsequently reads
 read_count bytes into the IO buffer at specified read offset.
 Returns `ZX_ERR_SHOULD_WAIT` if pipe device is not readable.

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
        </tr><tr>
            <td><code>read_count</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>read_offset</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>res</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>actual</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>















## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-goldfish-pipe/goldfish-pipe.fidl#11">SIGNAL_READABLE</a></td>
            <td>
                    <code>16777216</code>
                </td>
                <td><code>uint32</code></td>
            <td> Signal that will be active on event handle if the Read() method
 will return data.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-goldfish-pipe/goldfish-pipe.fidl#15">SIGNAL_WRITABLE</a></td>
            <td>
                    <code>33554432</code>
                </td>
                <td><code>uint32</code></td>
            <td> Signal that will be active on event handle if the Write() method
 will accept data.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-goldfish-pipe/goldfish-pipe.fidl#19">SIGNAL_HANGUP</a></td>
            <td>
                    <code>67108864</code>
                </td>
                <td><code>uint32</code></td>
            <td> Signal that will be active on event handle if the device has been
 disconnected.
</td>
        </tr>
    
</table>

