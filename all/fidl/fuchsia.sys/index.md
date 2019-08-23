Project: /_project.yaml
Book: /_book.yaml

# fuchsia.sys


## **PROTOCOLS**

## ComponentController {:#ComponentController}
*Defined in [fuchsia.sys/component_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/component_controller.fidl#36)*

 An interface for controlling components.

 Closing this interface implicitly kills the controlled component unless
 the `Detach` method has been called.

 If the component exits, this interface will be closed.

 Typically obtained via `Launcher.CreateComponent`.

### Kill {:#Kill}

 Terminates the component.

 This ComponentController connection is closed when the component has
 terminated.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Detach {:#Detach}

 Decouples the lifetime of the component from this controller.

 After calling `Detach`, the component will not be implicitly killed when
 this interface is closed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### OnTerminated {:#OnTerminated}

 Event that is triggered when the component is terminated.

 This event provides the return code of the process and reason for
 its termination. The return_code is only valid if the termination
 reason is EXITED. If the termination reason is not EXITED, the
 return code is guaranteed not to be 0.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>return_code</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>termination_reason</code></td>
            <td>
                <code><a class='link' href='#TerminationReason'>TerminationReason</a></code>
            </td>
        </tr></table>

### OnDirectoryReady {:#OnDirectoryReady}

 Event that is triggered when the component's output directory is mounted.

 This event will not be triggered for every component, only those that
 serve a directory over their `PA_DIRECTORY_REQUEST` handle.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## Environment {:#Environment}
*Defined in [fuchsia.sys/environment.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/environment.fidl#32)*

 An interface for managing a set of applications.

 Applications run inside environments, which provide ambient services and
 support for their lifecycle.

### CreateNestedEnvironment {:#CreateNestedEnvironment}

 Creates a new environment nested inside this environment.

 When applications are created inside the nested environment using the
 environment's `Launcher`, the environment requests the
 environment services from `host_directory` before passing those services to
 the newly created application in its `StartupInfo`.

 The `controller` can be used to control the lifecycle of the created
 environment. Note that by default the environment will be killed
 automatically when the `EnvironmentController`'s interface is closed. You
 can use `EnvironmentController.Detach` to disable this behavior.

 `label` defines the new environment's label/name. It must be unique within
 the parent environment (though not globally) and is used for isolating
 separate environments. It can also be used for diagnostic purposes. The
 label will be truncated if it is longer than `kLabelMaxLength`.

 `additional_services`, which may be empty, contains a list of services
 that the environment provides, which are hosted by
 `additional_services.host_directory`. If `options.inherit_parent_services`
 is false, `host_directory` must provide a `Loader` service if it wishes to
 allow new components to be loaded in the new environment.

 `options` provides additional options, see `EnvironmentOptions` for
 details.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>environment</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Environment'>Environment</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>controller</code></td>
            <td>
                <code>request&lt;<a class='link' href='#EnvironmentController'>EnvironmentController</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>label</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>additional_services</code></td>
            <td>
                <code><a class='link' href='#ServiceList'>ServiceList</a>?</code>
            </td>
        </tr><tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#EnvironmentOptions'>EnvironmentOptions</a></code>
            </td>
        </tr></table>



### GetLauncher {:#GetLauncher}

 Gets the Launcher associated with this environment.

 Applications created using this application launcher will be given the
 environment services provided by this environment's `host_directory`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>launcher</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Launcher'>Launcher</a>&gt;</code>
            </td>
        </tr></table>



### GetServices {:#GetServices}

 Gets a superset of services provided by this environment's
 `host_directory`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>services</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ServiceProvider'>ServiceProvider</a>&gt;</code>
            </td>
        </tr></table>



### GetDirectory {:#GetDirectory}

 Gets a superset of services provided by this environment's
 `host_directory`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>directory_request</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



## EnvironmentController {:#EnvironmentController}
*Defined in [fuchsia.sys/environment_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/environment_controller.fidl#15)*

 An interface for controlling an environment.

 Closing this interface implicitly kills the controlled environment unless
 the `Detach` method has been called.

 If the environment is destroyed, this interface will be closed.

 Typically obtained via `Environment.CreateNestedEnvironment`.

### Kill {:#Kill}

 Terminates the environment.

 When an `Environment` is terminated, all applications launched
 in the environment (and in all transitively nested environments) are also
 killed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### Detach {:#Detach}

 Decouples the lifetime of the environment from this controller.

 After calling `Detach`, the environment will not be implicitly killed when
 this interface is closed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### OnCreated {:#OnCreated}

 Event that is triggered when the environment is created.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## JobProvider {:#JobProvider}
*Defined in [fuchsia.sys/job_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/job_provider.fidl#11)*

 An interface for providing a job handle. Instances of this interface are
 created in the context of an already-identified realm, so there is no need
 to explicitly identify the realm below.

### GetJob {:#GetJob}

 Gets the root job associated with the realm.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>job</code></td>
            <td>
                <code>handle&lt;job&gt;</code>
            </td>
        </tr></table>

## Launcher {:#Launcher}
*Defined in [fuchsia.sys/launcher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/launcher.fidl#78)*

 An interface for creating component instances.

 Typically obtained via `Environment.GetLauncher`.

### CreateComponent {:#CreateComponent}

 Creates a new instance of the component described by `launch_info`.

 The component instance is created in the `Environment`
 associated with this `Launcher`. When creating the component,
 the environment requests the environment services for this component from
 its `EnvironmentHost`.

 The `controller` can be used to control the lifecycle of the created
 component instance. If an `ComponentController`'s interface is
 requested, the component instance is killed when the interface is closed.

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
                <code>request&lt;<a class='link' href='#ComponentController'>ComponentController</a>&gt;?</code>
            </td>
        </tr></table>



## Loader {:#Loader}
*Defined in [fuchsia.sys/loader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/loader.fidl#9)*

 An interface for loading from packages.

### LoadUrl {:#LoadUrl}

 LoadUrl a package by url.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>url</code></td>
            <td>
                <code>string[2083]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>package</code></td>
            <td>
                <code><a class='link' href='#Package'>Package</a>?</code>
            </td>
        </tr></table>

## Runner {:#Runner}
*Defined in [fuchsia.sys/runner.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/runner.fidl#64)*

 An interface for running components.

 Typically exposed by components that provide execution environments for
 particular classes of programs. For example, the Dart virtual machine
 exposes this interface to run Dart programs.

### StartComponent {:#StartComponent}

 Execute the given component.

 Upon startup, the component is to be given the information in
 `startup_info`, but the mechanism by which the component receives that
 information is up to the component runner.

 The `controller` interface request typically originates from the
 `Launcher.CreateComponent` message that caused this component to be
 started.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>package</code></td>
            <td>
                <code><a class='link' href='#Package'>Package</a></code>
            </td>
        </tr><tr>
            <td><code>startup_info</code></td>
            <td>
                <code><a class='link' href='#StartupInfo'>StartupInfo</a></code>
            </td>
        </tr><tr>
            <td><code>controller</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ComponentController'>ComponentController</a>&gt;?</code>
            </td>
        </tr></table>



## ServiceProvider {:#ServiceProvider}
*Defined in [fuchsia.sys/service_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/service_provider.fidl#15)*

 An interface through which a client may request services from a host.
 Instances of this interface are created within the context of an
 already-identified client and host pair, so there is no need to explicitly
 identify the client or host in the methods below.

 This interface is deprecated.  Services should be published as directory
 entries instead, just like files.

### ConnectToService {:#ConnectToService}

 Asks the host to provide the service identified by `service_name` through
 the `channel` endpoint supplied by the caller. If the host is not willing
 or able to provide the requested service, it should close the `channel`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>channel</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>





## **STRUCTS**

### EnvironmentOptions {:#EnvironmentOptions}
*Defined in [fuchsia.sys/environment.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/environment.fidl#10)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>inherit_parent_services</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> True if this environment should inherit services provided by the
 parent environment.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>allow_parent_runners</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> True if components in this environment can share a runner provided
 by the parent environment. If false, a new runner will be started
 in this environment for components.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>kill_on_oom</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> True if this environment should be killed first in out of memory
 situations by setting the `ZX_PROP_JOB_KILL_ON_OOM` property on this
 environment's job.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>delete_storage_on_death</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> True if "persistent" storage requested by components in this environment should not actually
 be persistent, and instead be deleted when this environment is killed.
</td>
            <td>No default</td>
        </tr>
</table>

### FlatNamespace {:#FlatNamespace}
*Defined in [fuchsia.sys/flat_namespace.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/flat_namespace.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>paths</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td> The mount point for each of the directories below.

 For example, ["/pkg", "/svc"].
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>directories</code></td>
            <td>
                <code>vector&lt;channel&gt;</code>
            </td>
            <td> The directories mounted at each path in the namespace.
</td>
            <td>No default</td>
        </tr>
</table>

### FileDescriptor {:#FileDescriptor}
*Defined in [fuchsia.sys/launcher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/launcher.fidl#9)*



 An FDIO file descriptor.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>type0</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The FDIO types of the handle (e.g., `FA_FDIO_REMOTE`).
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>type1</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>type2</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>handle0</code></td>
            <td>
                <code>handle&lt;handle&gt;?</code>
            </td>
            <td> The handles for the file descriptor (e.g., a channel).
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>handle1</code></td>
            <td>
                <code>handle&lt;handle&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>handle2</code></td>
            <td>
                <code>handle&lt;handle&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### LaunchInfo {:#LaunchInfo}
*Defined in [fuchsia.sys/launcher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/launcher.fidl#23)*



 Information used to create an instance of a component and obtain
 services from it.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>url</code></td>
            <td>
                <code>string[2083]</code>
            </td>
            <td> The location from which to retrieve this component.

 This field will probably be replaced with a stronger notion of identity,
 such as an unforgeable token. This field is included in this iteration to
 ease the transition from the previous component interfaces.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>arguments</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
            <td> The arguments to be provided to the component.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>out</code></td>
            <td>
                <code><a class='link' href='#FileDescriptor'>FileDescriptor</a>?</code>
            </td>
            <td> The file descriptor to use for stdout.

 If null, the component will use the default stdout for the environment.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#FileDescriptor'>FileDescriptor</a>?</code>
            </td>
            <td> The file descriptor to use for stderr.

 If null, the component will use the default stderr for the environment.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>directory_request</code></td>
            <td>
                <code>handle&lt;channel&gt;?</code>
            </td>
            <td> The interface request for a Directory that is passed through to the
 component and arrives in the component as its `directory_request`
 interface request.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>flat_namespace</code></td>
            <td>
                <code><a class='link' href='#FlatNamespace'>FlatNamespace</a>?</code>
            </td>
            <td> A custom namespace that can be appended to the namespace generated by
 appmgr and provided to this component.
 Adding a mount point at standard paths like 'pkg' or 'svc' will be ignored.
 HACK(alhaad): Adding mount points for deprecated default directories like
 '/data' will override the default.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>additional_services</code></td>
            <td>
                <code><a class='link' href='#ServiceList'>ServiceList</a>?</code>
            </td>
            <td> A list of services to be added to this component's svc namespace. These
 services are in addition to those coming from Environment.
</td>
            <td>No default</td>
        </tr>
</table>

### ServiceList {:#ServiceList}
*Defined in [fuchsia.sys/launcher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/launcher.fidl#61)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>names</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td> A list of services that can be requested from `provider`.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>provider</code></td>
            <td>
                <code><a class='link' href='#ServiceProvider'>ServiceProvider</a>?</code>
            </td>
            <td> A service provider to get the services listed in `names` from.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>host_directory</code></td>
            <td>
                <code>handle&lt;channel&gt;?</code>
            </td>
            <td> A channel to the directory hosting the services in `names`.
</td>
            <td>No default</td>
        </tr>
</table>

### StartupInfo {:#StartupInfo}
*Defined in [fuchsia.sys/runner.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/runner.fidl#13)*



 Information given to components at startup.

 For ELF binaries, this information is provided in the initialization
 message given to `libc` by `fuchsia.process.Launcher`.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>launch_info</code></td>
            <td>
                <code><a class='link' href='#LaunchInfo'>LaunchInfo</a></code>
            </td>
            <td> The launch info for the component to start.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>flat_namespace</code></td>
            <td>
                <code><a class='link' href='#FlatNamespace'>FlatNamespace</a></code>
            </td>
            <td> The namespace in which to run the component.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>program_metadata</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ProgramMetadata'>ProgramMetadata</a>&gt;?</code>
            </td>
            <td> Key string value string map of the component's program metadata,
 obtained from its component manifest.
</td>
            <td>No default</td>
        </tr>
</table>

### ProgramMetadata {:#ProgramMetadata}
*Defined in [fuchsia.sys/runner.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/runner.fidl#29)*



 Program information about a component.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Key for program metadata pair. E.g. "binary" for an ELF binary
 component, or "data" for a flutter/dart component.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Value for program metadata pair. E.g. "bin/app" for a "binary" key, or
 "data/foo" for a flutter/dart component.
</td>
            <td>No default</td>
        </tr>
</table>

### Package {:#Package}
*Defined in [fuchsia.sys/runner.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/runner.fidl#42)*



 A binary representation of a component.

 Typically provided to `Runner.StartComponent` when starting a component.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a>?</code>
            </td>
            <td> A read-only binary representation of the component. For example, if the
 component is intended to run in the Dart virtual machine, this data
 might contain a dartx package.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>directory</code></td>
            <td>
                <code>handle&lt;channel&gt;?</code>
            </td>
            <td> A directory containing the contents of the package. For example, if the
 component is stored in pkgfs, this directory will be the pkgfs
 directory containing the package.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>resolved_url</code></td>
            <td>
                <code>string[2083]</code>
            </td>
            <td> Resolved URL of the component. This is the url specified in
 `startup_info` after following redirects and resolving relative paths.
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### TerminationReason {:#TerminationReason}
Type: <code>uint32</code>

*Defined in [fuchsia.sys/component_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/component_controller.fidl#7)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>EXITED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>URL_INVALID</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>PACKAGE_NOT_FOUND</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>INTERNAL_ERROR</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>PROCESS_CREATION_ERROR</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>RUNNER_FAILED</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>RUNNER_TERMINATED</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNSUPPORTED</code></td>
            <td><code>8</code></td>
            <td></td>
        </tr></table>











## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/environment.fidl#8">kLabelMaxLength</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
            <td> Maximum length for an environment label.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/types.fidl#11">MAX_URL_LENGTH</a></td>
            <td>
                    <code>2083</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    
</table>

