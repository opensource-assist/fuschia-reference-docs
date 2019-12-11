[TOC]

# fuchsia.sys


## **PROTOCOLS**

## ComponentController {#ComponentController}
*Defined in [fuchsia.sys/component_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/component_controller.fidl#36)*

<p>An interface for controlling components.</p>
<p>Closing this interface implicitly kills the controlled component unless
the <code>Detach</code> method has been called.</p>
<p>If the component exits, this interface will be closed.</p>
<p>Typically obtained via <code>Launcher.CreateComponent</code>.</p>

### Kill {#Kill}

<p>Terminates the component.</p>
<p>This ComponentController connection is closed when the component has
terminated.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Detach {#Detach}

<p>Decouples the lifetime of the component from this controller.</p>
<p>After calling <code>Detach</code>, the component will not be implicitly killed when
this interface is closed.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### OnTerminated {#OnTerminated}

<p>Event that is triggered when the component is terminated.</p>
<p>This event provides the return code of the process and reason for
its termination. The return_code is only valid if the termination
reason is EXITED. If the termination reason is not EXITED, the
return code is guaranteed not to be 0.</p>



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

### OnDirectoryReady {#OnDirectoryReady}

<p>Event that is triggered when the component's output directory is mounted.</p>
<p>This event will not be triggered for every component, only those that
serve a directory over their <code>PA_DIRECTORY_REQUEST</code> handle.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## Environment {#Environment}
*Defined in [fuchsia.sys/environment.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/environment.fidl#32)*

<p>An interface for managing a set of applications.</p>
<p>Applications run inside environments, which provide ambient services and
support for their lifecycle.</p>

### CreateNestedEnvironment {#CreateNestedEnvironment}

<p>Creates a new environment nested inside this environment.</p>
<p>When applications are created inside the nested environment using the
environment's <code>Launcher</code>, the environment requests the
environment services from <code>host_directory</code> before passing those services to
the newly created application in its <code>StartupInfo</code>.</p>
<p>The <code>controller</code> can be used to control the lifecycle of the created
environment. Note that by default the environment will be killed
automatically when the <code>EnvironmentController</code>'s interface is closed. You
can use <code>EnvironmentController.Detach</code> to disable this behavior.</p>
<p><code>label</code> defines the new environment's label/name. It must be unique within
the parent environment (though not globally) and is used for isolating
separate environments. It can also be used for diagnostic purposes. The
label will be truncated if it is longer than <code>kLabelMaxLength</code>.</p>
<p><code>additional_services</code>, which may be empty, contains a list of services
that the environment provides, which are hosted by
<code>additional_services.host_directory</code>. If <code>options.inherit_parent_services</code>
is false, <code>host_directory</code> must provide a <code>Loader</code> service if it wishes to
allow new components to be loaded in the new environment.</p>
<p><code>options</code> provides additional options, see <code>EnvironmentOptions</code> for
details.</p>

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



### GetLauncher {#GetLauncher}

<p>Gets the Launcher associated with this environment.</p>
<p>Applications created using this application launcher will be given the
environment services provided by this environment's <code>host_directory</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>launcher</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Launcher'>Launcher</a>&gt;</code>
            </td>
        </tr></table>



### GetServices {#GetServices}

<p>Gets a superset of services provided by this environment's
<code>host_directory</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>services</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ServiceProvider'>ServiceProvider</a>&gt;</code>
            </td>
        </tr></table>



### GetDirectory {#GetDirectory}

<p>Gets a superset of services provided by this environment's
<code>host_directory</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>directory_request</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



## EnvironmentController {#EnvironmentController}
*Defined in [fuchsia.sys/environment_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/environment_controller.fidl#15)*

<p>An interface for controlling an environment.</p>
<p>Closing this interface implicitly kills the controlled environment unless
the <code>Detach</code> method has been called.</p>
<p>If the environment is destroyed, this interface will be closed.</p>
<p>Typically obtained via <code>Environment.CreateNestedEnvironment</code>.</p>

### Kill {#Kill}

<p>Terminates the environment.</p>
<p>When an <code>Environment</code> is terminated, all applications launched
in the environment (and in all transitively nested environments) are also
killed.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### Detach {#Detach}

<p>Decouples the lifetime of the environment from this controller.</p>
<p>After calling <code>Detach</code>, the environment will not be implicitly killed when
this interface is closed.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### OnCreated {#OnCreated}

<p>Event that is triggered when the environment is created.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## JobProvider {#JobProvider}
*Defined in [fuchsia.sys/job_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/job_provider.fidl#11)*

<p>An interface for providing a job handle. Instances of this interface are
created in the context of an already-identified realm, so there is no need
to explicitly identify the realm below.</p>

### GetJob {#GetJob}

<p>Gets the root job associated with the realm.</p>

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

## Launcher {#Launcher}
*Defined in [fuchsia.sys/launcher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/launcher.fidl#78)*

<p>An interface for creating component instances.</p>
<p>Typically obtained via <code>Environment.GetLauncher</code>.</p>

### CreateComponent {#CreateComponent}

<p>Creates a new instance of the component described by <code>launch_info</code>.</p>
<p>The component instance is created in the <code>Environment</code>
associated with this <code>Launcher</code>. When creating the component,
the environment requests the environment services for this component from
its <code>EnvironmentHost</code>.</p>
<p>The <code>controller</code> can be used to control the lifecycle of the created
component instance. If an <code>ComponentController</code>'s interface is
requested, the component instance is killed when the interface is closed.</p>

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



## Loader {#Loader}
*Defined in [fuchsia.sys/loader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/loader.fidl#9)*

<p>An interface for loading from packages.</p>

### LoadUrl {#LoadUrl}

<p>LoadUrl a package by url.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>url</code></td>
            <td>
                <code><a class='link' href='#component_url'>component_url</a></code>
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

## Runner {#Runner}
*Defined in [fuchsia.sys/runner.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/runner.fidl#64)*

<p>An interface for running components.</p>
<p>Typically exposed by components that provide execution environments for
particular classes of programs. For example, the Dart virtual machine
exposes this interface to run Dart programs.</p>

### StartComponent {#StartComponent}

<p>Execute the given component.</p>
<p>Upon startup, the component is to be given the information in
<code>startup_info</code>, but the mechanism by which the component receives that
information is up to the component runner.</p>
<p>The <code>controller</code> interface request typically originates from the
<code>Launcher.CreateComponent</code> message that caused this component to be
started.</p>

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



## ServiceProvider {#ServiceProvider}
*Defined in [fuchsia.sys/service_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/service_provider.fidl#15)*

<p>An interface through which a client may request services from a host.
Instances of this interface are created within the context of an
already-identified client and host pair, so there is no need to explicitly
identify the client or host in the methods below.</p>
<p>This interface is deprecated.  Services should be published as directory
entries instead, just like files.</p>

### ConnectToService {#ConnectToService}

<p>Asks the host to provide the service identified by <code>service_name</code> through
the <code>channel</code> endpoint supplied by the caller. If the host is not willing
or able to provide the requested service, it should close the <code>channel</code>.</p>

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

### EnvironmentOptions {#EnvironmentOptions}
*Defined in [fuchsia.sys/environment.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/environment.fidl#10)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>inherit_parent_services</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>True if this environment should inherit services provided by the
parent environment.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>use_parent_runners</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>True if components in this environment will share a runner provided
by the parent environment. If false, a new runner will be started
in this environment for components.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>kill_on_oom</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>True if this environment should be killed first in out of memory
situations by setting the <code>ZX_PROP_JOB_KILL_ON_OOM</code> property on this
environment's job.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>delete_storage_on_death</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>True if &quot;persistent&quot; storage requested by components in this environment should not actually
be persistent, and instead be deleted when this environment is killed.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### FlatNamespace {#FlatNamespace}
*Defined in [fuchsia.sys/flat_namespace.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/flat_namespace.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>paths</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td><p>The mount point for each of the directories below.</p>
<p>For example, [&quot;/pkg&quot;, &quot;/svc&quot;].</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>directories</code></td>
            <td>
                <code>vector&lt;channel&gt;</code>
            </td>
            <td><p>The directories mounted at each path in the namespace.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### FileDescriptor {#FileDescriptor}
*Defined in [fuchsia.sys/launcher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/launcher.fidl#9)*



<p>An FDIO file descriptor.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>type0</code></td>
            <td>
                <code>int32</code>
            </td>
            <td><p>The FDIO types of the handle (e.g., <code>FA_FDIO_REMOTE</code>).</p>
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
            <td><p>The handles for the file descriptor (e.g., a channel).</p>
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

### LaunchInfo {#LaunchInfo}
*Defined in [fuchsia.sys/launcher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/launcher.fidl#23)*



<p>Information used to create an instance of a component and obtain
services from it.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>url</code></td>
            <td>
                <code><a class='link' href='#component_url'>component_url</a></code>
            </td>
            <td><p>The location from which to retrieve this component.</p>
<p>This field will probably be replaced with a stronger notion of identity,
such as an unforgeable token. This field is included in this iteration to
ease the transition from the previous component interfaces.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>arguments</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
            <td><p>The arguments to be provided to the component.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>out</code></td>
            <td>
                <code><a class='link' href='#FileDescriptor'>FileDescriptor</a>?</code>
            </td>
            <td><p>The file descriptor to use for stdout.</p>
<p>If null, the component will use the default stdout for the environment.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#FileDescriptor'>FileDescriptor</a>?</code>
            </td>
            <td><p>The file descriptor to use for stderr.</p>
<p>If null, the component will use the default stderr for the environment.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>directory_request</code></td>
            <td>
                <code>handle&lt;channel&gt;?</code>
            </td>
            <td><p>The interface request for a Directory that is passed through to the
component and arrives in the component as its <code>directory_request</code>
interface request.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>flat_namespace</code></td>
            <td>
                <code><a class='link' href='#FlatNamespace'>FlatNamespace</a>?</code>
            </td>
            <td><p>A custom namespace that can be appended to the namespace generated by
appmgr and provided to this component.
Adding a mount point at standard paths like 'pkg' or 'svc' will be ignored.
HACK(alhaad): Adding mount points for deprecated default directories like
'/data' will override the default.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>additional_services</code></td>
            <td>
                <code><a class='link' href='#ServiceList'>ServiceList</a>?</code>
            </td>
            <td><p>A list of services to be added to this component's svc namespace. These
services are in addition to those coming from Environment.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### ServiceList {#ServiceList}
*Defined in [fuchsia.sys/launcher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/launcher.fidl#61)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>names</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td><p>A list of services that can be requested from <code>provider</code>.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>provider</code></td>
            <td>
                <code><a class='link' href='#ServiceProvider'>ServiceProvider</a>?</code>
            </td>
            <td><p>A service provider to get the services listed in <code>names</code> from.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>host_directory</code></td>
            <td>
                <code>handle&lt;channel&gt;?</code>
            </td>
            <td><p>A channel to the directory hosting the services in <code>names</code>.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### StartupInfo {#StartupInfo}
*Defined in [fuchsia.sys/runner.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/runner.fidl#13)*



<p>Information given to components at startup.</p>
<p>For ELF binaries, this information is provided in the initialization
message given to <code>libc</code> by <code>fuchsia.process.Launcher</code>.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>launch_info</code></td>
            <td>
                <code><a class='link' href='#LaunchInfo'>LaunchInfo</a></code>
            </td>
            <td><p>The launch info for the component to start.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>flat_namespace</code></td>
            <td>
                <code><a class='link' href='#FlatNamespace'>FlatNamespace</a></code>
            </td>
            <td><p>The namespace in which to run the component.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>program_metadata</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ProgramMetadata'>ProgramMetadata</a>&gt;?</code>
            </td>
            <td><p>Key string value string map of the component's program metadata,
obtained from its component manifest.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### ProgramMetadata {#ProgramMetadata}
*Defined in [fuchsia.sys/runner.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/runner.fidl#29)*



<p>Program information about a component.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>Key for program metadata pair. E.g. &quot;binary&quot; for an ELF binary
component, or &quot;data&quot; for a flutter/dart component.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>Value for program metadata pair. E.g. &quot;bin/app&quot; for a &quot;binary&quot; key, or
&quot;data/foo&quot; for a flutter/dart component.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### Package {#Package}
*Defined in [fuchsia.sys/runner.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/runner.fidl#42)*



<p>A binary representation of a component.</p>
<p>Typically provided to <code>Runner.StartComponent</code> when starting a component.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a>?</code>
            </td>
            <td><p>A read-only binary representation of the component. For example, if the
component is intended to run in the Dart virtual machine, this data
might contain a dartx package.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>directory</code></td>
            <td>
                <code>handle&lt;channel&gt;?</code>
            </td>
            <td><p>A directory containing the contents of the package. For example, if the
component is stored in pkgfs, this directory will be the pkgfs
directory containing the package.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>resolved_url</code></td>
            <td>
                <code><a class='link' href='#component_url'>component_url</a></code>
            </td>
            <td><p>Resolved URL of the component. This is the url specified in
<code>startup_info</code> after following redirects and resolving relative paths.</p>
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### TerminationReason {#TerminationReason}
Type: <code>uint32</code>

*Defined in [fuchsia.sys/component_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/component_controller.fidl#7)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>0</code></td>
            <td><p>The channel closed without giving a termination reason.</p>
</td>
        </tr><tr>
            <td><code>EXITED</code></td>
            <td><code>1</code></td>
            <td><p>Component ran and exited with a given return_code.</p>
</td>
        </tr><tr>
            <td><code>URL_INVALID</code></td>
            <td><code>2</code></td>
            <td><p>The given URL given to launch was invalid.</p>
</td>
        </tr><tr>
            <td><code>PACKAGE_NOT_FOUND</code></td>
            <td><code>3</code></td>
            <td><p>The requested package could not be found.</p>
</td>
        </tr><tr>
            <td><code>INTERNAL_ERROR</code></td>
            <td><code>4</code></td>
            <td><p>An internal error happened during the launch process.</p>
</td>
        </tr><tr>
            <td><code>PROCESS_CREATION_ERROR</code></td>
            <td><code>5</code></td>
            <td><p>Process creation failed.</p>
</td>
        </tr><tr>
            <td><code>RUNNER_FAILED</code></td>
            <td><code>6</code></td>
            <td><p>A Runner failed to start.</p>
</td>
        </tr><tr>
            <td><code>RUNNER_TERMINATED</code></td>
            <td><code>7</code></td>
            <td><p>A Runner terminated while attempting to run a component.</p>
</td>
        </tr><tr>
            <td><code>UNSUPPORTED</code></td>
            <td><code>8</code></td>
            <td><p>Attempted to use an unsupported feature.</p>
</td>
        </tr></table>











## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="kLabelMaxLength">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/environment.fidl#8">kLabelMaxLength</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Maximum length for an environment label.</p>
</td>
        </tr>
    <tr id="MAX_URL_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/types.fidl#11">MAX_URL_LENGTH</a></td>
            <td>
                    <code>2083</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    
</table>



## **TYPE ALIASES**

<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr id="component_url">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys/types.fidl#9">component_url</a></td>
            <td>
                <code>string</code>[<code><a class='link' href='#MAX_URL_LENGTH'>MAX_URL_LENGTH</a></code>]</td>
            <td><p>A URL used to retrieve, launch, and load a component from a specified network
location, or to identify a component when connecting to it.</p>
</td>
        </tr></table>

