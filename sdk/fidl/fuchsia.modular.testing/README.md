[TOC]

# fuchsia.modular.testing


## **PROTOCOLS**

## TestHarness {#TestHarness}
*Defined in [fuchsia.modular.testing/test_harness.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.testing/test_harness.fidl#29)*

<p>The <code>TestHarness</code> service is used to run the modular runtime under a
hermetic environment and drive integration tests under it. Tests may use
this service to intercept components and assume their role. Additionally,
tests may use <code>TestHarness/ConnectToModularService()</code> to get capabilities
for controlling stories (using PuppetMaster) and connecting to agents
(using ComponentContext).</p>
<p>Closing the <code>TestHarness</code> connection will kill the <code>TestHarness</code> environment
including the modular runtime running under it.</p>
<p>On error, this connection is closed with the following epitaphs:</p>
<ul>
<li><code>ZX_ERR_INVALID_ARGS</code>: Run() failed to execute succesfully.</li>
<li><code>ZX_ERR_BAD_STATE</code>: Other methods are called before Run() is called.</li>
<li><code>ZX_ERR_ALREADY_BOUND</code>: Run() was already called.</li>
<li><code>ZX_ERR_ALREADY_EXISTS</code>: The same environment service is being provided
twice.</li>
</ul>

### Run {#Run}

<p>Initializes an instance of the modular runtime in an enclosed
environment, configured with parameters provided in <code>spec</code>. Closing the
<code>TestHarness</code> connection will kill the enclosed environment.</p>
<p>This protocol connection is closed if Run() fails, with the following
epitaphs:</p>
<ul>
<li><code>ZX_ERR_INVALID_ARGS</code>: <code>spec</code> is mal-formed.</li>
<li><code>ZX_ERR_ALREADY_EXISTS</code>: The same environment service is being provided
twice in <code>spec.env_services</code></li>
<li><code>ZX_ERR_ALREADY_BOUND</code>: Run() was already called.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>spec</code></td>
            <td>
                <code><a class='link' href='#TestHarnessSpec'>TestHarnessSpec</a></code>
            </td>
        </tr></table>



### OnNewComponent {#OnNewComponent}

<p>This event is sent when a component specified in
<code>TestHarnessSpec.components_to_intercept</code> is created.
<code>startup_info.launch_info.url</code> contains the component URL.</p>
<p>Closing <code>intercepted_component</code> will signal to the component manager
that this component has exited unexpectedly. Prefer to use
InterceptedComponent/Exit to provide exit code and reason.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>startup_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sys/'>fuchsia.sys</a>/<a class='link' href='../fuchsia.sys/#StartupInfo'>StartupInfo</a></code>
            </td>
        </tr><tr>
            <td><code>intercepted_component</code></td>
            <td>
                <code><a class='link' href='#InterceptedComponent'>InterceptedComponent</a></code>
            </td>
        </tr></table>

### ConnectToModularService {#ConnectToModularService}

<p>Tests may use this method to connect to services provided by the modular
runtime. These services share the same component namespace for any
resources they create (e.g., entities, message queues, and module
names).</p>
<p>This protocol connection is closed with the following epitaphs:</p>
<ul>
<li><code>ZX_ERR_BAD_STATE</code>: if <code>ConnectToModularService()</code> is called before
<code>Run()</code>.</li>
<li><code>ZX_ERR_INVALID_ARGS</code>: if <code>service</code> is not set to a value.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service</code></td>
            <td>
                <code><a class='link' href='#ModularService'>ModularService</a></code>
            </td>
        </tr></table>



### ConnectToEnvironmentService {#ConnectToEnvironmentService}

<p>Connects to environment services injected into the TestHarness
environment.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>request</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



### ParseConfig {#ParseConfig}

<p>Parses a JSON modular configuration string into BasemgrConfig and
SessionmgrConfig. This method may be called before <code>Run()</code> is called.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>basemgr_config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular.session/'>fuchsia.modular.session</a>/<a class='link' href='../fuchsia.modular.session/#BasemgrConfig'>BasemgrConfig</a></code>
            </td>
        </tr><tr>
            <td><code>sessionmgr_config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular.session/'>fuchsia.modular.session</a>/<a class='link' href='../fuchsia.modular.session/#SessionmgrConfig'>SessionmgrConfig</a></code>
            </td>
        </tr></table>

## InterceptedComponent {#InterceptedComponent}
*Defined in [fuchsia.modular.testing/test_harness.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.testing/test_harness.fidl#84)*

<p>InterceptedComponent represents an intercepted component's lifecycle.
Closing this connection causes the component to be killed, and is
equivalent in behaviour to the <code>ComponentController</code> being closed.</p>

### Exit {#Exit}

<p>Signals that component has exit'd with the specified exit code. The
values here are bubbled up to the
<code>fuchsia.sys.ComponentController.OnTerminated</code> event. The <code>OnKill</code> event
is sent, and this InterceptedComponent handle is closed.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>exit_code</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>reason</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sys/'>fuchsia.sys</a>/<a class='link' href='../fuchsia.sys/#TerminationReason'>TerminationReason</a></code>
            </td>
        </tr></table>



### OnKill {#OnKill}

<p>The event is sent when the component is killed by the associated
<code>fuchsia.sys.ComponentController</code>, or when <code>Exit()</code> is called.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## **STRUCTS**

### ComponentService {#ComponentService}
*Defined in [fuchsia.modular.testing/test_harness.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.testing/test_harness.fidl#183)*



<p>Describes a service to be provided by a component instance.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>Name of the service.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>url</code></td>
            <td>
                <code>string[2083]</code>
            </td>
            <td><p>URL of the component which will provide the service.
The service is retrieved from this component's /out/svc namespace.</p>
</td>
            <td>No default</td>
        </tr>
</table>





## **TABLES**

### TestHarnessSpec {#TestHarnessSpec}


*Defined in [fuchsia.modular.testing/test_harness.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.testing/test_harness.fidl#110)*

<p>Defines the setup of an environment running an instance of the modular
framework used for testing purposes. This table is supplied to
<code>TestHarness.Run()</code>. A malformed <code>TestHarnessSpec</code> will cause <code>TestHarness</code>
connection to close with an epitaph of <code>ZX_ERR_INVALID_ARGS</code>.</p>
<p>By default, the following services are made available to the hermetic
environment:</p>
<ul>
<li>fuchsia.identity.account.AccountManager</li>
<li>fuchsia.devicesettings.DeviceSettingsManager</li>
</ul>
<p>Additional services may be supplied using using
<code>TestHarnessSpec.env_services_to_inherit</code> and
<code>TestHarnessSpec.injected_services</code>. Additional services override the
default services listed above.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>basemgr_config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular.session/'>fuchsia.modular.session</a>/<a class='link' href='../fuchsia.modular.session/#BasemgrConfig'>BasemgrConfig</a></code>
            </td>
            <td><p>Configuration for basemgr. See <code>fuchsia.modular.session.BasemgrConfig</code>
for a description of the defaults.</p>
<p>The test harness will amend <code>basemgr_config</code> before passing it off to
the modular runtime in the following way:</p>
<ul>
<li>If <code>basemgr_config.base_shell.app_config.url</code> is not set, the test
harness will use a base shell which automatically logs into the
session.</li>
<li>If <code>basemgr_config.session_shell_map[0].config.app_config.url</code> is not
set, the test harness will use a shell which automatically starts new
stories.</li>
<li>If <code>basemgr_config.story_shell.app_config.url</code> is not set, the test
harness use a minimally functioning story shell which displays all
mods in a story.</li>
</ul>
<p>To intercept and mock the shells, users may provide fake URLs for the
shells and specify that the fake URL be intercepted using
<code>components_to_intercept</code>.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>sessionmgr_config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular.session/'>fuchsia.modular.session</a>/<a class='link' href='../fuchsia.modular.session/#SessionmgrConfig'>SessionmgrConfig</a></code>
            </td>
            <td><p>Configuration for sessionmgr. See
<code>fuchsia.modular.session.SessionmgrConfig</code> for a description of the
defaults.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>components_to_intercept</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#InterceptSpec'>InterceptSpec</a>&gt;</code>
            </td>
            <td><p>List of component URLs (and additional .cmx contents) to intercept.</p>
</td>
        </tr><tr>
            <td>6</td>
            <td><code>env_services</code></td>
            <td>
                <code><a class='link' href='#EnvironmentServicesSpec'>EnvironmentServicesSpec</a></code>
            </td>
            <td><p>Options to configure the test harness environment. Use this to inject
services into the environment.</p>
<p>Optional.</p>
</td>
        </tr><tr>
            <td>7</td>
            <td><code>environment_suffix</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>Suffix to the environment name.
The default environment name is 'mth_{random number from 0 to 99999}'.
When provided, the environment_suffix additionally appends a '_' and
the string to the end of the environment name. The overall name gets
truncated at 32 characters.</p>
<p>Optional.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>env_services_to_inherit</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td><p>DEPRECATED. Use |env_services.service_dir| to pass through services from
parent environment.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code></code></td>
            <td>
                <code></code>
            </td>
            <td></td>
        </tr></table>

### EnvironmentServicesSpec {#EnvironmentServicesSpec}


*Defined in [fuchsia.modular.testing/test_harness.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.testing/test_harness.fidl#165)*

<p>Options for configuring the test harness environment with services.</p>
<p>If the same service is provided in more than one place, <code>TestHarness</code>
connection is closed with a <code>ZX_ERR_ALREADY_EXISTS</code> epitaph.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>service_dir</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
            <td><p>A directory of services to be provided to the test harness environment.</p>
<p>Optional.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>services_from_components</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ComponentService'>ComponentService</a>&gt;</code>
            </td>
            <td><p>A list of services provided by components to inject into the test
harness environment. Multiple services may be provided by the same
component, but only one instance of the component is launched to serve
its services. Components are started when one of their services is
requested, and are kept alive for the duration of the test harness
environment's life.</p>
<p>Optional.</p>
</td>
        </tr></table>

### InterceptSpec {#InterceptSpec}


*Defined in [fuchsia.modular.testing/test_harness.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.testing/test_harness.fidl#194)*

<p>Describes a component to intercept. Malformed parameters result in closing
<code>TestHarness</code> with a <code>ZX_ERR_INVALID_ARGS</code> epitaph.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>component_url</code></td>
            <td>
                <code>string[2083]</code>
            </td>
            <td><p>Required. Must be a valid component URL (e.g., fuchsia-pkg://..), or is
considered malformed.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>extra_cmx_contents</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td><p>The .cmx contents of this component's manifest. A minimal manifest is
constructed by default. If set, the contents of <code>extra_cmx_contents</code>
override the default constructed manifest, which only has the required
&quot;program.binary&quot; field defined.</p>
<p><code>extra_cmx_contents</code> must be a valid .cmx JSON. Example:</p>
<p>{
&quot;sandbox&quot;: {
&quot;services&quot;: [
&quot;fuchsia.sys.Launcher&quot;,
]
}
}</p>
</td>
        </tr></table>





## **XUNIONS**

### ModularService {#ModularService}
*Defined in [fuchsia.modular.testing/test_harness.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.testing/test_harness.fidl#75)*

<p>Describes which service to connect to using <code>ConnectToModularService()</code>.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>puppet_master</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/#PuppetMaster'>PuppetMaster</a>&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>component_context</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/#ComponentContext'>ComponentContext</a>&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>agent_context</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/#AgentContext'>AgentContext</a>&gt;</code>
            </td>
            <td></td>
        </tr></table>







