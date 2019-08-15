Project: /_project.yaml
Book: /_book.yaml

# fuchsia.virtualization


## **PROTOCOLS**

## BalloonController {:#BalloonController}
*Defined in [fuchsia.virtualization/balloon_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/balloon_controller.fidl#17)*

 A `BalloonController` controls a guest instance's memory balloon.

### GetNumPages {:#GetNumPages}

 Get the number of pages in the memory balloon.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>num_pages</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### RequestNumPages {:#RequestNumPages}

 Request a number of pages to be supplied to the memory balloon.

 If `num_pages` is greater than the current value, the guest instance will
 provide additional pages to the memory balloon. If `num_pages` is less
 than the current value, the guest instance is free to reclaim pages from
 the memory balloon.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>num_pages</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### GetMemStats {:#GetMemStats}

 Get memory statistics of the guest instance.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>mem_stats</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#MemStat'>MemStat</a>&gt;?</code>
            </td>
        </tr></table>

## Guest {:#Guest}
*Defined in [fuchsia.virtualization/guest.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/guest.fidl#9)*

 A `Guest` provides access to services of a guest instance.

### GetSerial {:#GetSerial}

 Get the socket for the primary serial device of the guest. The details
 regarding what output is produced and what input is accepted are
 determined by each guest.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>socket</code></td>
            <td>
                <code>handle&lt;socket&gt;</code>
            </td>
        </tr></table>

## Manager {:#Manager}
*Defined in [fuchsia.virtualization/manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/manager.fidl#29)*


### Create {:#Create}

 Create a new environment in which guests can be launched.

 The `label` is a string that is used for diagnostic purposes, such as
 naming resources and dumping debug info.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>label</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr><tr>
            <td><code>env</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Realm'>Realm</a>&gt;</code>
            </td>
        </tr></table>



### List {:#List}

 Query for existing guest environments.

 This is intended for diagnostic purposes only.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>env_infos</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#EnvironmentInfo'>EnvironmentInfo</a>&gt;</code>
            </td>
        </tr></table>

### Connect {:#Connect}

 Connect to a currently running guest environment identified by `id`. The
 `id` can be found via a call to `List`.

 This is intended for diagnostic purposes only.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>env</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Realm'>Realm</a>&gt;</code>
            </td>
        </tr></table>



## WaylandDispatcher {:#WaylandDispatcher}
*Defined in [fuchsia.virtualization/realm.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/realm.fidl#44)*

 An interface that will receive channels for Wayland connections.

### OnNewConnection {:#OnNewConnection}

 Inform dispatcher of new connection.

 When a client opens a new connection to the virtio_wl device, a new
 zx::channel will be created for that connection. The virtio_wl device
 will retain one endpoint of that channel and the other endpoint will be
 provided to this method. The messages on the channel will be Wayland
 protocol messages as sent by the client. Each channel datagram will
 contain 1 or more complete Wayland messages.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>channel</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



## Realm {:#Realm}
*Defined in [fuchsia.virtualization/realm.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/realm.fidl#107)*


### LaunchInstance {:#LaunchInstance}

 Launch a new guest instance into this environment. The `cid` of the
 instance is returned so that it can be uniquely identified.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>launch_info</code></td>
            <td>
                <code><a class='link' href='#LaunchInfo'>LaunchInfo</a></code>
            </td>
        </tr><tr>
            <td><code>controller</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Guest'>Guest</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>cid</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### ListInstances {:#ListInstances}

 Query for guests running in this environment.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>instances</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#InstanceInfo'>InstanceInfo</a>&gt;</code>
            </td>
        </tr></table>

### ConnectToInstance {:#ConnectToInstance}

 Connect to a currently running guest instance identified by `cid`. The
 `cid` can be found via the return value of `LaunchInstance` or a call to
 `ListInstances`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>cid</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>controller</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Guest'>Guest</a>&gt;</code>
            </td>
        </tr></table>



### ConnectToBalloon {:#ConnectToBalloon}

 Connect to the memory balloon of a currently running guest instance
 identified by `cid`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>cid</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>controller</code></td>
            <td>
                <code>request&lt;<a class='link' href='#BalloonController'>BalloonController</a>&gt;</code>
            </td>
        </tr></table>



### GetHostVsockEndpoint {:#GetHostVsockEndpoint}

 Returns an interface that can be used to access the host vsock endpoint.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>endpoint</code></td>
            <td>
                <code>request&lt;<a class='link' href='#HostVsockEndpoint'>HostVsockEndpoint</a>&gt;</code>
            </td>
        </tr></table>



## GuestVsockAcceptor {:#GuestVsockAcceptor}
*Defined in [fuchsia.virtualization/vsock.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/vsock.fidl#20)*

 Exposed by guests capable of listening via vsocks. On a request to establish
 a connection, the `Accept` method will be called. If the port is open and
 accepting connections, the implementation should return `ZX_OK`.

 Also see `GuestVsockEndpoint`.

### Accept {:#Accept}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>src_cid</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>src_port</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>port</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>handle</code></td>
            <td>
                <code>handle&lt;handle&gt;?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

## HostVsockAcceptor {:#HostVsockAcceptor}
*Defined in [fuchsia.virtualization/vsock.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/vsock.fidl#29)*

 Exposed by a host capable of listening via vsocks. A variant of a
 `GuestVsockAcceptor` that is responsible for creating the `handle` with which
 to communicate. The `handle` will be either a socket or a channel, depending
 on the current configuration.

### Accept {:#Accept}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>src_cid</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>src_port</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>port</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>handle</code></td>
            <td>
                <code>handle&lt;handle&gt;?</code>
            </td>
        </tr></table>

## HostVsockConnector {:#HostVsockConnector}
*Defined in [fuchsia.virtualization/vsock.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/vsock.fidl#39)*

 Exposed by a host capable of connecting via vsocks. This allows a guest to
 identify itself via {src_cid, src_port}, and request to connect to
 {cid, port}. The host should return `ZX_OK`, and create a handle with which
 to communicate. The `handle` will be either a socket or a channel, depending
 on the current configuration.

### Connect {:#Connect}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>src_cid</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>src_port</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>cid</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>port</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>handle</code></td>
            <td>
                <code>handle&lt;handle&gt;?</code>
            </td>
        </tr></table>

## GuestVsockEndpoint {:#GuestVsockEndpoint}
*Defined in [fuchsia.virtualization/vsock.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/vsock.fidl#50)*

 Exposed by guests capable of handling vsock traffic. During
 initialization the Manager will assign a unique CID to this endpoint and
 provide a `HostVsockConnector` that can be used to establish outbound
 connections. The implementation should provide a `GuestVsockAcceptor`
 implementation that can handle any inbound connection requests.

### SetContextId {:#SetContextId}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>cid</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>connector</code></td>
            <td>
                <code><a class='link' href='#HostVsockConnector'>HostVsockConnector</a></code>
            </td>
        </tr><tr>
            <td><code>acceptor</code></td>
            <td>
                <code>request&lt;<a class='link' href='#GuestVsockAcceptor'>GuestVsockAcceptor</a>&gt;</code>
            </td>
        </tr></table>



### OnShutdown {:#OnShutdown}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>src_cid</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>src_port</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>dst_cid</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>dst_port</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

## HostVsockEndpoint {:#HostVsockEndpoint}
*Defined in [fuchsia.virtualization/vsock.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/vsock.fidl#58)*

 Exposed by a host to provide the ability for listeners to be multiplexed by
 port and to manage dynamic port allocation for outbound connections.

### Listen {:#Listen}

 Register `acceptor` to be invoked for any connection requests to `port`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>port</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>acceptor</code></td>
            <td>
                <code><a class='link' href='#HostVsockAcceptor'>HostVsockAcceptor</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Connect {:#Connect}

 Similar to `HostVsockConnector.Connect` except the `src_cid` is
 `HOST_CID` and `src_port` is generated automatically.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>cid</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>port</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>handle</code></td>
            <td>
                <code>handle&lt;handle&gt;?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>



## **STRUCTS**

### MemStat {:#MemStat}
*Defined in [fuchsia.virtualization/balloon_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/balloon_controller.fidl#10)*



 Contains a memory statistic for the balloon device.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>tag</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>val</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### EnvironmentInfo {:#EnvironmentInfo}
*Defined in [fuchsia.virtualization/manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/manager.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> A globally unique identifier for this environment.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>label</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The string provided to `Manager.Create`.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>instances</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#InstanceInfo'>InstanceInfo</a>&gt;</code>
            </td>
            <td> List of guests running in this environment.
</td>
            <td>No default</td>
        </tr>
</table>

### InstanceInfo {:#InstanceInfo}
*Defined in [fuchsia.virtualization/manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/manager.fidl#18)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>cid</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Context ID to use to address this guest for vsocket communications. This
 can also be used to uniquely identify a guest within an environment.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>label</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The `label` string originally provided in the `LaunchInfo` structure
 or, if it was the null, the `url`
</td>
            <td>No default</td>
        </tr>
</table>

### BlockDevice {:#BlockDevice}
*Defined in [fuchsia.virtualization/realm.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/realm.fidl#31)*



 Properties describing a single block device in the system.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>string[20]</code>
            </td>
            <td> A label used to identify the block device.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>mode</code></td>
            <td>
                <code><a class='link' href='#BlockMode'>BlockMode</a></code>
            </td>
            <td> The access mode for the block backing file.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>format</code></td>
            <td>
                <code><a class='link' href='#BlockFormat'>BlockFormat</a></code>
            </td>
            <td> The data format of the backing file.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>file</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io/index.html'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/index.html#File'>File</a></code>
            </td>
            <td> The underlying file that stores the drive contents.
</td>
            <td>No default</td>
        </tr>
</table>

### WaylandDevice {:#WaylandDevice}
*Defined in [fuchsia.virtualization/realm.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/realm.fidl#57)*



 Properties describing a virtio_wl device.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>memory</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The amount of guest-physical address space to allocate for virtio_wl
 buffers.

 Default to a 1GiB allocation.
</td>
            <td>1073741824</td>
        </tr><tr>
            <td><code>dispatcher</code></td>
            <td>
                <code><a class='link' href='#WaylandDispatcher'>WaylandDispatcher</a></code>
            </td>
            <td> The dispatcher for new virtio_wl connections.
</td>
            <td>No default</td>
        </tr>
</table>

### MagmaDevice {:#MagmaDevice}
*Defined in [fuchsia.virtualization/realm.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/realm.fidl#69)*



 Properties describing a virtio_magma device.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>memory</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The amount of guest-physical address space to allocate for virtio_magma
 buffers.

 Default to a 16GiB allocation.
</td>
            <td>17179869184</td>
        </tr>
</table>

### LaunchInfo {:#LaunchInfo}
*Defined in [fuchsia.virtualization/realm.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/realm.fidl#77)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>url</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The URL of the package to launch.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>args</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
            <td> Arguments that will be passed to the VMM binary when launching this guest.

 See ///src/virtualization/bin/vmm/guest_config.cc for valid options.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>label</code></td>
            <td>
                <code>string?</code>
            </td>
            <td> A diagnostic string to associate with this instance.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>flat_namespace</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sys/index.html'>fuchsia.sys</a>/<a class='link' href='../fuchsia.sys/index.html#FlatNamespace'>FlatNamespace</a>?</code>
            </td>
            <td> A flat namespace to be appended to the default namespace for the VMM
 process.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>block_devices</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#BlockDevice'>BlockDevice</a>&gt;?</code>
            </td>
            <td> A set of block devices to add to the virtual machine.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>wayland_device</code></td>
            <td>
                <code><a class='link' href='#WaylandDevice'>WaylandDevice</a>?</code>
            </td>
            <td> An optional virtio_wl device.

 If not provided, no virtio_wl device will be created by the VMM.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>magma_device</code></td>
            <td>
                <code><a class='link' href='#MagmaDevice'>MagmaDevice</a>?</code>
            </td>
            <td> An optional virtio_magma device.

 If not provided, no virtio_magma device will be created by the VMM.
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### BlockMode {:#BlockMode}
Type: <code>uint32</code>

*Defined in [fuchsia.virtualization/realm.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/realm.fidl#11)*

 Mode of the file backing a block device.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>READ_WRITE</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>READ_ONLY</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>VOLATILE_WRITE</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### BlockFormat {:#BlockFormat}
Type: <code>uint32</code>

*Defined in [fuchsia.virtualization/realm.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/realm.fidl#21)*

 Data format of the file backing a block device.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>RAW</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>QCOW</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>











## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/realm.fidl#28">MAX_BLOCK_DEVICE_ID_SIZE</a></td>
            <td>
                    <code>20</code>
                </td>
                <td><code>uint64</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/vsock.fidl#13">HOST_CID</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    
</table>

