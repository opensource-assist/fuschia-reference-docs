[TOC]

# fuchsia.sys.internal


## **PROTOCOLS**

## ComponentEventProvider {#ComponentEventProvider}
*Defined in [fuchsia.sys.internal/component_event_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys.internal/component_event_provider.fidl#12)*

<p>Service exposed by appmgr that enables a component (such as archivist) to listen for
lifecycle events of components in the realm tree.</p>

### SetListener {#SetListener}

<p>Requests a hook to get lifecycle events for the realm from where this service
was connected to.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='#ComponentEventListener'>ComponentEventListener</a></code>
            </td>
        </tr></table>



## ComponentEventListener {#ComponentEventListener}
*Defined in [fuchsia.sys.internal/component_event_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys.internal/component_event_provider.fidl#22)*

<p>Listener for events about the lifecycle of components.</p>
<p>When the listener is created it will receive <code>OnStart</code> calls for all
components that were already in the Realm tree.</p>

### OnStart {#OnStart}

<p>Notifies the client that a component has started in the realm.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>component</code></td>
            <td>
                <code><a class='link' href='#SourceIdentity'>SourceIdentity</a></code>
            </td>
        </tr></table>



### OnStop {#OnStop}

<p>Notifies the client that a component has stopped.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>component</code></td>
            <td>
                <code><a class='link' href='#SourceIdentity'>SourceIdentity</a></code>
            </td>
        </tr></table>



### OnDiagnosticsDirReady {#OnDiagnosticsDirReady}

<p>Notifies the client that the out/diagnostics directory of a component is ready
and provides a handle to it.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>component</code></td>
            <td>
                <code><a class='link' href='#SourceIdentity'>SourceIdentity</a></code>
            </td>
        </tr><tr>
            <td><code>directory</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#Directory'>Directory</a></code>
            </td>
        </tr></table>









## **TABLES**

### SourceIdentity {#SourceIdentity}


*Defined in [fuchsia.sys.internal/source_identity.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys.internal/source_identity.fidl#18)*

<p>Identifies a component uniquely within the observing realm.
Example: hub/r/sys/4566/c/http.cmx/19226/out/objects
moniker: [root, sys, http.cmx]
component_url: &quot;fuchsia-pkg://fuchsia.com/http#meta/http.cmx&quot;
component_name: &quot;http.cmx&quot;
instance_id: 19226</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>moniker</code></td>
            <td>
                <code>vector&lt;string&gt;[25]</code>
            </td>
            <td><p>The path to the component from the observing realm.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>component_url</code></td>
            <td>
                <code>string[4096]</code>
            </td>
            <td><p>The URL from which the component was loaded.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>component_name</code></td>
            <td>
                <code>string[255]</code>
            </td>
            <td><p>The name of the component.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>instance_id</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td><p>The ID of the component.</p>
</td>
        </tr></table>









## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="MAXIMUM_MONIKER_SEGMENTS">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys.internal/source_identity.fidl#7">MAXIMUM_MONIKER_SEGMENTS</a></td>
            <td>
                    <code>25</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr id="COMPONENT_NAME_MAX_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys.internal/source_identity.fidl#8">COMPONENT_NAME_MAX_LENGTH</a></td>
            <td>
                    <code>255</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr id="STRING_MAX_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys.internal/source_identity.fidl#9">STRING_MAX_LENGTH</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr id="MAX_URL_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.sys.internal/source_identity.fidl#10">MAX_URL_LENGTH</a></td>
            <td>
                    <code>4096</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    
</table>



