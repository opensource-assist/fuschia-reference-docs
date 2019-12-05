[TOC]

# fuchsia.modular.session






## **ENUMS**

### CloudProvider {#CloudProvider}
Type: <code>uint32</code>

*Defined in [fuchsia.modular.session/modular_config.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.session/modular_config.fidl#147)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>LET_LEDGER_DECIDE</code></td>
            <td><code>1</code></td>
            <td><p>Use a cloud provider configured by Ledger.</p>
</td>
        </tr><tr>
            <td><code>FROM_ENVIRONMENT</code></td>
            <td><code>2</code></td>
            <td><p>Use a cloud provider available in the incoming namespace, rather than
initializing and instance within sessionmgr. This can be used to inject
a custom cloud provider.</p>
</td>
        </tr><tr>
            <td><code>NONE</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### BasemgrConfig {#BasemgrConfig}


*Defined in [fuchsia.modular.session/modular_config.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.session/modular_config.fidl#13)*

<p>Descriptions and defaults for these configurations are echoed in
peridot/docs/modular/guide/config.md.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>enable_cobalt</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>When set to false, Cobalt statistics are disabled.
Default: true</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>use_minfs</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>When set to true, wait for persistent data to initialize.
Default: true</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>use_session_shell_for_story_shell_factory</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Create story shells through StoryShellFactory exposed by the session
shell instead of creating separate story shell components. When set,
<code>story_shell_url</code> and any story shell args are ignored.
Default: false</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>base_shell</code></td>
            <td>
                <code><a class='link' href='#BaseShellConfig'>BaseShellConfig</a></code>
            </td>
            <td><p>Launch configurations specific to base shell.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>session_shell_map</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#SessionShellMapEntry'>SessionShellMapEntry</a>&gt;</code>
            </td>
            <td><p>A map of launch configurations specific to session shells.</p>
</td>
        </tr><tr>
            <td>6</td>
            <td><code>story_shell</code></td>
            <td>
                <code><a class='link' href='#StoryShellConfig'>StoryShellConfig</a></code>
            </td>
            <td><p>Launch configurations specific to story shell.</p>
</td>
        </tr><tr>
            <td>7</td>
            <td><code>sessionmgr</code></td>
            <td>
                <code><a class='link' href='#AppConfig'>AppConfig</a></code>
            </td>
            <td><p>Temporary placeholder to pass configurations to sessionmgr. Will be
removed with the completion of MF-10.</p>
</td>
        </tr></table>

### BaseShellConfig {#BaseShellConfig}


*Defined in [fuchsia.modular.session/modular_config.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.session/modular_config.fidl#42)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>app_config</code></td>
            <td>
                <code><a class='link' href='#AppConfig'>AppConfig</a></code>
            </td>
            <td><p>Contains the fuchsia package url and arguments to pass to the shell.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>keep_alive_after_login</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>When set to true, the base shell is kept alive after a log in. This is
used for testing because current integration tests expect base shell
to always be running.
Default: false</p>
</td>
        </tr></table>

### SessionShellMapEntry {#SessionShellMapEntry}


*Defined in [fuchsia.modular.session/modular_config.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.session/modular_config.fidl#53)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string[4096]</code>
            </td>
            <td><p>The name of the session shell represented by its url.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='#SessionShellConfig'>SessionShellConfig</a></code>
            </td>
            <td><p>The launch configurations for the session shell.</p>
</td>
        </tr></table>

### SessionShellConfig {#SessionShellConfig}


*Defined in [fuchsia.modular.session/modular_config.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.session/modular_config.fidl#61)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>app_config</code></td>
            <td>
                <code><a class='link' href='#AppConfig'>AppConfig</a></code>
            </td>
            <td><p>Contains the fuchsia package url and arguments to pass to the shell.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>display_usage</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.policy/'>fuchsia.ui.policy</a>/<a class='link' href='../fuchsia.ui.policy/#DisplayUsage'>DisplayUsage</a></code>
            </td>
            <td><p>The display usage policy for this session shell.</p>
<p>Optional: defaults to DisplayUsage::kUnknown.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>screen_height</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The screen height in millimeters for the session shell's display.</p>
<p>Optional: defaults to full screen.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>screen_width</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The screen width in millimeters for the session shell's display.</p>
<p>Optional: defaults to full screen.</p>
</td>
        </tr></table>

### StoryShellConfig {#StoryShellConfig}


*Defined in [fuchsia.modular.session/modular_config.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.session/modular_config.fidl#81)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>app_config</code></td>
            <td>
                <code><a class='link' href='#AppConfig'>AppConfig</a></code>
            </td>
            <td><p>Contains the fuchsia package url and arguments to pass to the shell.</p>
</td>
        </tr></table>

### SessionmgrConfig {#SessionmgrConfig}


*Defined in [fuchsia.modular.session/modular_config.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.session/modular_config.fidl#86)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>cloud_provider</code></td>
            <td>
                <code><a class='link' href='#CloudProvider'>CloudProvider</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>enable_cobalt</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>When set to false, Cobalt statistics are disabled. This is used for
testing.
Default: true</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>enable_story_shell_preload</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>When set to false, StoryShell instances are not warmed up as a startup
latency optimization. This is used for testing.
Default: true</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>use_memfs_for_ledger</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Tells the sessionmgr whether it should host+pass a memfs-backed
directory to the ledger for the user's repository, or to use
/data/LEDGER.
Default: false</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>startup_agents</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td><p>A list of fuchsia package urls that specify which agents to launch at
startup.</p>
</td>
        </tr><tr>
            <td>6</td>
            <td><code>session_agents</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td><p>A list of fuchsia package urls that specify which agents to launch at
startup with PuppetMaster and FocusProvider services.</p>
</td>
        </tr><tr>
            <td>7</td>
            <td><code>story_shell_url</code></td>
            <td>
                <code>string[4096]</code>
            </td>
            <td><p>The fuchsia package url for which story shell to use.</p>
</td>
        </tr><tr>
            <td>8</td>
            <td><code>component_args</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#AppConfig'>AppConfig</a>&gt;</code>
            </td>
            <td><p>A map of agents to the arguments they should be started with.</p>
</td>
        </tr><tr>
            <td>9</td>
            <td><code>use_parent_runner_for_story_realm</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Deprecated</p>
</td>
        </tr><tr>
            <td>10</td>
            <td><code>agent_service_index</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#AgentServiceIndexEntry'>AgentServiceIndexEntry</a>&gt;</code>
            </td>
            <td><p>A list of supported services and the URL of the agent known to provide
that service. Used by the Session Manager to implement
<code>ComponentContext</code> method ConnectToAgentService().</p>
</td>
        </tr></table>

### AppConfig {#AppConfig}


*Defined in [fuchsia.modular.session/modular_config.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.session/modular_config.fidl#130)*

<p>Used to pass around configuration references to apps such as base shell,
session shell, story shell, and agents.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>url</code></td>
            <td>
                <code>string[4096]</code>
            </td>
            <td><p>The fuchsia package url for app.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>args</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td><p>The arguments for the app.</p>
</td>
        </tr></table>

### AgentServiceIndexEntry {#AgentServiceIndexEntry}


*Defined in [fuchsia.modular.session/modular_config.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.session/modular_config.fidl#139)*

<p>A service and the URL of the agent known to provide that service.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>service_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The service name.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>agent_url</code></td>
            <td>
                <code>string[2083]</code>
            </td>
            <td><p>The fuchsia component url for agent.</p>
</td>
        </tr></table>

### ModularConfig {#ModularConfig}


*Defined in [fuchsia.modular.session/modular_config.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.session/modular_config.fidl#160)*

<p>Contains the configurations for the modular framework components.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>basemgr_config</code></td>
            <td>
                <code><a class='link' href='#BasemgrConfig'>BasemgrConfig</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>sessionmgr_config</code></td>
            <td>
                <code><a class='link' href='#SessionmgrConfig'>SessionmgrConfig</a></code>
            </td>
            <td></td>
        </tr></table>











