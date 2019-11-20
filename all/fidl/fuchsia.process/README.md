[TOC]

# fuchsia.process


## **PROTOCOLS**

## Launcher {#Launcher}
*Defined in [fuchsia.process/launcher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-process/launcher.fidl#118)*

<p>A low-level interface for launching processes.</p>
<p>This interface is used for manually assembling a process. The caller supplies
all the capabilities for the newly created process.</p>
<p>That create processes typically use <code>fdio_spawn</code> or <code>fdio_spawn_etc</code> rather
than using this interface directly. The <code>fdio_spawn</code> and <code>fdio_spawn_etc</code>
functions are implemented using this interface.</p>
<p>Debuggers and other clients that need to create processes in a suspended
state often use this interface directly. These clients use the
<code>CreateWithoutStarting</code> method to create the process without actually
starting it.</p>

### Launch {#Launch}

<p>Creates and starts the process described by <code>info</code>.</p>
<p>After processing this message, the <code>Launcher</code> is reset to its initial
state and is ready to launch another process.</p>
<p><code>process</code> is present if, and only if, <code>status</code> is <code>ZX_OK</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#LaunchInfo'>LaunchInfo</a></code>
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
            <td><code>process</code></td>
            <td>
                <code>handle&lt;process&gt;?</code>
            </td>
        </tr></table>

### CreateWithoutStarting {#CreateWithoutStarting}

<p>Creates the process described by <code>info</code> but does not start it.</p>
<p>After processing this message, the <code>Launcher</code> is reset to its initial
state and is ready to launch another process.</p>
<p>The caller is responsible for calling <code>zx_process_start</code> using the data
in <code>ProcessStartData</code> to actually start the process.</p>
<p><code>data</code> is present if, and only if, <code>status</code> is <code>ZX_OK</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#LaunchInfo'>LaunchInfo</a></code>
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
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='#ProcessStartData'>ProcessStartData</a>?</code>
            </td>
        </tr></table>

### AddArgs {#AddArgs}

<p>Adds the given arguments to the command-line for the process.</p>
<p>Calling this method multiple times concatenates the arguments.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>args</code></td>
            <td>
                <code>vector&lt;vector&gt;</code>
            </td>
        </tr></table>



### AddEnvirons {#AddEnvirons}

<p>Adds the given variables to the environment variables for the process.</p>
<p>Calling this method multiple times concatenates the variables.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>environ</code></td>
            <td>
                <code>vector&lt;vector&gt;</code>
            </td>
        </tr></table>



### AddNames {#AddNames}

<p>Adds the given names to the namespace for the process.</p>
<p>The paths in the namespace must be non-overlapping. See
<a href="https://fuchsia.dev/fuchsia-src/concepts/framework/namespaces">https://fuchsia.dev/fuchsia-src/concepts/framework/namespaces</a> for details.</p>
<p>Calling this method multiple times concatenates the names.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>names</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#NameInfo'>NameInfo</a>&gt;</code>
            </td>
        </tr></table>



### AddHandles {#AddHandles}

<p>Adds the given handles to the startup handles for the process.</p>
<p>Calling this method multiple times concatenates the handles.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>handles</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#HandleInfo'>HandleInfo</a>&gt;</code>
            </td>
        </tr></table>



## Resolver {#Resolver}
*Defined in [fuchsia.process/resolver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-process/resolver.fidl#29)*

<p>An interface for resolving names to executables and library loaders.</p>
<p>An executable itself is often not sufficient to create a working process
because many executables also load shared libraries. On Fuchsia, there is no
global pool of shared libraries. Instead, every process has an associated
<code>fuchsia.ldsvc.Loader</code>, which provides access to a private pool of shared
libraries appropriate for that process.</p>
<p>This interface provides a protocol for resolving a name into both the
<code>handle&lt;vmo&gt;</code> for the executable and the <code>fuchsia.ldsvc.Loader</code> for its
associated shared libraries.</p>
<p>This interface is rarely used directly. Instead, <code>fdio_spawn</code> and
<code>fdio_spawn_etc</code> use this interface internally when they try to run a file
with a <code>#!resolve</code> directive.</p>

### Resolve {#Resolve}

<p>Resolves the given <code>name</code> to an <code>executable</code> and an shared library
loader.</p>
<p>If present, the <code>executable</code> is suitable for use as the <code>executable</code>
property of <code>LaunchInfo</code>. If present, the <code>ldsvc</code> is suitable for use as
the <code>PA_LDSVC_LOADER</code> handle when launching the process.</p>
<p>For example, the resolver might locate the given <code>name</code> inside a package
and return the executable binary from the package as well as a shared
library loader scoped to that package.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string[2048]</code>
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
            <td><code>executable</code></td>
            <td>
                <code>handle&lt;vmo&gt;?</code>
            </td>
        </tr><tr>
            <td><code>ldsvc</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ldsvc/'>fuchsia.ldsvc</a>/<a class='link' href='../fuchsia.ldsvc/#Loader'>Loader</a>?</code>
            </td>
        </tr></table>



## **STRUCTS**

### HandleInfo {#HandleInfo}
*Defined in [fuchsia.process/launcher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-process/launcher.fidl#18)*



<p>Information about a handle provided to a process at startup.</p>
<p>Processes are given a set of initial handles as part of the bootstrapping
sequence. Some of these handles are associated with zx.procarg identifiers
that designate their intended use by the new process.</p>
<p>This structure represents one such handle and its associated zx.procarg
identifier.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>handle</code></td>
            <td>
                <code>handle&lt;handle&gt;</code>
            </td>
            <td><p>The handle to use for this process argument.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Process argument identifier.</p>
<p>See &lt;zircon/processargs.h&gt; for definitions of well-known process
arguments.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### NameInfo {#NameInfo}
*Defined in [fuchsia.process/launcher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-process/launcher.fidl#36)*



<p>A namespace entry provided to a process at startup.</p>
<p>Processes are given a set of initial handles as part of the bootstrapping
sequence. Some of these handles are associated with paths that designate
their intended use by the new process as namespace entries.</p>
<p>This structure represents one such handle and its associated namespace path.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>path</code></td>
            <td>
                <code>string[4096]</code>
            </td>
            <td><p>Path at which to install the associated directory.</p>
<p>Must be an absolute path (i.e., start with '/').</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>directory</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#Directory'>Directory</a></code>
            </td>
            <td><p>The associated directory.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### LaunchInfo {#LaunchInfo}
*Defined in [fuchsia.process/launcher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-process/launcher.fidl#47)*



<p>The information needed to launch a process.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>executable</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
            <td><p>The executable to run in the process.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>job</code></td>
            <td>
                <code>handle&lt;job&gt;</code>
            </td>
            <td><p>The job in which to create the process.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[32]</code>
            </td>
            <td><p>The name to assign to the created process.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### ProcessStartData {#ProcessStartData}
*Defined in [fuchsia.process/launcher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-process/launcher.fidl#61)*



<p>The information required to start a process.</p>
<p>To start the process, call <code>zx_process_start</code> with the arguments provided.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>process</code></td>
            <td>
                <code>handle&lt;process&gt;</code>
            </td>
            <td><p>The process that was created.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>root_vmar</code></td>
            <td>
                <code>handle&lt;vmar&gt;</code>
            </td>
            <td><p>The vmar object that was created when the process was created.</p>
<p>See <a href="https://fuchsia.dev/fuchsia-src/reference/syscalls/process_create.md">https://fuchsia.dev/fuchsia-src/reference/syscalls/process_create.md</a>.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>thread</code></td>
            <td>
                <code>handle&lt;thread&gt;</code>
            </td>
            <td><p>The initial thread for the process.</p>
<p>Should be passed to <code>zx_process_start</code> when starting the process.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>entry</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The address of the initial entry point in the process.</p>
<p>Should be passed to <code>zx_process_start</code> when starting the process.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>stack</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The stack pointer value for the initial thread of the process.</p>
<p>Should be passed to <code>zx_process_start</code> when starting the process.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>bootstrap</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
            <td><p>The bootstrap channel to pass to the process on startup.</p>
<p>Should be passed to <code>zx_process_start</code> when starting the process.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>vdso_base</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The base address of the vDSO to pass to the process on startup.</p>
<p>Should be passed to <code>zx_process_start</code> when starting the process.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>base</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The base load address of the ELF file loaded.</p>
<p>Most often used by debuggers or other tools that inspect the process.</p>
</td>
            <td>No default</td>
        </tr>
</table>













## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-process/launcher.fidl#102">MAX</a></td>
            <td>
                    <code>4294967295</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-process/resolver.fidl#11">MAX_RESOLVE_NAME_SIZE</a></td>
            <td>
                    <code>2048</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum size for a name used by <code>Resolver</code>.</p>
</td>
        </tr>
    
</table>

