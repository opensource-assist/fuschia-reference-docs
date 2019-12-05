[TOC]

# fuchsia.hardware.goldfish


## **PROTOCOLS**

## AddressSpaceDevice {#AddressSpaceDevice}
*Defined in [fuchsia.hardware.goldfish/goldfish_address_space.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.hardware.goldfish/goldfish_address_space.fidl#39)*


### AllocateBlock {#AllocateBlock}


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
        </tr><tr>
            <td><code>paddr</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;?</code>
            </td>
        </tr></table>

### DeallocateBlock {#DeallocateBlock}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>paddr</code></td>
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

### OpenChildDriver {#OpenChildDriver}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#AddressSpaceChildDriverType'>AddressSpaceChildDriverType</a></code>
            </td>
        </tr><tr>
            <td><code>req</code></td>
            <td>
                <code>request&lt;<a class='link' href='#AddressSpaceChildDriver'>AddressSpaceChildDriver</a>&gt;</code>
            </td>
        </tr></table>



## AddressSpaceChildDriver {#AddressSpaceChildDriver}
*Defined in [fuchsia.hardware.goldfish/goldfish_address_space.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.hardware.goldfish/goldfish_address_space.fidl#85)*


### AllocateBlock {#AllocateBlock}


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
        </tr><tr>
            <td><code>paddr</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;?</code>
            </td>
        </tr></table>

### DeallocateBlock {#DeallocateBlock}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>paddr</code></td>
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

### ClaimSharedBlock {#ClaimSharedBlock}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>offset</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
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
        </tr><tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;?</code>
            </td>
        </tr></table>

### UnclaimSharedBlock {#UnclaimSharedBlock}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
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
        </tr></table>

### Ping {#Ping}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ping</code></td>
            <td>
                <code><a class='link' href='#AddressSpaceChildDriverPingMessage'>AddressSpaceChildDriverPingMessage</a></code>
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
            <td><code>ping</code></td>
            <td>
                <code><a class='link' href='#AddressSpaceChildDriverPingMessage'>AddressSpaceChildDriverPingMessage</a></code>
            </td>
        </tr></table>

## ControlDevice {#ControlDevice}
*Defined in [fuchsia.hardware.goldfish/goldfish_control.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.hardware.goldfish/goldfish_control.fidl#17)*

<p>Interface for the Goldfish control driver providing color buffers.</p>

### CreateColorBuffer {#CreateColorBuffer}

<p>Create shared color buffer. Color buffer is automatically freed when
all references to <code>vmo</code> have been closed. Fails if VMO is not
associated with goldfish heap memory.
Returns ZX_ERR_ALREADY_EXISTS if color buffer has already been created.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr><tr>
            <td><code>width</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>format</code></td>
            <td>
                <code><a class='link' href='#ColorBufferFormatType'>ColorBufferFormatType</a></code>
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

### GetColorBuffer {#GetColorBuffer}

<p>Get color buffer for VMO. Fails if VMO is not associated with a color
buffer.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
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
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

## PipeDevice {#PipeDevice}
*Defined in [fuchsia.hardware.goldfish/goldfish_pipe.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.hardware.goldfish/goldfish_pipe.fidl#23)*

<p>Interface for the Goldfish pipe driver.</p>

### OpenPipe {#OpenPipe}

<p>Open pipe. A protocol request |pipe_request| provides an interface
to the pipe. Multiple pipes can be opened for a single device.
Closing the device connection will also close all pipe connections.
TODO(DX-1766): Unify <code>device</code> and <code>pipe</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>pipe_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Pipe'>Pipe</a>&gt;</code>
            </td>
        </tr></table>



## Pipe {#Pipe}
*Defined in [fuchsia.hardware.goldfish/goldfish_pipe.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.hardware.goldfish/goldfish_pipe.fidl#32)*


### SetBufferSize {#SetBufferSize}

<p>Request new IO buffer size. Can fail if out of memory. Discards
contents of existing buffer on success. Leaves existing buffer
intact on failure.</p>

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

### SetEvent {#SetEvent}

<p>Set event used to signal device state. Discards existing event
after having transferred device state to the new event.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>event</code></td>
            <td>
                <code>handle&lt;event&gt;</code>
            </td>
        </tr></table>



### GetBuffer {#GetBuffer}

<p>Acquire VMO for IO buffer. Can be called multiple times. Each call
returns a new handle to the VMO.</p>

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

### Read {#Read}

<p>Attempt to read up to count bytes into IO buffer at specified offset.
Returns <code>ZX_ERR_SHOULD_WAIT</code> if pipe device is not readable.</p>

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

### Write {#Write}

<p>Writes up to count bytes from the IO buffer at specified offset.
Returns <code>ZX_ERR_SHOULD_WAIT</code> if pipe device is not writable.</p>

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

### Call {#Call}

<p>Writes count bytes from the IO buffer at specified write
offset. Blocks if pipe device is not writable. Subsequently reads
read_count bytes into the IO buffer at specified read offset.
Returns <code>ZX_ERR_SHOULD_WAIT</code> if pipe device is not readable.</p>

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



## **STRUCTS**

### AddressSpaceChildDriverPingMessage {#AddressSpaceChildDriverPingMessage}
*Defined in [fuchsia.hardware.goldfish/goldfish_address_space.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.hardware.goldfish/goldfish_address_space.fidl#74)*



<p>After opening the child driver, the client and hardware communicate via a
child driver-specific protocol, with notifications driven by
Ping(), each of which writes and reads messages to the hardware
that follow this AddressSpaceChildDriverPingMessage struct.
Each child driver type will have its own semantics for each field.
It's common for child drivers to refer to offset/size plus a metadata
field. We also provide extra data fields for other use cases in
particular child drivers.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>offset</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>metadata</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>data0</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>data1</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>data2</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>data3</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### AddressSpaceChildDriverType {#AddressSpaceChildDriverType}
Type: <code>uint32</code>

*Defined in [fuchsia.hardware.goldfish/goldfish_address_space.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.hardware.goldfish/goldfish_address_space.fidl#11)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DEFAULT</code></td>
            <td><code>0</code></td>
            <td><p>The DEFAULT child driver type is for graphics.</p>
</td>
        </tr></table>

### ColorBufferFormatType {#ColorBufferFormatType}
Type: <code>uint32</code>

*Defined in [fuchsia.hardware.goldfish/goldfish_control.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.hardware.goldfish/goldfish_control.fidl#10)*

<p>Color buffer formats.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>RGBA</code></td>
            <td><code>6408</code></td>
            <td></td>
        </tr><tr>
            <td><code>BGRA</code></td>
            <td><code>32993</code></td>
            <td></td>
        </tr></table>











## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.hardware.goldfish/goldfish_pipe.fidl#11">SIGNAL_READABLE</a></td>
            <td>
                    <code>16777216</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Signal that will be active on event handle if the Read() method
will return data.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.hardware.goldfish/goldfish_pipe.fidl#15">SIGNAL_WRITABLE</a></td>
            <td>
                    <code>33554432</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Signal that will be active on event handle if the Write() method
will accept data.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.hardware.goldfish/goldfish_pipe.fidl#19">SIGNAL_HANGUP</a></td>
            <td>
                    <code>67108864</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Signal that will be active on event handle if the device has been
disconnected.</p>
</td>
        </tr>
    
</table>



