[TOC]

# fuchsia.session


## **PROTOCOLS**

## ElementManager {#ElementManager}
*Defined in [fuchsia.session/element_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.session/element_manager.fidl#20)*

<p>The ElementManager is responsible for service requests to add elements to a
session.</p>
<p>An Element is a component which is expected to be instantiated as a child
of the session and interact with the user in some way.</p>
<p>For example, a component acting as an element proposer may be listening to
the network for instructions to display an element to the user. When such
a network command is received, the element proposer proposes to add an
element to the session via the <code>ElementManager</code> protocol.</p>

### ProposeElement {#ProposeElement}

<p>Proposes to add an Element to the session.</p>
<p>If <code>ProposeElement()</code> returns without error, the caller can assume
the element is now part of the session. However, whether or not the
element component is actively running, or not, is left to the session's
discretion. For example, a session may decide to conserve resources by
suspending an element which is not in focus, or delay the running of an
element until a more appropriate time.</p>
<p><code>spec</code> describes the Element to add.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>spec</code></td>
            <td>
                <code><a class='link' href='#ElementSpec'>ElementSpec</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#ElementManager_ProposeElement_Result'>ElementManager_ProposeElement_Result</a></code>
            </td>
        </tr></table>

## Launcher {#Launcher}
*Defined in [fuchsia.session/launcher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.session/launcher.fidl#11)*

<p>A protocol used to launch sessions.</p>

### LaunchSession {#LaunchSession}

<p>Launches the session detailed in |configuration|.</p>
<p>If a session is currently running, the component associated with the running session will
be destroyed.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>configuration</code></td>
            <td>
                <code><a class='link' href='#SessionConfiguration'>SessionConfiguration</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Launcher_LaunchSession_Result'>Launcher_LaunchSession_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### ElementManager_ProposeElement_Response {#ElementManager_ProposeElement_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Launcher_LaunchSession_Response {#Launcher_LaunchSession_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>



## **ENUMS**

### ProposeElementError {#ProposeElementError}
Type: <code>uint32</code>

*Defined in [fuchsia.session/element_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.session/element_manager.fidl#35)*

<p>Errors which can be returned when attempting to add elements to a session.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NOT_FOUND</code></td>
            <td><code>1</code></td>
            <td><p>There was an error resolving the element's component url.</p>
</td>
        </tr><tr>
            <td><code>REJECTED</code></td>
            <td><code>2</code></td>
            <td><p>The session rejected the proposal to add the element.</p>
</td>
        </tr></table>

### LaunchSessionError {#LaunchSessionError}
Type: <code>uint32</code>

*Defined in [fuchsia.session/launcher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.session/launcher.fidl#20)*

<p>Errors returned when a session fails to launch.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NOT_FOUND</code></td>
            <td><code>1</code></td>
            <td><p>There was an error resolving the session's component url.</p>
</td>
        </tr><tr>
            <td><code>FAILED</code></td>
            <td><code>2</code></td>
            <td><p>The session failed to launch.</p>
</td>
        </tr></table>



## **TABLES**

### ElementSpec {#ElementSpec}


*Defined in [fuchsia.session/element_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.session/element_manager.fidl#44)*

<p>Describes an Element to be added to a session.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>component_url</code></td>
            <td>
                <code>string[4096]</code>
            </td>
            <td><p>The component URL of the Element.</p>
</td>
        </tr></table>

### SessionConfiguration {#SessionConfiguration}


*Defined in [fuchsia.session/launcher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.session/launcher.fidl#29)*

<p>Describes a session to launch.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>session_url</code></td>
            <td>
                <code>string[4096]</code>
            </td>
            <td><p>The component URL of the session.</p>
</td>
        </tr></table>



## **UNIONS**

### ElementManager_ProposeElement_Result {#ElementManager_ProposeElement_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#ElementManager_ProposeElement_Response'>ElementManager_ProposeElement_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ProposeElementError'>ProposeElementError</a></code>
            </td>
            <td></td>
        </tr></table>

### Launcher_LaunchSession_Result {#Launcher_LaunchSession_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Launcher_LaunchSession_Response'>Launcher_LaunchSession_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#LaunchSessionError'>LaunchSessionError</a></code>
            </td>
            <td></td>
        </tr></table>







