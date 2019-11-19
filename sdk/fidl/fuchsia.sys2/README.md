[TOC]

# fuchsia.sys2


## **PROTOCOLS**

## Realm {#Realm}
*Defined in [fuchsia.sys2/realm.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/realm.fidl#15)*

<p>A protocol used by a component instance to manage its own realm, such as for
binding to its children.</p>
<p>The component manager provides this service to components that use
<code>/svc/fuchsia.sys2.Realm</code>.</p>

### BindChild {#BindChild}

<p>Binds to a child component instance, causing it to start running if it
is not already. When this function successfully returns, <code>child</code> is
running and <code>exposed_dir</code> is bound to a directory that contains the
capabilities which the child exposed to its realm via
<code>ComponentDecl.exposes</code> (specified via &quot;expose&quot; declarations in the
component’s manifest).</p>
<p><code>exposed_dir</code> is a valid channel as long as <code>child</code> is running. <code>child</code>
will remain running until it either stops on its own, or <code>DestroyChild</code>
causes the child instance to be destroyed.</p>
<p>For example, if the child exposes a service <code>/svc/example.Echo</code> then
<code>exposed_dir</code> will contain that service at that path.</p>
<p>NOTE: <code>BindChild</code> does not support pipelining with <code>CreateChild</code>. If
<code>BindChild</code> is called on an instance before <code>CreateChild</code> successfully
returns, it may return <code>INSTANCE_NOT_FOUND</code>.</p>
<p>Errors:</p>
<ul>
<li><code>INVALID_ARGUMENTS</code>: <code>child</code> is not a valid child reference.  -</li>
<li><code>INSTANCE_NOT_FOUND</code>: <code>child</code> does not exist.</li>
<li><code>INSTANCE_CANNOT_START</code>: <code>child</code> was not running and there was an error
starting it.</li>
<li><code>INSTANCE_CANNOT_RESOLVE</code>: <code>child</code>'s component declaration failed to resolve.</li>
</ul>

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
                <code>request&lt;<a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#Directory'>Directory</a>&gt;</code>
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

### CreateChild {#CreateChild}

<p>Creates a child component instance dynamically. When this function
returns successfully, the instance exists, but it may not be running.</p>
<p>Errors:</p>
<ul>
<li><code>INVALID_ARGUMENTS</code>: <code>collection</code> is not a valid reference or <code>child</code>
is not a valid declaration.</li>
<li><code>COLLECTION_NOT_FOUND</code>: <code>collection</code> does not exist.</li>
<li><code>INSTANCE_ALREADY_EXISTS</code>: <code>decl.name</code> already exists in <code>collection</code>.</li>
<li><code>NO_SPACE</code>: Could not allocate storage for the new instance.</li>
</ul>

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

### DestroyChild {#DestroyChild}

<p>Destroys a dynamically-created component instance. When this function
returns, the client should assume the instance no longer exists.
However, some cleanup (such as stopping the component instance or
freeing its storage) may be performed in the background after the
function returns.</p>
<p>Errors:</p>
<ul>
<li><code>INVALID_ARGUMENTS</code>: <code>child</code> is not a valid reference or does not refer
to a dynamic instance.</li>
<li><code>INSTANCE_NOT_FOUND</code>: <code>child</code> does not exist.</li>
<li><code>COLLECTION_NOT_FOUND</code>: <code>collection</code> does not exist.</li>
</ul>

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

### ListChildren {#ListChildren}

<p>Returns an iterator that lists all instances in a collection.</p>
<p>NOTE: The results are not guaranteed to be consistent. Instances may be
created or destroyed while the iterator is live, but those changes
won't be observed by the iterator after this method returns.</p>
<p>Errors:</p>
<ul>
<li><code>INVALID_ARGUMENTS</code>: <code>collection</code> is not a valid reference.</li>
<li><code>COLLECTION_NOT_FOUND</code>: <code>collection</code> does not exist.</li>
</ul>

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

## ChildIterator {#ChildIterator}
*Defined in [fuchsia.sys2/realm.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/realm.fidl#81)*

<p>A protocol to iterate over the list of children in a realm.</p>

### Next {#Next}

<p>Advance the iterator and return the next batch of children.</p>
<p>Returns a vector of <code>ChildRef</code>. Returns an empty vector when there are
no more children.</p>

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

## ComponentResolver {#ComponentResolver}
*Defined in [fuchsia.sys2/component_resolver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/runtime/component_resolver.fidl#22)*

<p>An interface for resolving a URL to a component.</p>
<p>This interface is implemented by components that provide support
for loading components with a particular URL scheme.   For example,
the Fuchsia package component resolver exposes a service with this
interface to resolve component URLs using the &quot;fuchsia-pkg://&quot; scheme.</p>
<p>To use a resolver to resolve URLs within your realm, register it
in your realm's manifest.  (TODO: explain in more detail)</p>
<p>Note: The component manager is the only intended direct client of this
interface.</p>

### Resolve {#Resolve}

<p>Resolves a component with the given URL.</p>
<p><code>component_url</code> is the unescaped URL of the component to resolve.</p>
<p>If successful, returns <code>ZX_OK</code> and information about the component
that was resolved.</p>
<p>On failure, returns null <code>info</code> and...</p>
<ul>
<li><code>ZX_ERR_INVALID_ARGS</code>: The component's URL was malformed.</li>
<li><code>ZX_ERR_NOT_FOUND</code>: The component does not exist.</li>
<li><code>ZX_ERR_UNAVAILABLE</code>: The resolver was unable to retrieve or parse
the component's resources.</li>
</ul>

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

## ComponentRunner {#ComponentRunner}
*Defined in [fuchsia.sys2/component_runner.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/runtime/component_runner.fidl#23)*

<p>An interface for running components.</p>
<p>This interface is implemented by components that provide an execution
environment for running particular classes of programs.  For example,
the Dart virtual machine exposes a service with this interface to run
Dart programs.</p>
<p>To specify the runner needed to run your component, set the &quot;runner_url&quot;
property in your component's manifest.</p>
<p>Note: The component manager is the only intended direct client of this
interface.</p>

### Start {#Start}

<p>Starts running a new component instance described by <code>start_info</code>.</p>
<p>The caller of this method takes responsibility for binding client
connections and controlling the lifetime of the newly started
component instance through the requested <code>controller</code>.</p>

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



## ComponentController {#ComponentController}
*Defined in [fuchsia.sys2/component_runner.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/runtime/component_runner.fidl#94)*

<p>An interface for binding client connections and controlling the lifetime
of a component instance started using <code>ComponentRunner.Start()</code>.</p>
<p>When the controlled component instance terminates or becomes inaccessible
for any reason, the server invokes <code>OnEpitaph()</code> and closes its endpoint
of the controller interface.</p>
<p>LIFECYCLE</p>
<p>A component may exist in one of two states, Started or Stopped. The component
is Started from time <code>ComponentRunner.Start()</code> is called until the
ComponentRunner closes the ComponentController handle. The component then
transitions to Stopped.</p>
<p><code>Stop()</code> is called to indicate a ComponentRunner should end a component's
execution. <code>Kill()</code> indicates that a runner must halt a component's
execution immediately and close the ComponentController's server end. After
the ComponentController is closed the component manager can tear down the
namespace it hosts for the stopped component. The component manager may
call <code>Kill()</code> without first having called <code>Stop()</code>.</p>
<p>EPITAPH</p>
<p>This interface uses a FIDL epitaph to indicate that the controller
component instance has terminated and to describe its final disposition.</p>
<p>The following epitaph status codes have particular significance:</p>
<ul>
<li><code>ZX_OK</code>: The component instance was successfully terminated in response
to <code>Stop()</code> and its runtime resources have been fully released.</li>
<li><code>ZX_ERR_UNAVAILABLE</code>: The runner was unable to start the component
instance.  e.g. The runner could not retrieve the component's assets.</li>
<li><code>ERR_COMPONENT_DIED</code>: The component instance was started but
subsequently terminated unexpectedly.</li>
</ul>
<p>Other status codes (e.g. <code>ZX_ERR_PEER_CLOSED</code>) may indicate a failure
of the component runner itself.  The component manager may respond to such
failures by terminating the component runner's job to ensure system
stability.</p>

### Stop {#Stop}

<p>Requests the runner to stop the controlled component instance.</p>
<p>After stopping the component instance, the server should report
an epitaph then close its endpoint of the controller interface.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Kill {#Kill}

<p>Stop this component immediately. This ComponentRunner must immediately
kill the component instance, set an epitaph set on the channel, and
close the channel. After the channel closes, the component instance will
be considered by the component manager to be Stopped and the component's
namespace will be torn down.</p>
<p>Kill() may have been preceeded by Stop(), but that is not guaranteed.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## SystemController {#SystemController}
*Defined in [fuchsia.sys2/system_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/system_controller.fidl#10)*

<p>An interface implemented by ComponentManager that requests the
ComponentManager stop all components and exit.</p>

### Shutdown {#Shutdown}

<p>Stop all components, return an empty result, close this protocol's
channel, and exit ComponentManager. If this is the root ComponentManager
is exited we expect the system will reboot.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## WorkScheduler {#WorkScheduler}
*Defined in [fuchsia.sys2/work_scheduler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/work_scheduler.fidl#40)*

<p>Framework service: API for scheduling and canceling work. Each component instance can access
work items that it has scheduled (but not others' scheduled work items). Work items are
scheduled <em>roughly</em> at the specified time and frequency; the service implementation may specify
its notion of <em>roughly</em>, and may provide a configuration API to tune this notion.</p>
<p>Each scheduled work item is identified by a client-provided <code>WorkId</code>. Each scheduled work item
has a <code>WorkId</code> that is unique with respect to scheduled work items belonging to the same
component instance.</p>

### ScheduleWork {#ScheduleWork}

<p>Schedule a new work item identified by <code>work_id</code>. The work item is to be scheduled roughly
at the time corresponding to <code>work_request.start</code>. When <code>work_request.period</code> is specified,
reschedule work roughly every <code>work_request.period</code> until the the work item is canceled.</p>

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

### CancelWork {#CancelWork}

<p>Cancel the scheduled work item specified by <code>work_id</code>.</p>

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

## Worker {#Worker}
*Defined in [fuchsia.sys2/work_scheduler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/work_scheduler.fidl#57)*

<p>Component-exposed service: Work scheduler connects to this service to invoke scheduled work item
callbacks. The service implementation is responsible for invoking the code that corresponds to
the scheduled work item identified by <code>work_id</code>.</p>
<p>Note: The intent of exposing this service is to expose it to the <code>WorkScheduler</code> service
provider (i.e., the framework) and no one else.</p>

### DoWork {#DoWork}


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

## WorkSchedulerControl {#WorkSchedulerControl}
*Defined in [fuchsia.sys2/work_scheduler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/work_scheduler.fidl#69)*

<p>Framework service: Administrative API for controlling parameters of the <code>WorkScheduler</code>
framework service. So long as there are work items with deadlines in the next <code>batch_period</code>,
the <code>WorkScheduler</code> will sleep for <code>batch_period</code>, then wake up and immediately dispatch a batch
of work items: all those with past deadlines. It will repeat this process until no work items
would be scheduled in the next <code>batch_period</code>, at which point it will go to sleep until the next
deadline. This strategy ensures that each work item is dispatched approximately within
<code>batch_period</code> of its deadline.</p>

### GetBatchPeriod {#GetBatchPeriod}

<p>Get the current period between <code>WorkScheduler</code> attempts to dispatch a batch of work.
<code>batch_period</code> is a non-negative 64-bit integer in the range [0, 2^63-1], representing a
number of nanoseconds between dispatching batches of work.</p>

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

### SetBatchPeriod {#SetBatchPeriod}

<p>Set the current period between <code>WorkScheduler</code> attempts to batch and dispatch a batch of
work. <code>batch_period</code> is a non-negative 64-bit integer in the range [0, 2^63-1], representing
a number of nanoseconds between dispatching batches of work.</p>

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

### RealmRef {#RealmRef}
*Defined in [fuchsia.sys2/relative_refs.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/relative_refs.fidl#19)*



<p>A reference to a component’s containing realm, i.e. the parent component.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### SelfRef {#SelfRef}
*Defined in [fuchsia.sys2/relative_refs.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/relative_refs.fidl#22)*



<p>A reference to the component itself.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### ChildRef {#ChildRef}
*Defined in [fuchsia.sys2/relative_refs.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/relative_refs.fidl#25)*



<p>A reference to one of the component's child instances.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td><p>The name assigned to the child by its parent. If <code>collection</code> is set,
<code>name</code> is scoped to <code>collection</code> and the child is a dynamic instance.
Required.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>collection</code></td>
            <td>
                <code>string[100]?</code>
            </td>
            <td><p>The collection <code>name</code> belongs to. If omitted, <code>name</code> references a static
instance. This field must be omitted if the <code>ChildRef</code> is being used in
a component declaration. Optional.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### CollectionRef {#CollectionRef}
*Defined in [fuchsia.sys2/relative_refs.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/relative_refs.fidl#37)*



<p>A reference to one of the component's collections.</p>


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

### StorageRef {#StorageRef}
*Defined in [fuchsia.sys2/relative_refs.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/relative_refs.fidl#42)*



<p>A reference to one of the component's storage sections.</p>


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

### FrameworkRef {#FrameworkRef}
*Defined in [fuchsia.sys2/relative_refs.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/relative_refs.fidl#47)*



<p>A reference to the component framework itself.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Moniker {#Moniker}
*Defined in [fuchsia.sys2/moniker.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/moniker.fidl#19)*



<p>A moniker encodes the relationship between two component instances that
exist in the component instance tree at runtime.</p>
<p>To understand this better, consider two component instances labeled &quot;A&quot;
and &quot;B&quot; that are both children of a component instance labeled &quot;P&quot;.</p>
<p>At runtime, when &quot;B&quot; requests a service from &quot;A&quot; through a channel
established by the component manager, the component manager may provide
&quot;A&quot; with a moniker that encodes &quot;B's&quot; identity relative to &quot;A&quot; itself.
The moniker's encoded value describes the directed path to traverse from
&quot;A&quot; (the moniker's origin) to &quot;B&quot; (the moniker's referent), passing
through &quot;P&quot; (their common ancestor).</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>encoded_value</code></td>
            <td>
                <code>string[4096]</code>
            </td>
            <td><p>An opaque representation of the moniker's relation.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### Realm_BindChild_Response {#Realm_BindChild_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Realm_CreateChild_Response {#Realm_CreateChild_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Realm_DestroyChild_Response {#Realm_DestroyChild_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Realm_ListChildren_Response {#Realm_ListChildren_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### ComponentNamespace {#ComponentNamespace}
*Defined in [fuchsia.sys2/component_namespace.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/runtime/component_namespace.fidl#21)*



<p>A namespace specifies the set of directories that a component instance
receives at start-up.  Each component instance's namespace is tailored
to provide access to a set of files and services that are appropriate
to that component instance's role in the system (its sandbox).</p>
<p>By convention, a component's namespace typically contains some or all
of the following directories:</p>
<ul>
<li>&quot;/svc&quot;: A directory containing services that the component requested
to use via its &quot;import&quot; declarations.</li>
<li>&quot;/pkg&quot;: A directory containing the component's package, including its
binaries, libraries, and other assets.</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>paths</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td><p>The mount point for each of the directories below, each including a
leading slash.  For example, [&quot;/pkg&quot;, &quot;/svc&quot;, &quot;/config/data&quot;].</p>
<p>Each mount point must be unique and non-overlapping.
For example, [&quot;/foo&quot;, &quot;/foo/bar&quot;] is invalid.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>directories</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#Directory'>Directory</a>&gt;</code>
            </td>
            <td><p>The directories mounted at each path in the namespace.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### WorkScheduler_ScheduleWork_Response {#WorkScheduler_ScheduleWork_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### WorkScheduler_CancelWork_Response {#WorkScheduler_CancelWork_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Worker_DoWork_Response {#Worker_DoWork_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### WorkSchedulerControl_GetBatchPeriod_Response {#WorkSchedulerControl_GetBatchPeriod_Response}
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

### WorkSchedulerControl_SetBatchPeriod_Response {#WorkSchedulerControl_SetBatchPeriod_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>



## **ENUMS**

### StartupMode {#StartupMode}
Type: <code>uint32</code>

*Defined in [fuchsia.sys2/child_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/child_decl.fidl#30)*

<p>Describes under what conditions the component may be started.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>LAZY</code></td>
            <td><code>0</code></td>
            <td><p>Start component instance only when another instance binds to it.</p>
</td>
        </tr><tr>
            <td><code>EAGER</code></td>
            <td><code>1</code></td>
            <td><p>Start component instance as soon as parent starts. This mode is only
supported for statically declared children -- a dynamic instance may only be
started by binding to it.</p>
</td>
        </tr></table>

### Durability {#Durability}
Type: <code>uint32</code>

*Defined in [fuchsia.sys2/collection_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/collection_decl.fidl#18)*

<p>The durability of component instances created in a collection.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>PERSISTENT</code></td>
            <td><code>1</code></td>
            <td><p>An instance exists until either it or its parent is destroyed.</p>
</td>
        </tr><tr>
            <td><code>TRANSIENT</code></td>
            <td><code>2</code></td>
            <td><p>An instance exists until either its parent instance is stopped
or it is explicitly destroyed.</p>
</td>
        </tr></table>

### StorageType {#StorageType}
Type: <code>uint32</code>

*Defined in [fuchsia.sys2/storage_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/storage_decl.fidl#8)*

<p>The type of storage offered by this component.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DATA</code></td>
            <td><code>1</code></td>
            <td><p>General data storage.</p>
</td>
        </tr><tr>
            <td><code>CACHE</code></td>
            <td><code>2</code></td>
            <td><p>Cache storage that may be deleted at any time by the system.</p>
</td>
        </tr><tr>
            <td><code>META</code></td>
            <td><code>3</code></td>
            <td><p>Meta storage that will be used by component manager to persist metadata
and other information about the component</p>
</td>
        </tr></table>

### Error {#Error}
Type: <code>uint32</code>

*Defined in [fuchsia.sys2/error.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/error.fidl#8)*

<p>Standard error codes for component framework protocols.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INTERNAL</code></td>
            <td><code>1</code></td>
            <td><p>Component manager encountered an otherwise unspecified error while
performing the operation.</p>
</td>
        </tr><tr>
            <td><code>INVALID_ARGUMENTS</code></td>
            <td><code>2</code></td>
            <td><p>At least one argument had an invalid format.</p>
</td>
        </tr><tr>
            <td><code>UNSUPPORTED</code></td>
            <td><code>3</code></td>
            <td><p>The feature is not yet supported.</p>
</td>
        </tr><tr>
            <td><code>INSTANCE_NOT_FOUND</code></td>
            <td><code>4</code></td>
            <td><p>The component instance was not found.</p>
</td>
        </tr><tr>
            <td><code>INSTANCE_ALREADY_EXISTS</code></td>
            <td><code>5</code></td>
            <td><p>The component instance already exists.</p>
</td>
        </tr><tr>
            <td><code>INSTANCE_CANNOT_START</code></td>
            <td><code>6</code></td>
            <td><p>The component instance could not be started.</p>
</td>
        </tr><tr>
            <td><code>INSTANCE_CANNOT_RESOLVE</code></td>
            <td><code>7</code></td>
            <td><p>Failed to resolve the component's declaration.</p>
</td>
        </tr><tr>
            <td><code>COLLECTION_NOT_FOUND</code></td>
            <td><code>8</code></td>
            <td><p>The component collection was not found.</p>
</td>
        </tr><tr>
            <td><code>NO_SPACE</code></td>
            <td><code>9</code></td>
            <td><p>There was insufficient space to perform the operation.</p>
</td>
        </tr></table>



## **TABLES**

### ChildDecl {#ChildDecl}


*Defined in [fuchsia.sys2/child_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/child_decl.fidl#8)*

<p>Statically declares a child component instance.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td><p>The name assigned to the child by its parent.</p>
<p>Must be non-empty, unique among all siblings, and contain only the
following characters: [a-z0-9-_.].</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>url</code></td>
            <td>
                <code>string[4096]</code>
            </td>
            <td><p>The child component's URL.</p>
<p>Must be non-empty and a well-formed URL.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>startup</code></td>
            <td>
                <code><a class='link' href='#StartupMode'>StartupMode</a></code>
            </td>
            <td><p>The startup mode for the component instance.</p>
</td>
        </tr></table>

### CollectionDecl {#CollectionDecl}


*Defined in [fuchsia.sys2/collection_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/collection_decl.fidl#8)*

<p>Statically declares a component instance collection.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td><p>The name of the collection. Instances created in the collection are
scoped to this name.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>durability</code></td>
            <td>
                <code><a class='link' href='#Durability'>Durability</a></code>
            </td>
            <td><p>The durability of instances in the collection.</p>
</td>
        </tr></table>

### ComponentDecl {#ComponentDecl}


*Defined in [fuchsia.sys2/component_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/component_decl.fidl#14)*

<p>A component declaration.</p>
<p>This information is typically encoded in the component manifest (.cm file)
if it has one or may be generated at runtime by a component resolver for
those that don't.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>program</code></td>
            <td>
                <code><a class='link' href='../fuchsia.data/'>fuchsia.data</a>/<a class='link' href='../fuchsia.data/#Dictionary'>Dictionary</a></code>
            </td>
            <td><p>Information about the program to run when the component is executed.</p>
<p>The component manager provides the contents of this dictionary to the
component runner when executing the program. Each component runner can
freely define the contents of this dictionary as needed.</p>
<p>The system's default runner understands the following entries:</p>
<ul>
<li>
<p>&quot;binary&quot;: string
The path of the executable relative to the root of the package.
Typically an ELF binary.</p>
</li>
<li>
<p>&quot;args&quot;: vector of strings
The command-line arguments to provide to the executable at runtime.</p>
</li>
<li>
<p>&quot;env&quot;: dictionary of strings
The environment variables to provide to the executable at runtime.</p>
</li>
</ul>
<p>Other runners may define different entries.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>uses</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#UseDecl'>UseDecl</a>&gt;</code>
            </td>
            <td><p>List of capabilities used by the component. These consist of
capabilities offered to the component that are installed in its incoming
namespace.</p>
<p>The used capabilities must be unique and non-overlapping.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>exposes</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ExposeDecl'>ExposeDecl</a>&gt;</code>
            </td>
            <td><p>List of capabilities exposed by the component. These consist of
capabilities that are made visible to the containing realm. The parent
may <code>offer</code> these capabilities to its children, but not <code>use</code> them.</p>
<p>The exposed capabilities must be unique and non-overlapping.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>offers</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#OfferDecl'>OfferDecl</a>&gt;</code>
            </td>
            <td><p>List of capabilities offered to the component’s children. These consist
of capabilities that the given children may <code>use</code>, which may come from a
child, the containing realm, or the component's own outgoing namespace.</p>
<p>The offered capabilities must be unique and non-overlapping.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>facets</code></td>
            <td>
                <code><a class='link' href='../fuchsia.data/'>fuchsia.data</a>/<a class='link' href='../fuchsia.data/#Dictionary'>Dictionary</a></code>
            </td>
            <td><p>Additional metadata about the component.</p>
</td>
        </tr><tr>
            <td>6</td>
            <td><code>children</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ChildDecl'>ChildDecl</a>&gt;</code>
            </td>
            <td><p>The component's statically instantiated children. The children must have
unique names.</p>
</td>
        </tr><tr>
            <td>7</td>
            <td><code>collections</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#CollectionDecl'>CollectionDecl</a>&gt;</code>
            </td>
            <td><p>The component's collections. The collections must have unique names.</p>
</td>
        </tr><tr>
            <td>8</td>
            <td><code>storage</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#StorageDecl'>StorageDecl</a>&gt;</code>
            </td>
            <td><p>List of storage capabilities created by this component.
Storage capabilities can be offered to children.</p>
</td>
        </tr><tr>
            <td>9</td>
            <td><code>runners</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#RunnerDecl'>RunnerDecl</a>&gt;</code>
            </td>
            <td><p>List of runner capabilities created by this component.
Runner capabilities can be exposed to the parent's realm or offered to children.</p>
</td>
        </tr></table>

### ExposeServiceDecl {#ExposeServiceDecl}


*Defined in [fuchsia.sys2/expose_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/expose_decl.fidl#23)*

<p>Declares a service exposed to a component's containing realm, such as a
service exposed by the component or one of its children at runtime.</p>
<p>To learn more about services, see:
https://fuchsia.dev/fuchsia-src/glossary#service</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td><p>The provider of the capability relative to the component itself. Must
be <code>self</code> or <code>child</code>.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>Path identifying the service, by which it was presented to this
component.</p>
<p>Must be an absolute path starting with /.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>target</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td><p>The destination to which the service is exposed: either the component's realm or the
framework.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>target_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>The path by which the capability is being exposed.</p>
<p>Must be an absolute path starting with /.</p>
</td>
        </tr></table>

### ExposeLegacyServiceDecl {#ExposeLegacyServiceDecl}


*Defined in [fuchsia.sys2/expose_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/expose_decl.fidl#49)*

<p>Declares a legacy service exposed to a component's containing realm, such as
a legacy service exposed by the component or one of its children at runtime.</p>
<p>A legacy service is a service with a single instance, provided by a single
FIDL protocol.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td><p>The provider of the capability relative to the component itself. Must
be <code>self</code> or <code>child</code>.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>Path identifying the legacy service, by which it was presented to this
component.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>target</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td><p>The destination to which the legacy service is exposed: either the component's realm or the
framework.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>target_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>The path by which the capability is being exposed.</p>
<p>Must be an absolute path starting with /.</p>
</td>
        </tr></table>

### ExposeDirectoryDecl {#ExposeDirectoryDecl}


*Defined in [fuchsia.sys2/expose_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/expose_decl.fidl#70)*

<p>Declares a directory exposed to a component's containing realm, such as a
directory exposed by the component or one of its children at runtime.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td><p>The provider of the capability relative to the component itself. Must
be <code>self</code> or <code>child</code>.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>Path identifying the directory, by which it was presented to this
component.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>target</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td><p>The destination to which the directory is exposed: either the component's realm or the
framework.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>target_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>The path by which the capability is being exposed.</p>
<p>Must be an absolute path starting with /.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>rights</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io2/'>fuchsia.io2</a>/<a class='link' href='../fuchsia.io2/#Operations'>Operations</a></code>
            </td>
            <td><p>The rights to expose this directory with, required iff <code>source == self</code>.</p>
</td>
        </tr></table>

### ExposeRunnerDecl {#ExposeRunnerDecl}


*Defined in [fuchsia.sys2/expose_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/expose_decl.fidl#94)*

<p>Declares a runner exposed to a component's containing realm, such as a
runner exposed by the component or one of its children at runtime.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td><p>The provider of the capability relative to the component itself. Must
be <code>self</code> or <code>child</code>.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source_name</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td><p>The name of the runner, by which it was presented to this component.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>target</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td><p>The destination to which the runner is exposed: either the component's realm or the
framework.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>target_name</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td><p>The name by which the capability is being exposed.</p>
</td>
        </tr></table>

### OfferServiceDecl {#OfferServiceDecl}


*Defined in [fuchsia.sys2/offer_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/offer_decl.fidl#26)*

<p>Declares a service offered by a component to one of its children, which may
have been offered by the component's containing realm, the component itself,
or one of its other children.</p>
<p>To learn more about services, see:
https://fuchsia.dev/fuchsia-src/glossary#service</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td><p>The provider of the capability relative to the component itself. Must be
<code>realm</code>, <code>self</code>, or <code>child</code>.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>Path identifying the service being offered.</p>
<p>Must be an absolute path starting with /.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>target</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td><p>Reference to the target. Must be <code>child</code> or <code>collection</code>.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>target_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>The path under which the capability is being offered.</p>
<p>Must be an absolute path starting with /.</p>
</td>
        </tr></table>

### OfferLegacyServiceDecl {#OfferLegacyServiceDecl}


*Defined in [fuchsia.sys2/offer_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/offer_decl.fidl#51)*

<p>Declares a legacy service offered by a component to one of its children,
which may have been offered by the component's containing realm, the
component itself, or one of its other children.</p>
<p>A legacy service is a service with a single instance, provided by a single
FIDL protocol.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td><p>The provider of the capability relative to the component itself. Must be
<code>realm</code>, <code>self</code>, or <code>child</code>.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>Path identifying the legacy service being offered.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>target</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td><p>Reference to the target. Must be <code>child</code> or <code>collection</code>.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>target_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>The path under which the capability is being offered.</p>
<p>Must be an absolute path starting with /.</p>
</td>
        </tr></table>

### OfferDirectoryDecl {#OfferDirectoryDecl}


*Defined in [fuchsia.sys2/offer_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/offer_decl.fidl#71)*

<p>Declares a directory offered by a component to one of its children, which
may have been offered by the component's containing realm, the component
itself, or one of its other children.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td><p>The provider of the capability relative to the component itself. Must be
<code>realm</code>, <code>self</code>, or <code>child</code>.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>Path identifying the directory being offered.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>target</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td><p>Reference to the target of the capability. Must be <code>child</code> or
<code>collection</code>.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>target_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>The path under which the capability is being offered.</p>
<p>Must be an absolute path starting with /.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>rights</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io2/'>fuchsia.io2</a>/<a class='link' href='../fuchsia.io2/#Operations'>Operations</a></code>
            </td>
            <td><p>The rights this directory should be offered with, required iff <code>source == self</code>.</p>
</td>
        </tr></table>

### OfferStorageDecl {#OfferStorageDecl}


*Defined in [fuchsia.sys2/offer_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/offer_decl.fidl#95)*

<p>Declares a storage capability offered by a component to one of its children,
such as meta storage offered by the component's containing realm or cache
storage offered by the component itself.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#StorageType'>StorageType</a></code>
            </td>
            <td><p>The type of storage being offered.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td><p>The source of the storage capability. Must be <code>realm</code> or <code>storage</code>.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>target</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td><p>Reference to the target of the capability. Must be <code>child</code> or
<code>collection</code>.</p>
</td>
        </tr></table>

### OfferRunnerDecl {#OfferRunnerDecl}


*Defined in [fuchsia.sys2/offer_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/offer_decl.fidl#110)*

<p>Declares a runner offered by a component to one of its children, which may
have been offered by the component's containing realm, the component itself,
or one of its other children.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td><p>The provider of the capability relative to the component itself. Must be
<code>realm</code>, <code>self</code>, or <code>child</code>.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source_name</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td><p>Name of the runner being offered.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>target</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td><p>Reference to the target of the capability. Must be <code>child</code> or
<code>collection</code>.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>target_name</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td><p>Name under which the capability is being offered.</p>
</td>
        </tr></table>

### RunnerDecl {#RunnerDecl}


*Defined in [fuchsia.sys2/runner_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/runner_decl.fidl#8)*

<p>Declares a runner capability backed by a service.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td><p>The name of this runner.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td><p>The provider of the underlying service relative to the component itself.
Must be <code>realm</code>, <code>self</code>, or <code>child</code>.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>source_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>The path of the capability within the specified source.</p>
</td>
        </tr></table>

### StorageDecl {#StorageDecl}


*Defined in [fuchsia.sys2/storage_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/storage_decl.fidl#22)*

<p>Declares a storage capability backed by a directory from which data, cache,
or meta storage can be offered.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td><p>The name of this storage</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td><p>The provider of the underlying directory capability relative to the
component itself. Must be <code>realm</code>, <code>self</code>, or <code>child</code>.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>source_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>The incoming path to the directory capability. If &quot;source == SELF&quot;, this
is a path in the component's outgoing directory. Otherwise, it is the
path by which the capability was presented to the component.</p>
</td>
        </tr></table>

### UseServiceDecl {#UseServiceDecl}


*Defined in [fuchsia.sys2/use_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/use_decl.fidl#24)*

<p>Declares a service used by a component, which was offered to the component's
environment.</p>
<p>To learn more about services, see:
https://fuchsia.dev/fuchsia-src/glossary#service</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td><p>The provider of the service relative to the component itself. Must
be |realm| or |framework|.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>Path identifying the service, by which it was presented to this
component.</p>
<p>Must be an absolute path starting with /.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>target_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>The path where the capability should be installed in the component's
namespace.</p>
<p>Must be an absolute path starting with /.</p>
</td>
        </tr></table>

### UseLegacyServiceDecl {#UseLegacyServiceDecl}


*Defined in [fuchsia.sys2/use_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/use_decl.fidl#47)*

<p>Declares a legacy service used by a component, which was offered to the
component's environment.</p>
<p>A legacy service is a service with a single instance, provided by a single
FIDL protocol.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td><p>The provider of the legacy service relative to the component itself.
Must be |realm| or |framework|.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>Path identifying the legacy service, by which it was presented to this
component.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>target_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>The path where the capability should be installed in the component's
namespace.</p>
<p>Must be an absolute path starting with /.</p>
</td>
        </tr></table>

### UseDirectoryDecl {#UseDirectoryDecl}


*Defined in [fuchsia.sys2/use_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/use_decl.fidl#65)*

<p>Declares a directory used by a component, which was offered to the
component's environment.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Ref'>Ref</a></code>
            </td>
            <td><p>The provider of the directory relative to the component itself. Must
be |realm| or |framework|.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>Path identifying the directory, by which it was presented to this
component.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>target_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>The path where the capability should be installed in the component's
namespace.</p>
<p>Must be an absolute path starting with /.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>rights</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io2/'>fuchsia.io2</a>/<a class='link' href='../fuchsia.io2/#Operations'>Operations</a></code>
            </td>
            <td><p>The rights required by the component to use this directory.</p>
</td>
        </tr></table>

### UseStorageDecl {#UseStorageDecl}


*Defined in [fuchsia.sys2/use_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/use_decl.fidl#86)*

<p>Declares storage used by a component, which was offered to the component's
environment.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#StorageType'>StorageType</a></code>
            </td>
            <td><p>Type of storage used by the component.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>target_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>The path where the capability should be installed in the component's
namespace. Must not be set if <code>type</code> is <code>META</code>.</p>
<p>Must be an absolute path starting with /.</p>
</td>
        </tr></table>

### UseRunnerDecl {#UseRunnerDecl}


*Defined in [fuchsia.sys2/use_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/use_decl.fidl#99)*

<p>Declares a runner used by a component, which was offered to the component's
environment.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>source_name</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td><p>The name of the runner, as it was presented to this component by the
realm.</p>
</td>
        </tr></table>

### Component {#Component}


*Defined in [fuchsia.sys2/component.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/runtime/component.fidl#11)*

<p>A component is a unit of executable software.</p>
<p>This object provides the component's declaration, access to its package's
content, and relevant metadata.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>resolved_url</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The resolved URL of the component.
This is the canonical URL obtained by the component resolver after
after following redirects and resolving relative paths.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>decl</code></td>
            <td>
                <code><a class='link' href='#ComponentDecl'>ComponentDecl</a></code>
            </td>
            <td><p>The component's declaration.
This information is typically obtained from the component's manifest
or generated by the component resolver.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>package</code></td>
            <td>
                <code><a class='link' href='#Package'>Package</a></code>
            </td>
            <td><p>The package that contains the component.
By convention, the component's package is mapped to &quot;/pkg&quot; in its
namespace at runtime.</p>
<p>This is null if the component is not represented as a package.
In that case, it is the runner's responsibility to load the component's
resource from the <code>resolved_url</code>.  This mechanism is used for web
applications.</p>
</td>
        </tr></table>

### ComponentStartInfo {#ComponentStartInfo}


*Defined in [fuchsia.sys2/component_runner.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/runtime/component_runner.fidl#34)*

<p>Parameters for starting a new component instance.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>resolved_url</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The resolved URL of the component.
This is the canonical URL obtained by the component resolver after
following redirects and resolving relative paths.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>program</code></td>
            <td>
                <code><a class='link' href='../fuchsia.data/'>fuchsia.data</a>/<a class='link' href='../fuchsia.data/#Dictionary'>Dictionary</a></code>
            </td>
            <td><p>The component's program declaration.
This information originates from <code>ComponentDecl.program</code>.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>ns</code></td>
            <td>
                <code><a class='link' href='#ComponentNamespace'>ComponentNamespace</a></code>
            </td>
            <td><p>The namespace to provide to the component instance.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>outgoing_dir</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#Directory'>Directory</a>&gt;</code>
            </td>
            <td><p>The directory this component serves.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>runtime_dir</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#Directory'>Directory</a>&gt;</code>
            </td>
            <td><p>The directory served by the runner to present runtime information about
the component.</p>
</td>
        </tr></table>

### Package {#Package}


*Defined in [fuchsia.sys2/package.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/runtime/package.fidl#12)*

<p>A package is a signed collection of immutable files.</p>
<p>This object provides access to a package's content and relevant metadata.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>package_url</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The URL of the package itself.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>package_dir</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#Directory'>Directory</a></code>
            </td>
            <td><p>The package's content directory.</p>
</td>
        </tr></table>

### WorkRequest {#WorkRequest}


*Defined in [fuchsia.sys2/work_scheduler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/work_scheduler.fidl#22)*

<p>Parameters for a new piece of work to be scheduled.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>start</code></td>
            <td>
                <code><a class='link' href='#Start'>Start</a></code>
            </td>
            <td><p>Time when corresponding work item should be <em>first</em> scheduled.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>period</code></td>
            <td>
                <code>int64</code>
            </td>
            <td><p>Delay between repeated schedulings of corresponding work item. This is left unspecified for
one-shot work that should not repeat. Repeating work items are rescheduled indefinitely
until it is canceled.</p>
</td>
        </tr></table>



## **UNIONS**

### Realm_BindChild_Result {#Realm_BindChild_Result}
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

### Realm_CreateChild_Result {#Realm_CreateChild_Result}
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

### Realm_DestroyChild_Result {#Realm_DestroyChild_Result}
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

### Realm_ListChildren_Result {#Realm_ListChildren_Result}
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

### WorkScheduler_ScheduleWork_Result {#WorkScheduler_ScheduleWork_Result}
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

### WorkScheduler_CancelWork_Result {#WorkScheduler_CancelWork_Result}
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

### Worker_DoWork_Result {#Worker_DoWork_Result}
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

### WorkSchedulerControl_GetBatchPeriod_Result {#WorkSchedulerControl_GetBatchPeriod_Result}
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

### WorkSchedulerControl_SetBatchPeriod_Result {#WorkSchedulerControl_SetBatchPeriod_Result}
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

### ExposeDecl {#ExposeDecl}
*Defined in [fuchsia.sys2/expose_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/expose_decl.fidl#11)*

<p>Declares a capability exposed to either a component's containing realm or to the framework.
For example, a legacy service exposed by the component at runtime.</p>

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
        </tr><tr>
            <td><code>runner</code></td>
            <td>
                <code><a class='link' href='#ExposeRunnerDecl'>ExposeRunnerDecl</a></code>
            </td>
            <td></td>
        </tr></table>

### OfferDecl {#OfferDecl}
*Defined in [fuchsia.sys2/offer_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/offer_decl.fidl#12)*

<p>Declares a capability offered by a component to one of its children, which
may have been offered by the component's containing realm, the component
itself, or one of its other children.</p>

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
        </tr><tr>
            <td><code>runner</code></td>
            <td>
                <code><a class='link' href='#OfferRunnerDecl'>OfferRunnerDecl</a></code>
            </td>
            <td></td>
        </tr></table>

### Ref {#Ref}
*Defined in [fuchsia.sys2/relative_refs.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/relative_refs.fidl#9)*

<p>A reference to a capability source or destination relative to this
component.</p>

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

### UseDecl {#UseDecl}
*Defined in [fuchsia.sys2/use_decl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/decls/use_decl.fidl#11)*

<p>Declares a capability used by a component, which was offered to the
component's environment.</p>

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
        </tr><tr>
            <td><code>runner</code></td>
            <td>
                <code><a class='link' href='#UseRunnerDecl'>UseRunnerDecl</a></code>
            </td>
            <td></td>
        </tr></table>

### Start {#Start}
*Defined in [fuchsia.sys2/work_scheduler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys2/work_scheduler.fidl#13)*

<p>Different ways to specify when to schedule a work item for the first time.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>delay</code></td>
            <td>
                <code>int64</code>
            </td>
            <td><p>A non-negative delay to wait before scheduling work.</p>
</td>
        </tr><tr>
            <td><code>monotonic_time</code></td>
            <td>
                <code>int64</code>
            </td>
            <td><p>A fixed point in time to start scheduling work, interpreted like <code>ZX_CLOCK_MONOTONIC</code>:
number of nanoseconds since the system was powered on.</p>
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
            <td><p>Error produced when a component terminates unexpected.</p>
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

