Project: /_project.yaml
Book: /_book.yaml

# fuchsia.app.agent


## **PROTOCOLS**

## Agent {:#Agent}
*Defined in [fuchsia.app.agent/agent.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.agent/agent.fidl#30)*

 An agent is a component which provides services in support of modules in a
 story. Agents cannot show UI directly.

 - An agent is a singleton instance within the scope of a session.
 - Components can connect to an Agent using the Context service provided to
   each modular component class (fuchsia.app.agent, fuchsia.app.module,
   fuchsia.app.storyshell, fuchsia.app.sessionshell).
 - An agent vends services and resources to components that connect to it over a
   fuchsia.io.Directory.
 - An agent is started when someone wants to connect to it, or when a task it
   has scheduled has triggered.

 This FIDL interface MUST be implemented for agent components.

 For more info see:
 - peridot/docs/modular/agent.md
 - fuchsia.app.agent.Context for common methods provided by modular to agents.
 - fuchsia.app.Lifecycle for how agents receive lifecycle events.

### AcceptConnection {:#AcceptConnection}

 Called when a client of this agent wishes to acquire a service directory from this agent.

 `client` describes the identity of the client component. See ClientIdentity below.

 `directory_request` should be bound to a fuchsia.io.Directory implementation or closed
 if services are denied. The Agent implementation should keep `directory_request` bound
 and available until the client closes it. At this point, it must NOT assume that
 the client itself is gone, but rather that the client no longer wishes to open new
 services connections.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>client</code></td>
            <td>
                <code><a class='link' href='../fuchsia.app.agent/index.html#ClientIdentity'>ClientIdentity</a></code>
            </td>
        </tr><tr>
            <td><code>directory_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.io/index.html'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/index.html#Directory'>Directory</a>&gt;</code>
            </td>
        </tr></table>



### RunTask {:#RunTask}

 Called when a task identified by `task` is scheduled to run. Tasks are scheduled run when
 the conditions described in `task.type` become true. Tasks are scheduled using
 fuchsia.app.agent.Context/ScheduleTask().

 Agents must return from RunTask() when the task has finished. The Agent may be asked to
 terminate in the middle of task execution.

 TODO(MF-321): The current implementation permits the Agent to run a task until its callback
 returns, no matter how long. There is no mechanism to cancel an ongoing task.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>task</code></td>
            <td>
                <code><a class='link' href='../fuchsia.app.agent/index.html#TaskInfo'>TaskInfo</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## Context {:#Context}
*Defined in [fuchsia.app.agent/context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.agent/context.fidl#14)*

 An instance of this service is exposed to agents in their namespace. It
 exposes the base capabilities offered by modular to agents.

 See also: fuchsia.app.Agent

### ConnectToAgent {:#ConnectToAgent}

 Obtains a fuchsia.io.Directory of services from the agent specified in `request.handler`.
 Services are bound to `request.services`. The agent endpoint may close `request.services`
 at its discretion, at which point `request.controller` must be closed by the caller.

 If brokering a connection is successful, keeping `request.controller` open will ensure
 that the agent endpoint is not terminated.

 Failure to provide all required fields in `request` will close the
 Context channel with an ZX_ERR_INVALID_ARGS.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code><a class='link' href='../fuchsia.app/index.html'>fuchsia.app</a>/<a class='link' href='../fuchsia.app/index.html#AgentConnectionRequest'>AgentConnectionRequest</a></code>
            </td>
        </tr></table>



### ScheduleTask {:#ScheduleTask}

 Schedules the task described in `task_info`. When this task is scheduled to
 run, Agent.RunTask() is called.

 TODO(MF-40): Add a callback to task scheduling.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>task_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.app.agent/index.html#TaskInfo'>TaskInfo</a></code>
            </td>
        </tr></table>



### DeleteTask {:#DeleteTask}

 Deletes the task `name` (see TaskInfo.name), meaning no new runs of this task will be scheduled.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string[100]</code>
            </td>
        </tr></table>









## **TABLES**

### ClientIdentity {:#ClientIdentity}


*Defined in [fuchsia.app.agent/agent.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.agent/agent.fidl#54)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>component_url</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The component URL of the requesting client, as formatted at the time of component creation.

 Always set.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>story_id</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td> If the client is a module created by this agent (using
 fuchsia.app.sessioncontrol.StoryController), identifies the StoryId the agent specified at
 module creation time. Otherwise not set.

 See fuchsia.app.sessioncontrol.StoryController.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>module_id</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td> If the client is a module created by this agent (using
 fuchsia.app.sessioncontrol.StoryController), identifies the ModuleId the agent specified at
 module creation time. Otherwise not set.

 See fuchsia.app.sessioncontrol.StoryController.
</td>
        </tr></table>

### TaskInfo {:#TaskInfo}


*Defined in [fuchsia.app.agent/task.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.agent/task.fidl#15)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td> A client-provided task name that can be used later to refer to this task.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>schedule_condition</code></td>
            <td>
                <code><a class='link' href='../fuchsia.app.agent/index.html#ScheduleCondition'>ScheduleCondition</a></code>
            </td>
            <td> The condition that would cause this task to get scheduled.
</td>
        </tr></table>





## **XUNIONS**

### ScheduleCondition {:#ScheduleCondition}
*Defined in [fuchsia.app.agent/task.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.agent/task.fidl#25)*

 Describes the condition that needs to be met for a task to become scheduled.
 This is not yet complete and will be extended or changed.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>message_on_message_queue</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td> Triggers when a new message arrives on the queue named by `message_queue_message`.
</td>
        </tr><tr>
            <td><code>message_queue_deleted</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td> Triggers when a the message queue named by `message_queue_deleted` is deleted.

 `queue_deleted` is the token for the message queue that is to be watched.
 This allows both message queue readers and writers to watch for queue
 deletions.
</td>
        </tr><tr>
            <td><code>repeating_timer</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> Triggers the task approximately every time `repeating_timer` elapses.
 Once a task with `repeating_timer` is scheduled, it will trigger at
 approximately |now + repeating_timer|.
</td>
        </tr></table>





## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.agent/task.fidl#13">TASK_NAME_MAX_LENGTH</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    
</table>

