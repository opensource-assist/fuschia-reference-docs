Project: /_project.yaml
Book: /_book.yaml

# fuchsia.modular.testing


## **PROTOCOLS**

## TestHarness {:#TestHarness}
*Defined in [fuchsia.modular.testing/test_harness.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.testing/test_harness.fidl#29)*

 The `TestHarness` service is used to run the modular runtime under a
 hermetic environment and drive integration tests under it. Tests may use
 this service to intercept components and assume their role. Additionally,
 tests may use `TestHarness/ConnectToModularService()` to get capabilities
 for controlling stories (using PuppetMaster) and connecting to agents
 (using ComponentContext).

 Closing the `TestHarness` connection will kill the `TestHarness` environment
 including the modular runtime running under it.

 On error, this connection is closed with the following epitaphs:
 * `ZX_ERR_INVALID_ARGS`: Run() failed to execute succesfully.
 * `ZX_ERR_BAD_STATE`: Other methods are called before Run() is called.
 * `ZX_ERR_ALREADY_BOUND`: Run() was already called.
 * `ZX_ERR_ALREADY_EXISTS`: The same environment service is being provided
   twice.

### Run {:#Run}

 Initializes an instance of the modular runtime in an enclosed
 environment, configured with parameters provided in `spec`. Closing the
 `TestHarness` connection will kill the enclosed environment.

 This protocol connection is closed if Run() fails, with the following
 epitaphs:
  * `ZX_ERR_INVALID_ARGS`: `spec` is mal-formed.
  * `ZX_ERR_ALREADY_EXISTS`: The same environment service is being provided
    twice in `spec.env_services`
  * `ZX_ERR_ALREADY_BOUND`: Run() was already called.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>spec</code></td>
            <td>
                <code><a class='link' href='#TestHarnessSpec'>TestHarnessSpec</a></code>
            </td>
        </tr></table>



### OnNewComponent {:#OnNewComponent}

 This event is sent when a component specified in
 `TestHarnessSpec.components_to_intercept` is created.
 `startup_info.launch_info.url` contains the component URL.

 Closing `intercepted_component` will signal to the component manager
 that this component has exited unexpectedly. Prefer to use
 InterceptedComponent/Exit to provide exit code and reason.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>startup_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sys/index.html'>fuchsia.sys</a>/<a class='link' href='../fuchsia.sys/index.html#StartupInfo'>StartupInfo</a></code>
            </td>
        </tr><tr>
            <td><code>intercepted_component</code></td>
            <td>
                <code><a class='link' href='#InterceptedComponent'>InterceptedComponent</a></code>
            </td>
        </tr></table>

### ConnectToModularService {:#ConnectToModularService}

 Tests may use this method to connect to services provided by the modular
 runtime. These services share the same component namespace for any
 resources they create (e.g., entities, message queues, and module
 names).

 This protocol connection is closed with the following epitaphs:
  * `ZX_ERR_BAD_STATE`: if `ConnectToModularService()` is called before
   `Run()`.
  * `ZX_ERR_INVALID_ARGS`: if `service` is not set to a value.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service</code></td>
            <td>
                <code><a class='link' href='#ModularService'>ModularService</a></code>
            </td>
        </tr></table>



### ConnectToEnvironmentService {:#ConnectToEnvironmentService}

 Connects to environment services injected into the TestHarness
 environment.

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



### ParseConfig {:#ParseConfig}

 Parses a modular configuration from string into BasemgrConfig and
 SessionmgrConfig

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>config_path</code></td>
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
                <code><a class='link' href='../fuchsia.modular.session/index.html'>fuchsia.modular.session</a>/<a class='link' href='../fuchsia.modular.session/index.html#BasemgrConfig'>BasemgrConfig</a></code>
            </td>
        </tr><tr>
            <td><code>sessionmgr_config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular.session/index.html'>fuchsia.modular.session</a>/<a class='link' href='../fuchsia.modular.session/index.html#SessionmgrConfig'>SessionmgrConfig</a></code>
            </td>
        </tr></table>

## InterceptedComponent {:#InterceptedComponent}
*Defined in [fuchsia.modular.testing/test_harness.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.testing/test_harness.fidl#84)*

 InterceptedComponent represents an intercepted component's lifecycle.
 Closing this connection causes the component to be killed, and is
 equivalent in behaviour to the `ComponentController` being closed.

### Exit {:#Exit}

 Signals that component has exit'd with the specified exit code. The
 values here are bubbled up to the
 `fuchsia.sys.ComponentController.OnTerminated` event. The `OnKill` event
 is sent, and this InterceptedComponent handle is closed.

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
                <code><a class='link' href='../fuchsia.sys/index.html'>fuchsia.sys</a>/<a class='link' href='../fuchsia.sys/index.html#TerminationReason'>TerminationReason</a></code>
            </td>
        </tr></table>



### OnKill {:#OnKill}

 The event is sent when the component is killed by the associated
 `fuchsia.sys.ComponentController`, or when `Exit()` is called.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## TestHarness {:#TestHarness}
*Defined in [fuchsia.modular.testing/test_harness.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.testing/test_harness.fidl#29)*

 The `TestHarness` service is used to run the modular runtime under a
 hermetic environment and drive integration tests under it. Tests may use
 this service to intercept components and assume their role. Additionally,
 tests may use `TestHarness/ConnectToModularService()` to get capabilities
 for controlling stories (using PuppetMaster) and connecting to agents
 (using ComponentContext).

 Closing the `TestHarness` connection will kill the `TestHarness` environment
 including the modular runtime running under it.

 On error, this connection is closed with the following epitaphs:
 * `ZX_ERR_INVALID_ARGS`: Run() failed to execute succesfully.
 * `ZX_ERR_BAD_STATE`: Other methods are called before Run() is called.
 * `ZX_ERR_ALREADY_BOUND`: Run() was already called.
 * `ZX_ERR_ALREADY_EXISTS`: The same environment service is being provided
   twice.

### Run {:#Run}

 Initializes an instance of the modular runtime in an enclosed
 environment, configured with parameters provided in `spec`. Closing the
 `TestHarness` connection will kill the enclosed environment.

 This protocol connection is closed if Run() fails, with the following
 epitaphs:
  * `ZX_ERR_INVALID_ARGS`: `spec` is mal-formed.
  * `ZX_ERR_ALREADY_EXISTS`: The same environment service is being provided
    twice in `spec.env_services`
  * `ZX_ERR_ALREADY_BOUND`: Run() was already called.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>spec</code></td>
            <td>
                <code><a class='link' href='#TestHarnessSpec'>TestHarnessSpec</a></code>
            </td>
        </tr></table>



### OnNewComponent {:#OnNewComponent}

 This event is sent when a component specified in
 `TestHarnessSpec.components_to_intercept` is created.
 `startup_info.launch_info.url` contains the component URL.

 Closing `intercepted_component` will signal to the component manager
 that this component has exited unexpectedly. Prefer to use
 InterceptedComponent/Exit to provide exit code and reason.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>startup_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sys/index.html'>fuchsia.sys</a>/<a class='link' href='../fuchsia.sys/index.html#StartupInfo'>StartupInfo</a></code>
            </td>
        </tr><tr>
            <td><code>intercepted_component</code></td>
            <td>
                <code><a class='link' href='#InterceptedComponent'>InterceptedComponent</a></code>
            </td>
        </tr></table>

### ConnectToModularService {:#ConnectToModularService}

 Tests may use this method to connect to services provided by the modular
 runtime. These services share the same component namespace for any
 resources they create (e.g., entities, message queues, and module
 names).

 This protocol connection is closed with the following epitaphs:
  * `ZX_ERR_BAD_STATE`: if `ConnectToModularService()` is called before
   `Run()`.
  * `ZX_ERR_INVALID_ARGS`: if `service` is not set to a value.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service</code></td>
            <td>
                <code><a class='link' href='#ModularService'>ModularService</a></code>
            </td>
        </tr></table>



### ConnectToEnvironmentService {:#ConnectToEnvironmentService}

 Connects to environment services injected into the TestHarness
 environment.

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



### ParseConfig {:#ParseConfig}

 Parses a modular configuration from string into BasemgrConfig and
 SessionmgrConfig

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>config_path</code></td>
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
                <code><a class='link' href='../fuchsia.modular.session/index.html'>fuchsia.modular.session</a>/<a class='link' href='../fuchsia.modular.session/index.html#BasemgrConfig'>BasemgrConfig</a></code>
            </td>
        </tr><tr>
            <td><code>sessionmgr_config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular.session/index.html'>fuchsia.modular.session</a>/<a class='link' href='../fuchsia.modular.session/index.html#SessionmgrConfig'>SessionmgrConfig</a></code>
            </td>
        </tr></table>

## InterceptedComponent {:#InterceptedComponent}
*Defined in [fuchsia.modular.testing/test_harness.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.testing/test_harness.fidl#84)*

 InterceptedComponent represents an intercepted component's lifecycle.
 Closing this connection causes the component to be killed, and is
 equivalent in behaviour to the `ComponentController` being closed.

### Exit {:#Exit}

 Signals that component has exit'd with the specified exit code. The
 values here are bubbled up to the
 `fuchsia.sys.ComponentController.OnTerminated` event. The `OnKill` event
 is sent, and this InterceptedComponent handle is closed.

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
                <code><a class='link' href='../fuchsia.sys/index.html'>fuchsia.sys</a>/<a class='link' href='../fuchsia.sys/index.html#TerminationReason'>TerminationReason</a></code>
            </td>
        </tr></table>



### OnKill {:#OnKill}

 The event is sent when the component is killed by the associated
 `fuchsia.sys.ComponentController`, or when `Exit()` is called.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## **STRUCTS**

### ComponentService {:#ComponentService}
*Defined in [fuchsia.modular.testing/test_harness.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.testing/test_harness.fidl#183)*



 Describes a service to be provided by a component instance.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Name of the service.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>url</code></td>
            <td>
                <code>string[2083]</code>
            </td>
            <td> URL of the component which will provide the service.
 The service is retrieved from this component's /out/svc namespace.
</td>
            <td>No default</td>
        </tr>
</table>

### ComponentService {:#ComponentService}
*Defined in [fuchsia.modular.testing/test_harness.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.testing/test_harness.fidl#183)*



 Describes a service to be provided by a component instance.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Name of the service.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>url</code></td>
            <td>
                <code>string[2083]</code>
            </td>
            <td> URL of the component which will provide the service.
 The service is retrieved from this component's /out/svc namespace.
</td>
            <td>No default</td>
        </tr>
</table>





## **TABLES**

### TestHarnessSpec {:#TestHarnessSpec}


*Defined in [fuchsia.modular.testing/test_harness.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.testing/test_harness.fidl#110)*

 Defines the setup of an environment running an instance of the modular
 framework used for testing purposes. This table is supplied to
 `TestHarness.Run()`. A malformed `TestHarnessSpec` will cause `TestHarness`
 connection to close with an epitaph of `ZX_ERR_INVALID_ARGS`.

 By default, the following services are made available to the hermetic
 environment:
  * fuchsia.auth.account.AccountManager
  * fuchsia.devicesettings.DeviceSettingsManager

 Additional services may be supplied using using
 `TestHarnessSpec.env_services_to_inherit` and
 `TestHarnessSpec.injected_services`. Additional services override the
 default services listed above.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>basemgr_config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular.session/index.html'>fuchsia.modular.session</a>/<a class='link' href='../fuchsia.modular.session/index.html#BasemgrConfig'>BasemgrConfig</a></code>
            </td>
            <td> Configuration for basemgr. See `fuchsia.modular.session.BasemgrConfig`
 for a description of the defaults.

 The test harness will amend `basemgr_config` before passing it off to
 the modular runtime in the following way:
 * If `basemgr_config.base_shell.app_config.url` is not set, the test
   harness will use a base shell which automatically logs into the
   session.
 * If `basemgr_config.session_shell_map[0].config.app_config.url` is not
   set, the test harness will use a shell which automatically starts new
   stories.
 * If `basemgr_config.story_shell.app_config.url` is not set, the test
   harness use a minimally functioning story shell which displays all
   mods in a story.

 To intercept and mock the shells, users may provide fake URLs for the
 shells and specify that the fake URL be intercepted using
 `components_to_intercept`.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>sessionmgr_config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular.session/index.html'>fuchsia.modular.session</a>/<a class='link' href='../fuchsia.modular.session/index.html#SessionmgrConfig'>SessionmgrConfig</a></code>
            </td>
            <td> Configuration for sessionmgr. See
 `fuchsia.modular.session.SessionmgrConfig` for a description of the
 defaults.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>components_to_intercept</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#InterceptSpec'>InterceptSpec</a>&gt;</code>
            </td>
            <td> List of component URLs (and additional .cmx contents) to intercept.
</td>
        </tr><tr>
            <td>6</td>
            <td><code>env_services</code></td>
            <td>
                <code><a class='link' href='#EnvironmentServicesSpec'>EnvironmentServicesSpec</a></code>
            </td>
            <td> Options to configure the test harness environment. Use this to inject
 services into the environment.

 Optional.
</td>
        </tr><tr>
            <td>7</td>
            <td><code>environment_suffix</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Suffix to the environment name.
 The default environment name is 'mth_{random number from 0 to 99999}'.
 When provided, the environment_suffix additionally appends a '_' and
 the string to the end of the environment name. The overall name gets
 truncated at 32 characters.

 Optional.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>env_services_to_inherit</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td> DEPRECATED. Use |env_services.service_dir| to pass through services from
 parent environment.
</td>
        </tr><tr>
            <td>5</td>
            <td><code></code></td>
            <td>
                <code></code>
            </td>
            <td></td>
        </tr></table>

### EnvironmentServicesSpec {:#EnvironmentServicesSpec}


*Defined in [fuchsia.modular.testing/test_harness.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.testing/test_harness.fidl#165)*

 Options for configuring the test harness environment with services.

 If the same service is provided in more than one place, `TestHarness`
 connection is closed with a `ZX_ERR_ALREADY_EXISTS` epitaph.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>service_dir</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
            <td> A directory of services to be provided to the test harness environment.

 Optional.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>services_from_components</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ComponentService'>ComponentService</a>&gt;</code>
            </td>
            <td> A list of services provided by components to inject into the test
 harness environment. Multiple services may be provided by the same
 component, but only one instance of the component is launched to serve
 its services. Components are started when one of their services is
 requested, and are kept alive for the duration of the test harness
 environment's life.

 Optional.
</td>
        </tr></table>

### InterceptSpec {:#InterceptSpec}


*Defined in [fuchsia.modular.testing/test_harness.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.testing/test_harness.fidl#194)*

 Describes a component to intercept. Malformed parameters result in closing
 `TestHarness` with a `ZX_ERR_INVALID_ARGS` epitaph.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>component_url</code></td>
            <td>
                <code>string[2083]</code>
            </td>
            <td> Required. Must be a valid component URL (e.g., fuchsia-pkg://..), or is
 considered malformed.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>extra_cmx_contents</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
            <td> The .cmx contents of this component's manifest. A minimal manifest is
 constructed by default. If set, the contents of `extra_cmx_contents`
 override the default constructed manifest, which only has the required
 "program.binary" field defined.

 `extra_cmx_contents` must be a valid .cmx JSON. Example:

 {
   "sandbox": {
     "services": [
       "fuchsia.sys.Launcher",
     ]
   }
 }
</td>
        </tr></table>

### TestHarnessSpec {:#TestHarnessSpec}


*Defined in [fuchsia.modular.testing/test_harness.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.testing/test_harness.fidl#110)*

 Defines the setup of an environment running an instance of the modular
 framework used for testing purposes. This table is supplied to
 `TestHarness.Run()`. A malformed `TestHarnessSpec` will cause `TestHarness`
 connection to close with an epitaph of `ZX_ERR_INVALID_ARGS`.

 By default, the following services are made available to the hermetic
 environment:
  * fuchsia.auth.account.AccountManager
  * fuchsia.devicesettings.DeviceSettingsManager

 Additional services may be supplied using using
 `TestHarnessSpec.env_services_to_inherit` and
 `TestHarnessSpec.injected_services`. Additional services override the
 default services listed above.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>basemgr_config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular.session/index.html'>fuchsia.modular.session</a>/<a class='link' href='../fuchsia.modular.session/index.html#BasemgrConfig'>BasemgrConfig</a></code>
            </td>
            <td> Configuration for basemgr. See `fuchsia.modular.session.BasemgrConfig`
 for a description of the defaults.

 The test harness will amend `basemgr_config` before passing it off to
 the modular runtime in the following way:
 * If `basemgr_config.base_shell.app_config.url` is not set, the test
   harness will use a base shell which automatically logs into the
   session.
 * If `basemgr_config.session_shell_map[0].config.app_config.url` is not
   set, the test harness will use a shell which automatically starts new
   stories.
 * If `basemgr_config.story_shell.app_config.url` is not set, the test
   harness use a minimally functioning story shell which displays all
   mods in a story.

 To intercept and mock the shells, users may provide fake URLs for the
 shells and specify that the fake URL be intercepted using
 `components_to_intercept`.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>sessionmgr_config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular.session/index.html'>fuchsia.modular.session</a>/<a class='link' href='../fuchsia.modular.session/index.html#SessionmgrConfig'>SessionmgrConfig</a></code>
            </td>
            <td> Configuration for sessionmgr. See
 `fuchsia.modular.session.SessionmgrConfig` for a description of the
 defaults.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>components_to_intercept</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#InterceptSpec'>InterceptSpec</a>&gt;</code>
            </td>
            <td> List of component URLs (and additional .cmx contents) to intercept.
</td>
        </tr><tr>
            <td>6</td>
            <td><code>env_services</code></td>
            <td>
                <code><a class='link' href='#EnvironmentServicesSpec'>EnvironmentServicesSpec</a></code>
            </td>
            <td> Options to configure the test harness environment. Use this to inject
 services into the environment.

 Optional.
</td>
        </tr><tr>
            <td>7</td>
            <td><code>environment_suffix</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Suffix to the environment name.
 The default environment name is 'mth_{random number from 0 to 99999}'.
 When provided, the environment_suffix additionally appends a '_' and
 the string to the end of the environment name. The overall name gets
 truncated at 32 characters.

 Optional.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>env_services_to_inherit</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td> DEPRECATED. Use |env_services.service_dir| to pass through services from
 parent environment.
</td>
        </tr><tr>
            <td>5</td>
            <td><code></code></td>
            <td>
                <code></code>
            </td>
            <td></td>
        </tr></table>

### EnvironmentServicesSpec {:#EnvironmentServicesSpec}


*Defined in [fuchsia.modular.testing/test_harness.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.testing/test_harness.fidl#165)*

 Options for configuring the test harness environment with services.

 If the same service is provided in more than one place, `TestHarness`
 connection is closed with a `ZX_ERR_ALREADY_EXISTS` epitaph.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>service_dir</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
            <td> A directory of services to be provided to the test harness environment.

 Optional.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>services_from_components</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ComponentService'>ComponentService</a>&gt;</code>
            </td>
            <td> A list of services provided by components to inject into the test
 harness environment. Multiple services may be provided by the same
 component, but only one instance of the component is launched to serve
 its services. Components are started when one of their services is
 requested, and are kept alive for the duration of the test harness
 environment's life.

 Optional.
</td>
        </tr></table>

### InterceptSpec {:#InterceptSpec}


*Defined in [fuchsia.modular.testing/test_harness.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.testing/test_harness.fidl#194)*

 Describes a component to intercept. Malformed parameters result in closing
 `TestHarness` with a `ZX_ERR_INVALID_ARGS` epitaph.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>component_url</code></td>
            <td>
                <code>string[2083]</code>
            </td>
            <td> Required. Must be a valid component URL (e.g., fuchsia-pkg://..), or is
 considered malformed.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>extra_cmx_contents</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
            <td> The .cmx contents of this component's manifest. A minimal manifest is
 constructed by default. If set, the contents of `extra_cmx_contents`
 override the default constructed manifest, which only has the required
 "program.binary" field defined.

 `extra_cmx_contents` must be a valid .cmx JSON. Example:

 {
   "sandbox": {
     "services": [
       "fuchsia.sys.Launcher",
     ]
   }
 }
</td>
        </tr></table>





## **XUNIONS**

### ModularService {:#ModularService}
*Defined in [fuchsia.modular.testing/test_harness.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.testing/test_harness.fidl#75)*

 Describes which service to connect to using `ConnectToModularService()`.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>puppet_master</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/index.html#PuppetMaster'>PuppetMaster</a>&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>component_context</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/index.html#ComponentContext'>ComponentContext</a>&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>agent_context</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/index.html#AgentContext'>AgentContext</a>&gt;</code>
            </td>
            <td></td>
        </tr></table>

### ModularService {:#ModularService}
*Defined in [fuchsia.modular.testing/test_harness.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.testing/test_harness.fidl#75)*

 Describes which service to connect to using `ConnectToModularService()`.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>puppet_master</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/index.html#PuppetMaster'>PuppetMaster</a>&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>component_context</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/index.html#ComponentContext'>ComponentContext</a>&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>agent_context</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/index.html#AgentContext'>AgentContext</a>&gt;</code>
            </td>
            <td></td>
        </tr></table>





