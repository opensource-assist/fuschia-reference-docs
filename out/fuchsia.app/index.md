Project: /_project.yaml
Book: /_book.yaml

# fuchsia.app


## **PROTOCOLS**

## Context {:#Context}
*Defined in [fuchsia.app/context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app/context.fidl#12)*

 A common base protocol for fuchsia.app.(module`agent|*shell`).Context.
 Clients of those protocols will have access to all of these methods through those interfaces.

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
                <code><a class='link' href='../fuchsia.app/index.html#AgentConnectionRequest'>AgentConnectionRequest</a></code>
            </td>
        </tr></table>



## AgentController {:#AgentController}
*Defined in [fuchsia.app/context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app/context.fidl#45)*

 This interface is used by calls to *Context/ConnectToAgent() to signal to the framework to keep
 the agent alive, so long as the AgentController channel is open.





## **ENUMS**

### OngoingActivityType {:#OngoingActivityType}
Type: <code>uint32</code>

*Defined in [fuchsia.app/ongoing_activity.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app/ongoing_activity.fidl#8)*

 Ongoing activities are classified by the nature of their activity.


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



## **TABLES**

### AgentConnectionRequest {:#AgentConnectionRequest}


*Defined in [fuchsia.app/context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app/context.fidl#25)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>handler</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The component URL of the agent which is to provide services.

 Required.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>services</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.io/index.html'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/index.html#Directory'>Directory</a>&gt;</code>
            </td>
            <td> `services` will be connected to a directory of services provided by `handler`.

 Required.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>controller</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.app/index.html#AgentController'>AgentController</a>&gt;</code>
            </td>
            <td> The agent providing `services` stays alive so long as the channel backing `controller`
 is not dropped.

 Required.
</td>
        </tr></table>

### Intent {:#Intent}


*Defined in [fuchsia.app/intent.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app/intent.fidl#7)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>placeholder</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>









## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app/types.fidl#18">MESSAGE_QUEUE_NAME_MAX_LENGTH</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app/types.fidl#21">STORY_ID_MAX_LENGTH</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    
</table>

