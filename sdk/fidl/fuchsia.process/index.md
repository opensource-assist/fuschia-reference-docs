Project: /_project.yaml
Book: /_book.yaml

# fuchsia.process


## **PROTOCOLS**

## Launcher {:#Launcher}
*Defined in [fuchsia.process/launcher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-process/launcher.fidl#118)*

 A low-level interface for launching processes.

 This interface is used for manually assembling a process. The caller supplies
 all the capabilities for the newly created process.

 That create processes typically use `fdio_spawn` or `fdio_spawn_etc` rather
 than using this interface directly. The `fdio_spawn` and `fdio_spawn_etc`
 functions are implemented using this interface.

 Debuggers and other clients that need to create processes in a suspended
 state often use this interface directly. These clients use the
 `CreateWithoutStarting` method to create the process without actually
 starting it.

### Launch {:#Launch}

 Creates and starts the process described by `info`.

 After processing this message, the `Launcher` is reset to its initial
 state and is ready to launch another process.

 `process` is present if, and only if, `status` is ZX_OK.

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

### CreateWithoutStarting {:#CreateWithoutStarting}

 Creates the process described by `info` but does not start it.

 After processing this message, the `Launcher` is reset to its initial
 state and is ready to launch another process.

 The caller is responsible for calling `zx_process_start` using the data
 in `ProcessStartData` to actually start the process.

 `data` is present if, and only if, `status` is ZX_OK.

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

### AddArgs {:#AddArgs}

 Adds the given arguments to the command-line for the process.

 Calling this method multiple times concatenates the arguments.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>args</code></td>
            <td>
                <code>vector&lt;vector&gt;</code>
            </td>
        </tr></table>



### AddEnvirons {:#AddEnvirons}

 Adds the given variables to the environment variables for the process.

 Calling this method multiple times concatenates the variables.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>environ</code></td>
            <td>
                <code>vector&lt;vector&gt;</code>
            </td>
        </tr></table>



### AddNames {:#AddNames}

 Adds the given names to the namespace for the process.

 The paths in the namespace must be non-overlapping. See
 <https://fuchsia.googlesource.com/fuchsia/+/master/docs/the-book/namespaces.md>
 for details.

 Calling this method multiple times concatenates the names.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>names</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#NameInfo'>NameInfo</a>&gt;</code>
            </td>
        </tr></table>



### AddHandles {:#AddHandles}

 Adds the given handles to the startup handles for the process.

 Calling this method multiple times concatenates the handles.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>handles</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#HandleInfo'>HandleInfo</a>&gt;</code>
            </td>
        </tr></table>



## Resolver {:#Resolver}
*Defined in [fuchsia.process/resolver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-process/resolver.fidl#29)*

 An interface for resolving names to executables and library loaders.

 An executable itself is often not sufficient to create a working process
 because many executables also load shared libraries. On Fuchsia, there is no
 global pool of shared libraries. Instead, every process has an associated
 `fuchsia.ldsvc.Loader`, which provides access to a private pool of shared
 libraries appropriate for that process.

 This interface provides a protocol for resolving a name into both the
 `handle<vmo>` for the executable and the `fuchsia.ldsvc.Loader` for its
 associated shared libraries.

 This interface is rarely used directly. Instead, `fdio_spawn` and
 `fdio_spawn_etc` use this interface internally when they try to run a file
 with a `#!resolve` directive.

### Resolve {:#Resolve}

 Resolves the given `name` to an `executable` and an shared library
 loader.

 If present, the `executable` is suitable for use as the `executable`
 property of `LaunchInfo`. If present, the `ldsvc` is suitable for use as
 the PA_LDSVC_LOADER handle when launching the process.

 For example, the resolver might locate the given `name` inside a package
 and return the executable binary from the package as well as a shared
 library loader scoped to that package.

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
                <code><a class='link' href='../fuchsia.ldsvc/index.html'>fuchsia.ldsvc</a>/<a class='link' href='../fuchsia.ldsvc/index.html#Loader'>Loader</a>?</code>
            </td>
        </tr></table>



## **STRUCTS**

### HandleInfo {:#HandleInfo}
*Defined in [fuchsia.process/launcher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-process/launcher.fidl#18)*



 Information about a handle provided to a process at startup.

 Processes are given a set of initial handles as part of the bootstrapping
 sequence. Some of these handles are associated with zx.procarg identifiers
 that designate their intended use by the new process.

 This structure represents one such handle and its associated zx.procarg
 identifier.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>handle</code></td>
            <td>
                <code>handle&lt;handle&gt;</code>
            </td>
            <td> The handle to use for this process argument.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Process argument identifier.

 See <zircon/processargs.h> for definitions of well-known process
 arguments.
</td>
            <td>No default</td>
        </tr>
</table>

### NameInfo {:#NameInfo}
*Defined in [fuchsia.process/launcher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-process/launcher.fidl#36)*



 A namespace entry provided to a process at startup.

 Processes are given a set of initial handles as part of the bootstrapping
 sequence. Some of these handles are associated with paths that designate
 their intended use by the new process as namespace entries.

 This structure represents one such handle and its associated namespace path.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>path</code></td>
            <td>
                <code>string[4096]</code>
            </td>
            <td> Path at which to install the associated directory.

 Must be an absolute path (i.e., start with '/').
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>directory</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io/index.html'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/index.html#Directory'>Directory</a></code>
            </td>
            <td> The associated directory.
</td>
            <td>No default</td>
        </tr>
</table>

### LaunchInfo {:#LaunchInfo}
*Defined in [fuchsia.process/launcher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-process/launcher.fidl#47)*



 The information needed to launch a process.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>executable</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
            <td> The executable to run in the process.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>job</code></td>
            <td>
                <code>handle&lt;job&gt;</code>
            </td>
            <td> The job in which to create the process.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The name to assign to the created process.

</td>
            <td>No default</td>
        </tr>
</table>

### ProcessStartData {:#ProcessStartData}
*Defined in [fuchsia.process/launcher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-process/launcher.fidl#64)*



 The information required to start a process.

 To start the process, call `zx_process_start` with the arguments provided.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>process</code></td>
            <td>
                <code>handle&lt;process&gt;</code>
            </td>
            <td> The process that was created.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>root_vmar</code></td>
            <td>
                <code>handle&lt;vmar&gt;</code>
            </td>
            <td> The vmar object that was created when the process was created.

 See <https://fuchsia.googlesource.com/fuchsia/+/master/zircon/docs/syscalls/process_create.md>.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>thread</code></td>
            <td>
                <code>handle&lt;thread&gt;</code>
            </td>
            <td> The initial thread for the process.

 Should be passed to `zx_process_start` when starting the process.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>entry</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The address of the initial entry point in the process.

 Should be passed to `zx_process_start` when starting the process.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>stack</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The stack pointer value for the initial thread of the process.

 Should be passed to `zx_process_start` when starting the process.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>bootstrap</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
            <td> The bootstrap channel to pass to the process on startup.

 Should be passed to `zx_process_start` when starting the process.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>vdso_base</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The base address of the vDSO to pass to the process on startup.

 Should be passed to `zx_process_start` when starting the process.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>base</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The base load address of the ELF file loaded.

 Most often used by debuggers or other tools that inspect the process.
</td>
            <td>No default</td>
        </tr>
</table>













## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-process/resolver.fidl#11">MAX_RESOLVE_NAME_SIZE</a></td>
            <td>
                    <code>2048</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    
</table>

