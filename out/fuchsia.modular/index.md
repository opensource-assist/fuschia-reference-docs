Project: /_project.yaml
Book: /_book.yaml

# fuchsia.modular


## **PROTOCOLS**

## Agent {:#Agent}
*Defined in [fuchsia.modular/agent.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/agent/agent.fidl#38)*

 An agent is a component whose lifecycle is not tied to any Story.

 - An agent is a singleton instance.
 - Components can connect to an Agent using the
   fuchsia.modular.ComponentContext capability.
 - An agent vends services to components that connect to it over a
   ServiceProvider.
 - An agent is started when someone wants to connect to it, or when a task it
   has scheduled has triggered.

 This FIDL interface should be implemented by a component that is meant to be
 run as an Agent.

 When an agent application implements the `Lifecycle` interface, it can
 receive a signal for when it should stop. An agent may be stopped for the
 following reasons:

 (1) All `AgentController` connections associated with this agent are closed.

 (2) The system wants to optimize for resources.

 Once the framework delivers a `Lifecycle.Terminate()`, the agent application
 may exit itself, or is killed by framework after a timeout.

 For more info see:
 - fuchsia.modular.AgentContext and fuchsia.modular.ComponentContext for
   capabilities an agent has.
 - fuchsia.modular.Lifecycle for how Components get lifecycle events.

### Connect {:#Connect}

 Called when some component tries to connect to this agent. `requestor_url`
 identifies the requesting client. Different client roles are identified differently:
    * For Module clients in the general case, `requestor_url` will be the name provided at
      Module create time (ie, in calls to StoryPuppetMaster's StoryCommand.AddMod/mod_name)
      with :'s escaped (see below for a complete explanation).
    * For all other clients (Agents and Shells), `requestor_url` is set to the requesting
      component's URL.

 `services` must be connected to an implementation of fuchsia.sys.ServiceProvider offering
 services specific to the requesting client.

 Details on module naming: modules are named hierarchically based on what client created
 them. This is called a module path. If created by 1) an agent or 2) an existing module, the
 path is constructed differently.

 In the case of (2), the module path is the concatenation of the existing module's path with
 the new module's name, as provided by the parent module. In the case of (1), the module
 path is the concatenation of StoryCommand.AddMod/mod_name and
 StoryCommand.AddMod/surface_relation_parent.

 The full path is encoded into `requestor_url` as escape_colons(module_path).join(':').

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
                <code>request&lt;<a class='link' href='../fuchsia.sys/index.html'>fuchsia.sys</a>/<a class='link' href='../fuchsia.sys/index.html#ServiceProvider'>ServiceProvider</a>&gt;</code>
            </td>
        </tr></table>



### RunTask {:#RunTask}

 Called when some task identified by `task_id` is scheduled to run. The task
 was first posted by this Agent using `AgentContext.ScheduleTask()`. The
 return callback is called by this Agent when all work related to this task
 is completed. Note that the framework may call `Lifecycle.Terminate()`
 before RunTask returns.

 TODO(alhaad): The current implementation allows the Agent to run a task
 until its callback returns. If the task takes a long time to finish, the
 framework has no way to signal a request for termination other than to shut
 down the entire Agent instance. Instead, we should cap task length with
 strategies like budgets. Also, the Task should likely have its own
 connection that allows for more signalling.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>task_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## AgentContext {:#AgentContext}
*Defined in [fuchsia.modular/agent_context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/agent/agent_context.fidl#14)*

 An instance of this service is exposed to agents in their namespace.
 `AgentContext` allows an agent to schedule tasks which run in response to
 triggers. Triggers are conditions such as a message arriving on a
 MessageQueue.

### GetComponentContext {:#GetComponentContext}

 DEPRECATED: ComponentContext is now available in the
 namespace/environment for Modules.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#ComponentContext'>ComponentContext</a>&gt;</code>
            </td>
        </tr></table>



### GetEntityReferenceFactory {:#GetEntityReferenceFactory}

 Connects to an EntityReferenceFactory for this Agent. Entity references
 obtained from this EntityReferenceFactory will be resolved back to this
 Agent.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#EntityReferenceFactory'>EntityReferenceFactory</a>&gt;</code>
            </td>
        </tr></table>



### ScheduleTask {:#ScheduleTask}

 Schedules a task described in `task_info`. When this task is scheduled to
 run, Agent.RunTask() is called.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>task_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#TaskInfo'>TaskInfo</a></code>
            </td>
        </tr></table>



### ScheduleTaskWithCompletion {:#ScheduleTaskWithCompletion}

 Schedules a task described in `task_info`. When this task is scheduled
 to run, Agent.RunTask() is called. Executes the callback on completion.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>task_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#TaskInfo'>TaskInfo</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>done</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

### DeleteTask {:#DeleteTask}

 No new runs of this task will be scheduled.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>task_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### GetTokenManager {:#GetTokenManager}

 The auth token manager this Agent may use for accessing external services.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.auth/index.html'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/index.html#TokenManager'>TokenManager</a>&gt;</code>
            </td>
        </tr></table>



## AgentController {:#AgentController}
*Defined in [fuchsia.modular/agent_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/agent/agent_controller/agent_controller.fidl#12)*


## BaseShell {:#BaseShell}
*Defined in [fuchsia.modular/base_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/basemgr/base_shell.fidl#21)*


### Initialize {:#Initialize}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>base_shell_context</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#BaseShellContext'>BaseShellContext</a></code>
            </td>
        </tr><tr>
            <td><code>base_shell_params</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#BaseShellParams'>BaseShellParams</a></code>
            </td>
        </tr></table>



### GetAuthenticationUIContext {:#GetAuthenticationUIContext}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.auth/index.html'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/index.html#AuthenticationUIContext'>AuthenticationUIContext</a>&gt;</code>
            </td>
        </tr></table>



## BaseShellContext {:#BaseShellContext}
*Defined in [fuchsia.modular/base_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/basemgr/base_shell.fidl#35)*


### GetUserProvider {:#GetUserProvider}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#UserProvider'>UserProvider</a>&gt;</code>
            </td>
        </tr></table>



### GetPresentation {:#GetPresentation}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>presentation</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.ui.policy/index.html'>fuchsia.ui.policy</a>/<a class='link' href='../fuchsia.ui.policy/index.html#Presentation'>Presentation</a>&gt;</code>
            </td>
        </tr></table>



### Shutdown {:#Shutdown}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## UserProvider {:#UserProvider}
*Defined in [fuchsia.modular/user_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/basemgr/user_provider.fidl#13)*


### AddUser {:#AddUser}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>identity_provider</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular.auth/index.html'>fuchsia.modular.auth</a>/<a class='link' href='../fuchsia.modular.auth/index.html#IdentityProvider'>IdentityProvider</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>account</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular.auth/index.html'>fuchsia.modular.auth</a>/<a class='link' href='../fuchsia.modular.auth/index.html#Account'>Account</a>?</code>
            </td>
        </tr><tr>
            <td><code>error_code</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr></table>

### RemoveUser {:#RemoveUser}


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

### Login {:#Login}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>user_login_params</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#UserLoginParams'>UserLoginParams</a></code>
            </td>
        </tr></table>



### Login2 {:#Login2}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>user_login_params</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#UserLoginParams2'>UserLoginParams2</a></code>
            </td>
        </tr></table>



### PreviousUsers {:#PreviousUsers}


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
                <code>vector&lt;<a class='link' href='../fuchsia.modular.auth/index.html'>fuchsia.modular.auth</a>/<a class='link' href='../fuchsia.modular.auth/index.html#Account'>Account</a>&gt;</code>
            </td>
        </tr></table>

## Clipboard {:#Clipboard}
*Defined in [fuchsia.modular/clipboard.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/clipboard/clipboard.fidl#10)*


### Push {:#Push}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>text</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### Peek {:#Peek}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>text</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr></table>

## ComponentContext {:#ComponentContext}
*Defined in [fuchsia.modular/component_context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/component/component_context.fidl#14)*


### GetLedger {:#GetLedger}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.ledger/index.html'>fuchsia.ledger</a>/<a class='link' href='../fuchsia.ledger/index.html#Ledger'>Ledger</a>&gt;</code>
            </td>
        </tr></table>



### ConnectToAgent {:#ConnectToAgent}


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
                <code>request&lt;<a class='link' href='../fuchsia.sys/index.html'>fuchsia.sys</a>/<a class='link' href='../fuchsia.sys/index.html#ServiceProvider'>ServiceProvider</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>controller</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#AgentController'>AgentController</a>&gt;</code>
            </td>
        </tr></table>



### ConnectToAgentService {:#ConnectToAgentService}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#AgentServiceRequest'>AgentServiceRequest</a></code>
            </td>
        </tr></table>



### ObtainMessageQueue {:#ObtainMessageQueue}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>queue</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#MessageQueue'>MessageQueue</a>&gt;</code>
            </td>
        </tr></table>



### DeleteMessageQueue {:#DeleteMessageQueue}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### GetMessageSender {:#GetMessageSender}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue_token</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>sender</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#MessageSender'>MessageSender</a>&gt;</code>
            </td>
        </tr></table>



### GetEntityResolver {:#GetEntityResolver}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#EntityResolver'>EntityResolver</a>&gt;</code>
            </td>
        </tr></table>



### CreateEntityWithData {:#CreateEntityWithData}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>type_to_data</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#TypeToDataEntry'>TypeToDataEntry</a>&gt;</code>
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

### GetPackageName {:#GetPackageName}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>package_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

## MessageQueue {:#MessageQueue}
*Defined in [fuchsia.modular/message_queue.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/component/message_queue.fidl#31)*


### GetToken {:#GetToken}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue_token</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

### RegisterReceiver {:#RegisterReceiver}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>receiver</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#MessageReader'>MessageReader</a></code>
            </td>
        </tr></table>



## MessageSender {:#MessageSender}
*Defined in [fuchsia.modular/message_queue.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/component/message_queue.fidl#48)*


### Send {:#Send}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>message</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
        </tr></table>



## MessageReader {:#MessageReader}
*Defined in [fuchsia.modular/message_queue.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/component/message_queue.fidl#57)*


### OnReceive {:#OnReceive}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>message</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## ContextEngine {:#ContextEngine}
*Defined in [fuchsia.modular/context_engine.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/context_engine.fidl#10)*


### GetReader {:#GetReader}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>client_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ComponentScope'>ComponentScope</a></code>
            </td>
        </tr><tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#ContextReader'>ContextReader</a>&gt;</code>
            </td>
        </tr></table>



### GetWriter {:#GetWriter}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>client_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ComponentScope'>ComponentScope</a></code>
            </td>
        </tr><tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#ContextWriter'>ContextWriter</a>&gt;</code>
            </td>
        </tr></table>



### GetContextDebug {:#GetContextDebug}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#ContextDebug'>ContextDebug</a>&gt;</code>
            </td>
        </tr></table>



## ContextReader {:#ContextReader}
*Defined in [fuchsia.modular/context_reader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/context_reader.fidl#13)*


### Subscribe {:#Subscribe}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>query</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ContextQuery'>ContextQuery</a></code>
            </td>
        </tr><tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ContextListener'>ContextListener</a></code>
            </td>
        </tr></table>



### Get {:#Get}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>query</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ContextQuery'>ContextQuery</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>update</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ContextUpdate'>ContextUpdate</a></code>
            </td>
        </tr></table>

## ContextListener {:#ContextListener}
*Defined in [fuchsia.modular/context_reader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/context_reader.fidl#59)*


### OnContextUpdate {:#OnContextUpdate}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>update</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ContextUpdate'>ContextUpdate</a></code>
            </td>
        </tr></table>



## ContextWriter {:#ContextWriter}
*Defined in [fuchsia.modular/context_writer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/context_writer.fidl#8)*


### CreateValue {:#CreateValue}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value_writer</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#ContextValueWriter'>ContextValueWriter</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ContextValueType'>ContextValueType</a></code>
            </td>
        </tr></table>



### WriteEntityTopic {:#WriteEntityTopic}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>topic</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr></table>



## ContextValueWriter {:#ContextValueWriter}
*Defined in [fuchsia.modular/context_writer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/context_writer.fidl#29)*


### CreateChildValue {:#CreateChildValue}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value_writer</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#ContextValueWriter'>ContextValueWriter</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ContextValueType'>ContextValueType</a></code>
            </td>
        </tr></table>



### Set {:#Set}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>content</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr><tr>
            <td><code>metadata</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ContextMetadata'>ContextMetadata</a>?</code>
            </td>
        </tr></table>



## ContextDebug {:#ContextDebug}
*Defined in [fuchsia.modular/debug.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/debug.fidl#8)*


### Watch {:#Watch}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ContextDebugListener'>ContextDebugListener</a></code>
            </td>
        </tr></table>



### WaitUntilIdle {:#WaitUntilIdle}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## ContextDebugListener {:#ContextDebugListener}
*Defined in [fuchsia.modular/debug.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/debug.fidl#17)*


### OnValuesChanged {:#OnValuesChanged}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>values</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#ContextDebugValue'>ContextDebugValue</a>&gt;</code>
            </td>
        </tr></table>



### OnSubscriptionsChanged {:#OnSubscriptionsChanged}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>subscription</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#ContextDebugSubscription'>ContextDebugSubscription</a>&gt;</code>
            </td>
        </tr></table>



## Entity {:#Entity}
*Defined in [fuchsia.modular/entity.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/entity/entity.fidl#10)*

 A multi-typed data entity.

### GetTypes {:#GetTypes}

 Returns the types associated with this entity. Each entry in `types`
 references a well-known content type.

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

### GetData {:#GetData}

 Given one of the types returned from `GetTypes()` above, returns
 associated short-form data, or null if the type is absent from
 `GetTypes()`.

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
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a>?</code>
            </td>
        </tr></table>

### WriteData {:#WriteData}

 Sets the data for a particular type. This will precipitate an `OnUpdated`
 event with the associated type.

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
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#EntityWriteStatus'>EntityWriteStatus</a></code>
            </td>
        </tr></table>

### GetReference {:#GetReference}

 Gets the entity reference for this entity, which can be persisted and
 then later used to locate this entity. These references are weak
 references and are not sufficient to keep the entity alive.

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

### Watch {:#Watch}

 Begins watching for data changes on a particular type. The watcher
 immediately fires `OnUpdated` with the current value for the requested
 type (or null if the type is not present). Closing the `Entity` interface
 does not close the watcher.

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
                <code><a class='link' href='../fuchsia.modular/index.html#EntityWatcher'>EntityWatcher</a></code>
            </td>
        </tr></table>



## EntityWatcher {:#EntityWatcher}
*Defined in [fuchsia.modular/entity.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/entity/entity.fidl#37)*


### OnUpdated {:#OnUpdated}

 Fires on data updates for a particular type. If the type is initially not
 present, a null `data` pointer is produced. The type may only transition
 from absent to present at most once, as there is no deletion.

 No deduplication is performed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a>?</code>
            </td>
        </tr></table>



## EntityProvider {:#EntityProvider}
*Defined in [fuchsia.modular/entity_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/entity/entity_provider.fidl#21)*

 EntityProviders (agents) must implement and provide the `EntityProvider`
 service if they create entity references (using `EntityReferenceFactory`).
 This service is used by the framework to provide data for an `Entity`
 interface for an entity. This interface is requested by the framework in
 the agent's *application* outgoing services, and is closed by the framework
 when there are no more `Entity`s that need to be provided.

 In the below methods, `cookie` will have been previously passed to
 `EntityReferenceFactory.CreateReference()`, though this may have been in an
 earlier or remote app instance. Entity providers should attempt to resolve
 unfamiliar cookies or else treat the entities as empty and read-only.

### GetTypes {:#GetTypes}

 Returns the types associated with the requested entity. Each entry in
 `type` references a well-known content type.

 If the cookie cannot be resolved, the provider should produce an empty
 vector.

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

### GetData {:#GetData}

 Given one of the types returned from `GetTypes()` above, returns
 associated short-form data, or null if the type is absent from
 `GetTypes()`.

 If the cookie cannot be resolved, the provider should return null.

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
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a>?</code>
            </td>
        </tr></table>

### WriteData {:#WriteData}

 Sets the data for a particular type. This must precipitate an `OnUpdate`
 event with the associated type.

 If the cookie cannot be resolved, the provider should no-op with
 `EntityWriteStatus::READ_ONLY`.

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
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#EntityWriteStatus'>EntityWriteStatus</a></code>
            </td>
        </tr></table>

### Watch {:#Watch}

 Begins watching for data changes on a particular type. The watcher must
 immediately fire `OnUpdated` with the current value for the requested
 type (or null if the type is not present).

 No deduplication of events should be performed.

 At most one update may be in-flight at a time on a particular watcher;
 once a client is ready for another update, it will call the callback. At
 most one update should be queued for dispatch for a particular watcher;
 older updates should be dropped.

 If the cookie cannot be resolved, the provider should emit a single event
 with null data.

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
                <code><a class='link' href='../fuchsia.modular/index.html#EntityWatcher'>EntityWatcher</a></code>
            </td>
        </tr></table>



## EntityReferenceFactory {:#EntityReferenceFactory}
*Defined in [fuchsia.modular/entity_reference_factory.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/entity/entity_reference_factory.fidl#13)*


### CreateReference {:#CreateReference}


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

## EntityResolver {:#EntityResolver}
*Defined in [fuchsia.modular/entity_resolver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/entity/entity_resolver.fidl#10)*


### ResolveEntity {:#ResolveEntity}


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
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#Entity'>Entity</a>&gt;</code>
            </td>
        </tr></table>



## IntentHandler {:#IntentHandler}
*Defined in [fuchsia.modular/intent_handler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/intent/intent_handler.fidl#17)*


### HandleIntent {:#HandleIntent}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>intent</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#Intent'>Intent</a></code>
            </td>
        </tr></table>



## Lifecycle {:#Lifecycle}
*Defined in [fuchsia.modular/lifecycle.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/lifecycle/lifecycle.fidl#9)*


### Terminate {:#Terminate}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## ModuleContext {:#ModuleContext}
*Defined in [fuchsia.modular/module_context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_context.fidl#13)*

 This interface is exposed to all Module instances in a story. It allows to
 create Link instances and run more Module instances.

### GetLink {:#GetLink}

 Gets a Link instance with the given name.

 The Link instance has a name so that it can be recognized when the story
 is resumed. The name is unique in the scope of the Module instance. If
 the method is called again with the same argument by the same Module
 instance, a new connection to the same Link instance is obtained. It's
 up to the Module instance to ensure the name is unique within the scope
 of itself.

 TODO(thatguy): When no modules use null link names any more, make name
 required.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr><tr>
            <td><code>link</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#Link'>Link</a>&gt;</code>
            </td>
        </tr></table>



### AddModuleToStory {:#AddModuleToStory}

 Starts a new Module instance and adds it to the story. The Module to
 execute is identified by the contents of [intent] and the Module instance
 is given a [name] in the scope of the starting Module instance. The view
 for the Module is given to the story shell for display.

 Providing a [surface_relation] advises the StoryShell how to layout
 surfaces that the new module creates. If [surface_relation] is null then
 a default relation is used.

 If the method is called again with the same [name] by the same Module
 instance, but with different arguments, the existing Module instance is
 restarted with the changed arguments. If the other arguments don't
 change, just an additional ModuleController connection is made.

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
                <code><a class='link' href='../fuchsia.modular/index.html#Intent'>Intent</a></code>
            </td>
        </tr><tr>
            <td><code>module_controller</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#ModuleController'>ModuleController</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>surface_relation</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#SurfaceRelation'>SurfaceRelation</a>?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#StartModuleStatus'>StartModuleStatus</a></code>
            </td>
        </tr></table>

### EmbedModule {:#EmbedModule}

 Like AddModuleToStory(), but passes a [view_token] explicitly to embed
 the view of the requested Module instance in the view of the requesting
 Module instance, instead of relying on the story shell for display. If a
 Module instance with the same [name] and [intent] is already running,
 [view_token] is destroyed.

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
                <code><a class='link' href='../fuchsia.modular/index.html#Intent'>Intent</a></code>
            </td>
        </tr><tr>
            <td><code>module_controller</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#ModuleController'>ModuleController</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>view_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#ViewToken'>ViewToken</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#StartModuleStatus'>StartModuleStatus</a></code>
            </td>
        </tr></table>

### EmbedModule2 {:#EmbedModule2}


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
                <code><a class='link' href='../fuchsia.modular/index.html#Intent'>Intent</a></code>
            </td>
        </tr><tr>
            <td><code>module_controller</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#ModuleController'>ModuleController</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>view_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#ViewToken'>ViewToken</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#StartModuleStatus'>StartModuleStatus</a></code>
            </td>
        </tr></table>

### StartContainerInShell {:#StartContainerInShell}

 DEPRECATED: no longer implemented.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>container_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>parent_relation</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#SurfaceRelation'>SurfaceRelation</a></code>
            </td>
        </tr><tr>
            <td><code>layout</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#ContainerLayout'>ContainerLayout</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>relationships</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#ContainerRelationEntry'>ContainerRelationEntry</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>nodes</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#ContainerNode'>ContainerNode</a>&gt;</code>
            </td>
        </tr></table>



### GetComponentContext {:#GetComponentContext}

 DEPRECATED: ComponentContext is now available in the
 namespace/environment for Modules.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#ComponentContext'>ComponentContext</a>&gt;</code>
            </td>
        </tr></table>



### GetStoryId {:#GetStoryId}

 Gets the id for this story which may be used to create a suggestion
 proposal to resume this story, especially by agents.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

### RequestFocus {:#RequestFocus}

 Requests that the current story and module gain focus. It's up to the story
 shell and session shell to honor that request.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Active {:#Active}

 DEPRECATED in favor of using StartOngoingActivity().

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### RemoveSelfFromStory {:#RemoveSelfFromStory}

 When a module calls [RemoveSelfFromStory()] the framework will stop the
 module and remove it from the story. If there are no more running modules
 in the story the story will be deleted.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### RequestStoryVisibilityState {:#RequestStoryVisibilityState}

 Requests to update the visibility state of the current story within the
 session shell. The framework will decide whether to honor this request, then
 forward it to the session shell.

 Modules should not have any knowledge of the story's visibility state, nor
 should it ever operate with any assumption of the visibility state.

 Note that the framework keeps this state only in memory, which means that
 across reboots, the story visibility state will revert back to DEFAULT.
 This makes it unsafe for any component outside the framework to make
 assumptions about the story visibility state. Also, this differs from other
 UI states such as focus state, which is persisted across reboots.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>visibility_state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#StoryVisibilityState'>StoryVisibilityState</a></code>
            </td>
        </tr></table>



### StartOngoingActivity {:#StartOngoingActivity}

 Declares that activity of the given [type] is ongoing in this module.
 This information is forwarded to the session shell
 (cf. StoryProvider.WatchActivity() and StoryActivityWatcher).

 Modules should close [request] when the ongoing activity has stopped, and
 this will also signal to the session shell that the ongoing activity has
 stopped. For now, pausing media should count as a stopped ongoing activity,
 and when it is resumed it should be started as a new ongoing activity.
 Conversely, media playing in a continuous playlist (i.e playing the next
 video or song) should be treated as the same ongoing activity.
 Modules must request a connection per ongoing activity; a single connection
 may not be re-used for multiple ongoing activities.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#OngoingActivityType'>OngoingActivityType</a></code>
            </td>
        </tr><tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#OngoingActivity'>OngoingActivity</a>&gt;</code>
            </td>
        </tr></table>



### CreateEntity {:#CreateEntity}

 Creates a [fuchsia.modular.Entity] with the given [type] and [data]. The
 lifetime of the created entity is tied to the lifetime of the current story,
 but can be dereferenced by modules and agents outside the scope of the story.

 [entity_request] will be connected to the created entity, or closed if the
 creation fails.

 The returned [reference] is the entity reference for the created entity, or
 null if the entity creation failed.

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
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
        </tr><tr>
            <td><code>entity_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#Entity'>Entity</a>&gt;</code>
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

## OngoingActivity {:#OngoingActivity}
*Defined in [fuchsia.modular/module_context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_context.fidl#140)*

 This interface defines the protocol over which a Module can communicate about
 an ongoing activity to the framework. It is provided to Modules via
 ModuleContext.StartOngoingActivity().

## ModuleController {:#ModuleController}
*Defined in [fuchsia.modular/module_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_controller.fidl#12)*

 This interface is used by the caller of ModuleContext.StartModule() to
 control the started Module instance.

 Closing this connection doesn't affect its Module instance; it just
 relinquishes the ability of the caller to control the Module instance.

### Focus {:#Focus}

 Requests that this module become the focused module in the story.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Defocus {:#Defocus}

 Requests that this module be hidden in the story.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Stop {:#Stop}

 Requests the Module instance to stop. The running Module component's
 Lifecycle::Terminate() method is called, the instance is shut down and
 state within the framework is cleaned up.

 The result callback is called once the Module's runtime has been torn down.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### OnStateChange {:#OnStateChange}

 Called with the current state when it changes.
 DEPRECATED: Do not use this. ModuleState is a framework-internal concept
 and should not be exposed outside.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>new_state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ModuleState'>ModuleState</a></code>
            </td>
        </tr></table>

## ModuleResolver {:#ModuleResolver}
*Defined in [fuchsia.modular/module_resolver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module_resolver/module_resolver.fidl#8)*


### FindModules {:#FindModules}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>query</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#FindModulesQuery'>FindModulesQuery</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#FindModulesResponse'>FindModulesResponse</a></code>
            </td>
        </tr></table>

## FocusController {:#FocusController}
*Defined in [fuchsia.modular/focus.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/session/focus.fidl#22)*

 This file has interfaces for 2 pieces of information: (1) The story
 that is currently in focus and (2) stories that are visible to the
 user. Names of interfaces follow the usual patterns:

 {Focus,VisibleStories}Controller is used by session shell to update
 information whenever changes take place.

 FocusProvider is used by maxwell and session shell to
 query and get updates on which story is in focus on which device
 and visible stories on this device.

 Implemented by sessionmgr. Given to session shell through its namespace.

### Set {:#Set}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>focused_story_id</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr></table>



### WatchRequest {:#WatchRequest}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#FocusRequestWatcher'>FocusRequestWatcher</a></code>
            </td>
        </tr></table>



## FocusRequestWatcher {:#FocusRequestWatcher}
*Defined in [fuchsia.modular/focus.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/session/focus.fidl#31)*

 Implemented by session shell. OnFocusRequest() gets called whenever there
 is a new request to change focus on this device. Requests can be
 made via FocusProvider.Request().

### OnFocusRequest {:#OnFocusRequest}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



## FocusProvider {:#FocusProvider}
*Defined in [fuchsia.modular/focus.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/session/focus.fidl#38)*

 Implemented by sessionmgr. Given to session shell and session agents through
 their namespace. Focus is persisted on the ledger.

### Query {:#Query}

 Returns the stories that are focused across all devices.

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
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#FocusInfo'>FocusInfo</a>&gt;</code>
            </td>
        </tr></table>

### Watch {:#Watch}

 Watches for change in focus on any of the user's devices.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#FocusWatcher'>FocusWatcher</a></code>
            </td>
        </tr></table>



### Request {:#Request}

 Requests session shell to change focus on this device. If session shell
 responds to this request, focus shall be taken away from
 previously focused story and an update will be sent on
 FocusWatcher.OnFocusChange(). If `story_id` is NULL, the timeline
 is brought back into focus.


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_id</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr></table>



## FocusWatcher {:#FocusWatcher}
*Defined in [fuchsia.modular/focus.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/session/focus.fidl#58)*

 Implemented by anyone who is interested in getting updates when focus
 changes.

### OnFocusChange {:#OnFocusChange}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>focus_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#FocusInfo'>FocusInfo</a>?</code>
            </td>
        </tr></table>



## VisibleStoriesController {:#VisibleStoriesController}
*Defined in [fuchsia.modular/focus.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/session/focus.fidl#76)*

 Implemented by sessionmgr. Given to session shell through its namespace.

### Set {:#Set}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>visible_story_ids</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
        </tr></table>



## SessionShell {:#SessionShell}
*Defined in [fuchsia.modular/session_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/session/session_shell.fidl#16)*


### AttachView {:#AttachView}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ViewIdentifier'>ViewIdentifier</a></code>
            </td>
        </tr><tr>
            <td><code>view_holder_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#ViewHolderToken'>ViewHolderToken</a></code>
            </td>
        </tr></table>



### AttachView2 {:#AttachView2}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ViewIdentifier'>ViewIdentifier</a></code>
            </td>
        </tr><tr>
            <td><code>view_holder_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#ViewHolderToken'>ViewHolderToken</a></code>
            </td>
        </tr></table>



### DetachView {:#DetachView}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ViewIdentifier'>ViewIdentifier</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## SessionShellContext {:#SessionShellContext}
*Defined in [fuchsia.modular/session_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/session/session_shell.fidl#59)*


### GetAccount {:#GetAccount}


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
                <code><a class='link' href='../fuchsia.modular.auth/index.html'>fuchsia.modular.auth</a>/<a class='link' href='../fuchsia.modular.auth/index.html#Account'>Account</a>?</code>
            </td>
        </tr></table>

### GetComponentContext {:#GetComponentContext}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#ComponentContext'>ComponentContext</a>&gt;</code>
            </td>
        </tr></table>



### GetDeviceName {:#GetDeviceName}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

### GetFocusController {:#GetFocusController}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#FocusController'>FocusController</a>&gt;</code>
            </td>
        </tr></table>



### GetFocusProvider {:#GetFocusProvider}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#FocusProvider'>FocusProvider</a>&gt;</code>
            </td>
        </tr></table>



### GetLink {:#GetLink}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#Link'>Link</a>&gt;</code>
            </td>
        </tr></table>



### GetPresentation {:#GetPresentation}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.ui.policy/index.html'>fuchsia.ui.policy</a>/<a class='link' href='../fuchsia.ui.policy/index.html#Presentation'>Presentation</a>&gt;</code>
            </td>
        </tr></table>



### GetSpeechToText {:#GetSpeechToText}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.speech/index.html'>fuchsia.speech</a>/<a class='link' href='../fuchsia.speech/index.html#SpeechToText'>SpeechToText</a>&gt;</code>
            </td>
        </tr></table>



### GetStoryProvider {:#GetStoryProvider}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#StoryProvider'>StoryProvider</a>&gt;</code>
            </td>
        </tr></table>



### GetVisibleStoriesController {:#GetVisibleStoriesController}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#VisibleStoriesController'>VisibleStoriesController</a>&gt;</code>
            </td>
        </tr></table>



### Logout {:#Logout}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## SessionShellPresentationProvider {:#SessionShellPresentationProvider}
*Defined in [fuchsia.modular/session_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/session/session_shell.fidl#87)*


### GetPresentation {:#GetPresentation}


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
                <code>request&lt;<a class='link' href='../fuchsia.ui.policy/index.html'>fuchsia.ui.policy</a>/<a class='link' href='../fuchsia.ui.policy/index.html#Presentation'>Presentation</a>&gt;</code>
            </td>
        </tr></table>



### WatchVisualState {:#WatchVisualState}


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
                <code><a class='link' href='../fuchsia.modular/index.html#StoryVisualStateWatcher'>StoryVisualStateWatcher</a></code>
            </td>
        </tr></table>



## Link {:#Link}
*Defined in [fuchsia.modular/link.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/link.fidl#49)*


### Get {:#Get}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>path</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>json_data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a>?</code>
            </td>
        </tr></table>

### Set {:#Set}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>path</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
        </tr><tr>
            <td><code>json_data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
        </tr></table>



### Erase {:#Erase}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>path</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr></table>



### GetEntity {:#GetEntity}


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
                <code>string?</code>
            </td>
        </tr></table>

### SetEntity {:#SetEntity}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>entity_reference</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr></table>



### Watch {:#Watch}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#LinkWatcher'>LinkWatcher</a></code>
            </td>
        </tr></table>



### WatchAll {:#WatchAll}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#LinkWatcher'>LinkWatcher</a></code>
            </td>
        </tr></table>



### Sync {:#Sync}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## LinkWatcher {:#LinkWatcher}
*Defined in [fuchsia.modular/link.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/link.fidl#119)*


### Notify {:#Notify}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>json</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
        </tr></table>



## PuppetMaster {:#PuppetMaster}
*Defined in [fuchsia.modular/puppet_master.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/puppet_master.fidl#52)*


### ControlStory {:#ControlStory}


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
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#StoryPuppetMaster'>StoryPuppetMaster</a>&gt;</code>
            </td>
        </tr></table>



### DeleteStory {:#DeleteStory}


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

### GetStories {:#GetStories}


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

## StoryPuppetMaster {:#StoryPuppetMaster}
*Defined in [fuchsia.modular/puppet_master.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/puppet_master.fidl#77)*


### Enqueue {:#Enqueue}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>commands</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#StoryCommand'>StoryCommand</a>&gt;</code>
            </td>
        </tr></table>



### Execute {:#Execute}


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
                <code><a class='link' href='../fuchsia.modular/index.html#ExecuteResult'>ExecuteResult</a></code>
            </td>
        </tr></table>

### SetCreateOptions {:#SetCreateOptions}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_options</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#StoryOptions'>StoryOptions</a></code>
            </td>
        </tr></table>



### SetStoryInfoExtra {:#SetStoryInfoExtra}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_info_extra</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#StoryInfoExtraEntry'>StoryInfoExtraEntry</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#StoryPuppetMaster_SetStoryInfoExtra_Result'>StoryPuppetMaster_SetStoryInfoExtra_Result</a></code>
            </td>
        </tr></table>

## StoryController {:#StoryController}
*Defined in [fuchsia.modular/story_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_controller.fidl#14)*


### GetInfo {:#GetInfo}


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
                <code><a class='link' href='../fuchsia.modular/index.html#StoryInfo'>StoryInfo</a></code>
            </td>
        </tr><tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#StoryState'>StoryState</a></code>
            </td>
        </tr></table>

### RequestStart {:#RequestStart}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Stop {:#Stop}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### TakeAndLoadSnapshot {:#TakeAndLoadSnapshot}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#ViewToken'>ViewToken</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### Watch {:#Watch}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#StoryWatcher'>StoryWatcher</a></code>
            </td>
        </tr></table>



### GetActiveModules {:#GetActiveModules}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>module_data</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#ModuleData'>ModuleData</a>&gt;</code>
            </td>
        </tr></table>

### GetModules {:#GetModules}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>module_data</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#ModuleData'>ModuleData</a>&gt;</code>
            </td>
        </tr></table>

### GetModuleController {:#GetModuleController}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>module_path</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr><tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#ModuleController'>ModuleController</a>&gt;</code>
            </td>
        </tr></table>



### GetLink {:#GetLink}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>link_path</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#LinkPath'>LinkPath</a></code>
            </td>
        </tr><tr>
            <td><code>link</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#Link'>Link</a>&gt;</code>
            </td>
        </tr></table>



## StoryWatcher {:#StoryWatcher}
*Defined in [fuchsia.modular/story_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_controller.fidl#57)*


### OnStateChange {:#OnStateChange}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>new_state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#StoryState'>StoryState</a></code>
            </td>
        </tr></table>



### OnModuleAdded {:#OnModuleAdded}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>module_data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ModuleData'>ModuleData</a></code>
            </td>
        </tr></table>



### OnModuleFocused {:#OnModuleFocused}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>module_path</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr></table>



## StoryLinksWatcher {:#StoryLinksWatcher}
*Defined in [fuchsia.modular/story_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_controller.fidl#73)*


### OnNewLink {:#OnNewLink}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>link_path</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#LinkPath'>LinkPath</a></code>
            </td>
        </tr></table>



## StoryProvider {:#StoryProvider}
*Defined in [fuchsia.modular/story_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_provider.fidl#14)*


### GetStories {:#GetStories}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#StoryProviderWatcher'>StoryProviderWatcher</a>?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_infos</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#StoryInfo'>StoryInfo</a>&gt;</code>
            </td>
        </tr></table>

### GetStoryInfo {:#GetStoryInfo}


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
                <code><a class='link' href='../fuchsia.modular/index.html#StoryInfo'>StoryInfo</a>?</code>
            </td>
        </tr></table>

### GetController {:#GetController}


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
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#StoryController'>StoryController</a>&gt;</code>
            </td>
        </tr></table>



### PreviousStories {:#PreviousStories}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_infos</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#StoryInfo'>StoryInfo</a>&gt;</code>
            </td>
        </tr></table>

### Watch {:#Watch}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#StoryProviderWatcher'>StoryProviderWatcher</a></code>
            </td>
        </tr></table>



### WatchActivity {:#WatchActivity}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#StoryActivityWatcher'>StoryActivityWatcher</a></code>
            </td>
        </tr></table>



## StoryProviderWatcher {:#StoryProviderWatcher}
*Defined in [fuchsia.modular/story_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_provider.fidl#44)*


### OnChange {:#OnChange}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#StoryInfo'>StoryInfo</a></code>
            </td>
        </tr><tr>
            <td><code>story_state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#StoryState'>StoryState</a></code>
            </td>
        </tr><tr>
            <td><code>story_visibility_state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#StoryVisibilityState'>StoryVisibilityState</a></code>
            </td>
        </tr></table>



### OnDelete {:#OnDelete}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



## StoryActivityWatcher {:#StoryActivityWatcher}
*Defined in [fuchsia.modular/story_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_provider.fidl#95)*


### OnStoryActivityChange {:#OnStoryActivityChange}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>activities</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#OngoingActivityType'>OngoingActivityType</a>&gt;</code>
            </td>
        </tr></table>



## StoryShell {:#StoryShell}
*Defined in [fuchsia.modular/story_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell.fidl#21)*


### Initialize {:#Initialize}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_shell_context</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#StoryShellContext'>StoryShellContext</a></code>
            </td>
        </tr></table>



### AddSurface {:#AddSurface}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_connection</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ViewConnection'>ViewConnection</a></code>
            </td>
        </tr><tr>
            <td><code>surface_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#SurfaceInfo'>SurfaceInfo</a></code>
            </td>
        </tr></table>



### AddSurface2 {:#AddSurface2}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_connection</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ViewConnection2'>ViewConnection2</a></code>
            </td>
        </tr><tr>
            <td><code>surface_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#SurfaceInfo'>SurfaceInfo</a></code>
            </td>
        </tr></table>



### FocusSurface {:#FocusSurface}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>surface_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### DefocusSurface {:#DefocusSurface}


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

### AddContainer {:#AddContainer}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>containerName</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>parentId</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr><tr>
            <td><code>relation</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#SurfaceRelation'>SurfaceRelation</a></code>
            </td>
        </tr><tr>
            <td><code>layout</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#ContainerLayout'>ContainerLayout</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>relationships</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#ContainerRelationEntry'>ContainerRelationEntry</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>views</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#ContainerView'>ContainerView</a>&gt;</code>
            </td>
        </tr></table>



### AddContainer2 {:#AddContainer2}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>containerName</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>parentId</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr><tr>
            <td><code>relation</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#SurfaceRelation'>SurfaceRelation</a></code>
            </td>
        </tr><tr>
            <td><code>layout</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#ContainerLayout'>ContainerLayout</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>relationships</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#ContainerRelationEntry'>ContainerRelationEntry</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>views</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#ContainerView2'>ContainerView2</a>&gt;</code>
            </td>
        </tr></table>



### OnSurfaceFocused {:#OnSurfaceFocused}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>surface_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

### RemoveSurface {:#RemoveSurface}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>surface_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### ReconnectView {:#ReconnectView}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_connection</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ViewConnection'>ViewConnection</a></code>
            </td>
        </tr></table>



### ReconnectView2 {:#ReconnectView2}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_connection</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ViewConnection2'>ViewConnection2</a></code>
            </td>
        </tr></table>



### UpdateSurface {:#UpdateSurface}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_connection</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ViewConnection'>ViewConnection</a></code>
            </td>
        </tr><tr>
            <td><code>surface_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#SurfaceInfo'>SurfaceInfo</a></code>
            </td>
        </tr></table>



### UpdateSurface2 {:#UpdateSurface2}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_connection</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ViewConnection2'>ViewConnection2</a></code>
            </td>
        </tr><tr>
            <td><code>surface_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#SurfaceInfo'>SurfaceInfo</a></code>
            </td>
        </tr></table>



## StoryShellContext {:#StoryShellContext}
*Defined in [fuchsia.modular/story_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell.fidl#167)*


### GetPresentation {:#GetPresentation}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.ui.policy/index.html'>fuchsia.ui.policy</a>/<a class='link' href='../fuchsia.ui.policy/index.html#Presentation'>Presentation</a>&gt;</code>
            </td>
        </tr></table>



### WatchVisualState {:#WatchVisualState}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#StoryVisualStateWatcher'>StoryVisualStateWatcher</a></code>
            </td>
        </tr></table>



### GetLink {:#GetLink}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#Link'>Link</a>&gt;</code>
            </td>
        </tr></table>



### RequestView {:#RequestView}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>surface_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### OnSurfaceOffScreen {:#OnSurfaceOffScreen}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>surface_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



## StoryVisualStateWatcher {:#StoryVisualStateWatcher}
*Defined in [fuchsia.modular/story_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell.fidl#188)*


### OnVisualStateChange {:#OnVisualStateChange}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>visual_state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#StoryVisualState'>StoryVisualState</a></code>
            </td>
        </tr></table>



## StoryShellFactory {:#StoryShellFactory}
*Defined in [fuchsia.modular/story_shell_factory.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell_factory.fidl#11)*


### AttachStory {:#AttachStory}


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
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#StoryShell'>StoryShell</a>&gt;</code>
            </td>
        </tr></table>



### DetachStory {:#DetachStory}


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

## IntelligenceServices {:#IntelligenceServices}
*Defined in [fuchsia.modular/intelligence_services.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/user_intelligence/intelligence_services.fidl#10)*


### GetContextReader {:#GetContextReader}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>context_reader</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#ContextReader'>ContextReader</a>&gt;</code>
            </td>
        </tr></table>



### GetContextWriter {:#GetContextWriter}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>context_writer</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#ContextWriter'>ContextWriter</a>&gt;</code>
            </td>
        </tr></table>



## UserIntelligenceProvider {:#UserIntelligenceProvider}
*Defined in [fuchsia.modular/user_intelligence_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/user_intelligence/user_intelligence_provider.fidl#10)*


### GetComponentIntelligenceServices {:#GetComponentIntelligenceServices}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>scope</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ComponentScope'>ComponentScope</a></code>
            </td>
        </tr><tr>
            <td><code>services</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#IntelligenceServices'>IntelligenceServices</a>&gt;</code>
            </td>
        </tr></table>



### GetSpeechToText {:#GetSpeechToText}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>speech_to_text</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.speech/index.html'>fuchsia.speech</a>/<a class='link' href='../fuchsia.speech/index.html#SpeechToText'>SpeechToText</a>&gt;</code>
            </td>
        </tr></table>



### StartAgents {:#StartAgents}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>user_intelligence_context</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ComponentContext'>ComponentContext</a></code>
            </td>
        </tr><tr>
            <td><code>session_agents</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr><tr>
            <td><code>startup_agents</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr></table>



### GetServicesForAgent {:#GetServicesForAgent}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>agent_url</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service_list</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sys/index.html'>fuchsia.sys</a>/<a class='link' href='../fuchsia.sys/index.html#ServiceList'>ServiceList</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### TaskInfo {:#TaskInfo}
*Defined in [fuchsia.modular/agent_context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/agent/agent_context.fidl#40)*



 Used to describe a task to the framework.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>task_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td> An agent provided task id that can be used later to refer to this task.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>trigger_condition</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#TriggerCondition'>TriggerCondition</a></code>
            </td>
            <td> The condition that would cause this task to get scheduled.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>persistent</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If set to true, the trigger condition will be persisted on the user's
 ledger and will be available across reboots and devices.
</td>
            <td>No default</td>
        </tr>
</table>

### BaseShellParams {:#BaseShellParams}
*Defined in [fuchsia.modular/base_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/basemgr/base_shell.fidl#49)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>presentation</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.policy/index.html'>fuchsia.ui.policy</a>/<a class='link' href='../fuchsia.ui.policy/index.html#Presentation'>Presentation</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### UserLoginParams {:#UserLoginParams}
*Defined in [fuchsia.modular/user_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/basemgr/user_provider.fidl#48)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>account_id</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### UserLoginParams2 {:#UserLoginParams2}
*Defined in [fuchsia.modular/user_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/basemgr/user_provider.fidl#55)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>account_id</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TypeToDataEntry {:#TypeToDataEntry}
*Defined in [fuchsia.modular/component_context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/component/component_context.fidl#91)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>type</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AppConfig {:#AppConfig}
*Defined in [fuchsia.modular/config.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/config/config.fidl#9)*





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

### ContextQuery {:#ContextQuery}
*Defined in [fuchsia.modular/context_reader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/context_reader.fidl#28)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>selector</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#ContextQueryEntry'>ContextQueryEntry</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ContextQueryEntry {:#ContextQueryEntry}
*Defined in [fuchsia.modular/context_reader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/context_reader.fidl#35)*





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
                <code><a class='link' href='../fuchsia.modular/index.html#ContextSelector'>ContextSelector</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ContextSelector {:#ContextSelector}
*Defined in [fuchsia.modular/context_reader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/context_reader.fidl#40)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>meta</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ContextMetadata'>ContextMetadata</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ContextValueType'>ContextValueType</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ContextUpdate {:#ContextUpdate}
*Defined in [fuchsia.modular/context_reader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/context_reader.fidl#72)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>values</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#ContextUpdateEntry'>ContextUpdateEntry</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ContextUpdateEntry {:#ContextUpdateEntry}
*Defined in [fuchsia.modular/context_reader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/context_reader.fidl#78)*





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
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#ContextValue'>ContextValue</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ContextDebugValue {:#ContextDebugValue}
*Defined in [fuchsia.modular/debug.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/debug.fidl#29)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>parent_ids</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ContextValue'>ContextValue</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ContextDebugSubscription {:#ContextDebugSubscription}
*Defined in [fuchsia.modular/debug.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/debug.fidl#35)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>debug_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#SubscriptionDebugInfo'>SubscriptionDebugInfo</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>query</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ContextQuery'>ContextQuery</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SubscriptionDebugInfo {:#SubscriptionDebugInfo}
*Defined in [fuchsia.modular/debug.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/debug.fidl#44)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>client_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ComponentScope'>ComponentScope</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ContextMetadata {:#ContextMetadata}
*Defined in [fuchsia.modular/metadata.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/metadata.fidl#18)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>story</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#StoryMetadata'>StoryMetadata</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>mod</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ModuleMetadata'>ModuleMetadata</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>entity</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#EntityMetadata'>EntityMetadata</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>link</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#LinkMetadata'>LinkMetadata</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StoryMetadata {:#StoryMetadata}
*Defined in [fuchsia.modular/metadata.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/metadata.fidl#27)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>focused</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#FocusedState'>FocusedState</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ModuleMetadata {:#ModuleMetadata}
*Defined in [fuchsia.modular/metadata.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/metadata.fidl#34)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>url</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>path</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>focused</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#FocusedState'>FocusedState</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### EntityMetadata {:#EntityMetadata}
*Defined in [fuchsia.modular/metadata.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/metadata.fidl#40)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>topic</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### LinkMetadata {:#LinkMetadata}
*Defined in [fuchsia.modular/metadata.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/metadata.fidl#45)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>module_path</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FocusedState {:#FocusedState}
*Defined in [fuchsia.modular/metadata.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/metadata.fidl#62)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#FocusedStateState'>FocusedStateState</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ContextValue {:#ContextValue}
*Defined in [fuchsia.modular/value.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/value.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ContextValueType'>ContextValueType</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>content</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>meta</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ContextMetadata'>ContextMetadata</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Intent {:#Intent}
*Defined in [fuchsia.modular/intent.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/intent/intent.fidl#11)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>action</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>handler</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>parameters</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#IntentParameter'>IntentParameter</a>&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### IntentParameter {:#IntentParameter}
*Defined in [fuchsia.modular/intent.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/intent/intent.fidl#28)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#IntentParameterData'>IntentParameterData</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### LinkPath {:#LinkPath}
*Defined in [fuchsia.modular/link_path.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/link_path.fidl#12)*



 Addresses a Link within a story. A LinkPath struct should be treated as an
 opaque unique identifier of a link instance.  The `module_path` and
 `link_name` components are leftovers from legacy code and have no external
 meaning.
 TODO(thatguy,lindkvist): Replace this structure with a vector<>. MI4-1021


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

### ModuleData {:#ModuleData}
*Defined in [fuchsia.modular/module_data.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_data.fidl#8)*



 Information about a Module instance in a story.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>module_url</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The URL of the Module binary.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>module_path</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td> The named path leading up to this Module instance. The last name in this
 array is the name by which the Module was started by the parent Module
 instance calling StartModule().
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>parameter_map</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ModuleParameterMap'>ModuleParameterMap</a></code>
            </td>
            <td> Contains the mapping of Mod parameter name to Link instances for this mod.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>module_source</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ModuleSource'>ModuleSource</a></code>
            </td>
            <td> The way in which this Module instance was first started in the story,
 either by request from another Module instance (INTERNAL) or by request
 from outside the story (i.e. by suggestion from an agent - EXTERNAL).
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>surface_relation</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#SurfaceRelation'>SurfaceRelation</a>?</code>
            </td>
            <td> The `surface_relation` that was used to start this Module instance with.
 The same is used when re-inflating the Module instance when the story is
 resumed. A SurfaceRelation value of null represents an embedded Module
 instance (started by EmbedModule()) that is not managed by the story shell.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>module_deleted</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> True if this module was removed from its story either through
 ModuleController.Stop() or ModuleContext.RemoveSelfFromStory().
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>intent</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#Intent'>Intent</a>?</code>
            </td>
            <td> The intent that was issued to start add this Module instance to the story.
 Some Module instances may have been added not by an Intent, for example as
 the initial module of a story. For those the field may be null.

 TODO(thatguy,mesch): This field should now always be set, so make it
 required once the framework is cleaned up enough to guarantee this
 statement.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>is_embedded</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, this module was started by a parent module using
 ModuleContext.EmbedModule(), and its view is not managed by the
 StoryShell.
</td>
            <td>false</td>
        </tr>
</table>

### ModuleParameterMap {:#ModuleParameterMap}
*Defined in [fuchsia.modular/module_data.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_data.fidl#61)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>entries</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#ModuleParameterMapEntry'>ModuleParameterMapEntry</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ModuleParameterMapEntry {:#ModuleParameterMapEntry}
*Defined in [fuchsia.modular/module_data.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_data.fidl#65)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string?</code>
            </td>
            <td> A null [name] is allowed for backwards compatibility with default links.
 TODO(thatguy); When no modules use null link names any more, make this
 required.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>link_path</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#LinkPath'>LinkPath</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ModuleManifest {:#ModuleManifest}
*Defined in [fuchsia.modular/module_manifest.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_manifest.fidl#8)*



 Metadata that define the runtime properties of a Module.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>binary</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The relative path from the root of the package where the Module executable
 file can be found.
 TODO(MF-94): Extract a module's URL from its cmx manifest instead of
 here.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>suggestion_headline</code></td>
            <td>
                <code>string?</code>
            </td>
            <td> A human-readable string that can be used when suggesting this Module.
 DEPRECATED.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>intent_filters</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#IntentFilter'>IntentFilter</a>&gt;?</code>
            </td>
            <td> A list of intents that this module is able to handle.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>composition_pattern</code></td>
            <td>
                <code>string?</code>
            </td>
            <td> Identifies the pattern with which to compose this module with others.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>placeholder_color</code></td>
            <td>
                <code>string?</code>
            </td>
            <td> Defines the color of the placeholder widget used while the module loads.
</td>
            <td>No default</td>
        </tr>
</table>

### IntentFilter {:#IntentFilter}
*Defined in [fuchsia.modular/module_manifest.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_manifest.fidl#30)*



 This struct is used to describe an intent that a module is able to handle.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>action</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The action this module is able to handle.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>parameter_constraints</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#ParameterConstraint'>ParameterConstraint</a>&gt;</code>
            </td>
            <td> Includes the name and types of entities for the parameters required to
 execute specified [action].
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>action_display</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ActionDisplay'>ActionDisplay</a></code>
            </td>
            <td> Defines presentation properties for suggestions of this action.
</td>
            <td>No default</td>
        </tr>
</table>

### ParameterConstraint {:#ParameterConstraint}
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
            <td> The entity type that is valid for this parameter.
</td>
            <td>No default</td>
        </tr>
</table>

### FindModulesQuery {:#FindModulesQuery}
*Defined in [fuchsia.modular/module_resolver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module_resolver/module_resolver.fidl#30)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>handler</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
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
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#FindModulesParameterConstraint'>FindModulesParameterConstraint</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FindModulesParameterConstraint {:#FindModulesParameterConstraint}
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

### FindModulesResponse {:#FindModulesResponse}
*Defined in [fuchsia.modular/module_resolver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module_resolver/module_resolver.fidl#51)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#FindModulesStatus'>FindModulesStatus</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>results</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#FindModulesResult'>FindModulesResult</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FindModulesResult {:#FindModulesResult}
*Defined in [fuchsia.modular/module_resolver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module_resolver/module_resolver.fidl#56)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>module_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>manifest</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ModuleManifest'>ModuleManifest</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FocusInfo {:#FocusInfo}
*Defined in [fuchsia.modular/focus.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/session/focus.fidl#63)*



 Specifies the focused story of a device.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>device_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The id of the device.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>focused_story_id</code></td>
            <td>
                <code>string?</code>
            </td>
            <td> The id of the focused story.  If null, no stories are focused.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>last_focus_change_timestamp</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The time the focused story on the device `device_id` was last
 changed. 0 if no focus has ever been set for device `device_id`.
</td>
            <td>No default</td>
        </tr>
</table>

### ViewIdentifier {:#ViewIdentifier}
*Defined in [fuchsia.modular/session_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/session/session_shell.fidl#51)*





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

### CreateLinkInfo {:#CreateLinkInfo}
*Defined in [fuchsia.modular/create_link.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/create_link.fidl#10)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>initial_data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>allowed_types</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#LinkAllowedTypes'>LinkAllowedTypes</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### LinkAllowedTypes {:#LinkAllowedTypes}
*Defined in [fuchsia.modular/create_link.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/create_link.fidl#21)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>allowed_entity_types</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### CreateModuleParameterMapInfo {:#CreateModuleParameterMapInfo}
*Defined in [fuchsia.modular/create_module_parameter_map.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/create_module_parameter_map.fidl#8)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>property_info</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#CreateModuleParameterMapEntry'>CreateModuleParameterMapEntry</a>&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### CreateModuleParameterMapEntry {:#CreateModuleParameterMapEntry}
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
                <code><a class='link' href='../fuchsia.modular/index.html#CreateModuleParameterInfo'>CreateModuleParameterInfo</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StoryPuppetMaster_SetStoryInfoExtra_Response {:#StoryPuppetMaster_SetStoryInfoExtra_Response}
*Defined in [fuchsia.modular/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#157)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### ExecuteResult {:#ExecuteResult}
*Defined in [fuchsia.modular/puppet_master.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/puppet_master.fidl#37)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ExecuteStatus'>ExecuteStatus</a></code>
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

### WatchSessionOptions {:#WatchSessionOptions}
*Defined in [fuchsia.modular/puppet_master.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/puppet_master.fidl#74)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### SetFocusState {:#SetFocusState}
*Defined in [fuchsia.modular/story_command.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_command.fidl#37)*





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

### AddMod {:#AddMod}
*Defined in [fuchsia.modular/story_command.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_command.fidl#43)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>mod_name</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>mod_name_transitional</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>intent</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#Intent'>Intent</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>surface_relation</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#SurfaceRelation'>SurfaceRelation</a></code>
            </td>
            <td></td>
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

### RemoveMod {:#RemoveMod}
*Defined in [fuchsia.modular/story_command.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_command.fidl#73)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>mod_name</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>mod_name_transitional</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetLinkValue {:#SetLinkValue}
*Defined in [fuchsia.modular/story_command.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_command.fidl#91)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>path</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#LinkPath'>LinkPath</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FocusMod {:#FocusMod}
*Defined in [fuchsia.modular/story_command.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_command.fidl#97)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>mod_name</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>mod_name_transitional</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetKindOfProtoStoryOption {:#SetKindOfProtoStoryOption}
*Defined in [fuchsia.modular/story_command.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_command.fidl#115)*





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

### StoryInfo {:#StoryInfo}
*Defined in [fuchsia.modular/story_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_info.fidl#8)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>url</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>last_focus_time</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>extra</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#StoryInfoExtraEntry'>StoryInfoExtraEntry</a>&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StoryInfoExtraEntry {:#StoryInfoExtraEntry}
*Defined in [fuchsia.modular/story_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_info.fidl#28)*





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

### StoryOptions {:#StoryOptions}
*Defined in [fuchsia.modular/story_options.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_options.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>kind_of_proto_story</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ViewConnection {:#ViewConnection}
*Defined in [fuchsia.modular/story_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell.fidl#107)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>surface_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>view_holder_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#ViewHolderToken'>ViewHolderToken</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ViewConnection2 {:#ViewConnection2}
*Defined in [fuchsia.modular/story_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell.fidl#116)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>surface_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>view_holder_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#ViewHolderToken'>ViewHolderToken</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SurfaceInfo {:#SurfaceInfo}
*Defined in [fuchsia.modular/story_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell.fidl#125)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>parent_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>surface_relation</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#SurfaceRelation'>SurfaceRelation</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>module_manifest</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ModuleManifest'>ModuleManifest</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>module_source</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ModuleSource'>ModuleSource</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ContainerView {:#ContainerView}
*Defined in [fuchsia.modular/story_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell.fidl#143)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>node_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>view_holder_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#ViewHolderToken'>ViewHolderToken</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ContainerView2 {:#ContainerView2}
*Defined in [fuchsia.modular/story_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell.fidl#154)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>node_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>view_holder_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#ViewHolderToken'>ViewHolderToken</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ContainerLayout {:#ContainerLayout}
*Defined in [fuchsia.modular/container.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/surface/container.fidl#11)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>surfaces</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#LayoutEntry'>LayoutEntry</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### LayoutEntry {:#LayoutEntry}
*Defined in [fuchsia.modular/container.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/surface/container.fidl#17)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>node_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>rectangle</code></td>
            <td>
                <code>float32[4]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ContainerRelationEntry {:#ContainerRelationEntry}
*Defined in [fuchsia.modular/container.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/surface/container.fidl#32)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>node_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>parent_node_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>relationship</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#SurfaceRelation'>SurfaceRelation</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ContainerNode {:#ContainerNode}
*Defined in [fuchsia.modular/container.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/surface/container.fidl#59)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>node_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>intent</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#Intent'>Intent</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SurfaceRelation {:#SurfaceRelation}
*Defined in [fuchsia.modular/surface.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/surface/surface.fidl#11)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>arrangement</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#SurfaceArrangement'>SurfaceArrangement</a></code>
            </td>
            <td></td>
            <td><a class='link' href='../fuchsia.modular/index.html#NONE'>NONE</a></td>
        </tr><tr>
            <td><code>dependency</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#SurfaceDependency'>SurfaceDependency</a></code>
            </td>
            <td></td>
            <td><a class='link' href='../fuchsia.modular/index.html#NONE'>NONE</a></td>
        </tr><tr>
            <td><code>emphasis</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>1.0</td>
        </tr>
</table>

### GlobalScope {:#GlobalScope}
*Defined in [fuchsia.modular/scope.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/user_intelligence/scope.fidl#21)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### ModuleScope {:#ModuleScope}
*Defined in [fuchsia.modular/scope.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/user_intelligence/scope.fidl#24)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>url</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>story_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>module_path</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AgentScope {:#AgentScope}
*Defined in [fuchsia.modular/scope.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/user_intelligence/scope.fidl#30)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>url</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StoryScope {:#StoryScope}
*Defined in [fuchsia.modular/scope.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/user_intelligence/scope.fidl#34)*





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



## **ENUMS**

### FocusedStateState {:#FocusedStateState}
Type: <code>uint32</code>

*Defined in [fuchsia.modular/metadata.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/metadata.fidl#66)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>FOCUSED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>NOT_FOCUSED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### ContextValueType {:#ContextValueType}
Type: <code>uint32</code>

*Defined in [fuchsia.modular/value_type.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/value_type.fidl#7)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>STORY</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>MODULE</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>AGENT</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>ENTITY</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>LINK</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr></table>

### EntityWriteStatus {:#EntityWriteStatus}
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
            <td></td>
        </tr><tr>
            <td><code>READ_ONLY</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### StartModuleStatus {:#StartModuleStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.modular/module_context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_context.fidl#132)*

 Communicates the status of an Intent to a Module.


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

### OngoingActivityType {:#OngoingActivityType}
Type: <code>uint32</code>

*Defined in [fuchsia.modular/module_context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_context.fidl#143)*



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

### ModuleSource {:#ModuleSource}
Type: <code>uint32</code>

*Defined in [fuchsia.modular/module_data.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_data.fidl#50)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INTERNAL</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>EXTERNAL</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### ModuleState {:#ModuleState}
Type: <code>uint32</code>

*Defined in [fuchsia.modular/module_state.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_state.fidl#21)*

 State used to notify about state transitions of a Module
 instance. This is very similar to the StoryState, however it's not entirely
 the same and hence a separate type. A module cannot have an INITIAL state,
 because it's started as soon as it is created, and it gets deleted as soon as
 it reaches the STOPPED state, whileas a story can be restarted.

 Currently possible state transitions (and the events that cause
 them) are:

            -> RUNNING     ModuleContext.AddModuleToStory() or
                           ModuleContext.EmbedModule() or
                           StoryController.AddModule()
   RUNNING  -> STOPPED     ModuleController.Stop() or StoryController.Stop()
   RUNNING  -> ERROR       application exits


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>RUNNING</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>STOPPED</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERROR</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr></table>

### FindModulesStatus {:#FindModulesStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.modular/module_resolver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module_resolver/module_resolver.fidl#43)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SUCCESS</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNKNOWN_HANDLER</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### ExecuteStatus {:#ExecuteStatus}
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

### ConfigureStoryError {:#ConfigureStoryError}
Type: <code>int32</code>

*Defined in [fuchsia.modular/puppet_master.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/puppet_master.fidl#32)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ERR_STORY_ALREADY_CREATED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### StoryVisualState {:#StoryVisualState}
Type: <code>uint32</code>

*Defined in [fuchsia.modular/story_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell.fidl#193)*



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

### StoryState {:#StoryState}
Type: <code>uint32</code>

*Defined in [fuchsia.modular/story_state.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_state.fidl#16)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>RUNNING</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>STOPPING</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>STOPPED</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### StoryVisibilityState {:#StoryVisibilityState}
Type: <code>uint32</code>

*Defined in [fuchsia.modular/story_visibility_state.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_visibility_state.fidl#17)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DEFAULT</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>IMMERSIVE</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### SurfaceArrangement {:#SurfaceArrangement}
Type: <code>uint32</code>

*Defined in [fuchsia.modular/surface.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/surface/surface.fidl#24)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NONE</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>COPRESENT</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>SEQUENTIAL</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>ONTOP</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### SurfaceDependency {:#SurfaceDependency}
Type: <code>uint32</code>

*Defined in [fuchsia.modular/surface.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/surface/surface.fidl#42)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NONE</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>DEPENDENT</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### AgentServiceRequest {:#AgentServiceRequest}


*Defined in [fuchsia.modular/component_context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/component/component_context.fidl#74)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>service_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>channel</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>handler</code></td>
            <td>
                <code>string[2083]</code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>agent_controller</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.modular/index.html#AgentController'>AgentController</a>&gt;</code>
            </td>
            <td></td>
        </tr></table>

### ActionDisplay {:#ActionDisplay}


*Defined in [fuchsia.modular/module_manifest.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_manifest.fidl#49)*

 Defines how a suggestion of an action will be presented.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>display_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#DisplayInfo'>DisplayInfo</a></code>
            </td>
            <td> Defines presentation fields for a suggestion. The string fields might be
 templated and will be filled from data in `parameter_mapping`.
 For example: "Listen to $artistName"
</td>
        </tr><tr>
            <td>2</td>
            <td><code>parameter_mapping</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular/index.html#ParameterMapping'>ParameterMapping</a>&gt;</code>
            </td>
            <td> Fields to be replaced in the given `display_info` templated strings.
 In the example above, we would map name=artistName to the intent field
 artist.name where artist is the intent parameter name and name a field
 of it.
</td>
        </tr></table>

### DisplayInfo {:#DisplayInfo}


*Defined in [fuchsia.modular/module_manifest.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_manifest.fidl#63)*

 Presentation information about the suggestion.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>title</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The title of the suggestion.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>subtitle</code></td>
            <td>
                <code>string</code>
            </td>
            <td> A subtitle for the suggestion.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>icon</code></td>
            <td>
                <code>string</code>
            </td>
            <td> A url from which to fetch the icon of the suggestion.
</td>
        </tr></table>

### ParameterMapping {:#ParameterMapping}


*Defined in [fuchsia.modular/module_manifest.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module/module_manifest.fidl#75)*

 Defines pairs that will be replaced in the DisplayInfo.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The name of the variable to be replaced in the template.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>parameter_property</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The path in the intent parameter to get that name.
 PARAMETER_PROPERTY = string | string . PARAMETER_PROPERTY
 The first string in the dot-separated string is the name of the intent
 parameter and the following are nested subfields.
</td>
        </tr></table>



## **UNIONS**

### TriggerCondition {:#TriggerCondition}
*Defined in [fuchsia.modular/agent_context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/agent/agent_context.fidl#54)*

 Describes the condition that needs to be met for a task to become scheduled.
 This is not yet complete and will be extended or changed.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>message_on_queue</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Triggers when there is a new message on a message queue.

 `message_on_queue` is the name of the message queue to be watched. This
 means that only the component that originally obtained the message queue
 will be able to observe new message events.
</td>
        </tr><tr>
            <td><code>queue_deleted</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Triggers when a message queue is deleted.

 `queue_deleted` is the token for the message queue that is to be watched.
 This allows both message queue readers and writers to watch for queue
 deletions.
</td>
        </tr><tr>
            <td><code>alarm_in_seconds</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Fires an inexact repeating alarm every `alarm_in_seconds` seconds that'll
 satisfy this trigger condition. The first alarm fires in
 `alarm_in_seconds` seconds.
</td>
        </tr></table>

### IntentParameterData {:#IntentParameterData}
*Defined in [fuchsia.modular/intent.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/intent/intent.fidl#37)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>entity_reference</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>json</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>entity_type</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td></td>
        </tr></table>

### CreateModuleParameterInfo {:#CreateModuleParameterInfo}
*Defined in [fuchsia.modular/create_module_parameter_map.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/create_module_parameter_map.fidl#18)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>link_path</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#LinkPath'>LinkPath</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>create_link</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#CreateLinkInfo'>CreateLinkInfo</a></code>
            </td>
            <td></td>
        </tr></table>

### StoryPuppetMaster_SetStoryInfoExtra_Result {:#StoryPuppetMaster_SetStoryInfoExtra_Result}
*Defined in [fuchsia.modular/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#160)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#StoryPuppetMaster_SetStoryInfoExtra_Response'>StoryPuppetMaster_SetStoryInfoExtra_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ConfigureStoryError'>ConfigureStoryError</a></code>
            </td>
            <td></td>
        </tr></table>

### StoryCommand {:#StoryCommand}
*Defined in [fuchsia.modular/story_command.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_command.fidl#17)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>set_focus_state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#SetFocusState'>SetFocusState</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>add_mod</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#AddMod'>AddMod</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>remove_mod</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#RemoveMod'>RemoveMod</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_link_value</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#SetLinkValue'>SetLinkValue</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>focus_mod</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#FocusMod'>FocusMod</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_kind_of_proto_story_option</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#SetKindOfProtoStoryOption'>SetKindOfProtoStoryOption</a></code>
            </td>
            <td></td>
        </tr></table>

### ComponentScope {:#ComponentScope}
*Defined in [fuchsia.modular/scope.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/user_intelligence/scope.fidl#10)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>global_scope</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#GlobalScope'>GlobalScope</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>module_scope</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#ModuleScope'>ModuleScope</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>agent_scope</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#AgentScope'>AgentScope</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>story_scope</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html#StoryScope'>StoryScope</a></code>
            </td>
            <td></td>
        </tr></table>







