Project: /_project.yaml
Book: /_book.yaml

# fuchsia.sys2


## **PROTOCOLS**

## Realm {:#Realm}
*Defined in [fuchsia.sys2/realm.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/realm.fidl#15)*

 A protocol used by a component instance to manage its own realm, such as for
 binding to its children.

 The component manager provides this service to components that use
 `/svc/fuchsia.sys2.Realm`.

### BindChild {:#BindChild}

 Binds to a child component instance, causing it to start running if it
 is not already. When this function successfully returns, `child` is
 running and `exposed_dir` is bound to a directory that contains the
 capabilities which the child exposed to its realm via
 `ComponentDecl.exposes` (specified via "expose" declarations in the
 component’s manifest).

 `exposed_dir` is a valid channel as long as `child` is running. `child`
 will remain running until it either stops on its own, or `DestroyChild`
 causes the child instance to be destroyed.

 For example, if the child exposes a service `/svc/example.Echo` then
 `exposed_dir` will contain that service at that path.

 NOTE: `BindChild` does not support pipelining with `CreateChild`. If
 `BindChild` is called on an instance before `CreateChild` successfully
 returns, it may return `INSTANCE_NOT_FOUND`.

 Errors:
 - `INVALID_ARGUMENTS`: `child` is not a valid child reference.  -
 - `INSTANCE_NOT_FOUND`: `child` does not exist.
 - `INSTANCE_CANNOT_START`: `child` was not running and there was an error
   starting it.
 - `INSTANCE_CANNOT_RESOLVE`: `child`'s component declaration failed to resolve.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>child</code></td>
            <td>
                <code><a class='link' href='#ChildRef'>ChildRef</a></code>
            </td>
        </tr><tr>
            <td><code>exposed_dir</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.io/index.html'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/index.html#Directory'>Directory</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Realm_BindChild_Result'>Realm_BindChild_Result</a></code>
            </td>
        </tr></table>

### CreateChild {:#CreateChild}

 Creates a child component instance dynamically. When this function
 returns successfully, the instance exists, but it may not be running.

 Errors:
 - `INVALID_ARGUMENTS`: `collection` is not a valid reference or `child`
   is not a valid declaration.
 - `COLLECTION_NOT_FOUND`: `collection` does not exist.
 - `INSTANCE_ALREADY_EXISTS`: `decl.name` already exists in `collection`.
 - `NO_SPACE`: Could not allocate storage for the new instance.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>collection</code></td>
            <td>
                <code><a class='link' href='#CollectionRef'>CollectionRef</a></code>
            </td>
        </tr><tr>
            <td><code>decl</code></td>
            <td>
                <code><a class='link' href='#ChildDecl'>ChildDecl</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Realm_CreateChild_Result'>Realm_CreateChild_Result</a></code>
            </td>
        </tr></table>

### DestroyChild {:#DestroyChild}

 Destroys a dynamically-created component instance. When this function
 returns, the client should assume the instance no longer exists.
 However, some cleanup (such as stopping the component instance or
 freeing its storage) may be performed in the background after the
 function returns.

 Errors:
 - `INVALID_ARGUMENTS`: `child` is not a valid reference or does not refer
   to a dynamic instance.
 - `INSTANCE_NOT_FOUND`: `child` does not exist.
 - `COLLECTION_NOT_FOUND`: `collection` does not exist.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>child</code></td>
            <td>
                <code><a class='link' href='#ChildRef'>ChildRef</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Realm_DestroyChild_Result'>Realm_DestroyChild_Result</a></code>
            </td>
        </tr></table>

### ListChildren {:#ListChildren}

 Returns an iterator that lists all instances in a collection.

 NOTE: The results are not guaranteed to be consistent. Instances may be
 created or destroyed while the iterator is live, but those changes
 won't be observed by the iterator after this method returns.

 Errors:
 - `INVALID_ARGUMENTS`: `collection` is not a valid reference.
 - `COLLECTION_NOT_FOUND`: `collection` does not exist.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>collection</code></td>
            <td>
                <code><a class='link' href='#CollectionRef'>CollectionRef</a></code>
            </td>
        </tr><tr>
            <td><code>iter</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ChildIterator'>ChildIterator</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Realm_ListChildren_Result'>Realm_ListChildren_Result</a></code>
            </td>
        </tr></table>

## ChildIterator {:#ChildIterator}
*Defined in [fuchsia.sys2/realm.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/realm.fidl#81)*

 A protocol to iterate over the list of children in a realm.

### Next {:#Next}

 Advance the iterator and return the next batch of children.

 Returns a vector of `ChildRef`. Returns an empty vector when there are
 no more children.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>children</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ChildRef'>ChildRef</a>&gt;</code>
            </td>
        </tr></table>

## ComponentResolver {:#ComponentResolver}
*Defined in [fuchsia.sys2/component_resolver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/runtime/component_resolver.fidl#22)*

 An interface for resolving a URL to a component.

 This interface is implemented by components that provide support
 for loading components with a particular URL scheme.   For example,
 the Fuchsia package component resolver exposes a service with this
 interface to resolve component URLs using the "fuchsia-pkg://" scheme.

 To use a resolver to resolve URLs within your realm, register it
 in your realm's manifest.  (TODO: explain in more detail)

 Note: The component manager is the only intended direct client of this
 interface.

### Resolve {:#Resolve}

 Resolves a component with the given URL.

 `component_url` is the unescaped URL of the component to resolve.

 If successful, returns `ZX_OK` and information about the component
 that was resolved.

 On failure, returns null `info` and...
 - `ZX_ERR_INVALID_ARGS`: The component's URL was malformed.
 - `ZX_ERR_NOT_FOUND`: The component does not exist.
 - `ZX_ERR_UNAVAILABLE`: The resolver was unable to retrieve or parse
   the component's resources.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>component_url</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>component</code></td>
            <td>
                <code><a class='link' href='#Component'>Component</a></code>
            </td>
        </tr></table>

## ComponentRunner {:#ComponentRunner}
*Defined in [fuchsia.sys2/component_runner.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/runtime/component_runner.fidl#23)*

 An interface for running components.

 This interface is implemented by components that provide an execution
 environment for running particular classes of programs.  For example,
 the Dart virtual machine exposes a service with this interface to run
 Dart programs.

 To specify the runner needed to run your component, set the "runner_url"
 property in your component's manifest.

 Note: The component manager is the only intended direct client of this
 interface.

### Start {:#Start}

 Starts running a new component instance described by `start_info`.

 The caller of this method takes responsibility for binding client
 connections and controlling the lifetime of the newly started
 component instance through the requested `controller`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>start_info</code></td>
            <td>
                <code><a class='link' href='#ComponentStartInfo'>ComponentStartInfo</a></code>
            </td>
        </tr><tr>
            <td><code>controller</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ComponentController'>ComponentController</a>&gt;</code>
            </td>
        </tr></table>



## ComponentController {:#ComponentController}
*Defined in [fuchsia.sys2/component_runner.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/runtime/component_runner.fidl#94)*

 An interface for binding client connections and controlling the lifetime
 of a component instance started using `ComponentRunner.Start()`.

 When the controlled component instance terminates or becomes inaccessible
 for any reason, the server invokes `OnEpitaph()` and closes its endpoint
 of the controller interface.

 LIFECYCLE

 A component may exist in one of two states, Started or Stopped. The component
 is Started from time `ComponentRunner.Start()` is called until the
 ComponentRunner closes the ComponentController handle. The component then
 transitions to Stopped.

 `Stop()` is called to indicate a ComponentRunner should end a component's
 execution. `Kill()` indicates that a runner must halt a component's
 execution immediately and close the ComponentController's server end. After
 the ComponentController is closed the component manager can tear down the
 namespace it hosts for the stopped component. The component manager may
 call `Kill()` without first having called `Stop()`.

 EPITAPH

 This interface uses a FIDL epitaph to indicate that the controller
 component instance has terminated and to describe its final disposition.

 The following epitaph status codes have particular significance:

 - `ZX_OK`: The component instance was successfully terminated in response
   to `Stop()` and its runtime resources have been fully released.
 - `ZX_ERR_UNAVAILABLE`: The runner was unable to start the component
   instance.  e.g. The runner could not retrieve the component's assets.
 - `ERR_COMPONENT_DIED`: The component instance was started but
   subsequently terminated unexpectedly.

 Other status codes (e.g. `ZX_ERR_PEER_CLOSED`) may indicate a failure
 of the component runner itself.  The component manager may respond to such
 failures by terminating the component runner's job to ensure system
 stability.

### Stop {:#Stop}

 Requests the runner to stop the controlled component instance.

 After stopping the component instance, the server should report
 an epitaph then close its endpoint of the controller interface.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Kill {:#Kill}

 Stop this component immediately. This ComponentRunner must immediately
 kill the component instance, set an epitaph set on the channel, and
 close the channel. After the channel closes, the component instance will
 be considered by the component manager to be Stopped and the component's
 namespace will be torn down.

 Kill() may have been preceeded by Stop(), but that is not guaranteed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## SystemController {:#SystemController}
*Defined in [fuchsia.sys2/system_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/system_controller.fidl#10)*

 An interface implemented by ComponentManager that requests the
 ComponentManager stop all components and exit.

### Shutdown {:#Shutdown}

 Stop all components, return an empty result, close this protocol's
 channel, and exit ComponentManager. If this is the root ComponentManager
 is exited we expect the system will reboot.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## WorkScheduler {:#WorkScheduler}
*Defined in [fuchsia.sys2/work_scheduler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/work_scheduler.fidl#40)*

 Framework service: API for scheduling and canceling work. Each component instance can access
 work items that it has scheduled (but not others' scheduled work items). Work items are
 scheduled _roughly_ at the specified time and frequency; the service implementation may specify
 its notion of _roughly_, and may provide a configuration API to tune this notion.

 Each scheduled work item is identified by a client-provided `WorkId`. Each scheduled work item
 has a `WorkId` that is unique with respect to scheduled work items belonging to the same
 component instance.

### ScheduleWork {:#ScheduleWork}

 Schedule a new work item identified by `work_id`. The work item is to be scheduled roughly
 at the time corresponding to `work_request.start`. When `work_request.period` is specified,
 reschedule work roughly every `work_request.period` until the the work item is canceled.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>work_id</code></td>
            <td>
                <code>string[100]</code>
            </td>
        </tr><tr>
            <td><code>work_request</code></td>
            <td>
                <code><a class='link' href='#WorkRequest'>WorkRequest</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#WorkScheduler_ScheduleWork_Result'>WorkScheduler_ScheduleWork_Result</a></code>
            </td>
        </tr></table>

### CancelWork {:#CancelWork}

 Cancel the scheduled work item specified by `work_id`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>work_id</code></td>
            <td>
                <code>string[100]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#WorkScheduler_CancelWork_Result'>WorkScheduler_CancelWork_Result</a></code>
            </td>
        </tr></table>

## Worker {:#Worker}
*Defined in [fuchsia.sys2/work_scheduler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/work_scheduler.fidl#57)*

 Component-exposed service: Work scheduler connects to this service to invoke scheduled work item
 callbacks. The service implementation is responsible for invoking the code that corresponds to
 the scheduled work item identified by `work_id`.

 Note: The intent of exposing this service is to expose it to the `WorkScheduler` service
 provider (i.e., the framework) and no one else.

### DoWork {:#DoWork}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>work_id</code></td>
            <td>
                <code>string[100]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Worker_DoWork_Result'>Worker_DoWork_Result</a></code>
            </td>
        </tr></table>

## WorkSchedulerControl {:#WorkSchedulerControl}
*Defined in [fuchsia.sys2/work_scheduler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/work_scheduler.fidl#69)*

 Framework service: Administrative API for controlling parameters of the `WorkScheduler`
 framework service. So long as there are work items with deadlines in the next `batch_period`,
 the `WorkScheduler` will sleep for `batch_period`, then wake up and immediately dispatch a batch
 of work items: all those with past deadlines. It will repeat this process until no work items
 would be scheduled in the next `batch_period`, at which point it will go to sleep until the next
 deadline. This strategy ensures that each work item is dispatched approximately within
 `batch_period` of its deadline.

### GetBatchPeriod {:#GetBatchPeriod}

 Get the current period between `WorkScheduler` attempts to dispatch a batch of work.
 `batch_period` is a non-negative 64-bit integer in the range [0, 2^63-1], representing a
 number of nanoseconds between dispatching batches of work.

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
                <code><a class='link' href='#WorkSchedulerControl_GetBatchPeriod_Result'>WorkSchedulerControl_GetBatchPeriod_Result</a></code>
            </td>
        </tr></table>

### SetBatchPeriod {:#SetBatchPeriod}

 Set the current period between `WorkScheduler` attempts to batch and dispatch a batch of
 work. `batch_period` is a non-negative 64-bit integer in the range [0, 2^63-1], representing
 a number of nanoseconds between dispatching batches of work.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>batch_period</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#WorkSchedulerControl_SetBatchPeriod_Result'>WorkSchedulerControl_SetBatchPeriod_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### RealmRef {:#RealmRef}
*Defined in [fuchsia.sys2/relative_refs.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/relative_refs.fidl#19)*



 A reference to a component’s containing realm, i.e. the parent component.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### SelfRef {:#SelfRef}
*Defined in [fuchsia.sys2/relative_refs.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/relative_refs.fidl#22)*



 A reference to the component itself.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### ChildRef {:#ChildRef}
*Defined in [fuchsia.sys2/relative_refs.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/relative_refs.fidl#25)*



 A reference to one of the component's child instances.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td> The name assigned to the child by its parent. If `collection` is set,
 `name` is scoped to `collection` and the child is a dynamic instance.
 Required.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>collection</code></td>
            <td>
                <code>string[100]?</code>
            </td>
            <td> The collection `name` belongs to. If omitted, `name` references a static
 instance. This field must be omitted if the `ChildRef` is being used in
 a component declaration. Optional.
</td>
            <td>No default</td>
        </tr>
</table>

### CollectionRef {:#CollectionRef}
*Defined in [fuchsia.sys2/relative_refs.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/relative_refs.fidl#37)*



 A reference to one of the component's collections.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StorageRef {:#StorageRef}
*Defined in [fuchsia.sys2/relative_refs.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/relative_refs.fidl#42)*



 A reference to one of the component's storage sections.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FrameworkRef {:#FrameworkRef}
*Defined in [fuchsia.sys2/relative_refs.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/relative_refs.fidl#47)*



 A reference to the component framework itself.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Moniker {:#Moniker}
*Defined in [fuchsia.sys2/moniker.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/moniker.fidl#19)*



 A moniker encodes the relationship between two component instances that
 exist in the component instance tree at runtime.

 To understand this better, consider two component instances labeled "A"
 and "B" that are both children of a component instance labeled "P".

 At runtime, when "B" requests a service from "A" through a channel
 established by the component manager, the component manager may provide
 "A" with a moniker that encodes "B's" identity relative to "A" itself.
 The moniker's encoded value describes the directed path to traverse from
 "A" (the moniker's origin) to "B" (the moniker's referent), passing
 through "P" (their common ancestor).


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>encoded_value</code></td>
            <td>
                <code>string[4096]</code>
            </td>
            <td> An opaque representation of the moniker's relation.
</td>
            <td>No default</td>
        </tr>
</table>

### Realm_BindChild_Response {:#Realm_BindChild_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Realm_CreateChild_Response {:#Realm_CreateChild_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Realm_DestroyChild_Response {:#Realm_DestroyChild_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Realm_ListChildren_Response {:#Realm_ListChildren_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### ComponentNamespace {:#ComponentNamespace}
*Defined in [fuchsia.sys2/component_namespace.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/runtime/component_namespace.fidl#21)*



 A namespace specifies the set of directories that a component instance
 receives at start-up.  Each component instance's namespace is tailored
 to provide access to a set of files and services that are appropriate
 to that component instance's role in the system (its sandbox).

 By convention, a component's namespace typically contains some or all
 of the following directories:

 - "/svc": A directory containing services that the component requested
           to use via its "import" declarations.
 - "/pkg": A directory containing the component's package, including its
           binaries, libraries, and other assets.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>paths</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td> The mount point for each of the directories below, each including a
 leading slash.  For example, ["/pkg", "/svc", "/config/data"].

 Each mount point must be unique and non-overlapping.
 For example, ["/foo", "/foo/bar"] is invalid.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>directories</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.io/index.html'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/index.html#Directory'>Directory</a>&gt;</code>
            </td>
            <td> The directories mounted at each path in the namespace.
</td>
            <td>No default</td>
        </tr>
</table>

### WorkScheduler_ScheduleWork_Response {:#WorkScheduler_ScheduleWork_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### WorkScheduler_CancelWork_Response {:#WorkScheduler_CancelWork_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Worker_DoWork_Response {:#Worker_DoWork_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### WorkSchedulerControl_GetBatchPeriod_Response {:#WorkSchedulerControl_GetBatchPeriod_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>batch_period</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### WorkSchedulerControl_SetBatchPeriod_Response {:#WorkSchedulerControl_SetBatchPeriod_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>



## **ENUMS**

### StartupMode {:#StartupMode}
Type: <code>uint32</code>

*Defined in [fuchsia.sys2/child_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/child_decl.fidl#7)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>LAZY</code></td>
            <td><code>0</code></td>
            <td> Start component instance only when another instance binds to it.
</td>
        </tr><tr>
            <td><code>EAGER</code></td>
            <td><code>1</code></td>
            <td> Start component instance as soon as parent starts.
</td>
        </tr></table>

### Durability {:#Durability}
Type: <code>uint32</code>

*Defined in [fuchsia.sys2/collection_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/collection_decl.fidl#18)*

 The durability of component instances created in a collection.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>PERSISTENT</code></td>
            <td><code>1</code></td>
            <td> An instance exists until either it or its parent is destroyed.
</td>
        </tr><tr>
            <td><code>TRANSIENT</code></td>
            <td><code>2</code></td>
            <td> An instance exists until either its parent instance is stopped
 or it is explicitly destroyed.
</td>
        </tr></table>

### StorageType {:#StorageType}
Type: <code>uint32</code>

*Defined in [fuchsia.sys2/storage_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/storage_decl.fidl#8)*

 The type of storage offered by this component.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DATA</code></td>
            <td><code>1</code></td>
            <td> General data storage.
</td>
        </tr><tr>
            <td><code>CACHE</code></td>
            <td><code>2</code></td>
            <td> Cache storage that may be deleted at any time by the system.
</td>
        </tr><tr>
            <td><code>META</code></td>
            <td><code>3</code></td>
            <td> Meta storage that will be used by component manager to persist metadata
 and other information about the component
</td>
        </tr></table>

### Error {:#Error}
Type: <code>uint32</code>

*Defined in [fuchsia.sys2/error.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/error.fidl#8)*

 Standard error codes for component framework protocols.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INTERNAL</code></td>
            <td><code>1</code></td>
            <td> Component manager encountered an otherwise unspecified error while
 performing the operation.
</td>
        </tr><tr>
            <td><code>INVALID_ARGUMENTS</code></td>
            <td><code>2</code></td>
            <td> At least one argument had an invalid format.
</td>
        </tr><tr>
            <td><code>UNSUPPORTED</code></td>
            <td><code>3</code></td>
            <td> The feature is not yet supported.
</td>
        </tr><tr>
            <td><code>INSTANCE_NOT_FOUND</code></td>
            <td><code>4</code></td>
            <td> The component instance was not found.
</td>
        </tr><tr>
            <td><code>INSTANCE_ALREADY_EXISTS</code></td>
            <td><code>5</code></td>
            <td> The component instance already exists.
</td>
        </tr><tr>
            <td><code>INSTANCE_CANNOT_START</code></td>
            <td><code>6</code></td>
            <td> The component instance could not be started.
</td>
        </tr><tr>
            <td><code>INSTANCE_CANNOT_RESOLVE</code></td>
            <td><code>7</code></td>
            <td> Failed to resolve the component's declaration.
</td>
        </tr><tr>
            <td><code>COLLECTION_NOT_FOUND</code></td>
            <td><code>8</code></td>
            <td> The component collection was not found.
</td>
        </tr><tr>
            <td><code>NO_SPACE</code></td>
            <td><code>9</code></td>
            <td> There was insufficient space to perform the operation.
</td>
        </tr></table>



## **TABLES**

### ChildDecl {:#ChildDecl}


*Defined in [fuchsia.sys2/child_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/child_decl.fidl#15)*

 Statically declares a child component instance.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td> The name assigned to the child by its parent.

 Must be non-empty, unique among all siblings, and contain only the
 following characters: [a-z0-9-_.].
</td>
        </tr><tr>
            <td>2</td>
            <td><code>url</code></td>
            <td>
                <code>string[4096]</code>
            </td>
            <td> The child component's URL.

 Must be non-empty and a well-formed URL.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>startup</code></td>
            <td>
                <code><a class='link' href='#StartupMode'>StartupMode</a></code>
            </td>
            <td> The startup mode for the component instance.
</td>
        </tr></table>

### CollectionDecl {:#CollectionDecl}


*Defined in [fuchsia.sys2/collection_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/collection_decl.fidl#8)*

 Statically declares a component instance collection.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td> The name of the collection. Instances created in the collection are
 scoped to this name.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>durability</code></td>
            <td>
                <code><a class='link' href='#Durability'>Durability</a></code>
            </td>
            <td> The durability of instances in the collection.
</td>
        </tr></table>

### ComponentDecl {:#ComponentDecl}


*Defined in [fuchsia.sys2/component_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/component_decl.fidl#14)*

 A component declaration.

 This information is typically encoded in the component manifest (.cm file)
 if it has one or may be generated at runtime by a component resolver for
 those that don't.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>program</code></td>
            <td>
                <code><a class='link' href='../fuchsia.data/index.html'>fuchsia.data</a>/<a class='link' href='../fuchsia.data/index.html#Dictionary'>Dictionary</a></code>
            </td>
            <td> Information about the program to run when the component is executed.

 The component manager provides the contents of this dictionary to the
 component runner when executing the program. Each component runner can
 freely define the contents of this dictionary as needed.

 The system's default runner understands the following entries:

 - "binary": string
   The path of the executable relative to the root of the package.
   Typically an ELF binary.

 - "args": vector of strings
   The command-line arguments to provide to the executable at runtime.

 - "env": dictionary of strings
   The environment variables to provide to the executable at runtime.

 Other runners may define different entries.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>uses</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#UseDecl'>UseDecl</a>&gt;</code>
            </td>
            <td> List of capabilities used by the component. These consist of
 capabilities offered to the component that are installed in its incoming
 namespace.

 The used capabilities must be unique and non-overlapping.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>exposes</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ExposeDecl'>ExposeDecl</a>&gt;</code>
            </td>
            <td> List of capabilities exposed by the component. These consist of
 capabilities that are made visible to the containing realm. The parent
 may `offer` these capabilities to its children, but not `use` them.

 The exposed capabilities must be unique and non-overlapping.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>offers</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#OfferDecl'>OfferDecl</a>&gt;</code>
            </td>
            <td> List of capabilities offered to the component’s children. These consist
 of capabilities that the given children may `use`, which may come from a
 child, the containing realm, or the component's own outgoing namespace.

 The offered capabilities must be unique and non-overlapping.
</td>
        </tr><tr>
            <td>5</td>
            <td><code>facets</code></td>
            <td>
                <code><a class='link' href='../fuchsia.data/index.html'>fuchsia.data</a>/<a class='link' href='../fuchsia.data/index.html#Dictionary'>Dictionary</a></code>
            </td>
            <td> Additional metadata about the component.
</td>
        </tr><tr>
            <td>6</td>
            <td><code>children</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ChildDecl'>ChildDecl</a>&gt;</code>
            </td>
            <td> The component's statically instantiated children. The children must have
 unique names.
</td>
        </tr><tr>
            <td>7</td>
            <td><code>collections</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#CollectionDecl'>CollectionDecl</a>&gt;</code>
            </td>
            <td> The component's collections. The collections must have unique names.
</td>
        </tr><tr>
            <td>8</td>
            <td><code>storage</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#StorageDecl'>StorageDecl</a>&gt;</code>
            </td>
            <td> List of storage capabilities created by this component.
 Storage capabilities can be offered to children.
</td>
        </tr><tr>
            <td>9</td>
            <td><code>runners</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#RunnerDecl'>RunnerDecl</a>&gt;</code>
            </td>
            <td> List of runner capabilities created by this component.
 Runner capabilities can be exposed to the parent's realm or offered to children.
</td>
        </tr></table>

### ExposeServiceDecl {:#ExposeServiceDecl}


*Defined in [fuchsia.sys2/expose_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/expose_decl.fidl#20)*

 Declares a service exposed to a component's containing realm, such as a
 service exposed by the component or one of its children at runtime.

 To learn more about services, see:
 https://fuchsia.dev/fuchsia-src/glossary#service


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td> The provider of the capability relative to the component itself. Must
 be `self` or `child`.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td> Path identifying the service, by which it was presented to this
 component.

 Must be an absolute path starting with /.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>target</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td> The destination to which the service is exposed: either the component's realm or the
 framework.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>target_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td> The path by which the capability is being exposed.

 Must be an absolute path starting with /.
</td>
        </tr></table>

### ExposeLegacyServiceDecl {:#ExposeLegacyServiceDecl}


*Defined in [fuchsia.sys2/expose_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/expose_decl.fidl#46)*

 Declares a legacy service exposed to a component's containing realm, such as
 a legacy service exposed by the component or one of its children at runtime.

 A legacy service is a service with a single instance, provided by a single
 FIDL protocol.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td> The provider of the capability relative to the component itself. Must
 be `self` or `child`.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td> Path identifying the legacy service, by which it was presented to this
 component.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>target</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td> The destination to which the legacy service is exposed: either the component's realm or the
 framework.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>target_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td> The path by which the capability is being exposed.

 Must be an absolute path starting with /.
</td>
        </tr></table>

### ExposeDirectoryDecl {:#ExposeDirectoryDecl}


*Defined in [fuchsia.sys2/expose_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/expose_decl.fidl#67)*

 Declares a directory exposed to a component's containing realm, such as a
 directory exposed by the component or one of its children at runtime.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td> The provider of the capability relative to the component itself. Must
 be `self` or `child`.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td> Path identifying the directory, by which it was presented to this
 component.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>target</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td> The destination to which the directory is exposed: either the component's realm or the
 framework.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>target_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td> The path by which the capability is being exposed.

 Must be an absolute path starting with /.
</td>
        </tr></table>

### ExposeRunnerDecl {:#ExposeRunnerDecl}


*Defined in [fuchsia.sys2/expose_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/expose_decl.fidl#88)*

 Declares a runner exposed to a component's containing realm, such as a
 runner exposed by the component or one of its children at runtime.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td> The provider of the capability relative to the component itself. Must
 be `self` or `child`.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source_name</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td> The name of the runner, by which it was presented to this component.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>target</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td> The destination to which the runner is exposed: either the component's realm or the
 framework.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>target_name</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td> The name by which the capability is being exposed.
</td>
        </tr></table>

### OfferServiceDecl {:#OfferServiceDecl}


*Defined in [fuchsia.sys2/offer_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/offer_decl.fidl#23)*

 Declares a service offered by a component to one of its children, which may
 have been offered by the component's containing realm, the component itself,
 or one of its other children.

 To learn more about services, see:
 https://fuchsia.dev/fuchsia-src/glossary#service


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td> The provider of the capability relative to the component itself. Must be
 `realm`, `self`, or `child`.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td> Path identifying the service being offered.

 Must be an absolute path starting with /.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>target</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td> Reference to the target. Must be `child` or `collection`.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>target_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td> The path under which the capability is being offered.

 Must be an absolute path starting with /.
</td>
        </tr></table>

### OfferLegacyServiceDecl {:#OfferLegacyServiceDecl}


*Defined in [fuchsia.sys2/offer_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/offer_decl.fidl#48)*

 Declares a legacy service offered by a component to one of its children,
 which may have been offered by the component's containing realm, the
 component itself, or one of its other children.

 A legacy service is a service with a single instance, provided by a single
 FIDL protocol.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td> The provider of the capability relative to the component itself. Must be
 `realm`, `self`, or `child`.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td> Path identifying the legacy service being offered.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>target</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td> Reference to the target. Must be `child` or `collection`.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>target_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td> The path under which the capability is being offered.

 Must be an absolute path starting with /.
</td>
        </tr></table>

### OfferDirectoryDecl {:#OfferDirectoryDecl}


*Defined in [fuchsia.sys2/offer_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/offer_decl.fidl#68)*

 Declares a directory offered by a component to one of its children, which
 may have been offered by the component's containing realm, the component
 itself, or one of its other children.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td> The provider of the capability relative to the component itself. Must be
 `realm`, `self`, or `child`.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td> Path identifying the directory being offered.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>target</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td> Reference to the target of the capability. Must be `child` or
 `collection`.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>target_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td> The path under which the capability is being offered.

 Must be an absolute path starting with /.
</td>
        </tr></table>

### OfferStorageDecl {:#OfferStorageDecl}


*Defined in [fuchsia.sys2/offer_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/offer_decl.fidl#89)*

 Declares a storage capability offered by a component to one of its children,
 such as meta storage offered by the component's containing realm or cache
 storage offered by the component itself.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#StorageType'>StorageType</a></code>
            </td>
            <td> The type of storage being offered.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td> The source of the storage capability. Must be `realm` or `storage`.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>target</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td> Reference to the target of the capability. Must be `child` or
 `collection`.
</td>
        </tr></table>

### OfferRunnerDecl {:#OfferRunnerDecl}


*Defined in [fuchsia.sys2/offer_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/offer_decl.fidl#104)*

 Declares a runner offered by a component to one of its children, which may
 have been offered by the component's containing realm, the component itself,
 or one of its other children.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td> The provider of the capability relative to the component itself. Must be
 `realm`, `self`, or `child`.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source_name</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td> Name of the runner being offered.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>target</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td> Reference to the target of the capability. Must be `child` or
 `collection`.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>target_name</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td> Name under which the capability is being offered.
</td>
        </tr></table>

### RunnerDecl {:#RunnerDecl}


*Defined in [fuchsia.sys2/runner_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/runner_decl.fidl#8)*

 Declares a runner capability backed by a service.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td> The name of this runner.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td> The provider of the underlying service relative to the component itself.
 Must be `realm`, `self`, or `child`.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>source_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td> The path of the capability within the specified source.
</td>
        </tr></table>

### StorageDecl {:#StorageDecl}


*Defined in [fuchsia.sys2/storage_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/storage_decl.fidl#22)*

 Declares a storage capability backed by a directory from which data, cache,
 or meta storage can be offered.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td> The name of this storage
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td> The provider of the underlying directory capability relative to the
 component itself. Must be `realm`, `self`, or `child`.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>source_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td> The incoming path to the directory capability. If "source == SELF", this
 is a path in the component's outgoing directory. Otherwise, it is the
 path by which the capability was presented to the component.
</td>
        </tr></table>

### UseServiceDecl {:#UseServiceDecl}


*Defined in [fuchsia.sys2/use_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/use_decl.fidl#21)*

 Declares a service used by a component, which was offered to the component's
 environment.

 To learn more about services, see:
 https://fuchsia.dev/fuchsia-src/glossary#service


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td> The provider of the service relative to the component itself. Must
 be |realm| or |framework|.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td> Path identifying the service, by which it was presented to this
 component.

 Must be an absolute path starting with /.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>target_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td> The path where the capability should be installed in the component's
 namespace.

 Must be an absolute path starting with /.
</td>
        </tr></table>

### UseLegacyServiceDecl {:#UseLegacyServiceDecl}


*Defined in [fuchsia.sys2/use_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/use_decl.fidl#44)*

 Declares a legacy service used by a component, which was offered to the
 component's environment.

 A legacy service is a service with a single instance, provided by a single
 FIDL protocol.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td> The provider of the legacy service relative to the component itself.
 Must be |realm| or |framework|.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td> Path identifying the legacy service, by which it was presented to this
 component.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>target_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td> The path where the capability should be installed in the component's
 namespace.

 Must be an absolute path starting with /.
</td>
        </tr></table>

### UseDirectoryDecl {:#UseDirectoryDecl}


*Defined in [fuchsia.sys2/use_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/use_decl.fidl#62)*

 Declares a directory used by a component, which was offered to the
 component's environment.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td> The provider of the directory relative to the component itself. Must
 be |realm| or |framework|.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td> Path identifying the directory, by which it was presented to this
 component.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>target_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td> The path where the capability should be installed in the component's
 namespace.

 Must be an absolute path starting with /.
</td>
        </tr></table>

### UseStorageDecl {:#UseStorageDecl}


*Defined in [fuchsia.sys2/use_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/use_decl.fidl#80)*

 Declares storage used by a component, which was offered to the component's
 environment.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#StorageType'>StorageType</a></code>
            </td>
            <td> Type of storage used by the component.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>target_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td> The path where the capability should be installed in the component's
 namespace. Must not be set if `type` is `META`.

 Must be an absolute path starting with /.
</td>
        </tr></table>

### UseRunnerDecl {:#UseRunnerDecl}


*Defined in [fuchsia.sys2/use_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/use_decl.fidl#93)*

 Declares a runner used by a component, which was offered to the component's
 environment.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td> The name of the runner, as it was presented to this component.
</td>
        </tr></table>

### Component {:#Component}


*Defined in [fuchsia.sys2/component.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/runtime/component.fidl#11)*

 A component is a unit of executable software.

 This object provides the component's declaration, access to its package's
 content, and relevant metadata.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>resolved_url</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The resolved URL of the component.
 This is the canonical URL obtained by the component resolver after
 after following redirects and resolving relative paths.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>decl</code></td>
            <td>
                <code><a class='link' href='#ComponentDecl'>ComponentDecl</a></code>
            </td>
            <td> The component's declaration.
 This information is typically obtained from the component's manifest
 or generated by the component resolver.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>package</code></td>
            <td>
                <code><a class='link' href='#Package'>Package</a></code>
            </td>
            <td> The package that contains the component.
 By convention, the component's package is mapped to "/pkg" in its
 namespace at runtime.

 This is null if the component is not represented as a package.
 In that case, it is the runner's responsibility to load the component's
 resource from the `resolved_url`.  This mechanism is used for web
 applications.

</td>
        </tr></table>

### ComponentStartInfo {:#ComponentStartInfo}


*Defined in [fuchsia.sys2/component_runner.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/runtime/component_runner.fidl#34)*

 Parameters for starting a new component instance.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>resolved_url</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The resolved URL of the component.
 This is the canonical URL obtained by the component resolver after
 after following redirects and resolving relative paths.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>program</code></td>
            <td>
                <code><a class='link' href='../fuchsia.data/index.html'>fuchsia.data</a>/<a class='link' href='../fuchsia.data/index.html#Dictionary'>Dictionary</a></code>
            </td>
            <td> The component's program declaration.
 This information originates from `ComponentDecl.program`.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>ns</code></td>
            <td>
                <code><a class='link' href='#ComponentNamespace'>ComponentNamespace</a></code>
            </td>
            <td> The namespace to provide to the component instance.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>outgoing_dir</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.io/index.html'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/index.html#Directory'>Directory</a>&gt;</code>
            </td>
            <td> The directory this component serves.
</td>
        </tr><tr>
            <td>5</td>
            <td><code>runtime_dir</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.io/index.html'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/index.html#Directory'>Directory</a>&gt;</code>
            </td>
            <td> The directory served by the runner to present runtime information about
 the component.
</td>
        </tr></table>

### Package {:#Package}


*Defined in [fuchsia.sys2/package.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/runtime/package.fidl#12)*

 A package is a signed collection of immutable files.

 This object provides access to a package's content and relevant metadata.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>package_url</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The URL of the package itself.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>package_dir</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io/index.html'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/index.html#Directory'>Directory</a></code>
            </td>
            <td> The package's content directory.
</td>
        </tr></table>

### WorkRequest {:#WorkRequest}


*Defined in [fuchsia.sys2/work_scheduler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/work_scheduler.fidl#22)*

 Parameters for a new piece of work to be scheduled.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>start</code></td>
            <td>
                <code><a class='link' href='#Start'>Start</a></code>
            </td>
            <td> Time when corresponding work item should be _first_ scheduled.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>period</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> Delay between repeated schedulings of corresponding work item. This is left unspecified for
 one-shot work that should not repeat. Repeating work items are rescheduled indefinitely
 until it is canceled.
</td>
        </tr></table>



## **UNIONS**

### Realm_BindChild_Result {:#Realm_BindChild_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Realm_BindChild_Response'>Realm_BindChild_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Realm_CreateChild_Result {:#Realm_CreateChild_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Realm_CreateChild_Response'>Realm_CreateChild_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Realm_DestroyChild_Result {:#Realm_DestroyChild_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Realm_DestroyChild_Response'>Realm_DestroyChild_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Realm_ListChildren_Result {:#Realm_ListChildren_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Realm_ListChildren_Response'>Realm_ListChildren_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### WorkScheduler_ScheduleWork_Result {:#WorkScheduler_ScheduleWork_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#WorkScheduler_ScheduleWork_Response'>WorkScheduler_ScheduleWork_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### WorkScheduler_CancelWork_Result {:#WorkScheduler_CancelWork_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#WorkScheduler_CancelWork_Response'>WorkScheduler_CancelWork_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Worker_DoWork_Result {:#Worker_DoWork_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Worker_DoWork_Response'>Worker_DoWork_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### WorkSchedulerControl_GetBatchPeriod_Result {:#WorkSchedulerControl_GetBatchPeriod_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#WorkSchedulerControl_GetBatchPeriod_Response'>WorkSchedulerControl_GetBatchPeriod_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### WorkSchedulerControl_SetBatchPeriod_Result {:#WorkSchedulerControl_SetBatchPeriod_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#WorkSchedulerControl_SetBatchPeriod_Response'>WorkSchedulerControl_SetBatchPeriod_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>



## **XUNIONS**

### ExposeDecl {:#ExposeDecl}
*Defined in [fuchsia.sys2/expose_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/expose_decl.fidl#9)*

 Declares a capability exposed to either a component's containing realm or to the framework.
 For example, a legacy service exposed by the component at runtime.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>service</code></td>
            <td>
                <code><a class='link' href='#ExposeServiceDecl'>ExposeServiceDecl</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>legacy_service</code></td>
            <td>
                <code><a class='link' href='#ExposeLegacyServiceDecl'>ExposeLegacyServiceDecl</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>directory</code></td>
            <td>
                <code><a class='link' href='#ExposeDirectoryDecl'>ExposeDirectoryDecl</a></code>
            </td>
            <td></td>
        </tr></table>

### OfferDecl {:#OfferDecl}
*Defined in [fuchsia.sys2/offer_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/offer_decl.fidl#10)*

 Declares a capability offered by a component to one of its children, which
 may have been offered by the component's containing realm, the component
 itself, or one of its other children.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>service</code></td>
            <td>
                <code><a class='link' href='#OfferServiceDecl'>OfferServiceDecl</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>legacy_service</code></td>
            <td>
                <code><a class='link' href='#OfferLegacyServiceDecl'>OfferLegacyServiceDecl</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>directory</code></td>
            <td>
                <code><a class='link' href='#OfferDirectoryDecl'>OfferDirectoryDecl</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>storage</code></td>
            <td>
                <code><a class='link' href='#OfferStorageDecl'>OfferStorageDecl</a></code>
            </td>
            <td></td>
        </tr></table>

### Ref {:#Ref}
*Defined in [fuchsia.sys2/relative_refs.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/relative_refs.fidl#9)*

 A reference to a capability source or destination relative to this
 component.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>realm</code></td>
            <td>
                <code><a class='link' href='#RealmRef'>RealmRef</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>self</code></td>
            <td>
                <code><a class='link' href='#SelfRef'>SelfRef</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>child</code></td>
            <td>
                <code><a class='link' href='#ChildRef'>ChildRef</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>collection</code></td>
            <td>
                <code><a class='link' href='#CollectionRef'>CollectionRef</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>storage</code></td>
            <td>
                <code><a class='link' href='#StorageRef'>StorageRef</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>framework</code></td>
            <td>
                <code><a class='link' href='#FrameworkRef'>FrameworkRef</a></code>
            </td>
            <td></td>
        </tr></table>

### UseDecl {:#UseDecl}
*Defined in [fuchsia.sys2/use_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/use_decl.fidl#9)*

 Declares a capability used by a component, which was offered to the
 component's environment.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>service</code></td>
            <td>
                <code><a class='link' href='#UseServiceDecl'>UseServiceDecl</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>legacy_service</code></td>
            <td>
                <code><a class='link' href='#UseLegacyServiceDecl'>UseLegacyServiceDecl</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>directory</code></td>
            <td>
                <code><a class='link' href='#UseDirectoryDecl'>UseDirectoryDecl</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>storage</code></td>
            <td>
                <code><a class='link' href='#UseStorageDecl'>UseStorageDecl</a></code>
            </td>
            <td></td>
        </tr></table>

### Start {:#Start}
*Defined in [fuchsia.sys2/work_scheduler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/work_scheduler.fidl#13)*

 Different ways to specify when to schedule a work item for the first time.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>delay</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> A non-negative delay to wait before scheduling work.
</td>
        </tr><tr>
            <td><code>monotonic_time</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> A fixed point in time to start scheduling work, interpreted like `ZX_CLOCK_MONOTONIC`:
 number of nanoseconds since the system was powered on.
</td>
        </tr></table>





## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/constants.fidl#7">MAX_FACET_NAME_LENGTH</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/constants.fidl#8">MAX_CHILD_NAME_LENGTH</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/constants.fidl#9">MAX_COLLECTION_NAME_LENGTH</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/constants.fidl#10">MAX_RUNNER_NAME_LENGTH</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/constants.fidl#11">MAX_STORAGE_NAME_LENGTH</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/constants.fidl#12">MAX_PATH_LENGTH</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/constants.fidl#13">MAX_URL_LENGTH</a></td>
            <td>
                    <code>4096</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/constants.fidl#14">MAX_MONIKER_LENGTH</a></td>
            <td>
                    <code>4096</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/constants.fidl#17">ERR_COMPONENT_DIED</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>int32</code></td>
            <td> Error produced when a component terminates unexpected.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/work_scheduler.fidl#9">MAX_WORK_ID_LENGTH</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    
</table>

