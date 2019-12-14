[TOC]

# fuchsia.netemul.guest


## **PROTOCOLS**

## GuestDiscovery {#GuestDiscovery}
*Defined in [fuchsia.netemul.guest/fuchsia.netemul.guest_interaction.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/virtualization/lib/guest_interaction/fidl/fuchsia.netemul.guest_interaction.fidl#15)*

<p>Enables discovery of guest VM's for control in tests.</p>

### GetGuest {#GetGuest}

<p>Finds the guest VM specified by realm name/guest name pair and connects to it to enable
file transfers and execution of commands.  If <code>realm_name</code> is null, <code>DEFAULT_REALM</code> is
used instead.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>realm_name</code></td>
            <td>
                <code>string[1024]?</code>
            </td>
        </tr><tr>
            <td><code>guest_name</code></td>
            <td>
                <code>string[1024]</code>
            </td>
        </tr><tr>
            <td><code>guest</code></td>
            <td>
                <code>request&lt;<a class='link' href='#GuestInteraction'>GuestInteraction</a>&gt;</code>
            </td>
        </tr></table>



## CommandListener {#CommandListener}
*Defined in [fuchsia.netemul.guest/fuchsia.netemul.guest_interaction.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/virtualization/lib/guest_interaction/fidl/fuchsia.netemul.guest_interaction.fidl#30)*


### OnStarted {#OnStarted}

<p>Signal to a client that is attempting to exec inside of a guest whether
or not the subprocess was successfully started.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

### OnTerminated {#OnTerminated}

<p>Signal to a client that the Exec request has completed.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr><tr>
            <td><code>return_code</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

## GuestInteraction {#GuestInteraction}
*Defined in [fuchsia.netemul.guest/fuchsia.netemul.guest_interaction.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/virtualization/lib/guest_interaction/fidl/fuchsia.netemul.guest_interaction.fidl#39)*


### PutFile {#PutFile}

<p>Take a local file from the Fuchsia host and transfer it to a destination
location on the guest under test.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>local_file</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#File'>File</a></code>
            </td>
        </tr><tr>
            <td><code>remote_path</code></td>
            <td>
                <code>string[1024]</code>
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

### GetFile {#GetFile}

<p>Pull a file from the guest under test and copy it to the specified
location on the Fuchsia host.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>remote_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
        </tr><tr>
            <td><code>local_file</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#File'>File</a></code>
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

### ExecuteCommand {#ExecuteCommand}

<p>Execute command on the guest under test and return the resulting output,
error, and return code.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>command</code></td>
            <td>
                <code>string[1024]</code>
            </td>
        </tr><tr>
            <td><code>env</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#EnvironmentVariable'>EnvironmentVariable</a>&gt;[1024]</code>
            </td>
        </tr><tr>
            <td><code>stdin</code></td>
            <td>
                <code>handle&lt;socket&gt;?</code>
            </td>
        </tr><tr>
            <td><code>stdout</code></td>
            <td>
                <code>handle&lt;socket&gt;?</code>
            </td>
        </tr><tr>
            <td><code>stderr</code></td>
            <td>
                <code>handle&lt;socket&gt;?</code>
            </td>
        </tr><tr>
            <td><code>command_listener</code></td>
            <td>
                <code>request&lt;<a class='link' href='#CommandListener'>CommandListener</a>&gt;</code>
            </td>
        </tr></table>





## **STRUCTS**

### EnvironmentVariable {#EnvironmentVariable}
*Defined in [fuchsia.netemul.guest/fuchsia.netemul.guest_interaction.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/virtualization/lib/guest_interaction/fidl/fuchsia.netemul.guest_interaction.fidl#25)*



<p>Represents a key/value pair to be injected into an environment where a command is executed.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>













## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="GUEST_INTERACTION_MAX_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/src/virtualization/lib/guest_interaction/fidl/fuchsia.netemul.guest_interaction.fidl#10">GUEST_INTERACTION_MAX_LENGTH</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="DEFAULT_REALM">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/src/virtualization/lib/guest_interaction/fidl/fuchsia.netemul.guest_interaction.fidl#11">DEFAULT_REALM</a></td>
            <td><code>gis_default</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    
</table>



