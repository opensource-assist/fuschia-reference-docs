[TOC]

# fuchsia.virtualization


## **PROTOCOLS**

## BalloonController {#BalloonController}
*Defined in [fuchsia.virtualization/balloon_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/balloon_controller.fidl#17)*

<p>A <code>BalloonController</code> controls a guest instance's memory balloon.</p>

### GetNumPages {#GetNumPages}

<p>Get the number of pages in the memory balloon.</p>

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

### RequestNumPages {#RequestNumPages}

<p>Request a number of pages to be supplied to the memory balloon.</p>
<p>If <code>num_pages</code> is greater than the current value, the guest instance will
provide additional pages to the memory balloon. If <code>num_pages</code> is less
than the current value, the guest instance is free to reclaim pages from
the memory balloon.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>num_pages</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### GetMemStats {#GetMemStats}

<p>Get memory statistics of the guest instance.</p>

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
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr><tr>
            <td><code>mem_stats</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#MemStat'>MemStat</a>&gt;?</code>
            </td>
        </tr></table>

## Guest {#Guest}
*Defined in [fuchsia.virtualization/guest.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/guest.fidl#9)*

<p>A <code>Guest</code> provides access to services of a guest instance.</p>

### GetSerial {#GetSerial}

<p>Get the socket for the primary serial device of the guest. The details
regarding what output is produced and what input is accepted are
determined by each guest.</p>

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

## Manager {#Manager}
*Defined in [fuchsia.virtualization/manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/manager.fidl#29)*


### Create {#Create}

<p>Create a new environment in which guests can be launched.</p>
<p>The <code>label</code> is a string that is used for diagnostic purposes, such as
naming resources and dumping debug info.</p>

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



### List {#List}

<p>Query for existing guest environments.</p>
<p>This is intended for diagnostic purposes only.</p>

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

### Connect {#Connect}

<p>Connect to a currently running guest environment identified by <code>id</code>. The
<code>id</code> can be found via a call to <code>List</code>.</p>
<p>This is intended for diagnostic purposes only.</p>

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



## WaylandDispatcher {#WaylandDispatcher}
*Defined in [fuchsia.virtualization/realm.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/realm.fidl#44)*

<p>An interface that will receive channels for Wayland connections.</p>

### OnNewConnection {#OnNewConnection}

<p>Inform dispatcher of new connection.</p>
<p>When a client opens a new connection to the virtio_wl device, a new
zx::channel will be created for that connection. The virtio_wl device
will retain one endpoint of that channel and the other endpoint will be
provided to this method. The messages on the channel will be Wayland
protocol messages as sent by the client. Each channel datagram will
contain 1 or more complete Wayland messages.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>channel</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



## Realm {#Realm}
*Defined in [fuchsia.virtualization/realm.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/realm.fidl#107)*


### LaunchInstance {#LaunchInstance}

<p>Launch a new guest instance into this environment. The <code>cid</code> of the
instance is returned so that it can be uniquely identified.</p>

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

### ListInstances {#ListInstances}

<p>Query for guests running in this environment.</p>

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

### ConnectToInstance {#ConnectToInstance}

<p>Connect to a currently running guest instance identified by <code>cid</code>. The
<code>cid</code> can be found via the return value of <code>LaunchInstance</code> or a call to
<code>ListInstances</code>.</p>

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



### ConnectToBalloon {#ConnectToBalloon}

<p>Connect to the memory balloon of a currently running guest instance
identified by <code>cid</code>.</p>

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



### GetHostVsockEndpoint {#GetHostVsockEndpoint}

<p>Returns an interface that can be used to access the host vsock endpoint.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>endpoint</code></td>
            <td>
                <code>request&lt;<a class='link' href='#HostVsockEndpoint'>HostVsockEndpoint</a>&gt;</code>
            </td>
        </tr></table>



## GuestVsockAcceptor {#GuestVsockAcceptor}
*Defined in [fuchsia.virtualization/vsock.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/vsock.fidl#20)*

<p>Exposed by guests capable of listening via vsocks. On a request to establish
a connection, the <code>Accept</code> method will be called. If the port is open and
accepting connections, the implementation should return <code>ZX_OK</code>.</p>
<p>Also see <code>GuestVsockEndpoint</code>.</p>

### Accept {#Accept}


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
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

## HostVsockAcceptor {#HostVsockAcceptor}
*Defined in [fuchsia.virtualization/vsock.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/vsock.fidl#29)*

<p>Exposed by a host capable of listening via vsocks. A variant of a
<code>GuestVsockAcceptor</code> that is responsible for creating the <code>handle</code> with which
to communicate. The <code>handle</code> will be either a socket or a channel, depending
on the current configuration.</p>

### Accept {#Accept}


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
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr><tr>
            <td><code>handle</code></td>
            <td>
                <code>handle&lt;handle&gt;?</code>
            </td>
        </tr></table>

## HostVsockConnector {#HostVsockConnector}
*Defined in [fuchsia.virtualization/vsock.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/vsock.fidl#39)*

<p>Exposed by a host capable of connecting via vsocks. This allows a guest to
identify itself via {src_cid, src_port}, and request to connect to
{cid, port}. The host should return <code>ZX_OK</code>, and create a handle with which
to communicate. The <code>handle</code> will be either a socket or a channel, depending
on the current configuration.</p>

### Connect {#Connect}


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
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr><tr>
            <td><code>handle</code></td>
            <td>
                <code>handle&lt;handle&gt;?</code>
            </td>
        </tr></table>

## GuestVsockEndpoint {#GuestVsockEndpoint}
*Defined in [fuchsia.virtualization/vsock.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/vsock.fidl#50)*

<p>Exposed by guests capable of handling vsock traffic. During
initialization the Manager will assign a unique CID to this endpoint and
provide a <code>HostVsockConnector</code> that can be used to establish outbound
connections. The implementation should provide a <code>GuestVsockAcceptor</code>
implementation that can handle any inbound connection requests.</p>

### SetContextId {#SetContextId}


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



### OnShutdown {#OnShutdown}




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

## HostVsockEndpoint {#HostVsockEndpoint}
*Defined in [fuchsia.virtualization/vsock.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/vsock.fidl#58)*

<p>Exposed by a host to provide the ability for listeners to be multiplexed by
port and to manage dynamic port allocation for outbound connections.</p>

### Listen {#Listen}

<p>Register <code>acceptor</code> to be invoked for any connection requests to <code>port</code>.</p>

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
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

### Connect {#Connect}

<p>Similar to <code>HostVsockConnector.Connect</code> except the <code>src_cid</code> is
<code>HOST_CID</code> and <code>src_port</code> is generated automatically.</p>

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
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### MemStat {#MemStat}
*Defined in [fuchsia.virtualization/balloon_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/balloon_controller.fidl#10)*



<p>Contains a memory statistic for the balloon device.</p>


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

### EnvironmentInfo {#EnvironmentInfo}
*Defined in [fuchsia.virtualization/manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/manager.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>A globally unique identifier for this environment.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>label</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The string provided to <code>Manager.Create</code>.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>instances</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#InstanceInfo'>InstanceInfo</a>&gt;</code>
            </td>
            <td><p>List of guests running in this environment.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### InstanceInfo {#InstanceInfo}
*Defined in [fuchsia.virtualization/manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/manager.fidl#18)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>cid</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Context ID to use to address this guest for vsocket communications. This
can also be used to uniquely identify a guest within an environment.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>label</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The <code>label</code> string originally provided in the <code>LaunchInfo</code> structure
or, if it was the null, the <code>url</code></p>
</td>
            <td>No default</td>
        </tr>
</table>

### BlockDevice {#BlockDevice}
*Defined in [fuchsia.virtualization/realm.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/realm.fidl#31)*



<p>Properties describing a single block device in the system.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>string[20]</code>
            </td>
            <td><p>A label used to identify the block device.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>mode</code></td>
            <td>
                <code><a class='link' href='#BlockMode'>BlockMode</a></code>
            </td>
            <td><p>The access mode for the block backing file.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>format</code></td>
            <td>
                <code><a class='link' href='#BlockFormat'>BlockFormat</a></code>
            </td>
            <td><p>The data format of the backing file.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>file</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#File'>File</a></code>
            </td>
            <td><p>The underlying file that stores the drive contents.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### WaylandDevice {#WaylandDevice}
*Defined in [fuchsia.virtualization/realm.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/realm.fidl#57)*



<p>Properties describing a virtio_wl device.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>memory</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The amount of guest-physical address space to allocate for virtio_wl
buffers.</p>
<p>Default to a 1GiB allocation.</p>
</td>
            <td>1073741824</td>
        </tr><tr>
            <td><code>dispatcher</code></td>
            <td>
                <code><a class='link' href='#WaylandDispatcher'>WaylandDispatcher</a></code>
            </td>
            <td><p>The dispatcher for new virtio_wl connections.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### MagmaDevice {#MagmaDevice}
*Defined in [fuchsia.virtualization/realm.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/realm.fidl#69)*



<p>Properties describing a virtio_magma device.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>memory</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The amount of guest-physical address space to allocate for virtio_magma
buffers.</p>
<p>Default to a 16GiB allocation.</p>
</td>
            <td>17179869184</td>
        </tr>
</table>

### LaunchInfo {#LaunchInfo}
*Defined in [fuchsia.virtualization/realm.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/realm.fidl#77)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>url</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The URL of the package to launch.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>args</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
            <td><p>Arguments that will be passed to the VMM binary when launching this guest.</p>
<p>See ///src/virtualization/bin/vmm/guest_config.cc for valid options.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>label</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>A diagnostic string to associate with this instance.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>flat_namespace</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sys/'>fuchsia.sys</a>/<a class='link' href='../fuchsia.sys/#FlatNamespace'>FlatNamespace</a>?</code>
            </td>
            <td><p>A flat namespace to be appended to the default namespace for the VMM
process.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>block_devices</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#BlockDevice'>BlockDevice</a>&gt;?</code>
            </td>
            <td><p>A set of block devices to add to the virtual machine.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>wayland_device</code></td>
            <td>
                <code><a class='link' href='#WaylandDevice'>WaylandDevice</a>?</code>
            </td>
            <td><p>An optional virtio_wl device.</p>
<p>If not provided, no virtio_wl device will be created by the VMM.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>magma_device</code></td>
            <td>
                <code><a class='link' href='#MagmaDevice'>MagmaDevice</a>?</code>
            </td>
            <td><p>An optional virtio_magma device.</p>
<p>If not provided, no virtio_magma device will be created by the VMM.</p>
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### BlockMode {#BlockMode}
Type: <code>uint32</code>

*Defined in [fuchsia.virtualization/realm.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/realm.fidl#11)*

<p>Mode of the file backing a block device.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>READ_WRITE</code></td>
            <td><code>0</code></td>
            <td><p>Reads and writes are allowed.</p>
</td>
        </tr><tr>
            <td><code>READ_ONLY</code></td>
            <td><code>1</code></td>
            <td><p>Only reads are allowed.</p>
</td>
        </tr><tr>
            <td><code>VOLATILE_WRITE</code></td>
            <td><code>2</code></td>
            <td><p>Writes are allowed, but are stored in memory, not to disk.</p>
</td>
        </tr></table>

### BlockFormat {#BlockFormat}
Type: <code>uint32</code>

*Defined in [fuchsia.virtualization/realm.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/realm.fidl#21)*

<p>Data format of the file backing a block device.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>RAW</code></td>
            <td><code>0</code></td>
            <td><p>Raw IO. All reads and writes go directly to disk as a flat file.</p>
</td>
        </tr><tr>
            <td><code>QCOW</code></td>
            <td><code>1</code></td>
            <td><p>QCOW image. All reads and writes go to a QCOW image.</p>
</td>
        </tr></table>











## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="MAX_BLOCK_DEVICE_ID_SIZE">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/realm.fidl#28">MAX_BLOCK_DEVICE_ID_SIZE</a></td>
            <td>
                    <code>20</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr id="HOST_CID">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization/vsock.fidl#13">HOST_CID</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td><p><code>HOST_CID</code> is the reserved context ID (CID) of the host.</p>
<p>CIDs for guests are assigned by the Manager and can be found in the
corresponding <code>InstanceInfo</code> structure.</p>
</td>
        </tr>
    
</table>



