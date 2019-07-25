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
                <code>request&lt;<a class='link' href='#ComponentContext'>ComponentContext</a>&gt;</code>
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
                <code>request&lt;<a class='link' href='#EntityReferenceFactory'>EntityReferenceFactory</a>&gt;</code>
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
                <code><a class='link' href='#TaskInfo'>TaskInfo</a></code>
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
                <code><a class='link' href='#TaskInfo'>TaskInfo</a></code>
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

 This interface is used by the caller of ComponentContext::ConnectToAgent() to
 tell the framework that it is still interested in keeping this Agent running.

 The system counts AgentController connections and terminates this Agent if
 the count goes to zero.

## BaseShell {:#BaseShell}
*Defined in [fuchsia.modular/base_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/basemgr/base_shell.fidl#21)*

 This interface is implemented by a base shell. Dependencies are passed to it
 in Initialize() on startup. The base shell is also expected to implement
 Lifecycle in order to receive a Terminate() call on teardown.

 In one component instance there can only be one BaseShell service instance.
 The ViewOwner request is sent to the separate ViewProvider service. This way,
 the base shell may be implemented as a flutter component.

 Teardown may be initiated by the base shell calling
 BaseShellContext.Shutdown(), or by the system shutting down.

### Initialize {:#Initialize}


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



### GetAuthenticationUIContext {:#GetAuthenticationUIContext}

 This method may be invoked by the basemgr to request an
 AuthenticationUIContext. `request` will then be used to request the base
 shell to show login screen during a UserProvider.AddUser() or if a token
 needs to be refreshed.

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

 This interface allows the `BaseShell` to request capabilities from the
 `Basemgr` in a way that is more explicit about the services that are
 offered than a generic `ServiceProvider`.

### GetUserProvider {:#GetUserProvider}

 Acquires the user provider service, which is used to add/remove/list and
 authenticate users.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#UserProvider'>UserProvider</a>&gt;</code>
            </td>
        </tr></table>



### GetPresentation {:#GetPresentation}

 Acquires the presentation service, which is assumed to already be
 connected to the presenter.

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

 This requests the shutdown of the basemgr.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## UserProvider {:#UserProvider}
*Defined in [fuchsia.modular/user_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/basemgr/user_provider.fidl#13)*

 Given by the `Basemgr` to the `BaseShell` at Initialize() so the
 `BaseShell` can get information about the users of this device from the
 `Basemgr`, and act on the provided information (including extending the
 user database).

### AddUser {:#AddUser}

 Adds information of a user that can be used to authenticate her/him to this
 device. Once successfully added, the user can login to the same device via
 Login().

 `identity_provider` is the identity provider to use for identification.

 `device_name` is what the user wants to name the device. If null or empty
 the device's current hostname will be used.

 `account` is NULL if there was an error during identification and
 `error_code` is set.

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

 Removes information of a user from the local user database.

 `account_id` is received from either AddUser() or PreviousUsers().

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

 Uses the credentials provided in AddUser() to start a user session. This
 would mean syncing with the user's ledger instance and displaying a user
 shell with all of the user's stories.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>user_login_params</code></td>
            <td>
                <code><a class='link' href='#UserLoginParams'>UserLoginParams</a></code>
            </td>
        </tr></table>



### Login2 {:#Login2}

 DEPRECATED: For transitional purposes only.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>user_login_params</code></td>
            <td>
                <code><a class='link' href='#UserLoginParams2'>UserLoginParams2</a></code>
            </td>
        </tr></table>



### PreviousUsers {:#PreviousUsers}

 List of all users who have authenticated to this device in the past.

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

 An interface that provides clients with the ability to store and
 retrieve text.

### Push {:#Push}

 Pushes `text` onto the clipboard.

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

 Peeks at the current topmost item on the clipboard and returns
 it, or null if no such item exists.

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

 Provided to all component instances in their respective initialization
 information by the framework. For example, a Module gets it from its
 ModuleContext and an Agent gets it from its AgentContext.

### GetLedger {:#GetLedger}

 Gets the Ledger associated with this component. This ledger instance is
 unique to this component (nb. not the component instance) under this user.

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

 Used to start an agent in the user scope if it isn't already running, and
 connect to it.

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
                <code>request&lt;<a class='link' href='#AgentController'>AgentController</a>&gt;</code>
            </td>
        </tr></table>



### ConnectToAgentService {:#ConnectToAgentService}

 Connects to an agent that provides the given `request.service_name`, and
 then connects the given `request.channel` to that service.
 `request.agent_controller` must be kept alive until the service is no
 longer required.

 If an error is encountered, the `request.channel` will be closed with
 a status code, such as:
   * ZX_ERR_NOT_FOUND -- if a `request.handler` agent URL is not
     specified, and an agent for the `request.service_name` is not found
   * ZX_ERR_PEER_CLOSED -- if `request.service_name` is not available from
     the agent (either specified or discovered)

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code><a class='link' href='#AgentServiceRequest'>AgentServiceRequest</a></code>
            </td>
        </tr></table>



### ObtainMessageQueue {:#ObtainMessageQueue}

 Used to create or delete a message queue or retrieve an existing queue
 identified by `name`. `name` is local to the calling component instance.

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
                <code>request&lt;<a class='link' href='#MessageQueue'>MessageQueue</a>&gt;</code>
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

 Gets a MessageSender service that can be used to send a message to a queue
 identified by `queue_token`. Token for a MessageQueue is obtained from its
 GetToken() method. The token is unique within the scope of the user, i.e.
 it can be used by other component instances than the one that created the
 message queue.

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
                <code>request&lt;<a class='link' href='#MessageSender'>MessageSender</a>&gt;</code>
            </td>
        </tr></table>



### GetEntityResolver {:#GetEntityResolver}

 Gets the EntityResolver service, which can be used to resolve an entity
 reference to an Entity interface.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#EntityResolver'>EntityResolver</a>&gt;</code>
            </td>
        </tr></table>



### CreateEntityWithData {:#CreateEntityWithData}

 Creates a new entity from `type_to_data` such that duplicate types are
 overriden by subsequent entries.

 This is a useful way to represent small immutable entities without having
 to provide the entity using an Agent. The types and data together must be
 within 16KB in size.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>type_to_data</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#TypeToDataEntry'>TypeToDataEntry</a>&gt;</code>
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

 Gets the package name of this component.


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

 A message queue is a named, locally persistent FIFO data structure. Message
 queues are created, read from, and deleted by component instances through
 their ComponentContext service.

 A message queue is created by a component instance from its component context
 in order to receive messages in it.

 A sender token that identifies the queue can be obtained from the message
 queue connection and passed to other components. This enables the other
 component to send messages to the queue. A sender token does not allow a
 component to read messages from a queue.

 The name of a queue is local to the component instance, i.e. it can only be
 used by the component instance that created the queue to access it. The name
 can specifically be used to obtain a MessageReader connection for the message
 queue.

 The existence of message queues and their tokens is synchronized across
 devices, allowing components with instances on multiple devices to route
 messages within each device. For example, modules can use sender tokens on
 different devices and see those messages delivered to the agent instance on
 the same device. However, individual messages are local to a device.

### GetToken {:#GetToken}

 Gets a sender token associated with this queue. It can be used by other
 components to send messages to this queue.

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

 Registers a receiver for this MessageQueue. MessageReader.OnReceive() is
 called when there is an unread message. There can be at most one receiver
 registered for a message queue at any time. Registering a new receiver
 replaces the previous one.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>receiver</code></td>
            <td>
                <code><a class='link' href='#MessageReader'>MessageReader</a></code>
            </td>
        </tr></table>



## MessageSender {:#MessageSender}
*Defined in [fuchsia.modular/message_queue.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/component/message_queue.fidl#48)*

 Used to send a message to a message queue. The MessageSender connection is
 obtained from ComponentContext.GetMessageSender() using a queue token of the
 MessageQueue. The queue token is obtained by the component that created the
 message queue and is then passed to the other component through services
 specific to either component.

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

 A component instance may implement and register a MessageReader interface
 using MessageQueue.RegisterReceiver(). When there are new unread messages,
 they are sent to MessageReader.OnReceive(). TODO(vardhan): There is a
 conflict with C++ fidl bindings for 'MessageReceiver'. After that is fixed,
 rename this interface to MessageReceiver.

### OnReceive {:#OnReceive}

 Called when there is a new message to be received. Once an OnReceive()
 responds back, the message is acknowledged as having been received and the
 next one is sent when available. If a client's OnReceive() does not respond
 before the MessageReader interface is closed, then a future MessageReader
 for this message queue will receive the unacknowledged message again.

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

 Top-level service provider interface that vends services to read and write
 context data.

### GetReader {:#GetReader}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>client_info</code></td>
            <td>
                <code><a class='link' href='#ComponentScope'>ComponentScope</a></code>
            </td>
        </tr><tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ContextReader'>ContextReader</a>&gt;</code>
            </td>
        </tr></table>



### GetWriter {:#GetWriter}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>client_info</code></td>
            <td>
                <code><a class='link' href='#ComponentScope'>ComponentScope</a></code>
            </td>
        </tr><tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ContextWriter'>ContextWriter</a>&gt;</code>
            </td>
        </tr></table>



### GetContextDebug {:#GetContextDebug}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ContextDebug'>ContextDebug</a>&gt;</code>
            </td>
        </tr></table>



## ContextReader {:#ContextReader}
*Defined in [fuchsia.modular/context_reader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/context_reader.fidl#13)*

 Exposes access to Context values, each of which are explicitly named by a
 'topic'. Each topic has a known/pre-defined value representation.

 This interface is meant to be used in the scope of a single Fuchsia
 component.

### Subscribe {:#Subscribe}

 When any conditions that would cause the resulting set of context values
 selected by `query` to change, a ContextUpdate is sent to `listener`.

 The current state of values selected by `query` are sent to `listener`
 immediately.

 The subscription will continue to stay active as long as the `listener`
 handle is not closed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>query</code></td>
            <td>
                <code><a class='link' href='#ContextQuery'>ContextQuery</a></code>
            </td>
        </tr><tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='#ContextListener'>ContextListener</a></code>
            </td>
        </tr></table>



### Get {:#Get}

 Returns the current context state matching `query`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>query</code></td>
            <td>
                <code><a class='link' href='#ContextQuery'>ContextQuery</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>update</code></td>
            <td>
                <code><a class='link' href='#ContextUpdate'>ContextUpdate</a></code>
            </td>
        </tr></table>

## ContextListener {:#ContextListener}
*Defined in [fuchsia.modular/context_reader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/context_reader.fidl#59)*


### OnContextUpdate {:#OnContextUpdate}

 Receives a full snapshot of context state every time context is updated
 in such a way that results in a changed set of values for the ContextQuery
 used in the subscription for this listener.


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>update</code></td>
            <td>
                <code><a class='link' href='#ContextUpdate'>ContextUpdate</a></code>
            </td>
        </tr></table>



## ContextWriter {:#ContextWriter}
*Defined in [fuchsia.modular/context_writer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/context_writer.fidl#8)*


### CreateValue {:#CreateValue}

 Creates and returns a ContextValueWriter for a future value of `type`,
 allowing the client to set and update the contents at a later time.  The
 value is removed from the Context service when `value_writer` is closed or
 a connection error occurs.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value_writer</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ContextValueWriter'>ContextValueWriter</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#ContextValueType'>ContextValueType</a></code>
            </td>
        </tr></table>



### WriteEntityTopic {:#WriteEntityTopic}

 This method is here to make transitioning from topic-based context
 publishing to CreateValue() easier and will be removed eventually.
 Internally, calls CreateValue() with type = ContextValueType.ENTITY,
 and sets metadata.entity.topic = topic, unless WriteEntityTopic() was
 called already on this instance with the same `topic` value. In that case,
 performs an upate instead of adding a new value.

 Leaving `value` null removes the topic value from the Context service.


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

 Like ContextWriter.CreateValue(), but creates the new value as a child to
 this value.


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value_writer</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ContextValueWriter'>ContextValueWriter</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#ContextValueType'>ContextValueType</a></code>
            </td>
        </tr></table>



### Set {:#Set}

 Updates the content and/or metadata of this value. If either `content` or
 `metadata` are left null, the existing values will remain.

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
                <code><a class='link' href='#ContextMetadata'>ContextMetadata</a>?</code>
            </td>
        </tr></table>



## ContextDebug {:#ContextDebug}
*Defined in [fuchsia.modular/debug.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/debug.fidl#8)*


### Watch {:#Watch}

 The watch will stay active until the `listener` handle is closed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='#ContextDebugListener'>ContextDebugListener</a></code>
            </td>
        </tr></table>



### WaitUntilIdle {:#WaitUntilIdle}

 Waits until Context Engine has reached a steady state such that no further
 activity will occur unless acted upon from the outside.

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

 Called any time a value is added, updated or removed. Each element in
 `values` represents a single add, update or remove operation.  Values are
 guaranteed to appear before their children in the case that a parent and
 its child are included in the same update.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>values</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ContextDebugValue'>ContextDebugValue</a>&gt;</code>
            </td>
        </tr></table>



### OnSubscriptionsChanged {:#OnSubscriptionsChanged}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>subscription</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ContextDebugSubscription'>ContextDebugSubscription</a>&gt;</code>
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
                <code><a class='link' href='#EntityWriteStatus'>EntityWriteStatus</a></code>
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
                <code><a class='link' href='#EntityWatcher'>EntityWatcher</a></code>
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
                <code><a class='link' href='#EntityWriteStatus'>EntityWriteStatus</a></code>
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
                <code><a class='link' href='#EntityWatcher'>EntityWatcher</a></code>
            </td>
        </tr></table>



## EntityReferenceFactory {:#EntityReferenceFactory}
*Defined in [fuchsia.modular/entity_reference_factory.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/entity/entity_reference_factory.fidl#13)*

 Agents use this interface to create Entity references that can subsequently
 be dereferenced into an `Entity` interface using `EntityResolver`.
 Agents that create entity references must also expose an `EntityProvider`
 service in their application's outgoing services, so that agents can provide
 data for `Entity`s that they create. This interface is available through an
 agent's `AgentContext`.

### CreateReference {:#CreateReference}

 Agents call this to manufacture a reference for an Entity they will
 provide. Returns an opaque, persistable `entity_reference` that components
 can resolve into an `Entity` interface using `EntityResolver`. When data is
 requested from an `Entity` interface resolved from this `entity_reference`,
 the `cookie` associated with this `entity_reference` will be passed back to
 the `EntityProvider` of the Agent that originally created this reference.

 `cookie` should uniquely identify the `Entity` within the scope of the
 calling entity provider. For example, it may be used as the primary key
 value for a database.

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

 This interface is given to all components in their `ComponentContext`. Any
 component can resolve an entity reference into an `Entity`.

### ResolveEntity {:#ResolveEntity}

 Finds and binds `entity_request` to an Entity handle for the Entity
 referenced by `entity_reference`. If an error occurs, `entity_request`
 will be closed.

 This method is called by any component who wants to use an Entity using an
 entity reference. A component has to get an entity reference (directly or
 indirectly) from an agent, for example through some fidl interface. The
 agent will create an entity reference using EntityReferenceFactory. During
 entity resolution, that agent then provides data for the Entity
 through an EntityProvider service it exposes. Thus, any Agent that wishes
 to use EntityReferenceFactory to dispense entity references through its
 agent services MUST also implement the EntityProvider service.

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



## IntentHandler {:#IntentHandler}
*Defined in [fuchsia.modular/intent_handler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/intent/intent_handler.fidl#17)*

 The IntentHandler interface is exposed by modules which wish to handle
 intents on the behalf of other modules or agents.

 The modular framework expects any module which declares support for intent
 handling in its module manifest to expose IntentHandler in its outgoing
 services.

 Any time the framework receives an intent which is to be handled by a specific
 module its `IntentHandler` will be called with the intent it is meant to handle.

### HandleIntent {:#HandleIntent}

 Handles the provided intent. Any links referenced in the intent parameters
 will be in the namespace of the handling component, and can be retrieved via
 `ModuleContext.GetLink`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>intent</code></td>
            <td>
                <code><a class='link' href='#Intent'>Intent</a></code>
            </td>
        </tr></table>



## Lifecycle {:#Lifecycle}
*Defined in [fuchsia.modular/lifecycle.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/lifecycle/lifecycle.fidl#9)*

 An interface implemented by applications that wish to terminate gracefully.

### Terminate {:#Terminate}

 The client of this application has requested that this application
 terminate gracefully.

 If the application does not terminate itself in a timely manner, the client
 may forcibly terminate the application.

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
                <code>request&lt;<a class='link' href='#Link'>Link</a>&gt;</code>
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
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#ViewToken'>ViewToken</a></code>
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
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#ViewToken'>ViewToken</a></code>
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
                <code><a class='link' href='#SurfaceRelation'>SurfaceRelation</a></code>
            </td>
        </tr><tr>
            <td><code>layout</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ContainerLayout'>ContainerLayout</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>relationships</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ContainerRelationEntry'>ContainerRelationEntry</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>nodes</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ContainerNode'>ContainerNode</a>&gt;</code>
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
                <code>request&lt;<a class='link' href='#ComponentContext'>ComponentContext</a>&gt;</code>
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
                <code><a class='link' href='#StoryVisibilityState'>StoryVisibilityState</a></code>
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
                <code><a class='link' href='#OngoingActivityType'>OngoingActivityType</a></code>
            </td>
        </tr><tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#OngoingActivity'>OngoingActivity</a>&gt;</code>
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
                <code><a class='link' href='#ModuleState'>ModuleState</a></code>
            </td>
        </tr></table>

## ModuleResolver {:#ModuleResolver}
*Defined in [fuchsia.modular/module_resolver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module_resolver/module_resolver.fidl#8)*


### FindModules {:#FindModules}

 Finds Modules (contained in Fuchsia packages) that satisfy the constraints
 specified in `query`. Module resolution is done by matching the requested
 `query.action` and `query.parameter_constraints` (with both names and
 types) against actions and constraints specified in module manifests.

 If no results could be found, `response.results` will be empty.

 For detailed information on the resolution process, see
 docs/modular/module_resolution.md.


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
                <code><a class='link' href='#FocusRequestWatcher'>FocusRequestWatcher</a></code>
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
                <code>vector&lt;<a class='link' href='#FocusInfo'>FocusInfo</a>&gt;</code>
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
                <code><a class='link' href='#FocusWatcher'>FocusWatcher</a></code>
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
                <code><a class='link' href='#FocusInfo'>FocusInfo</a>?</code>
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

 This interface is implemented by a session shell and is used by the
 sessionmgr to hand to the session shell views of stories, or to notify that
 the view of a story is about to be closed.

### AttachView {:#AttachView}

 Displays the given story view. The story this view belongs to is
 identified by `view_id.story_id`.
 DEPRECATED.  For transitional purposes only.

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
                <code><a class='link' href='#ViewIdentifier'>ViewIdentifier</a></code>
            </td>
        </tr><tr>
            <td><code>view_holder_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#ViewHolderToken'>ViewHolderToken</a></code>
            </td>
        </tr></table>



### DetachView {:#DetachView}

 Instructs the session shell to detach the view identified by `view_id`
 that was previously provided by AttachView() from the UI of the session
 shell. The view will be closed soon after DetachView() returns, or when a
 timeout is reached.

 It is customary for the session shell to display a placeholder before a
 view is attached for a given view identifier, or after it was detached.

 If the story identified by `view_id.story_id` is about to be deleted, the
 Shell will observe a call to StoryProviderWatcher.OnDelete() sometime
 after DetachView() returns.

 If the session for which this session shell is responsible for is being
 terminated, or the session shell is stopped because it's replaced by
 another session shell, DetachView() will *not* be called at all, and the
 shell will rather observe a call to Lifecycle.Terminate().

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

## SessionShellContext {:#SessionShellContext}
*Defined in [fuchsia.modular/session_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/session/session_shell.fidl#59)*

 This interface allows a `SessionShell` to request capabilities from its
 creator in a way that is more explicit about the services that are
 offered than a generic `ServiceProvider`.

### GetAccount {:#GetAccount}

 The account associated with the currently logged-in user. It's NULL if
 logged into GUEST mode.

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
                <code>request&lt;<a class='link' href='#ComponentContext'>ComponentContext</a>&gt;</code>
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
                <code>request&lt;<a class='link' href='#FocusController'>FocusController</a>&gt;</code>
            </td>
        </tr></table>



### GetFocusProvider {:#GetFocusProvider}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#FocusProvider'>FocusProvider</a>&gt;</code>
            </td>
        </tr></table>



### GetLink {:#GetLink}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Link'>Link</a>&gt;</code>
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
                <code>request&lt;<a class='link' href='#StoryProvider'>StoryProvider</a>&gt;</code>
            </td>
        </tr></table>



### GetVisibleStoriesController {:#GetVisibleStoriesController}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#VisibleStoriesController'>VisibleStoriesController</a>&gt;</code>
            </td>
        </tr></table>



### Logout {:#Logout}

 Requests logout of the user. This causes the basemgr to tear down the
 `Sessionmgr` instance of the user.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## SessionShellPresentationProvider {:#SessionShellPresentationProvider}
*Defined in [fuchsia.modular/session_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/session/session_shell.fidl#87)*

 Session shell provides this service to the framework which may plumb it to
 different subscribers, such as story shell and intelligence provider.

 EXPERIMENTAL Service that allows consumers of a given story to get a
 connection to a Presentation, and visual state services provided by the user
 shell. This allows story shell implementations to coordinate event and focus
 handling. An analog mechanism exists between BaseShell and SessionShell.

### GetPresentation {:#GetPresentation}

 When a StoryShell calls StoryShellContext.GetPresentation(), this request
 arrives here.

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

 When a StoryShell calls StoryShellContext.WatchVisualState(), this request
 arrives here.

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



## Link {:#Link}
*Defined in [fuchsia.modular/link.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/link.fidl#49)*

 This interface is implemented by the story runner. The ModuleContext service
 acts as a factory for it.

 An instance of Link holds one of two types of values:

 (1) A JSON string that can be modified incrementally or completely
     overwritten, depending on the use of Set() and Update(). The JSON string
     is set to "null" when the Link is created.

 (2) An entity reference that can be set or retrieved with SetEntity() and
     GetEntity().

 Each Module instance receives one Link instance for each parameter of its
 action template in its ModuleContext. It receives its ModuleContext in
 Module.Initialize() or in its service namespace. The Module can access its
 Links by calling ModuleContext.GetLink() with the intent parameter name as
 the link name. These instances are shared with the parent Module if there is
 any, or with the StoryController client if the Module is a top level Module
 of a Story. A Module can create additional Link instances by calling
 ModuleContext.GetLink() with any other link name. Why would it do that? To
 share the new Link instance with Modules it requests to start in turn, or to
 record its own state in the story record, so that it is transferred to other
 devices that run the same story, or to persist it for later resumption of the
 story.

 A client may obtain another handle to the same Link instance by calling
 GetLink() with the same name again.

 A client of Link can set the JSON string stored in the instance and register
 a handler (an implementation of the LinkWatcher interface) to be notified of
 changes to the JSON string in the Link. A client may or may not be notified
 of changes it itself makes to the Link value, depending on whether it
 registers with WatchAll() or Watch(), respectively. If the client registers
 with Watch(), then it will not be notified of changes made through the same
 Link connection.

 No service name: returned from ModuleContext.GetLink().

### Get {:#Get}

 Gets the value at the given `path`, which is represented using the JSON
 Pointer specification (https://tools.ietf.org/html/rfc6901).

 `json_data` is a UTF8 encoded string representing valid JSON.

 Returns null if `path` does not exist. Returns the entire JSON object
 if `path` is either null or an empty array. Returns the string "null" if
 the link is empty.

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

 Set() overwrites the value/object/array at the given `path`. Set also
 overwrites any values or arrays as necessary to ensure that `path` exists.
 The `json_data` parameter must be a UTF8 encoded JSON string.
 Either pass "null" to set the value to null, or use Erase to
 completely remove a member of an object. To replace the root, pass null for
 `path`.

 This call notifies Watchers, although this may be skipped if nothing
 changed.

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

 Erases the object member at the given `path`. If the path is not found or
 does not match the current structure of the JSON, the path will not be
 created and the call is ignored. The `path` parameter cannot be null or
 zero length because the root is a value, not a key. This call notifies
 Watchers, although this may be skipped if nothing changed.

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

 Returns the entity reference in this link. If no entity reference is
 present, returns a null fidl string.

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

 Sets this to be an Entity Link with the given `entity_reference`. The
 existing value of the link is overwritten. If `entity_reference` is null,
 then any existing value in the link is overwritten with the JSON string
 "null".

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

 Registers a watcher, which is notified whenever the document changes. This
 watcher will not be invoked for changes caused by calls made on this
 handle. The Notify() callback method will be immediately invoked with the
 value in the Link, even if it's empty.

 The LinkWatcher connection will be closed if the owning Link handle closed.
 All connections to a Link and LinkWatcher are closed once the story the
 link belongs to is stopped.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#LinkWatcher'>LinkWatcher</a></code>
            </td>
        </tr></table>



### WatchAll {:#WatchAll}

 Like Watch(), but the watcher is notified also of changes made through the
 same handle as the watcher is registered on.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#LinkWatcher'>LinkWatcher</a></code>
            </td>
        </tr></table>



### Sync {:#Sync}

 Waits for the completion of methods previously invoked on the same
 connection. Allows to create sequentiality across service instances without
 giving every method an empty return value. Nb. this makes no guarantees
 about sequentiality with methods invoked on different connections, even to
 the same Link instance.

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

 This interface is implemented by a client of Link.

 The Notify() method is invoked whenever the Link changes. The entire JSON
 string in the Link will be sent. In other words, this isn't an incremental
 notification. `json` cannot be null because an empty Link is the valid JSON
 document "null".

 No service name: created by Module.

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
                <code>request&lt;<a class='link' href='#StoryPuppetMaster'>StoryPuppetMaster</a>&gt;</code>
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
                <code>vector&lt;<a class='link' href='#StoryCommand'>StoryCommand</a>&gt;</code>
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
                <code><a class='link' href='#ExecuteResult'>ExecuteResult</a></code>
            </td>
        </tr></table>

### SetCreateOptions {:#SetCreateOptions}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_options</code></td>
            <td>
                <code><a class='link' href='#StoryOptions'>StoryOptions</a></code>
            </td>
        </tr></table>



### SetStoryInfoExtra {:#SetStoryInfoExtra}


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

## StoryController {:#StoryController}
*Defined in [fuchsia.modular/story_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_controller.fidl#14)*

 Used by the clients of StoryProvider (SessionShell) to interact with a single
 story. Created by StoryProvider.

 If `StoryController` is closed, the `StoryState` associated with this story
 does not change.

### GetInfo {:#GetInfo}

 Gets information associated with the story.

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

### RequestStart {:#RequestStart}

 Requests to run the story controlled by this `StoryController` instance.
 When the story starts, if not yet running, the view of the newly started
 story shell will be passed in a call to SessionShell.AttachView().

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Stop {:#Stop}

 Requests to stop the story controlled by this `StoryController`. If Start()
 requests are pending when this request is issued, the request is queued
 until the Start() requests complete. Before stopping the story, a snapshot
 of the story will be taken and saved. Returns when the story is stopped.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### TakeAndLoadSnapshot {:#TakeAndLoadSnapshot}

 Creates a new view with the given `view_owner` request to display
 snapshots. Takes a snapshot for the story controlled by this
 `StoryController` and then loads the snapshot to the created view such that
 it is rendered. The callback will be invoked once the view has been created
 and the snapshot has been loaded.

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

 Registers a watcher for changes of the story state.

 Note that stories can stop themselves at any time and it is advisable
 for the holder of a StoryController to provide a watcher.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#StoryWatcher'>StoryWatcher</a></code>
            </td>
        </tr></table>



### GetActiveModules {:#GetActiveModules}

 DEPRECATED

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
                <code>vector&lt;<a class='link' href='#ModuleData'>ModuleData</a>&gt;</code>
            </td>
        </tr></table>

### GetModules {:#GetModules}

 DEPRECATED

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
                <code>vector&lt;<a class='link' href='#ModuleData'>ModuleData</a>&gt;</code>
            </td>
        </tr></table>

### GetModuleController {:#GetModuleController}

 DEPRECATED
 (metadata about, and requesting changes to runtime state).

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
                <code>request&lt;<a class='link' href='#ModuleController'>ModuleController</a>&gt;</code>
            </td>
        </tr></table>



### GetLink {:#GetLink}

 DEPRECATED

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>link_path</code></td>
            <td>
                <code><a class='link' href='#LinkPath'>LinkPath</a></code>
            </td>
        </tr><tr>
            <td><code>link</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Link'>Link</a>&gt;</code>
            </td>
        </tr></table>



## StoryWatcher {:#StoryWatcher}
*Defined in [fuchsia.modular/story_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_controller.fidl#57)*

 Implemented by the client calling StoryController.Watch().

### OnStateChange {:#OnStateChange}

 Called with the current state right after registration, and subsequently
 when the state changes.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>new_state</code></td>
            <td>
                <code><a class='link' href='#StoryState'>StoryState</a></code>
            </td>
        </tr></table>



### OnModuleAdded {:#OnModuleAdded}

 DEPRECATED

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>module_data</code></td>
            <td>
                <code><a class='link' href='#ModuleData'>ModuleData</a></code>
            </td>
        </tr></table>



### OnModuleFocused {:#OnModuleFocused}

 DEPRECATED

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

 Implemented by the client calling StoryController.GetActiveLinks().

 DEPRECATED: StoryController is only to be used for Story concepts
 (metadata about, and requesting changes to runtime state).

### OnNewLink {:#OnNewLink}

 Called when a link becomes active in the story, i.e. when it is loaded into
 memory and connected with modules and watchers. After this notification,
 the Link can be obtained with GetLink() and further notifications can be
 obtained from watchers on the Link and connection error handlers on the
 LinkWatcher.

 Note that the Link remains active until there are no connections to it
 left. Hence in order to obtain a notification when the Link becomes
 inactive, a client must give up the Link connection after registering a
 LinkWatcher, and listen for the LinkWatcher connection to go down.

 This is EXPERIMENTAL. We certainly can make this simpler once we know it is
 what we need.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>link_path</code></td>
            <td>
                <code><a class='link' href='#LinkPath'>LinkPath</a></code>
            </td>
        </tr></table>



## StoryProvider {:#StoryProvider}
*Defined in [fuchsia.modular/story_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_provider.fidl#14)*

 Sessionmgr passes a connection to this service to the SessionShell so it can
 operate on stories for the user. It is also passed to other services that
 monitor or manipulate stories, specifically the maxwell services.

 Closing a `StoryProvider` connection has no effect on the state of the
 framework.

### GetStories {:#GetStories}

 Returns a list of existing stories. If `watcher` is provided, the client will
 be notified of story changes (new stories, deleted stories, runtime
 state changes).

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

### GetStoryInfo {:#GetStoryInfo}

 Requests detailed information about the given story. If the story doesn't
 exist, returns null.

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

### GetController {:#GetController}

 Obtains a controller for a previously created story identified by its story
 ID. Obtaining the controller doesn't run it yet. If the story doesn't
 exist, the interface request is closed.

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



### PreviousStories {:#PreviousStories}

 Returns info of known stories.
 DEPRECATED: In favor of GetStories().

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
                <code>vector&lt;<a class='link' href='#StoryInfo'>StoryInfo</a>&gt;</code>
            </td>
        </tr></table>

### Watch {:#Watch}

 Registers a watcher for changes in the story collection.
 DEPRECATED: In favor of GetStories().

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#StoryProviderWatcher'>StoryProviderWatcher</a></code>
            </td>
        </tr></table>



### WatchActivity {:#WatchActivity}

 Registers a watcher for ongoing story activity. Upon registration,
 StoryActivityWatcher.OnStoryActivity() will be called to update clients
 with the initial data. See StoryActivityWatcher for motivations.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#StoryActivityWatcher'>StoryActivityWatcher</a></code>
            </td>
        </tr></table>



## StoryProviderWatcher {:#StoryProviderWatcher}
*Defined in [fuchsia.modular/story_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_provider.fidl#44)*

 Implemented by clients of StoryProvider.

### OnChange {:#OnChange}

 Called in three different situations:

  * Immediately when a new watcher is registered with one OnChange()
    invocation with the current infor and state of each story known on the
    current device.

  * Every time a change to StoryInfo is applied to the record of the story
    kept on the current device, including a new story created on another
    device becoming known on this device for the first time.

  * Every time the StoryState of the story changes on this device. The
    StoryState on another device of a story known on this device is not made
    known on this device.

  * Every time the StoryVisibilityState of the story changes on this device.
    The StoryVisibilityState on another device of a story known on this
    device is not made known on this device.

    I.e. if the story is started or stopped on *another* device, it does
    *not* cause an OnChange() call on *this* device. Cf. OnDelete() below.

 The ID of the story the notifications are about are part of StoryInfo.

 `story_state` is STOPPED if the story was just created or just became known
 on this device and was not yet started on the current device. It's RUNNING
 when the story is started on the current device.

 `story_visibility_state` is DEFAULT until a mod on the current device
 requests for the visibility state to be changed.

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



### OnDelete {:#OnDelete}

 Called when a story record is permanently deleted. The deletion could
 have originated on this or on another device.

 If the story is running on this device at the time it is deleted,
 OnChange() will not be called first.

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

 Implemented by clients of StoryProvider in order to inform them about ongoing
 activities in stories. `activities` is the entire list of ongoing activities
 (represented by its type) within the story by the given `story_id`. If
 `activities` is empty, it means that there is no ongoing activity within the
 story.

 Clients can expect this event whenever there is a newly started/stopped
 ongoing activity, as well as when the client first registers for updates
 via StoryProvider.WatchActivity(). `activities` can contain duplicate
 OngoingActivityType's, ex. if a story is playing 2 videos at once.

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
                <code>vector&lt;<a class='link' href='#OngoingActivityType'>OngoingActivityType</a>&gt;</code>
            </td>
        </tr></table>



## StoryShell {:#StoryShell}
*Defined in [fuchsia.modular/story_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell.fidl#21)*

 This interface is implemented by a story shell. Dependencies are passed to it
 in Initialize() on startup. The story shell is also expected to implement
 Lifecycle in order to receive a Terminate() call on teardown.

 In one component instance there can only be one StoryShell service instance.
 The view token is sent to the separate View service. This way, the story
 shell may be implemented as a flutter component.

 Teardown may occur via the session shell calling StoryController.Stop(), the
 sessionmgr being terminated, or by the system shutting down.

### Initialize {:#Initialize}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_shell_context</code></td>
            <td>
                <code><a class='link' href='#StoryShellContext'>StoryShellContext</a></code>
            </td>
        </tr></table>



### AddSurface {:#AddSurface}

 Adds a new Surface and its corresponding view to be displayed by the
 StoryShell. More context that allows the story shell to decide how
 to layout will be added later. Also, interface to influence life cycle and
 focus is obviously missing.
 `view_connection` the new view and the associated Surface ID.
 `surface_info` metadata relating to the Surface.

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



### AddSurface2 {:#AddSurface2}

 DEPRECATED.  For transition purposes only.

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



### AddSurface3 {:#AddSurface3}

 For transition purposes only.

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



### FocusSurface {:#FocusSurface}

 Focuses the surface with surface_id, bringing it to the foreground.

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

 Defocuses the surface with surface_id, dismissing it to the background.

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

 Adds a container, with corresponding container layouts to the story.
 Optionally provide a parent_id to connect to, if omitted adds the
 Container node as the root of a new tree in the Story
 DEPRECATED

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
                <code><a class='link' href='#SurfaceRelation'>SurfaceRelation</a></code>
            </td>
        </tr><tr>
            <td><code>layout</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ContainerLayout'>ContainerLayout</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>relationships</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ContainerRelationEntry'>ContainerRelationEntry</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>views</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ContainerView'>ContainerView</a>&gt;</code>
            </td>
        </tr></table>



### AddContainer2 {:#AddContainer2}

 DEPRECATED.  For transition purposes only.

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
                <code><a class='link' href='#SurfaceRelation'>SurfaceRelation</a></code>
            </td>
        </tr><tr>
            <td><code>layout</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ContainerLayout'>ContainerLayout</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>relationships</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ContainerRelationEntry'>ContainerRelationEntry</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>views</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ContainerView2'>ContainerView2</a>&gt;</code>
            </td>
        </tr></table>



### OnSurfaceFocused {:#OnSurfaceFocused}

 Notify when a Surface is focused in the story. The focus could be from
 a user interaction or requested by the framework through
 StoryController#FocusModule.
 EXPERIMENTAL



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

 Remove the Surface with surface_id from the StoryShell entirely. This is
 final. The Surface is removed from the graph. If necessary, the
 associated Surface is defocused. There is no expectation that
 DefocusSurface is called before this.

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

 Reconnect the view in viewConnection.

 Called to reconnect views that have previously been added to the story
 shell via addSurface, and then disconnected. A ViewTokenPair is created
 and the View token is given to the child view.  The ViewHolder token
 is notified if the View is destroyed before it is connected.  Once the
 ViewHolder has been created using a Scenic `Session`, the Session will be
 notified when the view is available, if it becomes unavailable, or if
 it is disconnected.
 If a surface with a disconnected view is to be shown again, ReconnectView
 is called.

 E.g. called in response to StoryShell calling RequestView().

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_connection</code></td>
            <td>
                <code><a class='link' href='#ViewConnection'>ViewConnection</a></code>
            </td>
        </tr></table>



### ReconnectView2 {:#ReconnectView2}

 DEPRECATED.  For transition purposes only.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_connection</code></td>
            <td>
                <code><a class='link' href='#ViewConnection2'>ViewConnection2</a></code>
            </td>
        </tr></table>



### UpdateSurface {:#UpdateSurface}

 Update the surface
 This is called when the intent is to update the surface metadata in the
 story graph in place. Any fields, except for the surface_id can be
 updated. If no value or null is passed for a field it remains unchanged.
 This includes the `view_holder_token` inside the connection.

 E.g called when an intent resolves to a module that is known by the
 caller to already be running, to update associated metadata.

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



### UpdateSurface2 {:#UpdateSurface2}

 DEPRECATED.  For transition purposes only.

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



### UpdateSurface3 {:#UpdateSurface3}

 For transition purposes only.

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



## StoryShellContext {:#StoryShellContext}
*Defined in [fuchsia.modular/story_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell.fidl#188)*

 This interface provides the StoryShell instance with everything it needs to
 know or be able to do about the Story. Not much right now, but we expect this
 to increase.

### GetPresentation {:#GetPresentation}

 Requests a Presentation connection from the SessionShell. See
 SessionShellPresenationProvider in session_shell.fidl.

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

 Starts watching Story shell's visual state.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#StoryVisualStateWatcher'>StoryVisualStateWatcher</a></code>
            </td>
        </tr></table>



### GetLink {:#GetLink}

 Gets a Link instance that the story shell can use for persisting metadata.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Link'>Link</a>&gt;</code>
            </td>
        </tr></table>



### RequestView {:#RequestView}

 Requests a view for a Surface.
 Requests that a view for `surface_id` is provided through
 StoryShell.ReconnectView().

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

 Notification that the Surface is no longer on screen.

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
*Defined in [fuchsia.modular/story_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell.fidl#209)*

 Implemented by StoryShell to get notified about visual state changes.

### OnVisualStateChange {:#OnVisualStateChange}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>visual_state</code></td>
            <td>
                <code><a class='link' href='#StoryVisualState'>StoryVisualState</a></code>
            </td>
        </tr></table>



## StoryShellFactory {:#StoryShellFactory}
*Defined in [fuchsia.modular/story_shell_factory.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell_factory.fidl#11)*

 StoryShellFactory creates or returns an existing `StoryShell` for a particular story.
 This is intended to be implemented by session shells that want to implement
 StoryShell functionality themselves.

### AttachStory {:#AttachStory}

 Requests a StoryShell for the story with the given `story_id`.

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



### DetachStory {:#DetachStory}

 Instructs the session shell to teardown the story shell with the given `story_id`.
 This will be called before the story is stopped.

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

 A container for component-scoped services. This contains any and all
 services needed by any sort of Module/Agent.

### GetContextReader {:#GetContextReader}

 These are just here for illustrative purposes, and are not a complete
 list.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>context_reader</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ContextReader'>ContextReader</a>&gt;</code>
            </td>
        </tr></table>



### GetContextWriter {:#GetContextWriter}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>context_writer</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ContextWriter'>ContextWriter</a>&gt;</code>
            </td>
        </tr></table>



## UserIntelligenceProvider {:#UserIntelligenceProvider}
*Defined in [fuchsia.modular/user_intelligence_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/user_intelligence/user_intelligence_provider.fidl#10)*


### GetComponentIntelligenceServices {:#GetComponentIntelligenceServices}

 Creates an `IntelligenceServices` scoped to a specific Component,
 identified by `scope`.

 NOTE: Eventually `component_id` will become more complex, specifying
 information needed to evaluate access-control policies for downstream
 services.

 ANOTHER NOTE: `IntelligenceServices` is a short-term "big bucket" in which
 to put any and all services that are to be exposed to Agents and Modules.
 Once our understanding of the needs of Agents/Modules is clearer, we
 should break the bucket apart.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>scope</code></td>
            <td>
                <code><a class='link' href='#ComponentScope'>ComponentScope</a></code>
            </td>
        </tr><tr>
            <td><code>services</code></td>
            <td>
                <code>request&lt;<a class='link' href='#IntelligenceServices'>IntelligenceServices</a>&gt;</code>
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

 The `ComponentContext` is used to create agents and use message queues.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>user_intelligence_context</code></td>
            <td>
                <code><a class='link' href='#ComponentContext'>ComponentContext</a></code>
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

 A standard set of services provided to all agents at startup,
 along with services particuarly for this agent.

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
                <code><a class='link' href='#TriggerCondition'>TriggerCondition</a></code>
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



 Used to specify arguments to log into a user session.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>account_id</code></td>
            <td>
                <code>string?</code>
            </td>
            <td> `account_id` is received from either AddUser() or PreviousUsers(). It
 can be NULL which means logging-in using incognito mode.
</td>
            <td>No default</td>
        </tr>
</table>

### UserLoginParams2 {:#UserLoginParams2}
*Defined in [fuchsia.modular/user_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/basemgr/user_provider.fidl#55)*



 DEPRECATED, for backwards compatibility only


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>account_id</code></td>
            <td>
                <code>string?</code>
            </td>
            <td> `account_id` is received from either AddUser() or PreviousUsers(). It
 can be NULL which means logging-in in an incognito mode.
</td>
            <td>No default</td>
        </tr>
</table>

### TypeToDataEntry {:#TypeToDataEntry}
*Defined in [fuchsia.modular/component_context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/component/component_context.fidl#91)*



 Used by ComponentContext.CreateEntityWithData().


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



 Used to pass around configuration references to apps such as user
 shell, base shell, story shell.


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
                <code>vector&lt;<a class='link' href='#ContextQueryEntry'>ContextQueryEntry</a>&gt;</code>
            </td>
            <td> A map of ContextSelector structs. The keys are specified by the client.
 Each key gets a corresponding entry in `ContextUpdate.values` when it is
 generated in response to this query.
</td>
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
                <code><a class='link' href='#ContextSelector'>ContextSelector</a></code>
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
                <code><a class='link' href='#ContextMetadata'>ContextMetadata</a>?</code>
            </td>
            <td> A partial metadata struct. Any metadata value given in `meta` restricts
 the set of values in the eventual ContextUpdate to include only those
 whose metadata match values given.

 A null `meta` will match any value of the given `type`. Use this sparingly
 as a full update could become quite large.

 For example, to select all context values in a given story, one would
 specify:
    meta.value["story"]["id"] = "..."
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#ContextValueType'>ContextValueType</a></code>
            </td>
            <td> A string specifying the type of context object to return.
</td>
            <td>No default</td>
        </tr>
</table>

### ContextUpdate {:#ContextUpdate}
*Defined in [fuchsia.modular/context_reader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/context_reader.fidl#72)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>values</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ContextUpdateEntry'>ContextUpdateEntry</a>&gt;</code>
            </td>
            <td> A list of ContextValue for each key in `ContextQuery.selector`. An empty
 list means no values matched the given ContextSelector.
</td>
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
                <code>vector&lt;<a class='link' href='#ContextValue'>ContextValue</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ContextDebugValue {:#ContextDebugValue}
*Defined in [fuchsia.modular/debug.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/debug.fidl#29)*



 Represents a single update to a value. If `value` is omitted, the value with
 `id` was deleted.


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
                <code><a class='link' href='#ContextValue'>ContextValue</a>?</code>
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
                <code><a class='link' href='#SubscriptionDebugInfo'>SubscriptionDebugInfo</a>?</code>
            </td>
            <td> These are null when describing a subscription that was removed, although
 it's safe to condition only on `query`.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>query</code></td>
            <td>
                <code><a class='link' href='#ContextQuery'>ContextQuery</a>?</code>
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
                <code><a class='link' href='#ComponentScope'>ComponentScope</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ContextMetadata {:#ContextMetadata}
*Defined in [fuchsia.modular/metadata.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/context/metadata.fidl#18)*



 This struct serves two purposes. It is:

 1) Used to expose metadata along with each context node when interfacing
 with clients either publishing, or retieving, context values.

 2) Used while getting or querying for context values from a ContextReader to
 restrict the set of values returned by partially specifying a
 ContextMetadata struct.



<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>story</code></td>
            <td>
                <code><a class='link' href='#StoryMetadata'>StoryMetadata</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>mod</code></td>
            <td>
                <code><a class='link' href='#ModuleMetadata'>ModuleMetadata</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>entity</code></td>
            <td>
                <code><a class='link' href='#EntityMetadata'>EntityMetadata</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>link</code></td>
            <td>
                <code><a class='link' href='#LinkMetadata'>LinkMetadata</a>?</code>
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
                <code><a class='link' href='#FocusedState'>FocusedState</a>?</code>
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
                <code><a class='link' href='#FocusedState'>FocusedState</a>?</code>
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
            <td> These fields are identical to those in modular.LinkPath. Can't use
 modular.LinkPath directly because depending on lib/modular/fidl:link_path
 causes issues with Dart bindings (they try to import the file from the
 wrong package name), and depending on lib/modular/fidl causes a dependency
 cycle (lib/context -> lib/module -> lib/user_intelligence -> lib/context).

</td>
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



 bool type cannot be made optional (in StoryMetadata above), so we cannot
 differentiate between an unspecified value and false. So we have to create a
 struct with an enum in it to represent the boolean states, so that we can
 allow it to be null.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#FocusedStateState'>FocusedStateState</a></code>
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
                <code><a class='link' href='#ContextValueType'>ContextValueType</a></code>
            </td>
            <td> The type of value this describes.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>content</code></td>
            <td>
                <code>string?</code>
            </td>
            <td> If `type` == ContextType.ENTITY, contains the JSON encoded representation
 of the Entity's content.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>meta</code></td>
            <td>
                <code><a class='link' href='#ContextMetadata'>ContextMetadata</a></code>
            </td>
            <td> All metadata for the node. When this ContextValue is included in a
 ContextUpdate, `meta` will contain a merged view of metadata that is
 inclusive of all of this value node's ancestors.
</td>
            <td>No default</td>
        </tr>
</table>

### Intent {:#Intent}
*Defined in [fuchsia.modular/intent.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/intent/intent.fidl#11)*



 The Intent struct is a runtime descriptor for an abstract action to be initiated
 in Fuchsia. For details please see docs/intent.md.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>action</code></td>
            <td>
                <code>string?</code>
            </td>
            <td> The name of the action represented by this Intent.

 This is nullable for backwards compatibility.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>handler</code></td>
            <td>
                <code>string?</code>
            </td>
            <td> An explicit handler for the Intent. Specified as the component URL of the
 module.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>parameters</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#IntentParameter'>IntentParameter</a>&gt;?</code>
            </td>
            <td> The parameters that will be passed to the handler of `action`.
</td>
            <td>No default</td>
        </tr>
</table>

### IntentParameter {:#IntentParameter}
*Defined in [fuchsia.modular/intent.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/intent/intent.fidl#28)*



 A struct representing a parameter that is passed to the handler of an Intent's
 Action.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string?</code>
            </td>
            <td> The name of the parameter. The handler (i.e. selected mod) will be provided
 with the data for this parameter under a link called `name`.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='#IntentParameterData'>IntentParameterData</a></code>
            </td>
            <td> The data that will be passed to the intent handler.
</td>
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
                <code><a class='link' href='#ModuleParameterMap'>ModuleParameterMap</a></code>
            </td>
            <td> Contains the mapping of Mod parameter name to Link instances for this mod.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>module_source</code></td>
            <td>
                <code><a class='link' href='#ModuleSource'>ModuleSource</a></code>
            </td>
            <td> The way in which this Module instance was first started in the story,
 either by request from another Module instance (INTERNAL) or by request
 from outside the story (i.e. by suggestion from an agent - EXTERNAL).
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>surface_relation</code></td>
            <td>
                <code><a class='link' href='#SurfaceRelation'>SurfaceRelation</a>?</code>
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
                <code><a class='link' href='#Intent'>Intent</a>?</code>
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
                <code>vector&lt;<a class='link' href='#ModuleParameterMapEntry'>ModuleParameterMapEntry</a>&gt;</code>
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
                <code><a class='link' href='#LinkPath'>LinkPath</a></code>
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
                <code>vector&lt;<a class='link' href='#IntentFilter'>IntentFilter</a>&gt;?</code>
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
                <code>vector&lt;<a class='link' href='#ParameterConstraint'>ParameterConstraint</a>&gt;</code>
            </td>
            <td> Includes the name and types of entities for the parameters required to
 execute specified [action].
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>action_display</code></td>
            <td>
                <code><a class='link' href='#ActionDisplay'>ActionDisplay</a></code>
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



 Mirrors the information present in a Intent. Where a Intent is meant to
 interface between Modules and the Framework, this structure is specific to
 the interface between the Framework and the ModuleResolver.

 In that role, it has references to structures and concepts that are only
 visible within the abstraction layer of the Framework.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>handler</code></td>
            <td>
                <code>string?</code>
            </td>
            <td> The handler is a module URL; if the handler is specified, the search for
 (action, parameter_constraints) is scoped within the specified handler.
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

### FindModulesResult {:#FindModulesResult}
*Defined in [fuchsia.modular/module_resolver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/module_resolver/module_resolver.fidl#56)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>module_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The ID of the Module. For now, this is the URL of the Module binary.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>manifest</code></td>
            <td>
                <code><a class='link' href='#ModuleManifest'>ModuleManifest</a>?</code>
            </td>
            <td> The Module's manifest file (see docs/manifests/module.md).
</td>
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



 Identifies a view provided to a session shell. The values of the `story_id`
 field match those used in the `StoryProvider` interface, allowing
 identification of the same story across interfaces.

 This is a struct rather than a naked string to allow for future evolution of
 the identifier without changing the `SessionShell` API itself.


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



 Defines the attributes for a Link when the Link is created.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>initial_data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
            <td> Passed as root_json argument to StoryProvider.CreateStoryWithInfo()
 Link.Set() to set the value in the root link of the new Story's primary
 module.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>allowed_types</code></td>
            <td>
                <code><a class='link' href='#LinkAllowedTypes'>LinkAllowedTypes</a>?</code>
            </td>
            <td> If `allowed_types` is null, the Link contains JSON. No schema validation
 is performed.
</td>
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
            <td> The Link must contain an Entity (see Link.SetEntity()) that has at least
 one of `allowed_entity_types` in its `Entity.GetTypes()` return value.

 If empty, allows any Entity type.
</td>
            <td>No default</td>
        </tr>
</table>

### CreateModuleParameterMapInfo {:#CreateModuleParameterMapInfo}
*Defined in [fuchsia.modular/create_module_parameter_map.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/create_module_parameter_map.fidl#8)*



 Module parameters are named pointers to link instances.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>property_info</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#CreateModuleParameterMapEntry'>CreateModuleParameterMapEntry</a>&gt;?</code>
            </td>
            <td> Contains instructions to create each name in the parameter map.
</td>
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
                <code><a class='link' href='#CreateModuleParameterInfo'>CreateModuleParameterInfo</a></code>
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



 Adds a mod described by `intent` to the story with name `mod_name`. If
 `mod_name` already exists in the story, the mod is updated.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>mod_name</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td> The name of the mod within the story. The mod's name acts as the unique
 ID of the mod, scoped to the story in which it is contained. Since
 AddMod is reused for observation and mod names are vector<string>
 inside the framework, they are vector<string> here as well.

 Clients should treat the full vector as a single opaque value.

 Clients should provide `mod_name_transitional` instead.
 If both are provided, `mod_name` is ignored.

</td>
            <td>No default</td>
        </tr><tr>
            <td><code>mod_name_transitional</code></td>
            <td>
                <code>string?</code>
            </td>
            <td> The name of the mod within the story. This should be used instead of
 `mod_name`. If provided, it is equivalent to passing `mod_name` with
 a single item. If both are provided, `mod_name` is ignored.

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
            <td> `surface_relation` defines the visual relationship between this mod and the
 mod at `surface_parent_mod_name`.
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

### RemoveMod {:#RemoveMod}
*Defined in [fuchsia.modular/story_command.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_command.fidl#73)*



 Removes the mod under `mod_name` from the story.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>mod_name</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td> The name of the mod within the story.

 Clients should provide `mod_name_transitional` instead.
 If both are provided, `mod_name` is ignored.

</td>
            <td>No default</td>
        </tr><tr>
            <td><code>mod_name_transitional</code></td>
            <td>
                <code>string?</code>
            </td>
            <td> The name of the mod within the story. This should be used instead of
 `mod_name`. If provided, it is equivalent to passing `mod_name` with
 a single item. If both are provided, `mod_name` is ignored.

</td>
            <td>No default</td>
        </tr>
</table>

### SetLinkValue {:#SetLinkValue}
*Defined in [fuchsia.modular/story_command.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_command.fidl#91)*



 Sets the value of link at `path` to `value`.


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
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FocusMod {:#FocusMod}
*Defined in [fuchsia.modular/story_command.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_command.fidl#97)*



 Instructs the session shell to focus the mod under `mod_name`.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>mod_name</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td> The name of the mod within the story.

 Clients should provide `mod_name_transitional` instead.
 If both are provided, `mod_name` is ignored.

</td>
            <td>No default</td>
        </tr><tr>
            <td><code>mod_name_transitional</code></td>
            <td>
                <code>string?</code>
            </td>
            <td> The name of the mod within the story. This should be used instead of
 `mod_name`. If provided, it is equivalent to passing `mod_name` with
 a single item. If both are provided, `mod_name` is ignored.

</td>
            <td>No default</td>
        </tr>
</table>

### SetKindOfProtoStoryOption {:#SetKindOfProtoStoryOption}
*Defined in [fuchsia.modular/story_command.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_command.fidl#115)*



 Updates the kind_of_proto_story option in a story.


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



 Information about a story as provided to the SessionShell.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>url</code></td>
            <td>
                <code>string?</code>
            </td>
            <td> URL of the first module run in this story. This module is free to
 run more modules in the story. Used for display purposes only.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The ID of the Story, used to reference it in method arguments.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>last_focus_time</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> Wallclock time when the story was last focused. From
 ZX_CLOCK_UTC, thus nanoseconds since UNIX epoch (1970-01-01 00:00 UTC).

 A value of zero means the story has never been focused.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>extra</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#StoryInfoExtraEntry'>StoryInfoExtraEntry</a>&gt;?</code>
            </td>
            <td> Data the SessionShell wants to keep associated with this Story, like
 title, a color, or a display rank.
</td>
            <td>No default</td>
        </tr>
</table>

### StoryInfoExtraEntry {:#StoryInfoExtraEntry}
*Defined in [fuchsia.modular/story_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_info.fidl#41)*





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
            <td> Whether or not the story will be hidden on a call to
 StoryProvider#GetStories.
</td>
            <td>No default</td>
        </tr>
</table>

### ViewConnection {:#ViewConnection}
*Defined in [fuchsia.modular/story_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell.fidl#113)*



 A pair mapping a surface ID to a view (via `view_holder_token`).


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>surface_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The ID for the surface
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>view_holder_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#ViewHolderToken'>ViewHolderToken</a></code>
            </td>
            <td> Token for embedding the new view corresponding to the surface.
</td>
            <td>No default</td>
        </tr>
</table>

### ViewConnection2 {:#ViewConnection2}
*Defined in [fuchsia.modular/story_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell.fidl#122)*



 DEPRECATED, for transition purposes only.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>surface_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The ID for the surface
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>view_holder_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#ViewHolderToken'>ViewHolderToken</a></code>
            </td>
            <td> Token for embedding the new view corresponding to the surface.
</td>
            <td>No default</td>
        </tr>
</table>

### SurfaceInfo {:#SurfaceInfo}
*Defined in [fuchsia.modular/story_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell.fidl#131)*



 Contains metadata for a Surface.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>parent_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td> ID of the view that is parent of this Surface.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>surface_relation</code></td>
            <td>
                <code><a class='link' href='#SurfaceRelation'>SurfaceRelation</a>?</code>
            </td>
            <td> The relationship between the parent Surface and this new Surface. Used
 for layout optimization.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>module_manifest</code></td>
            <td>
                <code><a class='link' href='#ModuleManifest'>ModuleManifest</a>?</code>
            </td>
            <td> Information about the module populates the view.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>module_source</code></td>
            <td>
                <code><a class='link' href='#ModuleSource'>ModuleSource</a></code>
            </td>
            <td> How the Surface was generated. By an action internal to the story or by
 an external action.
</td>
            <td>No default</td>
        </tr>
</table>

### ContainerView {:#ContainerView}
*Defined in [fuchsia.modular/story_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell.fidl#164)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>node_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Name by which this container node is referenced in container layout and
 surface relationship specifications (cf. container.fidl)
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>view_holder_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#ViewHolderToken'>ViewHolderToken</a></code>
            </td>
            <td> Token for embedding the new view.  The view is resolved from the intent
 corresponding to `node_name`.
</td>
            <td>No default</td>
        </tr>
</table>

### ContainerView2 {:#ContainerView2}
*Defined in [fuchsia.modular/story_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell.fidl#175)*



 DEPRECATED, for transition purposes only.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>node_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Name by which this container node is referenced in container layout and
 surface relationship specifications (cf. container.fidl)
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>view_holder_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#ViewHolderToken'>ViewHolderToken</a></code>
            </td>
            <td> Token for embedding the new view.  The view is resolved from the intent
 corresponding to `node_name`.
</td>
            <td>No default</td>
        </tr>
</table>

### ContainerLayout {:#ContainerLayout}
*Defined in [fuchsia.modular/container.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/surface/container.fidl#11)*



 Specification of the layout of multiple surfaces in a module container. The
 surfaces are referenced by name in ContainerRelationEntry.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>surfaces</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#LayoutEntry'>LayoutEntry</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### LayoutEntry {:#LayoutEntry}
*Defined in [fuchsia.modular/container.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/surface/container.fidl#17)*



 Specification of the postion of one surface within a container layout,
 specified by a rectangle.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>node_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Surface name, referenced by container relation entry.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>rectangle</code></td>
            <td>
                <code>float32[4]</code>
            </td>
            <td> Layout, as rectangle in Dart conventions(left, top, width, height), as a
 proportion of the size of the container
</td>
            <td>No default</td>
        </tr>
</table>

### ContainerRelationEntry {:#ContainerRelationEntry}
*Defined in [fuchsia.modular/container.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/surface/container.fidl#32)*



 Specifies the surface relationship between modules started together in module
 container.



<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>node_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Surface name, referenced by layout.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>parent_node_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Surface name of the layout parent. This could be the container itself,
 rather than a module in it.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>relationship</code></td>
            <td>
                <code><a class='link' href='#SurfaceRelation'>SurfaceRelation</a></code>
            </td>
            <td> This surface relation between the surface identified by node_name and by
 parent_node_name.

 It is possible to specify a surface relationship of a module in a container
 to the container itself, as opposed to another module in the container.
 This expresses for example that a module can be dismissed individually, as
 opposed to dismissing the module dismisses the container as a whole.

</td>
            <td>No default</td>
        </tr>
</table>

### ContainerNode {:#ContainerNode}
*Defined in [fuchsia.modular/container.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/surface/container.fidl#59)*



 Specifies one module to start inside a container. The module is specified by
 a intent as usual. The node_name of the surface is referenced by container
 layout and by container relation entry.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>node_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Name by which this module is references in layout and surface relationship
 specifications (cf. above).
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>intent</code></td>
            <td>
                <code><a class='link' href='#Intent'>Intent</a></code>
            </td>
            <td> The intent to resolve to a module.
</td>
            <td>No default</td>
        </tr>
</table>

### SurfaceRelation {:#SurfaceRelation}
*Defined in [fuchsia.modular/surface.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/surface/surface.fidl#11)*



 Describes the relationship between two Surfaces.
 Provides information to the StoryShell for layout optimization.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>arrangement</code></td>
            <td>
                <code><a class='link' href='#SurfaceArrangement'>SurfaceArrangement</a></code>
            </td>
            <td> Advice on arranging these surfaces on the screen together.
</td>
            <td><a class='link' href='#SurfaceArrangement.NONE'>SurfaceArrangement.NONE</a></td>
        </tr><tr>
            <td><code>dependency</code></td>
            <td>
                <code><a class='link' href='#SurfaceDependency'>SurfaceDependency</a></code>
            </td>
            <td> Advice for dismissal of surfaces to be linked.
</td>
            <td><a class='link' href='#SurfaceDependency.NONE'>SurfaceDependency.NONE</a></td>
        </tr><tr>
            <td><code>emphasis</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> Relative emphasis of the child surface, relative to the parent.
 Influences relative areas of surfaces on screen.
</td>
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

*Defined in [fuchsia.modular/story_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell.fidl#214)*

 Defines the visual state of the Story shell.


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

 State of a Story. A story is either running, stopping, or stopped, separately
 on every device of the user. If it's running, it can also be focused, but
 that's tracked in a separate service, cf. FocusProvider in focus.fidl.

 Possible state transitions are:

   STOPPED  -> RUNNING
   RUNNING  -> STOPPING
   STOPPING -> STOPPED


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

 Visibility state of a Story within the session shell.
 This state describes how a story should be displayed within the session shell,
 regardless of whether the story is in focus or not. Focus state and
 visibility state are orthogonal concepts.
 E.g A story can be out-of-focus and be in IMMERSIVE state at the same time
 if a user was playing a video, exits, then re-enters the story. The
 expectation in this scenario is that the story is in IMMERSIVE state upon
 re-enter.

 All state transitions are possible.


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

 Expresses arrangement type.


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

 Links surface dismissal.


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

 Used by ComponentContext.ConnectToAgentService


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>service_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The name of the requested service.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>channel</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
            <td> The channel that will be used to communicate with the requested service.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>handler</code></td>
            <td>
                <code>string[2083]</code>
            </td>
            <td> The component URL of the Agent that is to provide the specified service.
 If no handler is specified, the framework will perform resolution to
 find an appropriate handler.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>agent_controller</code></td>
            <td>
                <code>request&lt;<a class='link' href='#AgentController'>AgentController</a>&gt;</code>
            </td>
            <td> The AgentController that keeps the agent alive.
</td>
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
                <code><a class='link' href='#DisplayInfo'>DisplayInfo</a></code>
            </td>
            <td> Defines presentation fields for a suggestion. The string fields might be
 templated and will be filled from data in `parameter_mapping`.
 For example: "Listen to $artistName"
</td>
        </tr><tr>
            <td>2</td>
            <td><code>parameter_mapping</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ParameterMapping'>ParameterMapping</a>&gt;</code>
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

### StoryInfo2 {:#StoryInfo2}


*Defined in [fuchsia.modular/story_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_info.fidl#30)*

 Information about a story as provided to the SessionShell.
 For transition purposes only.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>id</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The ID of the Story, used to reference it in method arguments.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>last_focus_time</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> Wallclock time when the story was last focused. From
 ZX_CLOCK_UTC, thus nanoseconds since UNIX epoch (1970-01-01 00:00 UTC).

 A value of zero means the story has never been focused.
</td>
        </tr></table>

### SurfaceInfo2 {:#SurfaceInfo2}


*Defined in [fuchsia.modular/story_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_shell.fidl#148)*

 Contains metadata for a Surface.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>parent_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td> ID of the view that is parent of this Surface.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>surface_relation</code></td>
            <td>
                <code><a class='link' href='#SurfaceRelation'>SurfaceRelation</a></code>
            </td>
            <td> The relationship between the parent Surface and this new Surface. Used
 for layout optimization.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>module_manifest</code></td>
            <td>
                <code><a class='link' href='#ModuleManifest'>ModuleManifest</a></code>
            </td>
            <td> Information about the module populates the view.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>module_source</code></td>
            <td>
                <code><a class='link' href='#ModuleSource'>ModuleSource</a></code>
            </td>
            <td> How the Surface was generated. By an action internal to the story or by
 an external action.
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
            <td> Set this if you already have an Entity reference at runtime.
 Entity.getTypes() will be used to set the constraints for this noun during
 resolution.
</td>
        </tr><tr>
            <td><code>json</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
            <td> Set this if you have structured JSON data. Values typically are a JSON
 object with a "@type" attribute and other associated data.  TODO(thatguy):
 We need to decide if we want to keep this in place, or deprecate this
 eventually and move entirely to using Entity references.

 DEPRECATED: Use `entity_reference`.
</td>
        </tr><tr>
            <td><code>entity_type</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td> Set this if you want to explicitly define this noun's allowed types. This
 is also useful in the cases where the noun has a 'direction' of type
 'output', and you wish to set the allowable output types from the Module
 (see docs/modular/manifests/action_template.md for a definition of
 'direction').

 Only one entry in `entity_type` must match the constraint specified by
 the Module for the constraint to be considered satisfied.
</td>
        </tr></table>

### CreateModuleParameterInfo {:#CreateModuleParameterInfo}
*Defined in [fuchsia.modular/create_module_parameter_map.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/create_module_parameter_map.fidl#18)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>link_path</code></td>
            <td>
                <code><a class='link' href='#LinkPath'>LinkPath</a></code>
            </td>
            <td> Instructs parameter map initialization to either use an existing Link
 (`link_path` is set) or create a new Link (`create_link` is set).
</td>
        </tr><tr>
            <td><code>create_link</code></td>
            <td>
                <code><a class='link' href='#CreateLinkInfo'>CreateLinkInfo</a></code>
            </td>
            <td></td>
        </tr></table>

### StoryPuppetMaster_SetStoryInfoExtra_Result {:#StoryPuppetMaster_SetStoryInfoExtra_Result}
*Defined in [fuchsia.modular/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#160)*


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

### StoryCommand {:#StoryCommand}
*Defined in [fuchsia.modular/story_command.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/story/story_command.fidl#17)*

 StoryCommands are POD structures that describe the set of operations that
 can be performed on a story by components outside the modular framework. All commands are:

   (1) Scoped to a single story
   (2) Idempotent: issuing the same command twice yields the same result
   (3) Symmetrical with observation: the same structures are used to describe
       operations to watchers of a story (through SessionWatcher) as are used
       to control a story.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>set_focus_state</code></td>
            <td>
                <code><a class='link' href='#SetFocusState'>SetFocusState</a></code>
            </td>
            <td> Sets the focus state of the story to `set_focus_state.focused`.
</td>
        </tr><tr>
            <td><code>add_mod</code></td>
            <td>
                <code><a class='link' href='#AddMod'>AddMod</a></code>
            </td>
            <td> Adds a Mod.
</td>
        </tr><tr>
            <td><code>remove_mod</code></td>
            <td>
                <code><a class='link' href='#RemoveMod'>RemoveMod</a></code>
            </td>
            <td> Removes an existing Mod.
</td>
        </tr><tr>
            <td><code>set_link_value</code></td>
            <td>
                <code><a class='link' href='#SetLinkValue'>SetLinkValue</a></code>
            </td>
            <td> Sets the value of a Link.
</td>
        </tr><tr>
            <td><code>focus_mod</code></td>
            <td>
                <code><a class='link' href='#FocusMod'>FocusMod</a></code>
            </td>
            <td> Brings focus to a mod.
</td>
        </tr><tr>
            <td><code>set_kind_of_proto_story_option</code></td>
            <td>
                <code><a class='link' href='#SetKindOfProtoStoryOption'>SetKindOfProtoStoryOption</a></code>
            </td>
            <td> Updates the kind_of_proto_story option in a story.
</td>
        </tr></table>

### ComponentScope {:#ComponentScope}
*Defined in [fuchsia.modular/scope.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular/user_intelligence/scope.fidl#10)*

 Specifies the access scope a given component has to services within Maxwell.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>global_scope</code></td>
            <td>
                <code><a class='link' href='#GlobalScope'>GlobalScope</a></code>
            </td>
            <td> Reserved for system-level services.
</td>
        </tr><tr>
            <td><code>module_scope</code></td>
            <td>
                <code><a class='link' href='#ModuleScope'>ModuleScope</a></code>
            </td>
            <td> Scope for a specific Module instance within a specific Story.
</td>
        </tr><tr>
            <td><code>agent_scope</code></td>
            <td>
                <code><a class='link' href='#AgentScope'>AgentScope</a></code>
            </td>
            <td> Scope for a specific Agent. Agents are not tied to a specific story.
</td>
        </tr><tr>
            <td><code>story_scope</code></td>
            <td>
                <code><a class='link' href='#StoryScope'>StoryScope</a></code>
            </td>
            <td> Scope for a specific Story, potentially containing several Module instances.
</td>
        </tr></table>







