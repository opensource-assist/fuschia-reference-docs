[TOC]

# fuchsia.modular


## **PROTOCOLS**

## Agent {#Agent}
*Defined in [fuchsia.modular/agent.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/agent/agent.fidl#38)*

<p>An agent is a component whose lifecycle is not tied to any Story.</p>
<ul>
<li>An agent is a singleton instance.</li>
<li>Components can connect to an Agent using the
fuchsia.modular.ComponentContext capability.</li>
<li>An agent vends services to components that connect to it over a
ServiceProvider.</li>
<li>An agent is started when someone wants to connect to it, or when a task it
has scheduled has triggered.</li>
</ul>
<p>This FIDL interface should be implemented by a component that is meant to be
run as an Agent.</p>
<p>When an agent application implements the <code>Lifecycle</code> interface, it can
receive a signal for when it should stop. An agent may be stopped for the
following reasons:</p>
<p>(1) All <code>AgentController</code> connections associated with this agent are closed.</p>
<p>(2) The system wants to optimize for resources.</p>
<p>Once the framework delivers a <code>Lifecycle.Terminate()</code>, the agent application
may exit itself, or is killed by framework after a timeout.</p>
<p>For more info see:</p>
<ul>
<li>fuchsia.modular.AgentContext and fuchsia.modular.ComponentContext for
capabilities an agent has.</li>
<li>fuchsia.modular.Lifecycle for how Components get lifecycle events.</li>
</ul>

### Connect {#Connect}

<p>Called when some component tries to connect to this agent. <code>requestor_url</code>
identifies the requesting client. Different client roles are identified differently:
* For Module clients in the general case, <code>requestor_url</code> will be the name provided at
Module create time (ie, in calls to StoryPuppetMaster's StoryCommand.AddMod/mod_name)
with :'s escaped (see below for a complete explanation).
* For all other clients (Agents and Shells), <code>requestor_url</code> is set to the requesting
component's URL.</p>
<p><code>services</code> must be connected to an implementation of fuchsia.sys.ServiceProvider offering
services specific to the requesting client.</p>
<p>Details on module naming: modules are named hierarchically based on what client created
them. This is called a module path. If created by 1) an agent or 2) an existing module, the
path is constructed differently.</p>
<p>In the case of (2), the module path is the concatenation of the existing module's path with
the new module's name, as provided by the parent module. In the case of (1), the module
path is the concatenation of StoryCommand.AddMod/mod_name and
StoryCommand.AddMod/surface_relation_parent.</p>
<p>The full path is encoded into <code>requestor_url</code> as escape_colons(module_path).join(':').</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>requestor_url</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>services</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.sys/'>fuchsia.sys</a>/<a class='link' href='../fuchsia.sys/#ServiceProvider'>ServiceProvider</a>&gt;</code>
            </td>
        </tr></table>



## AgentContext {#AgentContext}
*Defined in [fuchsia.modular/agent_context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/agent/agent_context.fidl#11)*

<p>An instance of this service is exposed to agents in their namespace.</p>

### GetComponentContext {#GetComponentContext}

<p>DEPRECATED: ComponentContext is now available in the
namespace/environment for Modules.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ComponentContext'>ComponentContext</a>&gt;</code>
            </td>
        </tr></table>



### GetEntityReferenceFactory {#GetEntityReferenceFactory}

<p>Connects to an EntityReferenceFactory for this Agent. Entity references
obtained from this EntityReferenceFactory will be resolved back to this
Agent.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#EntityReferenceFactory'>EntityReferenceFactory</a>&gt;</code>
            </td>
        </tr></table>



### GetTokenManager {#GetTokenManager}

<p>The auth token manager this Agent may use for accessing external services.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.auth/'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/#TokenManager'>TokenManager</a>&gt;</code>
            </td>
        </tr></table>



## AgentController {#AgentController}
*Defined in [fuchsia.modular/agent_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/agent/agent_controller/agent_controller.fidl#12)*

<p>This interface is used by the caller of ComponentContext::ConnectToAgent() to
tell the framework that it is still interested in keeping this Agent running.</p>
<p>The system counts AgentController connections and terminates this Agent if
the count goes to zero.</p>

## BaseShell {#BaseShell}
*Defined in [fuchsia.modular/base_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/basemgr/base_shell.fidl#18)*

<p>This interface is implemented by a base shell. Dependencies are passed to it
in Initialize() on startup. The base shell is also expected to implement
Lifecycle in order to receive a Terminate() call on teardown.</p>
<p>In one component instance there can only be one BaseShell service instance.
The ViewOwner request is sent to the separate ViewProvider service. This way,
the base shell may be implemented as a flutter component.</p>

### Initialize {#Initialize}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>base_shell_context</code></td>
            <td>
                <code><a class='link' href='#BaseShellContext'>BaseShellContext</a></code>
            </td>
        </tr><tr>
            <td><code>base_shell_params</code></td>
            <td>
                <code><a class='link' href='#BaseShellParams'>BaseShellParams</a></code>
            </td>
        </tr></table>



### GetAuthenticationUIContext {#GetAuthenticationUIContext}

<p>This method may be invoked by the basemgr to request an
AuthenticationUIContext. <code>request</code> will then be used to request the base
shell to show login screen during a UserProvider.AddUser() or if a token
needs to be refreshed.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.auth/'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/#AuthenticationUIContext'>AuthenticationUIContext</a>&gt;</code>
            </td>
        </tr></table>



## BaseShellContext {#BaseShellContext}
*Defined in [fuchsia.modular/base_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/basemgr/base_shell.fidl#32)*

<p>This interface allows the <code>BaseShell</code> to request capabilities from the
<code>Basemgr</code> in a way that is more explicit about the services that are
offered than a generic <code>ServiceProvider</code>.</p>

### GetUserProvider {#GetUserProvider}

<p>Acquires the user provider service, which is used to add/remove/list and
authenticate users.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#UserProvider'>UserProvider</a>&gt;</code>
            </td>
        </tr></table>



### GetPresentation {#GetPresentation}

<p>Acquires the presentation service, which is assumed to already be
connected to the presenter.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>presentation</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.ui.policy/'>fuchsia.ui.policy</a>/<a class='link' href='../fuchsia.ui.policy/#Presentation'>Presentation</a>&gt;</code>
            </td>
        </tr></table>



## UserProvider {#UserProvider}
*Defined in [fuchsia.modular/user_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/basemgr/user_provider.fidl#13)*

<p>Given by the <code>Basemgr</code> to the <code>BaseShell</code> at Initialize() so the
<code>BaseShell</code> can get information about the users of this device from the
<code>Basemgr</code>, and act on the provided information (including extending the
user database).</p>

### AddUser {#AddUser}

<p>Adds information of a user that can be used to authenticate her/him to this
device. Once successfully added, the user can login to the same device via
Login().</p>
<p><code>identity_provider</code> is the identity provider to use for identification.</p>
<p><code>device_name</code> is what the user wants to name the device. If null or empty
the device's current hostname will be used.</p>
<p><code>account</code> is NULL if there was an error during identification and
<code>error_code</code> is set.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>identity_provider</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular.auth/'>fuchsia.modular.auth</a>/<a class='link' href='../fuchsia.modular.auth/#IdentityProvider'>IdentityProvider</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>account</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular.auth/'>fuchsia.modular.auth</a>/<a class='link' href='../fuchsia.modular.auth/#Account'>Account</a>?</code>
            </td>
        </tr><tr>
            <td><code>error_code</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr></table>

### RemoveUser {#RemoveUser}

<p>Removes information of a user from the local user database.</p>
<p><code>account_id</code> is received from either AddUser() or PreviousUsers().</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>account_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error_code</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr></table>

### Login {#Login}

<p>Uses the credentials provided in AddUser() to start a user session. This
would mean syncing with the user's ledger instance and displaying a user
shell with all of the user's stories.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>user_login_params</code></td>
            <td>
                <code><a class='link' href='#UserLoginParams'>UserLoginParams</a></code>
            </td>
        </tr></table>



### Login2 {#Login2}

<p>DEPRECATED: For transitional purposes only.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>user_login_params</code></td>
            <td>
                <code><a class='link' href='#UserLoginParams2'>UserLoginParams2</a></code>
            </td>
        </tr></table>



### PreviousUsers {#PreviousUsers}

<p>List of all users who have authenticated to this device in the past.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>accounts</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular.auth/'>fuchsia.modular.auth</a>/<a class='link' href='../fuchsia.modular.auth/#Account'>Account</a>&gt;</code>
            </td>
        </tr></table>

## ComponentContext {#ComponentContext}
*Defined in [fuchsia.modular/component_context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/component/component_context.fidl#13)*

<p>Provided to all component instances in their respective initialization
information by the framework. For example, a Module gets it from its
ModuleContext and an Agent gets it from its AgentContext.</p>

### ConnectToAgent {#ConnectToAgent}

<p>Used to start an agent in the user scope if it isn't already running, and
connect to it.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>url</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>incoming_services</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.sys/'>fuchsia.sys</a>/<a class='link' href='../fuchsia.sys/#ServiceProvider'>ServiceProvider</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>controller</code></td>
            <td>
                <code>request&lt;<a class='link' href='#AgentController'>AgentController</a>&gt;</code>
            </td>
        </tr></table>



### ConnectToAgentService {#ConnectToAgentService}

<p>Connects to an agent that provides the given <code>request.service_name</code>, and
then connects the given <code>request.channel</code> to that service.
<code>request.agent_controller</code> must be kept alive until the service is no
longer required.</p>
<p>If an error is encountered, the <code>request.channel</code> will be closed with
a status code, such as:</p>
<ul>
<li><code>ZX_ERR_NOT_FOUND</code> -- if a <code>request.handler</code> agent URL is not
specified, and an agent for the <code>request.service_name</code> is not found</li>
<li><code>ZX_ERR_PEER_CLOSED</code> -- if <code>request.service_name</code> is not available from
the agent (either specified or discovered)</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code><a class='link' href='#AgentServiceRequest'>AgentServiceRequest</a></code>
            </td>
        </tr></table>



### GetEntityResolver {#GetEntityResolver}

<p>Gets the EntityResolver service, which can be used to resolve an entity
reference to an Entity interface.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#EntityResolver'>EntityResolver</a>&gt;</code>
            </td>
        </tr></table>



## Entity {#Entity}
*Defined in [fuchsia.modular/entity.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/entity/entity.fidl#10)*

<p>A multi-typed data entity.</p>

### GetTypes {#GetTypes}

<p>Returns the types associated with this entity. Each entry in <code>types</code>
references a well-known content type.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>types</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr></table>

### GetData {#GetData}

<p>Given one of the types returned from <code>GetTypes()</code> above, returns
associated short-form data, or null if the type is absent from
<code>GetTypes()</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>type</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a>?</code>
            </td>
        </tr></table>

### WriteData {#WriteData}

<p>Sets the data for a particular type. This will precipitate an <code>OnUpdated</code>
event with the associated type.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>type</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#EntityWriteStatus'>EntityWriteStatus</a></code>
            </td>
        </tr></table>

### GetReference {#GetReference}

<p>Gets the entity reference for this entity, which can be persisted and
then later used to locate this entity. These references are weak
references and are not sufficient to keep the entity alive.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>entity_reference</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

### Watch {#Watch}

<p>Begins watching for data changes on a particular type. The watcher
immediately fires <code>OnUpdated</code> with the current value for the requested
type (or null if the type is not present). Closing the <code>Entity</code> interface
does not close the watcher.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>type</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#EntityWatcher'>EntityWatcher</a></code>
            </td>
        </tr></table>



## EntityWatcher {#EntityWatcher}
*Defined in [fuchsia.modular/entity.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/entity/entity.fidl#37)*


### OnUpdated {#OnUpdated}

<p>Fires on data updates for a particular type. If the type is initially not
present, a null <code>data</code> pointer is produced. The type may only transition
from absent to present at most once, as there is no deletion.</p>
<p>No deduplication is performed.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a>?</code>
            </td>
        </tr></table>



## EntityProvider {#EntityProvider}
*Defined in [fuchsia.modular/entity_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/entity/entity_provider.fidl#21)*

<p>EntityProviders (agents) must implement and provide the <code>EntityProvider</code>
service if they create entity references (using <code>EntityReferenceFactory</code>).
This service is used by the framework to provide data for an <code>Entity</code>
interface for an entity. This interface is requested by the framework in
the agent's <em>application</em> outgoing services, and is closed by the framework
when there are no more <code>Entity</code>s that need to be provided.</p>
<p>In the below methods, <code>cookie</code> will have been previously passed to
<code>EntityReferenceFactory.CreateReference()</code>, though this may have been in an
earlier or remote app instance. Entity providers should attempt to resolve
unfamiliar cookies or else treat the entities as empty and read-only.</p>

### GetTypes {#GetTypes}

<p>Returns the types associated with the requested entity. Each entry in
<code>type</code> references a well-known content type.</p>
<p>If the cookie cannot be resolved, the provider should produce an empty
vector.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>cookie</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>types</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr></table>

### GetData {#GetData}

<p>Given one of the types returned from <code>GetTypes()</code> above, returns
associated short-form data, or null if the type is absent from
<code>GetTypes()</code>.</p>
<p>If the cookie cannot be resolved, the provider should return null.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>cookie</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a>?</code>
            </td>
        </tr></table>

### WriteData {#WriteData}

<p>Sets the data for a particular type. This must precipitate an <code>OnUpdate</code>
event with the associated type.</p>
<p>If the cookie cannot be resolved, the provider should no-op with
<code>EntityWriteStatus::READ_ONLY</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>cookie</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#EntityWriteStatus'>EntityWriteStatus</a></code>
            </td>
        </tr></table>

### Watch {#Watch}

<p>Begins watching for data changes on a particular type. The watcher must
immediately fire <code>OnUpdated</code> with the current value for the requested
type (or null if the type is not present).</p>
<p>No deduplication of events should be performed.</p>
<p>At most one update may be in-flight at a time on a particular watcher;
once a client is ready for another update, it will call the callback. At
most one update should be queued for dispatch for a particular watcher;
older updates should be dropped.</p>
<p>If the cookie cannot be resolved, the provider should emit a single event
with null data.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>cookie</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#EntityWatcher'>EntityWatcher</a></code>
            </td>
        </tr></table>



## EntityReferenceFactory {#EntityReferenceFactory}
*Defined in [fuchsia.modular/entity_reference_factory.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/entity/entity_reference_factory.fidl#13)*

<p>Agents use this interface to create Entity references that can subsequently
be dereferenced into an <code>Entity</code> interface using <code>EntityResolver</code>.
Agents that create entity references must also expose an <code>EntityProvider</code>
service in their application's outgoing services, so that agents can provide
data for <code>Entity</code>s that they create. This interface is available through an
agent's <code>AgentContext</code>.</p>

### CreateReference {#CreateReference}

<p>Agents call this to manufacture a reference for an Entity they will
provide. Returns an opaque, persistable <code>entity_reference</code> that components
can resolve into an <code>Entity</code> interface using <code>EntityResolver</code>. When data is
requested from an <code>Entity</code> interface resolved from this <code>entity_reference</code>,
the <code>cookie</code> associated with this <code>entity_reference</code> will be passed back to
the <code>EntityProvider</code> of the Agent that originally created this reference.</p>
<p><code>cookie</code> should uniquely identify the <code>Entity</code> within the scope of the
calling entity provider. For example, it may be used as the primary key
value for a database.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>cookie</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>entity_reference</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

## EntityResolver {#EntityResolver}
*Defined in [fuchsia.modular/entity_resolver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/entity/entity_resolver.fidl#10)*

<p>This interface is given to all components in their <code>ComponentContext</code>. Any
component can resolve an entity reference into an <code>Entity</code>.</p>

### ResolveEntity {#ResolveEntity}

<p>Finds and binds <code>entity_request</code> to an Entity handle for the Entity
referenced by <code>entity_reference</code>. If an error occurs, <code>entity_request</code>
will be closed.</p>
<p>This method is called by any component who wants to use an Entity using an
entity reference. A component has to get an entity reference (directly or
indirectly) from an agent, for example through some fidl interface. The
agent will create an entity reference using EntityReferenceFactory. During
entity resolution, that agent then provides data for the Entity
through an EntityProvider service it exposes. Thus, any Agent that wishes
to use EntityReferenceFactory to dispense entity references through its
agent services MUST also implement the EntityProvider service.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>entity_reference</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>entity_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Entity'>Entity</a>&gt;</code>
            </td>
        </tr></table>



## IntentHandler {#IntentHandler}
*Defined in [fuchsia.modular/intent_handler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/intent/intent_handler.fidl#17)*

<p>The IntentHandler interface is exposed by modules which wish to handle
intents on the behalf of other modules or agents.</p>
<p>The modular framework expects any module which declares support for intent
handling in its module manifest to expose IntentHandler in its outgoing
services.</p>
<p>Any time the framework receives an intent which is to be handled by a specific
module its <code>IntentHandler</code> will be called with the intent it is meant to handle.</p>

### HandleIntent {#HandleIntent}

<p>Handles the provided intent. Any links referenced in the intent parameters
will be in the namespace of the handling component, and can be retrieved via
<code>ModuleContext.GetLink</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>intent</code></td>
            <td>
                <code><a class='link' href='#Intent'>Intent</a></code>
            </td>
        </tr></table>



## Lifecycle {#Lifecycle}
*Defined in [fuchsia.modular/lifecycle.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/lifecycle/lifecycle.fidl#9)*

<p>An interface implemented by applications that wish to terminate gracefully.</p>

### Terminate {#Terminate}

<p>The client of this application has requested that this application
terminate gracefully.</p>
<p>If the application does not terminate itself in a timely manner, the client
may forcibly terminate the application.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## ModuleContext {#ModuleContext}
*Defined in [fuchsia.modular/module_context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_context.fidl#13)*

<p>This interface is exposed to all Module instances in a story. It allows to
create Link instances and run more Module instances.</p>

### AddModuleToStory {#AddModuleToStory}

<p>Starts a new Module instance and adds it to the story. The Module to
execute is identified by the contents of [intent] and the Module instance
is given a [name] in the scope of the starting Module instance. The view
for the Module is given to the story shell for display.</p>
<p>Providing a [surface_relation] advises the StoryShell how to layout
surfaces that the new module creates. If [surface_relation] is null then
a default relation is used.</p>
<p>If the method is called again with the same [name] by the same Module
instance, but with different arguments, the existing Module instance is
restarted with the changed arguments. If the other arguments don't
change, just an additional ModuleController connection is made.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>intent</code></td>
            <td>
                <code><a class='link' href='#Intent'>Intent</a></code>
            </td>
        </tr><tr>
            <td><code>module_controller</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ModuleController'>ModuleController</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>surface_relation</code></td>
            <td>
                <code><a class='link' href='#SurfaceRelation'>SurfaceRelation</a>?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#StartModuleStatus'>StartModuleStatus</a></code>
            </td>
        </tr></table>

### EmbedModule {#EmbedModule}

<p>Like AddModuleToStory(), but passes a [view_token] explicitly to embed
the view of the requested Module instance in the view of the requesting
Module instance, instead of relying on the story shell for display. If a
Module instance with the same [name] and [intent] is already running,
[view_token] is destroyed.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>intent</code></td>
            <td>
                <code><a class='link' href='#Intent'>Intent</a></code>
            </td>
        </tr><tr>
            <td><code>module_controller</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ModuleController'>ModuleController</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>view_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/#ViewToken'>ViewToken</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#StartModuleStatus'>StartModuleStatus</a></code>
            </td>
        </tr></table>

### RemoveSelfFromStory {#RemoveSelfFromStory}

<p>When a module calls [RemoveSelfFromStory()] the framework will stop the
module and remove it from the story. If there are no more running modules
in the story the story will be deleted.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### CreateEntity {#CreateEntity}

<p>Creates a [fuchsia.modular.Entity] with the given [type] and [data]. The
lifetime of the created entity is tied to the lifetime of the current story,
but can be dereferenced by modules and agents outside the scope of the story.</p>
<p>[entity_request] will be connected to the created entity, or closed if the
creation fails.</p>
<p>The returned [reference] is the entity reference for the created entity, or
null if the entity creation failed.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>type</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
        </tr><tr>
            <td><code>entity_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Entity'>Entity</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>entity_reference</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr></table>

## OngoingActivity {#OngoingActivity}
*Defined in [fuchsia.modular/module_context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_context.fidl#70)*

<p>This interface defines the protocol over which a Module can communicate about
an ongoing activity to the framework. It is provided to Modules via
ModuleContext.StartOngoingActivity().</p>

## ModuleController {#ModuleController}
*Defined in [fuchsia.modular/module_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_controller.fidl#12)*

<p>This interface is used by the caller of ModuleContext.StartModule() to
control the started Module instance.</p>
<p>Closing this connection doesn't affect its Module instance; it just
relinquishes the ability of the caller to control the Module instance.</p>

### Focus {#Focus}

<p>Requests that this module become the focused module in the story.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Defocus {#Defocus}

<p>Requests that this module be hidden in the story.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Stop {#Stop}

<p>Requests the Module instance to stop. The running Module component's
Lifecycle::Terminate() method is called, the instance is shut down and
state within the framework is cleaned up.</p>
<p>The result callback is called once the Module's runtime has been torn down.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### OnStateChange {#OnStateChange}

<p>Called with the current state when it changes.
DEPRECATED: Do not use this. ModuleState is a framework-internal concept
and should not be exposed outside.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>new_state</code></td>
            <td>
                <code><a class='link' href='#ModuleState'>ModuleState</a></code>
            </td>
        </tr></table>

## ModuleResolver {#ModuleResolver}
*Defined in [fuchsia.modular/module_resolver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module_resolver/module_resolver.fidl#8)*


### FindModules {#FindModules}

<p>Finds Modules (contained in Fuchsia packages) that satisfy the constraints
specified in <code>query</code>. Module resolution is done by matching the requested
<code>query.action</code> and <code>query.parameter_constraints</code> (with both names and
types) against actions and constraints specified in module manifests.</p>
<p>If no results could be found, <code>response.results</code> will be empty.</p>
<p>For detailed information on the resolution process, see
docs/modular/module_resolution.md.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>query</code></td>
            <td>
                <code><a class='link' href='#FindModulesQuery'>FindModulesQuery</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#FindModulesResponse'>FindModulesResponse</a></code>
            </td>
        </tr></table>

## FocusController {#FocusController}
*Defined in [fuchsia.modular/focus.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/session/focus.fidl#21)*

<p>This file has interfaces for 2 pieces of information: (1) The story
that is currently in focus and (2) stories that are visible to the
user. Names of interfaces follow the usual patterns:</p>
<p>{Focus,VisibleStories}Controller is used by session shell to update
information whenever changes take place.</p>
<p>FocusProvider is used by session shell to
query and get updates on which story is in focus on which device
and visible stories on this device.</p>
<p>Implemented by sessionmgr. Given to session shell through its namespace.</p>

### Set {#Set}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>focused_story_id</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr></table>



### WatchRequest {#WatchRequest}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#FocusRequestWatcher'>FocusRequestWatcher</a></code>
            </td>
        </tr></table>



## FocusRequestWatcher {#FocusRequestWatcher}
*Defined in [fuchsia.modular/focus.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/session/focus.fidl#30)*

<p>Implemented by session shell. OnFocusRequest() gets called whenever there
is a new request to change focus on this device. Requests can be
made via FocusProvider.Request().</p>

### OnFocusRequest {#OnFocusRequest}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



## FocusProvider {#FocusProvider}
*Defined in [fuchsia.modular/focus.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/session/focus.fidl#37)*

<p>Implemented by sessionmgr. Given to session shell and session agents through
their namespace. Focus is persisted on the ledger.</p>

### Query {#Query}

<p>Returns the stories that are focused across all devices.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>focused_stories</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#FocusInfo'>FocusInfo</a>&gt;</code>
            </td>
        </tr></table>

### Watch {#Watch}

<p>Watches for change in focus on any of the user's devices.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#FocusWatcher'>FocusWatcher</a></code>
            </td>
        </tr></table>



### Request {#Request}

<p>Requests session shell to change focus on this device. If session shell
responds to this request, focus shall be taken away from
previously focused story and an update will be sent on
FocusWatcher.OnFocusChange(). If <code>story_id</code> is NULL, the timeline
is brought back into focus.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_id</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr></table>



## FocusWatcher {#FocusWatcher}
*Defined in [fuchsia.modular/focus.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/session/focus.fidl#57)*

<p>Implemented by anyone who is interested in getting updates when focus
changes.</p>

### OnFocusChange {#OnFocusChange}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>focus_info</code></td>
            <td>
                <code><a class='link' href='#FocusInfo'>FocusInfo</a>?</code>
            </td>
        </tr></table>



## SessionShell {#SessionShell}
*Defined in [fuchsia.modular/session_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/session/session_shell.fidl#15)*

<p>This interface is implemented by a session shell and is used by the
sessionmgr to hand to the session shell views of stories, or to notify that
the view of a story is about to be closed.</p>

### AttachView {#AttachView}

<p>Displays the given story view. The story this view belongs to is
identified by <code>view_id.story_id</code>.
DEPRECATED.  For transitional purposes only.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_id</code></td>
            <td>
                <code><a class='link' href='#ViewIdentifier'>ViewIdentifier</a></code>
            </td>
        </tr><tr>
            <td><code>view_holder_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/#ViewHolderToken'>ViewHolderToken</a></code>
            </td>
        </tr></table>



### AttachView2 {#AttachView2}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_id</code></td>
            <td>
                <code><a class='link' href='#ViewIdentifier'>ViewIdentifier</a></code>
            </td>
        </tr><tr>
            <td><code>view_holder_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/#ViewHolderToken'>ViewHolderToken</a></code>
            </td>
        </tr></table>



### DetachView {#DetachView}

<p>Instructs the session shell to detach the view identified by <code>view_id</code>
that was previously provided by AttachView() from the UI of the session
shell. The view will be closed soon after DetachView() returns, or when a
timeout is reached.</p>
<p>It is customary for the session shell to display a placeholder before a
view is attached for a given view identifier, or after it was detached.</p>
<p>If the story identified by <code>view_id.story_id</code> is about to be deleted, the
Shell will observe a call to StoryProviderWatcher.OnDelete() sometime
after DetachView() returns.</p>
<p>If the session for which this session shell is responsible for is being
terminated, or the session shell is stopped because it's replaced by
another session shell, DetachView() will <em>not</em> be called at all, and the
shell will rather observe a call to Lifecycle.Terminate().</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_id</code></td>
            <td>
                <code><a class='link' href='#ViewIdentifier'>ViewIdentifier</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## SessionShellContext {#SessionShellContext}
*Defined in [fuchsia.modular/session_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/session/session_shell.fidl#57)*

<p>This interface allows a <code>SessionShell</code> to request capabilities from its
creator in a way that is more explicit about the services that are
offered than a generic <code>ServiceProvider</code>.</p>

### GetAccount {#GetAccount}

<p>The account associated with the currently logged-in user. It's NULL if
logged into GUEST mode.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>account</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular.auth/'>fuchsia.modular.auth</a>/<a class='link' href='../fuchsia.modular.auth/#Account'>Account</a>?</code>
            </td>
        </tr></table>

### GetComponentContext {#GetComponentContext}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ComponentContext'>ComponentContext</a>&gt;</code>
            </td>
        </tr></table>



### GetFocusController {#GetFocusController}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#FocusController'>FocusController</a>&gt;</code>
            </td>
        </tr></table>



### GetFocusProvider {#GetFocusProvider}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#FocusProvider'>FocusProvider</a>&gt;</code>
            </td>
        </tr></table>



### GetPresentation {#GetPresentation}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.ui.policy/'>fuchsia.ui.policy</a>/<a class='link' href='../fuchsia.ui.policy/#Presentation'>Presentation</a>&gt;</code>
            </td>
        </tr></table>



### GetStoryProvider {#GetStoryProvider}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#StoryProvider'>StoryProvider</a>&gt;</code>
            </td>
        </tr></table>



### Logout {#Logout}

<p>Requests logout of the user. This causes the basemgr to tear down the
<code>Sessionmgr</code> instance of the user.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Restart {#Restart}

<p>Restarts the session without logging out the user.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## SessionShellPresentationProvider {#SessionShellPresentationProvider}
*Defined in [fuchsia.modular/session_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/session/session_shell.fidl#83)*

<p>Session shell provides this service to the framework which may plumb it to
different subscribers, such as story shell and intelligence provider.</p>
<p>EXPERIMENTAL Service that allows consumers of a given story to get a
connection to a Presentation, and visual state services provided by the user
shell. This allows story shell implementations to coordinate event and focus
handling. An analog mechanism exists between BaseShell and SessionShell.</p>

### GetPresentation {#GetPresentation}

<p>When a StoryShell calls StoryShellContext.GetPresentation(), this request
arrives here.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.ui.policy/'>fuchsia.ui.policy</a>/<a class='link' href='../fuchsia.ui.policy/#Presentation'>Presentation</a>&gt;</code>
            </td>
        </tr></table>



### WatchVisualState {#WatchVisualState}

<p>When a StoryShell calls StoryShellContext.WatchVisualState(), this request
arrives here.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#StoryVisualStateWatcher'>StoryVisualStateWatcher</a></code>
            </td>
        </tr></table>



## PuppetMaster {#PuppetMaster}
*Defined in [fuchsia.modular/puppet_master.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/puppet_master.fidl#52)*


### ControlStory {#ControlStory}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#StoryPuppetMaster'>StoryPuppetMaster</a>&gt;</code>
            </td>
        </tr></table>



### DeleteStory {#DeleteStory}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### GetStories {#GetStories}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_names</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr></table>

## StoryPuppetMaster {#StoryPuppetMaster}
*Defined in [fuchsia.modular/puppet_master.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/puppet_master.fidl#75)*


### Enqueue {#Enqueue}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>commands</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#StoryCommand'>StoryCommand</a>&gt;</code>
            </td>
        </tr></table>



### Execute {#Execute}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#ExecuteResult'>ExecuteResult</a></code>
            </td>
        </tr></table>

### SetStoryInfoExtra {#SetStoryInfoExtra}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_info_extra</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#StoryInfoExtraEntry'>StoryInfoExtraEntry</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#StoryPuppetMaster_SetStoryInfoExtra_Result'>StoryPuppetMaster_SetStoryInfoExtra_Result</a></code>
            </td>
        </tr></table>

### Annotate {#Annotate}

<p>Attach the <code>annotations</code> to the story. If the story does not yet exist,
it will be created.</p>
<p>Existing annotations with the same key will be overwritten, or
deleted if new value is null.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>annotations</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Annotation'>Annotation</a>&gt;[50]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#StoryPuppetMaster_Annotate_Result'>StoryPuppetMaster_Annotate_Result</a></code>
            </td>
        </tr></table>

### AnnotateModule {#AnnotateModule}

<p>Attach the <code>annotations</code> to the module with the given <code>id</code>.
The module can be annotated before being added to the story, but if the
story does not yet exist, AnnotationError.NOT_FOUND is returned.</p>
<p>Existing annotations with the same key will be overwritten.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>module_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>annotations</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Annotation'>Annotation</a>&gt;[50]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#StoryPuppetMaster_AnnotateModule_Result'>StoryPuppetMaster_AnnotateModule_Result</a></code>
            </td>
        </tr></table>

## StoryController {#StoryController}
*Defined in [fuchsia.modular/story_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_controller.fidl#12)*

<p>Used by the clients of StoryProvider (SessionShell) to interact with a single
story. Created by StoryProvider.</p>
<p>If <code>StoryController</code> is closed, the <code>StoryState</code> associated with this story
does not change.</p>

### GetInfo {#GetInfo}

<p>Gets information associated with the story.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#StoryInfo'>StoryInfo</a></code>
            </td>
        </tr><tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#StoryState'>StoryState</a></code>
            </td>
        </tr></table>

### GetInfo2 {#GetInfo2}

<p>For transition purposes only.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#StoryInfo2'>StoryInfo2</a></code>
            </td>
        </tr><tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#StoryState'>StoryState</a></code>
            </td>
        </tr></table>

### RequestStart {#RequestStart}

<p>Requests to run the story controlled by this <code>StoryController</code> instance.
When the story starts, if not yet running, the view of the newly started
story shell will be passed in a call to SessionShell.AttachView().</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Stop {#Stop}

<p>Requests to stop the story controlled by this <code>StoryController</code>. If Start()
requests are pending when this request is issued, the request is queued
until the Start() requests complete. Before stopping the story, a snapshot
of the story will be taken and saved. Returns when the story is stopped.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### Watch {#Watch}

<p>Registers a watcher for changes of the story state.</p>
<p>Note that stories can stop themselves at any time and it is advisable
for the holder of a StoryController to provide a watcher.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#StoryWatcher'>StoryWatcher</a></code>
            </td>
        </tr></table>



### Annotate {#Annotate}

<p>Attach the <code>annotations</code> to the story.</p>
<p>Existing annotations with the same key will be overwritten.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>annotations</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Annotation'>Annotation</a>&gt;[50]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#StoryController_Annotate_Result'>StoryController_Annotate_Result</a></code>
            </td>
        </tr></table>

## StoryWatcher {#StoryWatcher}
*Defined in [fuchsia.modular/story_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_controller.fidl#45)*

<p>Implemented by the client calling StoryController.Watch().</p>

### OnStateChange {#OnStateChange}

<p>Called with the current state right after registration, and subsequently
when the state changes.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>new_state</code></td>
            <td>
                <code><a class='link' href='#StoryState'>StoryState</a></code>
            </td>
        </tr></table>



### OnModuleAdded {#OnModuleAdded}

<p>DEPRECATED</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>module_data</code></td>
            <td>
                <code><a class='link' href='#ModuleData'>ModuleData</a></code>
            </td>
        </tr></table>



### OnModuleFocused {#OnModuleFocused}

<p>DEPRECATED</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>module_path</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr></table>



## StoryProvider {#StoryProvider}
*Defined in [fuchsia.modular/story_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_provider.fidl#13)*

<p>Sessionmgr passes a connection to this service to the SessionShell so it can
operate on stories for the user.</p>
<p>Closing a <code>StoryProvider</code> connection has no effect on the state of the
framework.</p>

### GetStories {#GetStories}

<p>Returns a list of existing stories. If <code>watcher</code> is provided, the client will
be notified of story changes (new stories, deleted stories, runtime
state changes).</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#StoryProviderWatcher'>StoryProviderWatcher</a>?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_infos</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#StoryInfo'>StoryInfo</a>&gt;</code>
            </td>
        </tr></table>

### GetStories2 {#GetStories2}

<p>For transition purposes only.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#StoryProviderWatcher'>StoryProviderWatcher</a>?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_infos</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#StoryInfo2'>StoryInfo2</a>&gt;</code>
            </td>
        </tr></table>

### GetStoryInfo {#GetStoryInfo}

<p>Requests detailed information about the given story. If the story doesn't
exist, returns null.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_info</code></td>
            <td>
                <code><a class='link' href='#StoryInfo'>StoryInfo</a>?</code>
            </td>
        </tr></table>

### GetStoryInfo2 {#GetStoryInfo2}

<p>For transition purposes only.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_info</code></td>
            <td>
                <code><a class='link' href='#StoryInfo2'>StoryInfo2</a></code>
            </td>
        </tr></table>

### GetController {#GetController}

<p>Obtains a controller for a previously created story identified by its story
ID. Obtaining the controller doesn't run it yet. If the story doesn't
exist, the interface request is closed.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#StoryController'>StoryController</a>&gt;</code>
            </td>
        </tr></table>



### Watch {#Watch}

<p>Registers a watcher for changes in the story collection.
DEPRECATED: In favor of GetStories().</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#StoryProviderWatcher'>StoryProviderWatcher</a></code>
            </td>
        </tr></table>



## StoryProviderWatcher {#StoryProviderWatcher}
*Defined in [fuchsia.modular/story_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_provider.fidl#42)*

<p>Implemented by clients of StoryProvider.</p>

### OnChange {#OnChange}

<p>Called in three different situations:</p>
<ul>
<li>
<p>Immediately when a new watcher is registered with one OnChange()
invocation with the current infor and state of each story known on the
current device.</p>
</li>
<li>
<p>Every time a change to StoryInfo is applied to the record of the story
kept on the current device, including a new story created on another
device becoming known on this device for the first time.</p>
</li>
<li>
<p>Every time the StoryState of the story changes on this device. The
StoryState on another device of a story known on this device is not made
known on this device.</p>
</li>
<li>
<p>Every time the StoryVisibilityState of the story changes on this device.
The StoryVisibilityState on another device of a story known on this
device is not made known on this device.</p>
<p>I.e. if the story is started or stopped on <em>another</em> device, it does
<em>not</em> cause an OnChange() call on <em>this</em> device. Cf. OnDelete() below.</p>
</li>
</ul>
<p>The ID of the story the notifications are about are part of StoryInfo.</p>
<p><code>story_state</code> is STOPPED if the story was just created or just became known
on this device and was not yet started on the current device. It's RUNNING
when the story is started on the current device.</p>
<p><code>story_visibility_state</code> is DEFAULT until a mod on the current device
requests for the visibility state to be changed.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_info</code></td>
            <td>
                <code><a class='link' href='#StoryInfo'>StoryInfo</a></code>
            </td>
        </tr><tr>
            <td><code>story_state</code></td>
            <td>
                <code><a class='link' href='#StoryState'>StoryState</a></code>
            </td>
        </tr><tr>
            <td><code>story_visibility_state</code></td>
            <td>
                <code><a class='link' href='#StoryVisibilityState'>StoryVisibilityState</a></code>
            </td>
        </tr></table>



### OnChange2 {#OnChange2}

<p>For transition purposes only.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_info</code></td>
            <td>
                <code><a class='link' href='#StoryInfo2'>StoryInfo2</a></code>
            </td>
        </tr><tr>
            <td><code>story_state</code></td>
            <td>
                <code><a class='link' href='#StoryState'>StoryState</a></code>
            </td>
        </tr><tr>
            <td><code>story_visibility_state</code></td>
            <td>
                <code><a class='link' href='#StoryVisibilityState'>StoryVisibilityState</a></code>
            </td>
        </tr></table>



### OnDelete {#OnDelete}

<p>Called when a story record is permanently deleted. The deletion could
have originated on this or on another device.</p>
<p>If the story is running on this device at the time it is deleted,
OnChange() will not be called first.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



## StoryShell {#StoryShell}
*Defined in [fuchsia.modular/story_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell.fidl#21)*

<p>This interface is implemented by a story shell. Dependencies are passed to it
in Initialize() on startup. The story shell is also expected to implement
Lifecycle in order to receive a Terminate() call on teardown.</p>
<p>In one component instance there can only be one StoryShell service instance.
The view token is sent to the separate View service. This way, the story
shell may be implemented as a flutter component.</p>
<p>Teardown may occur via the session shell calling StoryController.Stop(), the
sessionmgr being terminated, or by the system shutting down.</p>

### Initialize {#Initialize}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_shell_context</code></td>
            <td>
                <code><a class='link' href='#StoryShellContext'>StoryShellContext</a></code>
            </td>
        </tr></table>



### AddSurface {#AddSurface}

<p>Adds a new Surface and its corresponding view to be displayed by the
StoryShell. More context that allows the story shell to decide how
to layout will be added later. Also, interface to influence life cycle and
focus is obviously missing.
<code>view_connection</code> the new view and the associated Surface ID.
<code>surface_info</code> metadata relating to the Surface.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_connection</code></td>
            <td>
                <code><a class='link' href='#ViewConnection'>ViewConnection</a></code>
            </td>
        </tr><tr>
            <td><code>surface_info</code></td>
            <td>
                <code><a class='link' href='#SurfaceInfo'>SurfaceInfo</a></code>
            </td>
        </tr></table>



### AddSurface2 {#AddSurface2}

<p>DEPRECATED.  For transition purposes only.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_connection</code></td>
            <td>
                <code><a class='link' href='#ViewConnection2'>ViewConnection2</a></code>
            </td>
        </tr><tr>
            <td><code>surface_info</code></td>
            <td>
                <code><a class='link' href='#SurfaceInfo'>SurfaceInfo</a></code>
            </td>
        </tr></table>



### AddSurface3 {#AddSurface3}

<p>For transition purposes only.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_connection</code></td>
            <td>
                <code><a class='link' href='#ViewConnection'>ViewConnection</a></code>
            </td>
        </tr><tr>
            <td><code>surface_info</code></td>
            <td>
                <code><a class='link' href='#SurfaceInfo2'>SurfaceInfo2</a></code>
            </td>
        </tr></table>



### FocusSurface {#FocusSurface}

<p>Focuses the surface with surface_id, bringing it to the foreground.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>surface_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### DefocusSurface {#DefocusSurface}

<p>Defocuses the surface with surface_id, dismissing it to the background.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>surface_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### OnSurfaceFocused {#OnSurfaceFocused}

<p>Notify when a Surface is focused in the story. The focus could be from
a user interaction or requested by the framework through
StoryController#FocusModule.
EXPERIMENTAL</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>surface_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

### RemoveSurface {#RemoveSurface}

<p>Remove the Surface with surface_id from the StoryShell entirely. This is
final. The Surface is removed from the graph. If necessary, the
associated Surface is defocused. There is no expectation that
DefocusSurface is called before this.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>surface_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### UpdateSurface {#UpdateSurface}

<p>Update the surface
This is called when the intent is to update the surface metadata in the
story graph in place. Any fields, except for the surface_id can be
updated. If no value or null is passed for a field it remains unchanged.
This includes the <code>view_holder_token</code> inside the connection.</p>
<p>E.g called when an intent resolves to a module that is known by the
caller to already be running, to update associated metadata.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_connection</code></td>
            <td>
                <code><a class='link' href='#ViewConnection'>ViewConnection</a></code>
            </td>
        </tr><tr>
            <td><code>surface_info</code></td>
            <td>
                <code><a class='link' href='#SurfaceInfo'>SurfaceInfo</a></code>
            </td>
        </tr></table>



### UpdateSurface2 {#UpdateSurface2}

<p>DEPRECATED.  For transition purposes only.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_connection</code></td>
            <td>
                <code><a class='link' href='#ViewConnection2'>ViewConnection2</a></code>
            </td>
        </tr><tr>
            <td><code>surface_info</code></td>
            <td>
                <code><a class='link' href='#SurfaceInfo'>SurfaceInfo</a></code>
            </td>
        </tr></table>



### UpdateSurface3 {#UpdateSurface3}

<p>For transition purposes only.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_connection</code></td>
            <td>
                <code><a class='link' href='#ViewConnection'>ViewConnection</a></code>
            </td>
        </tr><tr>
            <td><code>surface_info</code></td>
            <td>
                <code><a class='link' href='#SurfaceInfo2'>SurfaceInfo2</a></code>
            </td>
        </tr></table>



## StoryShellContext {#StoryShellContext}
*Defined in [fuchsia.modular/story_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell.fidl#135)*

<p>This interface provides the StoryShell instance with everything it needs to
know or be able to do about the Story. Not much right now, but we expect this
to increase.</p>

### GetPresentation {#GetPresentation}

<p>Requests a Presentation connection from the SessionShell. See
SessionShellPresenationProvider in session_shell.fidl.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.ui.policy/'>fuchsia.ui.policy</a>/<a class='link' href='../fuchsia.ui.policy/#Presentation'>Presentation</a>&gt;</code>
            </td>
        </tr></table>



### WatchVisualState {#WatchVisualState}

<p>Starts watching Story shell's visual state.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#StoryVisualStateWatcher'>StoryVisualStateWatcher</a></code>
            </td>
        </tr></table>



### RequestView {#RequestView}

<p>Requests a view for a Surface.
Requests that a view for <code>surface_id</code> is provided through
StoryShell.ReconnectView().</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>surface_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



## StoryVisualStateWatcher {#StoryVisualStateWatcher}
*Defined in [fuchsia.modular/story_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell.fidl#150)*

<p>Implemented by StoryShell to get notified about visual state changes.</p>

### OnVisualStateChange {#OnVisualStateChange}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>visual_state</code></td>
            <td>
                <code><a class='link' href='#StoryVisualState'>StoryVisualState</a></code>
            </td>
        </tr></table>



## StoryShellFactory {#StoryShellFactory}
*Defined in [fuchsia.modular/story_shell_factory.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell_factory.fidl#11)*

<p>StoryShellFactory creates or returns an existing <code>StoryShell</code> for a particular story.
This is intended to be implemented by session shells that want to implement
StoryShell functionality themselves.</p>

### AttachStory {#AttachStory}

<p>Requests a StoryShell for the story with the given <code>story_id</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>story_shell</code></td>
            <td>
                <code>request&lt;<a class='link' href='#StoryShell'>StoryShell</a>&gt;</code>
            </td>
        </tr></table>



### DetachStory {#DetachStory}

<p>Instructs the session shell to teardown the story shell with the given <code>story_id</code>.
This will be called before the story is stopped.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## **STRUCTS**

### Annotation {#Annotation}
*Defined in [fuchsia.modular/annotation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/annotation/annotation.fidl#10)*



<p>A user-defined annotation for a story or module.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code><a class='link' href='#AnnotationKey'>AnnotationKey</a></code>
            </td>
            <td><p>An identfier for this annotation.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#AnnotationValue'>AnnotationValue</a>?</code>
            </td>
            <td><p>The contents of this annotation.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### BaseShellParams {#BaseShellParams}
*Defined in [fuchsia.modular/base_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/basemgr/base_shell.fidl#43)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>presentation</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.policy/'>fuchsia.ui.policy</a>/<a class='link' href='../fuchsia.ui.policy/#Presentation'>Presentation</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### UserLoginParams {#UserLoginParams}
*Defined in [fuchsia.modular/user_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/basemgr/user_provider.fidl#48)*



<p>Used to specify arguments to log into a user session.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>account_id</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p><code>account_id</code> is received from either AddUser() or PreviousUsers(). It
can be NULL which means logging-in using incognito mode.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### UserLoginParams2 {#UserLoginParams2}
*Defined in [fuchsia.modular/user_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/basemgr/user_provider.fidl#55)*



<p>DEPRECATED, for backwards compatibility only</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>account_id</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p><code>account_id</code> is received from either AddUser() or PreviousUsers(). It
can be NULL which means logging-in in an incognito mode.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### AppConfig {#AppConfig}
*Defined in [fuchsia.modular/config.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/config/config.fidl#9)*



<p>Used to pass around configuration references to apps such as user
shell, base shell, story shell.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>url</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>args</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Intent {#Intent}
*Defined in [fuchsia.modular/intent.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/intent/intent.fidl#11)*



<p>The Intent struct is a runtime descriptor for an abstract action to be initiated
in Fuchsia. For details please see docs/intent.md.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>action</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>The name of the action represented by this Intent.</p>
<p>This is nullable for backwards compatibility.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>handler</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>An explicit handler for the Intent. Specified as the component URL of the
module.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>parameters</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#IntentParameter'>IntentParameter</a>&gt;?</code>
            </td>
            <td><p>The parameters that will be passed to the handler of <code>action</code>.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### IntentParameter {#IntentParameter}
*Defined in [fuchsia.modular/intent.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/intent/intent.fidl#28)*



<p>A struct representing a parameter that is passed to the handler of an Intent's
Action.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>The name of the parameter. The handler (i.e. selected mod) will be provided
with the data for this parameter under a link called <code>name</code>.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='#IntentParameterData'>IntentParameterData</a></code>
            </td>
            <td><p>The data that will be passed to the intent handler.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### LinkPath {#LinkPath}
*Defined in [fuchsia.modular/link_path.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/link_path.fidl#12)*



<p>Addresses a Link within a story. A LinkPath struct should be treated as an
opaque unique identifier of a link instance.  The <code>module_path</code> and
<code>link_name</code> components are leftovers from legacy code and have no external
meaning.
TODO(thatguy,lindkvist): Replace this structure with a vector&lt;&gt;. MI4-1021</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>module_path</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>link_name</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ModuleParameterMap {#ModuleParameterMap}
*Defined in [fuchsia.modular/module_data.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_data.fidl#66)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>entries</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ModuleParameterMapEntry'>ModuleParameterMapEntry</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ModuleParameterMapEntry {#ModuleParameterMapEntry}
*Defined in [fuchsia.modular/module_data.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_data.fidl#70)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>A null [name] is allowed for backwards compatibility with default links.
TODO(thatguy); When no modules use null link names any more, make this
required.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>link_path</code></td>
            <td>
                <code><a class='link' href='#LinkPath'>LinkPath</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ModuleManifest {#ModuleManifest}
*Defined in [fuchsia.modular/module_manifest.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_manifest.fidl#8)*



<p>Metadata that define the runtime properties of a Module.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>binary</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The relative path from the root of the package where the Module executable
file can be found.
TODO(MF-94): Extract a module's URL from its cmx manifest instead of
here.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>suggestion_headline</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>A human-readable string that can be used when suggesting this Module.
DEPRECATED.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>intent_filters</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#IntentFilter'>IntentFilter</a>&gt;?</code>
            </td>
            <td><p>A list of intents that this module is able to handle.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>composition_pattern</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>Identifies the pattern with which to compose this module with others.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>placeholder_color</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>Defines the color of the placeholder widget used while the module loads.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### IntentFilter {#IntentFilter}
*Defined in [fuchsia.modular/module_manifest.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_manifest.fidl#30)*



<p>This struct is used to describe an intent that a module is able to handle.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>action</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The action this module is able to handle.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>parameter_constraints</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ParameterConstraint'>ParameterConstraint</a>&gt;</code>
            </td>
            <td><p>Includes the name and types of entities for the parameters required to
execute specified [action].</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>action_display</code></td>
            <td>
                <code><a class='link' href='#ActionDisplay'>ActionDisplay</a></code>
            </td>
            <td><p>Defines presentation properties for suggestions of this action.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### ParameterConstraint {#ParameterConstraint}
*Defined in [fuchsia.modular/module_manifest.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_manifest.fidl#42)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The entity type that is valid for this parameter.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### FindModulesQuery {#FindModulesQuery}
*Defined in [fuchsia.modular/module_resolver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module_resolver/module_resolver.fidl#30)*



<p>Mirrors the information present in a Intent. Where a Intent is meant to
interface between Modules and the Framework, this structure is specific to
the interface between the Framework and the ModuleResolver.</p>
<p>In that role, it has references to structures and concepts that are only
visible within the abstraction layer of the Framework.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>handler</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>The handler is a module URL; if the handler is specified, the search for
(action, parameter_constraints) is scoped within the specified handler.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>action</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>parameter_constraints</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#FindModulesParameterConstraint'>FindModulesParameterConstraint</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FindModulesParameterConstraint {#FindModulesParameterConstraint}
*Defined in [fuchsia.modular/module_resolver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module_resolver/module_resolver.fidl#38)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>param_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>param_types</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FindModulesResponse {#FindModulesResponse}
*Defined in [fuchsia.modular/module_resolver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module_resolver/module_resolver.fidl#51)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#FindModulesStatus'>FindModulesStatus</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>results</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#FindModulesResult'>FindModulesResult</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FindModulesResult {#FindModulesResult}
*Defined in [fuchsia.modular/module_resolver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module_resolver/module_resolver.fidl#56)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>module_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The ID of the Module. For now, this is the URL of the Module binary.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>manifest</code></td>
            <td>
                <code><a class='link' href='#ModuleManifest'>ModuleManifest</a>?</code>
            </td>
            <td><p>The Module's manifest file (see docs/manifests/module.md).</p>
</td>
            <td>No default</td>
        </tr>
</table>

### FocusInfo {#FocusInfo}
*Defined in [fuchsia.modular/focus.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/session/focus.fidl#62)*



<p>Specifies the focused story of a device.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>device_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The id of the device.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>focused_story_id</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>The id of the focused story.  If null, no stories are focused.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>last_focus_change_timestamp</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The time the focused story on the device <code>device_id</code> was last
changed. 0 if no focus has ever been set for device <code>device_id</code>.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### ViewIdentifier {#ViewIdentifier}
*Defined in [fuchsia.modular/session_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/session/session_shell.fidl#49)*



<p>Identifies a view provided to a session shell. The values of the <code>story_id</code>
field match those used in the <code>StoryProvider</code> interface, allowing
identification of the same story across interfaces.</p>
<p>This is a struct rather than a naked string to allow for future evolution of
the identifier without changing the <code>SessionShell</code> API itself.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>story_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### CreateLinkInfo {#CreateLinkInfo}
*Defined in [fuchsia.modular/create_link.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/create_link.fidl#10)*



<p>Defines the attributes for a Link when the Link is created.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>initial_data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td><p>Passed as root_json argument to StoryProvider.CreateStoryWithInfo()
Link.Set() to set the value in the root link of the new Story's primary
module.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>allowed_types</code></td>
            <td>
                <code><a class='link' href='#LinkAllowedTypes'>LinkAllowedTypes</a>?</code>
            </td>
            <td><p>If <code>allowed_types</code> is null, the Link contains JSON. No schema validation
is performed.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### LinkAllowedTypes {#LinkAllowedTypes}
*Defined in [fuchsia.modular/create_link.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/create_link.fidl#21)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>allowed_entity_types</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td><p>The Link must contain an Entity (see Link.SetEntity()) that has at least
one of <code>allowed_entity_types</code> in its <code>Entity.GetTypes()</code> return value.</p>
<p>If empty, allows any Entity type.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### CreateModuleParameterMapInfo {#CreateModuleParameterMapInfo}
*Defined in [fuchsia.modular/create_module_parameter_map.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/create_module_parameter_map.fidl#8)*



<p>Module parameters are named pointers to link instances.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>property_info</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#CreateModuleParameterMapEntry'>CreateModuleParameterMapEntry</a>&gt;?</code>
            </td>
            <td><p>Contains instructions to create each name in the parameter map.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### CreateModuleParameterMapEntry {#CreateModuleParameterMapEntry}
*Defined in [fuchsia.modular/create_module_parameter_map.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/create_module_parameter_map.fidl#13)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#CreateModuleParameterInfo'>CreateModuleParameterInfo</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StoryPuppetMaster_SetStoryInfoExtra_Response {#StoryPuppetMaster_SetStoryInfoExtra_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### StoryPuppetMaster_Annotate_Response {#StoryPuppetMaster_Annotate_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### StoryPuppetMaster_AnnotateModule_Response {#StoryPuppetMaster_AnnotateModule_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### ExecuteResult {#ExecuteResult}
*Defined in [fuchsia.modular/puppet_master.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/puppet_master.fidl#37)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#ExecuteStatus'>ExecuteStatus</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>story_id</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>error_message</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetFocusState {#SetFocusState}
*Defined in [fuchsia.modular/story_command.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_command.fidl#39)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>focused</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AddMod {#AddMod}
*Defined in [fuchsia.modular/story_command.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_command.fidl#45)*



<p>Adds a mod described by <code>intent</code> to the story with name <code>mod_name</code>. If
<code>mod_name</code> already exists in the story, the mod is updated.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>mod_name</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td><p>The name of the mod within the story. The mod's name acts as the unique
ID of the mod, scoped to the story in which it is contained. Since
AddMod is reused for observation and mod names are vector<string>
inside the framework, they are vector<string> here as well.</p>
<p>Clients should treat the full vector as a single opaque value.</p>
<p>Clients should provide <code>mod_name_transitional</code> instead.
If both are provided, <code>mod_name</code> is ignored.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>mod_name_transitional</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>The name of the mod within the story. This should be used instead of
<code>mod_name</code>. If provided, it is equivalent to passing <code>mod_name</code> with
a single item. If both are provided, <code>mod_name</code> is ignored.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>intent</code></td>
            <td>
                <code><a class='link' href='#Intent'>Intent</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>surface_relation</code></td>
            <td>
                <code><a class='link' href='#SurfaceRelation'>SurfaceRelation</a></code>
            </td>
            <td><p><code>surface_relation</code> defines the visual relationship between this mod and the
mod at <code>surface_parent_mod_name</code>.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>surface_parent_mod_name</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### RemoveMod {#RemoveMod}
*Defined in [fuchsia.modular/story_command.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_command.fidl#75)*



<p>Removes the mod under <code>mod_name</code> from the story.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>mod_name</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td><p>The name of the mod within the story.</p>
<p>Clients should provide <code>mod_name_transitional</code> instead.
If both are provided, <code>mod_name</code> is ignored.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>mod_name_transitional</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>The name of the mod within the story. This should be used instead of
<code>mod_name</code>. If provided, it is equivalent to passing <code>mod_name</code> with
a single item. If both are provided, <code>mod_name</code> is ignored.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### SetLinkValue {#SetLinkValue}
*Defined in [fuchsia.modular/story_command.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_command.fidl#93)*



<p>Sets the value of link at <code>path</code> to <code>value</code>.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>path</code></td>
            <td>
                <code><a class='link' href='#LinkPath'>LinkPath</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FocusMod {#FocusMod}
*Defined in [fuchsia.modular/story_command.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_command.fidl#99)*



<p>Instructs the session shell to focus the mod under <code>mod_name</code>.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>mod_name</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td><p>The name of the mod within the story.</p>
<p>Clients should provide <code>mod_name_transitional</code> instead.
If both are provided, <code>mod_name</code> is ignored.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>mod_name_transitional</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>The name of the mod within the story. This should be used instead of
<code>mod_name</code>. If provided, it is equivalent to passing <code>mod_name</code> with
a single item. If both are provided, <code>mod_name</code> is ignored.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### SetKindOfProtoStoryOption {#SetKindOfProtoStoryOption}
*Defined in [fuchsia.modular/story_command.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_command.fidl#117)*



<p>Updates the kind_of_proto_story option in a story.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StoryController_Annotate_Response {#StoryController_Annotate_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### StoryInfo {#StoryInfo}
*Defined in [fuchsia.modular/story_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_info.fidl#8)*



<p>Information about a story as provided to the SessionShell.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>url</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>URL of the first module run in this story. This module is free to
run more modules in the story. Used for display purposes only.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The ID of the Story, used to reference it in method arguments.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>last_focus_time</code></td>
            <td>
                <code>int64</code>
            </td>
            <td><p>Wallclock time when the story was last focused. From
<code>ZX_CLOCK_UTC</code>, thus nanoseconds since UNIX epoch (1970-01-01 00:00 UTC).</p>
<p>A value of zero means the story has never been focused.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>extra</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#StoryInfoExtraEntry'>StoryInfoExtraEntry</a>&gt;?</code>
            </td>
            <td><p>Data the SessionShell wants to keep associated with this Story, like
title, a color, or a display rank.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### StoryInfoExtraEntry {#StoryInfoExtraEntry}
*Defined in [fuchsia.modular/story_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_info.fidl#47)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StoryOptions {#StoryOptions}
*Defined in [fuchsia.modular/story_options.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_options.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>kind_of_proto_story</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Whether or not the story will be hidden on a call to
StoryProvider#GetStories.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### ViewConnection {#ViewConnection}
*Defined in [fuchsia.modular/story_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell.fidl#76)*



<p>A pair mapping a surface ID to a view (via <code>view_holder_token</code>).</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>surface_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The ID for the surface</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>view_holder_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/#ViewHolderToken'>ViewHolderToken</a></code>
            </td>
            <td><p>Token for embedding the new view corresponding to the surface.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### ViewConnection2 {#ViewConnection2}
*Defined in [fuchsia.modular/story_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell.fidl#85)*



<p>DEPRECATED, for transition purposes only.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>surface_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The ID for the surface</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>view_holder_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/#ViewHolderToken'>ViewHolderToken</a></code>
            </td>
            <td><p>Token for embedding the new view corresponding to the surface.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### SurfaceInfo {#SurfaceInfo}
*Defined in [fuchsia.modular/story_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell.fidl#94)*



<p>Contains metadata for a Surface.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>parent_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>ID of the view that is parent of this Surface.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>surface_relation</code></td>
            <td>
                <code><a class='link' href='#SurfaceRelation'>SurfaceRelation</a>?</code>
            </td>
            <td><p>The relationship between the parent Surface and this new Surface. Used
for layout optimization.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>module_manifest</code></td>
            <td>
                <code><a class='link' href='#ModuleManifest'>ModuleManifest</a>?</code>
            </td>
            <td><p>Information about the module populates the view.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>module_source</code></td>
            <td>
                <code><a class='link' href='#ModuleSource'>ModuleSource</a></code>
            </td>
            <td><p>How the Surface was generated. By an action internal to the story or by
an external action.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### SurfaceRelation {#SurfaceRelation}
*Defined in [fuchsia.modular/surface.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/surface/surface.fidl#11)*



<p>Describes the relationship between two Surfaces.
Provides information to the StoryShell for layout optimization.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>arrangement</code></td>
            <td>
                <code><a class='link' href='#SurfaceArrangement'>SurfaceArrangement</a></code>
            </td>
            <td><p>Advice on arranging these surfaces on the screen together.</p>
</td>
            <td><a class='link' href='#SurfaceArrangement.NONE'>SurfaceArrangement.NONE</a></td>
        </tr><tr>
            <td><code>dependency</code></td>
            <td>
                <code><a class='link' href='#SurfaceDependency'>SurfaceDependency</a></code>
            </td>
            <td><p>Advice for dismissal of surfaces to be linked.</p>
</td>
            <td><a class='link' href='#SurfaceDependency.NONE'>SurfaceDependency.NONE</a></td>
        </tr><tr>
            <td><code>emphasis</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>Relative emphasis of the child surface, relative to the parent.
Influences relative areas of surfaces on screen.</p>
</td>
            <td>1</td>
        </tr>
</table>



## **ENUMS**

### AnnotationError {#AnnotationError}
Type: <code>uint32</code>

*Defined in [fuchsia.modular/annotation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/annotation/annotation.fidl#59)*

<p>Error returned from calls to Annotate().</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>VALUE_TOO_BIG</code></td>
            <td><code>1</code></td>
            <td><p>The <code>AnnotationValue.buffer</code> size exceeds the maximum length,
<code>MAX_ANNOTATION_VALUE_BUFFER_LENGTH_BYTES</code>.</p>
</td>
        </tr><tr>
            <td><code>TOO_MANY_ANNOTATIONS</code></td>
            <td><code>2</code></td>
            <td><p>The total number of annotations on the story or module being annotated
exceeds <code>MAX_ANNOTATIONS_PER_STORY</code> or <code>MAX_ANNOTATIONS_PER_MODULE</code>.</p>
</td>
        </tr><tr>
            <td><code>NOT_FOUND</code></td>
            <td><code>3</code></td>
            <td><p>The resource to be annotated was not found and could not be resolved
by, for example, waiting, or creating the missing resource automatically.
This error may be returned by StoryPuppetMaster.AnnotateModule(), which
can wait for a missing Module, but requires the Module's Story exist.</p>
</td>
        </tr></table>

### EntityWriteStatus {#EntityWriteStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.modular/entity.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/entity/entity.fidl#46)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OK</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERROR</code></td>
            <td><code>1</code></td>
            <td><p>Indicates a failure of the entity provider to write the update.</p>
</td>
        </tr><tr>
            <td><code>READ_ONLY</code></td>
            <td><code>2</code></td>
            <td><p>Entity providers are not necessarily required to support entity mutation.</p>
</td>
        </tr></table>

### StartModuleStatus {#StartModuleStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.modular/module_context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_context.fidl#62)*

<p>Communicates the status of an Intent to a Module.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SUCCESS</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>NO_MODULES_FOUND</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### OngoingActivityType {#OngoingActivityType}
Type: <code>uint32</code>

*Defined in [fuchsia.modular/module_context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_context.fidl#73)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNSPECIFIED</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>VIDEO</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>AUDIO</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### ModuleSource {#ModuleSource}
Type: <code>uint32</code>

*Defined in [fuchsia.modular/module_data.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_data.fidl#55)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INTERNAL</code></td>
            <td><code>0</code></td>
            <td><p>Module that was added to the story from within the story by another
module using ModuleContext.AddModuleToStory() or
ModuleContext.EmbedModule().</p>
</td>
        </tr><tr>
            <td><code>EXTERNAL</code></td>
            <td><code>1</code></td>
            <td><p>Module that was added to the story from outside the story using
PuppetMaster.</p>
</td>
        </tr></table>

### ModuleState {#ModuleState}
Type: <code>uint32</code>

*Defined in [fuchsia.modular/module_state.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_state.fidl#21)*

<p>State used to notify about state transitions of a Module
instance. This is very similar to the StoryState, however it's not entirely
the same and hence a separate type. A module cannot have an INITIAL state,
because it's started as soon as it is created, and it gets deleted as soon as
it reaches the STOPPED state, whileas a story can be restarted.</p>
<p>Currently possible state transitions (and the events that cause
them) are:</p>
<pre><code>        -&gt; RUNNING     ModuleContext.AddModuleToStory() or
                       ModuleContext.EmbedModule() or
                       StoryController.AddModule()
</code></pre>
<p>RUNNING  -&gt; STOPPED     ModuleController.Stop() or StoryController.Stop()
RUNNING  -&gt; ERROR       application exits</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>RUNNING</code></td>
            <td><code>2</code></td>
            <td><p>Module instance was created.</p>
</td>
        </tr><tr>
            <td><code>STOPPED</code></td>
            <td><code>4</code></td>
            <td><p>Module instance is stopped after Module.Stop(). No further transitions are
to be expected.</p>
</td>
        </tr><tr>
            <td><code>ERROR</code></td>
            <td><code>5</code></td>
            <td><p>Connection to the Module instance was closed without Stop() request. No
further transitions are to be expected.</p>
</td>
        </tr></table>

### FindModulesStatus {#FindModulesStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.modular/module_resolver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module_resolver/module_resolver.fidl#43)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SUCCESS</code></td>
            <td><code>0</code></td>
            <td><p>A search was successfully conducted.</p>
</td>
        </tr><tr>
            <td><code>UNKNOWN_HANDLER</code></td>
            <td><code>1</code></td>
            <td><p><code>FindModulesQuery.handler</code> was specified but the resolver doesn't know
about it.</p>
</td>
        </tr></table>

### ExecuteStatus {#ExecuteStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.modular/puppet_master.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/puppet_master.fidl#7)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OK</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVALID_COMMAND</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVALID_STORY_ID</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>STORY_MUST_HAVE_MODS</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVALID_MOD</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>NO_MODULES_FOUND</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>INTERNAL_ERROR</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr></table>

### ConfigureStoryError {#ConfigureStoryError}
Type: <code>int32</code>

*Defined in [fuchsia.modular/puppet_master.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/puppet_master.fidl#32)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ERR_STORY_ALREADY_CREATED</code></td>
            <td><code>1</code></td>
            <td><p>The story cannot be (re)configured because it was already created.</p>
</td>
        </tr></table>

### StoryVisualState {#StoryVisualState}
Type: <code>uint32</code>

*Defined in [fuchsia.modular/story_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell.fidl#155)*

<p>Defines the visual state of the Story shell.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>MINIMIZED</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>MAXIMIZED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>MAXIMIZED_OVERLAYED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### StoryState {#StoryState}
Type: <code>uint32</code>

*Defined in [fuchsia.modular/story_state.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_state.fidl#16)*

<p>State of a Story. A story is either running, stopping, or stopped, separately
on every device of the user. If it's running, it can also be focused, but
that's tracked in a separate service, cf. FocusProvider in focus.fidl.</p>
<p>Possible state transitions are:</p>
<p>STOPPED  -&gt; RUNNING
RUNNING  -&gt; STOPPING
STOPPING -&gt; STOPPED</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>RUNNING</code></td>
            <td><code>1</code></td>
            <td><p>Story was started using StoryController.Start().</p>
</td>
        </tr><tr>
            <td><code>STOPPING</code></td>
            <td><code>2</code></td>
            <td><p>Story is in the middle of stopping after StoryController.Stop() was
called.</p>
</td>
        </tr><tr>
            <td><code>STOPPED</code></td>
            <td><code>3</code></td>
            <td><p>Story was not yet run, or Story was stopped after StoryController.Stop()
was called.</p>
</td>
        </tr></table>

### StoryVisibilityState {#StoryVisibilityState}
Type: <code>uint32</code>

*Defined in [fuchsia.modular/story_visibility_state.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_visibility_state.fidl#17)*

<p>Visibility state of a Story within the session shell.
This state describes how a story should be displayed within the session shell,
regardless of whether the story is in focus or not. Focus state and
visibility state are orthogonal concepts.
E.g A story can be out-of-focus and be in IMMERSIVE state at the same time
if a user was playing a video, exits, then re-enters the story. The
expectation in this scenario is that the story is in IMMERSIVE state upon
re-enter.</p>
<p>All state transitions are possible.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DEFAULT</code></td>
            <td><code>1</code></td>
            <td><p>Default state for a story.</p>
</td>
        </tr><tr>
            <td><code>IMMERSIVE</code></td>
            <td><code>2</code></td>
            <td><p>Full-screen user experience, e.g. playing a video.</p>
</td>
        </tr></table>

### SurfaceArrangement {#SurfaceArrangement}
Type: <code>uint32</code>

*Defined in [fuchsia.modular/surface.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/surface/surface.fidl#24)*

<p>Expresses arrangement type.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NONE</code></td>
            <td><code>0</code></td>
            <td><p>No arrangement specified.</p>
</td>
        </tr><tr>
            <td><code>COPRESENT</code></td>
            <td><code>1</code></td>
            <td><p>Desire to present simultaneously.</p>
</td>
        </tr><tr>
            <td><code>SEQUENTIAL</code></td>
            <td><code>2</code></td>
            <td><p>The parent prefers to not be presented simultaneously with its child.
(The child may still become part of a simultaneous presentation depending
on the relationships between it and subsequently added surfaces).</p>
</td>
        </tr><tr>
            <td><code>ONTOP</code></td>
            <td><code>3</code></td>
            <td><p>Place this surface on top of and obscuring the parent surface. This is a
complete replacement, not a modal or inset presentation.</p>
</td>
        </tr></table>

### SurfaceDependency {#SurfaceDependency}
Type: <code>uint32</code>

*Defined in [fuchsia.modular/surface.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/surface/surface.fidl#42)*

<p>Links surface dismissal.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NONE</code></td>
            <td><code>0</code></td>
            <td><p>No dependency specified.</p>
</td>
        </tr><tr>
            <td><code>DEPENDENT</code></td>
            <td><code>1</code></td>
            <td><p>Child is dependent on parent.
If parent is dismissed, child is dismissed as well.</p>
</td>
        </tr></table>



## **TABLES**

### AgentServiceRequest {#AgentServiceRequest}


*Defined in [fuchsia.modular/component_context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/component/component_context.fidl#40)*

<p>Used by ComponentContext.ConnectToAgentService</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>service_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The name of the requested service.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>channel</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
            <td><p>The channel that will be used to communicate with the requested service.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>handler</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sys/'>fuchsia.sys</a>/<a class='link' href='../fuchsia.sys/#component_url'>component_url</a></code>
            </td>
            <td><p>The component URL of the Agent that is to provide the specified service.
If no handler is specified, the framework will perform resolution to
find an appropriate handler.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>agent_controller</code></td>
            <td>
                <code>request&lt;<a class='link' href='#AgentController'>AgentController</a>&gt;</code>
            </td>
            <td><p>The AgentController that keeps the agent alive.</p>
</td>
        </tr></table>

### ModuleData {#ModuleData}


*Defined in [fuchsia.modular/module_data.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_data.fidl#8)*

<p>Information about a Module instance in a story.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>module_url</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The URL of the Module binary.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>module_path</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td><p>The named path leading up to this Module instance. The last name in this
array is the name by which the Module was started by the parent Module
instance calling StartModule().</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>parameter_map</code></td>
            <td>
                <code><a class='link' href='#ModuleParameterMap'>ModuleParameterMap</a></code>
            </td>
            <td><p>Contains the mapping of Mod parameter name to Link instances for this mod.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>module_source</code></td>
            <td>
                <code><a class='link' href='#ModuleSource'>ModuleSource</a></code>
            </td>
            <td><p>The way in which this Module instance was first started in the story,
either by request from another Module instance (INTERNAL) or by request
from outside the story (i.e. by suggestion from an agent - EXTERNAL).</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>surface_relation</code></td>
            <td>
                <code><a class='link' href='#SurfaceRelation'>SurfaceRelation</a></code>
            </td>
            <td><p>The <code>surface_relation</code> that was used to start this Module instance with.
The same is used when re-inflating the Module instance when the story is
resumed. A SurfaceRelation value of null represents an embedded Module
instance (started by EmbedModule()) that is not managed by the story shell.</p>
</td>
        </tr><tr>
            <td>6</td>
            <td><code>module_deleted</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>True if this module was removed from its story either through
ModuleController.Stop() or ModuleContext.RemoveSelfFromStory().</p>
</td>
        </tr><tr>
            <td>7</td>
            <td><code>intent</code></td>
            <td>
                <code><a class='link' href='#Intent'>Intent</a></code>
            </td>
            <td><p>The intent that was issued to start add this Module instance to the story.
Some Module instances may have been added not by an Intent, for example as
the initial module of a story. For those the field may be null.</p>
<p>TODO(thatguy,mesch): This field should now always be set, so make it
required once the framework is cleaned up enough to guarantee this
statement.</p>
</td>
        </tr><tr>
            <td>8</td>
            <td><code>is_embedded</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>If true, this module was started by a parent module using
ModuleContext.EmbedModule(), and its view is not managed by the
StoryShell.</p>
</td>
        </tr><tr>
            <td>9</td>
            <td><code>annotations</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Annotation'>Annotation</a>&gt;[100]</code>
            </td>
            <td><p>Collection of user-defined key-value attributes that describe this surface (module).</p>
<p>The <code>Annotation.value</code> field of each <code>Annotation</code> is always set.</p>
</td>
        </tr></table>

### ActionDisplay {#ActionDisplay}


*Defined in [fuchsia.modular/module_manifest.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_manifest.fidl#49)*

<p>Defines how a suggestion of an action will be presented.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>display_info</code></td>
            <td>
                <code><a class='link' href='#DisplayInfo'>DisplayInfo</a></code>
            </td>
            <td><p>Defines presentation fields for a suggestion. The string fields might be
templated and will be filled from data in <code>parameter_mapping</code>.
For example: &quot;Listen to $artistName&quot;</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>parameter_mapping</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ParameterMapping'>ParameterMapping</a>&gt;</code>
            </td>
            <td><p>Fields to be replaced in the given <code>display_info</code> templated strings.
In the example above, we would map name=artistName to the intent field
artist.name where artist is the intent parameter name and name a field
of it.</p>
</td>
        </tr></table>

### DisplayInfo {#DisplayInfo}


*Defined in [fuchsia.modular/module_manifest.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_manifest.fidl#63)*

<p>Presentation information about the suggestion.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>title</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The title of the suggestion.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>subtitle</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>A subtitle for the suggestion.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>icon</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>A url from which to fetch the icon of the suggestion.</p>
</td>
        </tr></table>

### ParameterMapping {#ParameterMapping}


*Defined in [fuchsia.modular/module_manifest.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_manifest.fidl#75)*

<p>Defines pairs that will be replaced in the DisplayInfo.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The name of the variable to be replaced in the template.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>parameter_property</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The path in the intent parameter to get that name.
<code>PARAMETER_PROPERTY</code> = string | string . <code>PARAMETER_PROPERTY</code>
The first string in the dot-separated string is the name of the intent
parameter and the following are nested subfields.</p>
</td>
        </tr></table>

### StoryInfo2 {#StoryInfo2}


*Defined in [fuchsia.modular/story_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_info.fidl#30)*

<p>Information about a story as provided to the SessionShell.
For transition purposes only.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>id</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The ID of the Story, used to reference it in method arguments.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>last_focus_time</code></td>
            <td>
                <code>int64</code>
            </td>
            <td><p>Wallclock time when the story was last focused. From
ZX_CLOCK_UTC, thus nanoseconds since UNIX epoch (1970-01-01 00:00 UTC).</p>
<p>A value of zero means the story has never been focused.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>annotations</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Annotation'>Annotation</a>&gt;[100]</code>
            </td>
            <td><p>Collection of user-defined key-value attributes that describe
this story.</p>
<p>The <code>Annotation.value</code> field of each <code>Annotation</code> is always set.</p>
</td>
        </tr></table>

### SurfaceInfo2 {#SurfaceInfo2}


*Defined in [fuchsia.modular/story_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell.fidl#111)*

<p>Contains metadata for a Surface.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>parent_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>ID of the view that is parent of this Surface.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>surface_relation</code></td>
            <td>
                <code><a class='link' href='#SurfaceRelation'>SurfaceRelation</a></code>
            </td>
            <td><p>The relationship between the parent Surface and this new Surface. Used
for layout optimization.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>module_manifest</code></td>
            <td>
                <code><a class='link' href='#ModuleManifest'>ModuleManifest</a></code>
            </td>
            <td><p>Information about the module populates the view.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>module_source</code></td>
            <td>
                <code><a class='link' href='#ModuleSource'>ModuleSource</a></code>
            </td>
            <td><p>How the Surface was generated. By an action internal to the story or by
an external action.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>annotations</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Annotation'>Annotation</a>&gt;[100]</code>
            </td>
            <td><p>Collection of user-defined key-value attributes that describe this surface (module).</p>
<p>The <code>Annotation.value</code> field of each <code>Annotation</code> is always set.</p>
</td>
        </tr></table>



## **UNIONS**

### IntentParameterData {#IntentParameterData}
*Defined in [fuchsia.modular/intent.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/intent/intent.fidl#37)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>entity_reference</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>Set this if you already have an Entity reference at runtime.
Entity.getTypes() will be used to set the constraints for this noun during
resolution.</p>
</td>
        </tr><tr>
            <td><code>json</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td><p>Set this if you have structured JSON data. Values typically are a JSON
object with a &quot;@type&quot; attribute and other associated data.  TODO(thatguy):
We need to decide if we want to keep this in place, or deprecate this
eventually and move entirely to using Entity references.</p>
<p>DEPRECATED: Use <code>entity_reference</code>.</p>
</td>
        </tr><tr>
            <td><code>entity_type</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td><p>Set this if you want to explicitly define this noun's allowed types. This
is also useful in the cases where the noun has a 'direction' of type
'output', and you wish to set the allowable output types from the Module
(see docs/modular/manifests/action_template.md for a definition of
'direction').</p>
<p>Only one entry in <code>entity_type</code> must match the constraint specified by
the Module for the constraint to be considered satisfied.</p>
</td>
        </tr></table>

### CreateModuleParameterInfo {#CreateModuleParameterInfo}
*Defined in [fuchsia.modular/create_module_parameter_map.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/create_module_parameter_map.fidl#18)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>link_path</code></td>
            <td>
                <code><a class='link' href='#LinkPath'>LinkPath</a></code>
            </td>
            <td><p>Instructs parameter map initialization to either use an existing Link
(<code>link_path</code> is set) or create a new Link (<code>create_link</code> is set).</p>
</td>
        </tr><tr>
            <td><code>create_link</code></td>
            <td>
                <code><a class='link' href='#CreateLinkInfo'>CreateLinkInfo</a></code>
            </td>
            <td></td>
        </tr></table>

### StoryPuppetMaster_SetStoryInfoExtra_Result {#StoryPuppetMaster_SetStoryInfoExtra_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#StoryPuppetMaster_SetStoryInfoExtra_Response'>StoryPuppetMaster_SetStoryInfoExtra_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ConfigureStoryError'>ConfigureStoryError</a></code>
            </td>
            <td></td>
        </tr></table>

### StoryPuppetMaster_Annotate_Result {#StoryPuppetMaster_Annotate_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#StoryPuppetMaster_Annotate_Response'>StoryPuppetMaster_Annotate_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#AnnotationError'>AnnotationError</a></code>
            </td>
            <td></td>
        </tr></table>

### StoryPuppetMaster_AnnotateModule_Result {#StoryPuppetMaster_AnnotateModule_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#StoryPuppetMaster_AnnotateModule_Response'>StoryPuppetMaster_AnnotateModule_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#AnnotationError'>AnnotationError</a></code>
            </td>
            <td></td>
        </tr></table>

### StoryCommand {#StoryCommand}
*Defined in [fuchsia.modular/story_command.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_command.fidl#17)*

<p>StoryCommands are POD structures that describe the set of operations that
can be performed on a story by components outside the modular framework. All commands are:</p>
<p>(1) Scoped to a single story
(2) Idempotent: issuing the same command twice yields the same result
(3) Symmetrical with observation: the same structures are used to describe
operations to watchers of a story (through SessionWatcher) as are used
to control a story.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>set_focus_state</code></td>
            <td>
                <code><a class='link' href='#SetFocusState'>SetFocusState</a></code>
            </td>
            <td><p>Sets the focus state of the story to <code>set_focus_state.focused</code>.</p>
</td>
        </tr><tr>
            <td><code>add_mod</code></td>
            <td>
                <code><a class='link' href='#AddMod'>AddMod</a></code>
            </td>
            <td><p>Adds a Mod.</p>
</td>
        </tr><tr>
            <td><code>remove_mod</code></td>
            <td>
                <code><a class='link' href='#RemoveMod'>RemoveMod</a></code>
            </td>
            <td><p>Removes an existing Mod.</p>
</td>
        </tr><tr>
            <td><code>set_link_value</code></td>
            <td>
                <code><a class='link' href='#SetLinkValue'>SetLinkValue</a></code>
            </td>
            <td><p>Sets the value of a Link.
DEPRECATED. This command is a no-op.</p>
</td>
        </tr><tr>
            <td><code>focus_mod</code></td>
            <td>
                <code><a class='link' href='#FocusMod'>FocusMod</a></code>
            </td>
            <td><p>Brings focus to a mod.</p>
</td>
        </tr><tr>
            <td><code>set_kind_of_proto_story_option</code></td>
            <td>
                <code><a class='link' href='#SetKindOfProtoStoryOption'>SetKindOfProtoStoryOption</a></code>
            </td>
            <td><p>Updates the kind_of_proto_story option in a story.
DEPRECATED. This command is a no-op.</p>
</td>
        </tr></table>

### StoryController_Annotate_Result {#StoryController_Annotate_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#StoryController_Annotate_Response'>StoryController_Annotate_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#AnnotationError'>AnnotationError</a></code>
            </td>
            <td></td>
        </tr></table>



## **XUNIONS**

### AnnotationValue {#AnnotationValue}
*Defined in [fuchsia.modular/annotation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/annotation/annotation.fidl#52)*

<p>The value of a <a class='link' href='#Annotation'>Annotation</a>.</p>
<p>The actual field used depends on the type of annotation, which is
user-defined, and not enforced by the framework.</p>
<p>The size of <code>buffer</code> is limited to
<code>MAX_ANNOTATION_VALUE_BUFFER_LENGTH_BYTES</code> bytes.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>text</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>bytes</code></td>
            <td>
                <code>vector&lt;uint8&gt;[1024]</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td></td>
        </tr></table>





## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="MAX_ANNOTATIONS_PER_STORY">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/annotation/annotation.fidl#19">MAX_ANNOTATIONS_PER_STORY</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Maximum number of annotations on a single story.</p>
</td>
        </tr>
    <tr id="MAX_ANNOTATIONS_PER_MODULE">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/annotation/annotation.fidl#22">MAX_ANNOTATIONS_PER_MODULE</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Maximum number of annotations on a single module.</p>
</td>
        </tr>
    <tr id="MAX_ANNOTATIONS_PER_UPDATE">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/annotation/annotation.fidl#27">MAX_ANNOTATIONS_PER_UPDATE</a></td>
            <td>
                    <code>50</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Maximum number of annotations that can be passed to either method
Annotate() AnnotateModule() in fuchsia.modular protocols that support
annotations.</p>
</td>
        </tr>
    <tr id="MAX_ANNOTATION_KEY_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/annotation/annotation.fidl#30">MAX_ANNOTATION_KEY_LENGTH</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Maximum length of <a class='link' href='#AnnotationKey'>AnnotationKey</a>.</p>
</td>
        </tr>
    <tr id="MAX_ANNOTATION_VALUE_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/annotation/annotation.fidl#34">MAX_ANNOTATION_VALUE_LENGTH</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Maximum length of <a class='link' href='#AnnotationValue'>AnnotationValue</a> fields:
<code>text</code> and <code>bytes</code>.</p>
</td>
        </tr>
    <tr id="MAX_ANNOTATION_VALUE_BUFFER_LENGTH_BYTES">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/annotation/annotation.fidl#40">MAX_ANNOTATION_VALUE_BUFFER_LENGTH_BYTES</a></td>
            <td>
                    <code>102400</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Maximum length of the <a class='link' href='#AnnotationValue.buffer'>AnnotationValue.buffer</a> field, in
bytes.</p>
<p>Does not apply to other fields; see <a class='link' href='#MAX_ANNOTATION_VALUE_LENGTH'>MAX_ANNOTATION_VALUE_LENGTH</a>.</p>
</td>
        </tr>
    
</table>



## **TYPE ALIASES**

<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr id="AnnotationKey">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/annotation/annotation.fidl#43">AnnotationKey</a></td>
            <td>
                <code>string</code>[<code><a class='link' href='#MAX_ANNOTATION_KEY_LENGTH'>MAX_ANNOTATION_KEY_LENGTH</a></code>]</td>
            <td><p>An identifier for an <a class='link' href='#Annotation'>Annotation</a>.</p>
</td>
        </tr></table>

