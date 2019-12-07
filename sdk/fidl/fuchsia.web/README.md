[TOC]

# fuchsia.web


## **PROTOCOLS**

## ContextProvider {#ContextProvider}
*Defined in [fuchsia.web/context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/context.fidl#17)*

<p>The top-level service interface which allows for the creation of Context resources.</p>

### Create {#Create}

<p>Creates a new browser <a class='link' href='#fuchsia.web.Context'>fuchsia.web.Context</a> whose state is wholly independent and
isolated from other Contexts.</p>
<ul>
<li><code>context</code>: An interface request which will receive a bound <a class='link' href='#fuchsia.web.Context'>fuchsia.web.Context</a>
service.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>params</code></td>
            <td>
                <code><a class='link' href='#CreateContextParams'>CreateContextParams</a></code>
            </td>
        </tr><tr>
            <td><code>context</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Context'>Context</a>&gt;</code>
            </td>
        </tr></table>



## Context {#Context}
*Defined in [fuchsia.web/context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/context.fidl#151)*

<p>Manages browsing state (e.g. LocalStorage, cookies, etc) associated with a set of
<a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a>.</p>

### CreateFrame {#CreateFrame}

<p>Creates a new <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a> under this <a class='link' href='#fuchsia.web.Context'>fuchsia.web.Context</a>. Destruction of a
<a class='link' href='#fuchsia.web.Context'>fuchsia.web.Context</a> triggers the destruction of all of its associated
<a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a>. <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a> can be transferred to another component but
cannot be shared across multiple components.</p>
<ul>
<li><code>frame</code>: An interface request that will be bound to the created <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a>.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>frame</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Frame'>Frame</a>&gt;</code>
            </td>
        </tr></table>



### CreateFrameWithParams {#CreateFrameWithParams}

<p>Similar to <a class='link' href='../fuchsia.web.Context/'>fuchsia.web.Context</a>/<a class='link' href='../fuchsia.web.Context/#CreateFrame'>CreateFrame</a>, with extra parameters.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>params</code></td>
            <td>
                <code><a class='link' href='#CreateFrameParams'>CreateFrameParams</a></code>
            </td>
        </tr><tr>
            <td><code>frame</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Frame'>Frame</a>&gt;</code>
            </td>
        </tr></table>



### GetCookieManager {#GetCookieManager}

<p>Used to observe cookies for sites hosted under this Context.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>manager</code></td>
            <td>
                <code>request&lt;<a class='link' href='#CookieManager'>CookieManager</a>&gt;</code>
            </td>
        </tr></table>



### GetRemoteDebuggingPort {#GetRemoteDebuggingPort}

<p>Waits until debugging is available on one or more Frames, and returns the DevTools port
number. Multiple calls may be queued to received the port number.</p>
<p>If an error occured, the <a class='link' href='#fuchsia.web.ContextError'>fuchsia.web.ContextError</a> will be set to this value:</p>
<ul>
<li><code>REMOTE_DEBUGGING_PORT_NOT_OPENED</code>: |remote_debugging_port| was not set in
<a class='link' href='#fuchsia.web.CreateContextParams'>fuchsia.web.CreateContextParams</a> or the remote debugging service failed to start.</li>
</ul>

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
                <code><a class='link' href='#Context_GetRemoteDebuggingPort_Result'>Context_GetRemoteDebuggingPort_Result</a></code>
            </td>
        </tr></table>

## CookieManager {#CookieManager}
*Defined in [fuchsia.web/cookie.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/cookie.fidl#10)*

<p>Provides methods for monitoring and accessing browser cookie state.</p>

### ObserveCookieChanges {#ObserveCookieChanges}

<p>Observe changes to all cookies named <code>name</code> that would be sent in a request to <code>url</code>.</p>
<p>If neither <code>url</code> nor <code>name</code> are set then all cookies are observed. If only <code>url</code> is set
then all cookies for that URL are observed. If both are set then only cookies matching both
fields are observed.</p>
<p>|changes| iterates over a stream of cookie changes. Additions or updates are expressed as
complete cookies, while deletions are expressed as cookies with no <code>value</code> set.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>url</code></td>
            <td>
                <code>string[65536]?</code>
            </td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr><tr>
            <td><code>changes</code></td>
            <td>
                <code>request&lt;<a class='link' href='#CookiesIterator'>CookiesIterator</a>&gt;</code>
            </td>
        </tr></table>



### GetCookieList {#GetCookieList}

<p>Returns a list of Cookies, optionally limited to those matching <code>url</code>, and optionally
<code>name</code>. <code>cookies</code> iterates over the matching cookies, including their <code>value</code>s.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>url</code></td>
            <td>
                <code>string[65536]?</code>
            </td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr><tr>
            <td><code>cookies</code></td>
            <td>
                <code>request&lt;<a class='link' href='#CookiesIterator'>CookiesIterator</a>&gt;</code>
            </td>
        </tr></table>



## CookiesIterator {#CookiesIterator}
*Defined in [fuchsia.web/cookie.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/cookie.fidl#32)*

<p>Used to iterator over a set of cookies, or a stream of changes to cookies.</p>

### GetNext {#GetNext}

<p>Fetches the next batch of cookies, or of changes to cookies.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>changed_cookies</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Cookie'>Cookie</a>&gt;</code>
            </td>
        </tr></table>

## Debug {#Debug}
*Defined in [fuchsia.web/debug.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/debug.fidl#9)*

<p>The debug service which allows to enable the DevTools service on Contexts.</p>

### EnableDevTools {#EnableDevTools}

<p>Enables the DevTools service on every subsequent Context creation and
and delivers subsequent DevTools events to the supplied <code>listener</code>.
The callback indicates when the WebEngine is in a debuggable state.
Events will be sent to every <code>listener</code> registered with this method.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='#DevToolsListener'>DevToolsListener</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## DevToolsListener {#DevToolsListener}
*Defined in [fuchsia.web/debug.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/debug.fidl#18)*

<p>Interface used to observe DevTools service availability events.</p>

### OnContextDevToolsAvailable {#OnContextDevToolsAvailable}

<p>Called when the DevTools service is available on a new Context.</p>
<p><code>listener</code>: Channel over which DevTools events for the new Context will
be delivered. This channel will disconnect when the Context
is detroyed.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>listener</code></td>
            <td>
                <code>request&lt;<a class='link' href='#DevToolsPerContextListener'>DevToolsPerContextListener</a>&gt;</code>
            </td>
        </tr></table>



## DevToolsPerContextListener {#DevToolsPerContextListener}
*Defined in [fuchsia.web/debug.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/debug.fidl#29)*

<p>Interface supplied by the debugging component to observe the DevTools
service opening event.</p>

### OnHttpPortOpen {#OnHttpPortOpen}

<p>Called when the DevTools service starts accepting TCP connections on
<code>port</code>. <code>port</code> will remain open until the Context is destroyed.</p>
<p><code>port</code>: The port used by the service.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>port</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>



## Frame {#Frame}
*Defined in [fuchsia.web/frame.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/frame.fidl#44)*


### CreateView {#CreateView}

<p>Creates a new view using the specified <code>view_token</code>. Caller should pass the other end of
the token to <a class='link' href='../fuchsia.ui.gfx.ViewHolderArgs/'>fuchsia.ui.gfx.ViewHolderArgs</a>/<a class='link' href='../fuchsia.ui.gfx.ViewHolderArgs/#token'>token</a> to attach the new view to a view tree.</p>
<ul>
<li><code>view_token</code>: Token for the new view.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/#ViewToken'>ViewToken</a></code>
            </td>
        </tr></table>



### EnableHeadlessRendering {#EnableHeadlessRendering}

<p>Enables headless rendering of the Frame.
This is used when content depends on layout and/or animation events firing normally.
May only be used on a Context created with the <code>HEADLESS</code> feature flag.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### DisableHeadlessRendering {#DisableHeadlessRendering}

<p>Stops headless rendering of the Frame.
May only be used on a Context created with the <code>HEADLESS</code> feature flag.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### GetMediaPlayer {#GetMediaPlayer}

<p>Returns a <a class='link' href='#fuchsia.media.sessions2.Player'>fuchsia.media.sessions2.Player</a> interface through which media (i.e.
video/audio) playback in the frame may be observed, and/or controlled. Only one
<a class='link' href='#fuchsia.media.sessions2.Player'>fuchsia.media.sessions2.Player</a> may be active at a time, for each <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>player</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.media.sessions2/'>fuchsia.media.sessions2</a>/<a class='link' href='../fuchsia.media.sessions2/#Player'>Player</a>&gt;</code>
            </td>
        </tr></table>



### GetNavigationController {#GetNavigationController}

<p>Returns an interface through which the <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a> may be navigated to a desired
URL, reloaded, etc.</p>
<ul>
<li><code>controller</code>: An asynchronous interface request for the <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a>'s
<a class='link' href='#fuchsia.web.NavigationController'>fuchsia.web.NavigationController</a>.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>controller</code></td>
            <td>
                <code>request&lt;<a class='link' href='#NavigationController'>NavigationController</a>&gt;</code>
            </td>
        </tr></table>



### ExecuteJavaScript {#ExecuteJavaScript}

<p>Executes a UTF-8 encoded <code>script</code> in the <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a> if the
<a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a>'s URL has an origin which matches entries in <code>origins</code>.</p>
<p>At least one <code>origins</code> entry must be specified. If a wildcard <code>&quot;*&quot;</code> is specified in
<code>origins</code>, then the script will be evaluated unconditionally.</p>
<p>Returns the result of executing <code>script</code>, as a JSON-encoded string.</p>
<p>Note that scripts share the same execution context as the document,
meaning that document may modify variables, classes, or objects set by
the script in arbitrary or unpredictable ways.</p>
<p>If an error occured, the FrameError will be set to one of these values:</p>
<ul>
<li><code>BUFFER_NOT_UTF8</code>: <code>script</code> is not UTF-8 encoded.</li>
<li><code>INVALID_ORIGIN</code>: The <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a>'s current URL does not match any of the
values in <code>origins</code> or <code>origins</code> is an empty vector.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>origins</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr><tr>
            <td><code>script</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Frame_ExecuteJavaScript_Result'>Frame_ExecuteJavaScript_Result</a></code>
            </td>
        </tr></table>

### ExecuteJavaScriptNoResult {#ExecuteJavaScriptNoResult}

<p>Variant of <a class='link' href='../fuchsia.web.Frame/'>fuchsia.web.Frame</a>/<a class='link' href='../fuchsia.web.Frame/#ExecuteJavaScript'>ExecuteJavaScript</a> which executes the supplied script
without returning a result.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>origins</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr><tr>
            <td><code>script</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Frame_ExecuteJavaScriptNoResult_Result'>Frame_ExecuteJavaScriptNoResult_Result</a></code>
            </td>
        </tr></table>

### AddBeforeLoadJavaScript {#AddBeforeLoadJavaScript}

<p>Executes a UTF-8 encoded <code>script</code> for every subsequent page load where the
<a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a>'s URL has an origin reflected in <code>origins</code>. The script is executed
early, prior to the execution of the document's scripts.</p>
<p>Scripts are identified by a client-managed identifier <code>id</code>. Any script previously injected
using the same <code>id</code> will be replaced.</p>
<p>The order in which multiple bindings are executed is the same as the order in which the
bindings were added. If a script is added which clobbers an existing script of the same
<code>id</code>, the previous script's precedence in the injection order will be preserved.</p>
<p>At least one <code>origins</code> entry must be specified. If a wildcard <code>&quot;*&quot;</code> is specified in
<code>origins</code>, then the script will be evaluated unconditionally.</p>
<p>If an error occured, the <a class='link' href='#fuchsia.web.FrameError'>fuchsia.web.FrameError</a> will be set to one of these values:</p>
<ul>
<li><code>BUFFER_NOT_UTF8</code>: <code>script</code> is not UTF-8 encoded.</li>
<li><code>INVALID_ORIGIN</code>: <code>origins</code> is an empty vector.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>origins</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr><tr>
            <td><code>script</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Frame_AddBeforeLoadJavaScript_Result'>Frame_AddBeforeLoadJavaScript_Result</a></code>
            </td>
        </tr></table>

### RemoveBeforeLoadJavaScript {#RemoveBeforeLoadJavaScript}

<p>Removes a previously added JavaScript snippet identified by <code>id</code>. This is a no-op if there
is no JavaScript snippet identified by <code>id</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### PostMessage {#PostMessage}

<p>Posts a message to the frame's onMessage handler.</p>
<p><code>target_origin</code> restricts message delivery to the specified origin. If <code>target_origin</code> is
<code>&quot;*&quot;</code>, then the message will be sent to the document regardless of its origin.
See the
[https://html.spec.whatwg.org/multipage/web-messaging.html#posting-messages](HTML spec)
section 9.4.3 for more details on how the target origin policy is applied.</p>
<p>If an error occured, the <a class='link' href='#fuchsia.web.FrameError'>fuchsia.web.FrameError</a> will be set to one of these values:</p>
<ul>
<li><code>INTERNAL_ERROR</code>: The WebEngine failed to create a message pipe.</li>
<li><code>BUFFER_NOT_UTF8</code>: The script in <code>message</code>'s <code>data</code> property is not UTF-8 encoded.</li>
<li><code>INVALID_ORIGIN</code>: <code>origins</code> is an empty vector.</li>
<li><code>NO_DATA_IN_MESSAGE</code>: The <code>data</code> property is missing in <code>message</code>.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>target_origin</code></td>
            <td>
                <code>string[65536]</code>
            </td>
        </tr><tr>
            <td><code>message</code></td>
            <td>
                <code><a class='link' href='#WebMessage'>WebMessage</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Frame_PostMessage_Result'>Frame_PostMessage_Result</a></code>
            </td>
        </tr></table>

### SetNavigationEventListener {#SetNavigationEventListener}

<p>Sets the listener for handling page navigation events.</p>
<ul>
<li><code>listener</code>: The observer to use. Unregisters any existing listener is null.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='#NavigationEventListener'>NavigationEventListener</a>?</code>
            </td>
        </tr></table>



### SetJavaScriptLogLevel {#SetJavaScriptLogLevel}

<p>If set to a value other than <a class='link' href='../fuchsia.web.ConsoleLogLevel/'>fuchsia.web.ConsoleLogLevel</a>/<a class='link' href='../fuchsia.web.ConsoleLogLevel/#NONE'>NONE</a>, allows web content to
log messages to the system logger using the console APIs (<code>debug()</code>, <code>log()</code>, <code>info()</code>,
<code>warn()</code> and <code>error()</code>).</p>
<p>When logged to the system logger:</p>
<ul>
<li><code>debug()</code>, <code>log()</code> and <code>info()</code> logs are logged with
<a class='link' href='../fuchsia.logger.LogLevelFilter/'>fuchsia.logger.LogLevelFilter</a>/<a class='link' href='../fuchsia.logger.LogLevelFilter/#INFO'>INFO</a> severity level.</li>
<li><code>warn()</code> logs are logged with <a class='link' href='../fuchsia.logger.LogLevelFilter/'>fuchsia.logger.LogLevelFilter</a>/<a class='link' href='../fuchsia.logger.LogLevelFilter/#INFO'>INFO</a> severity level.</li>
<li><code>error()</code> logs are logged with <a class='link' href='../fuchsia.logger.LogLevelFilter/'>fuchsia.logger.LogLevelFilter</a>/<a class='link' href='../fuchsia.logger.LogLevelFilter/#INFO'>INFO</a> severity level.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>level</code></td>
            <td>
                <code><a class='link' href='#ConsoleLogLevel'>ConsoleLogLevel</a></code>
            </td>
        </tr></table>



### SetEnableInput {#SetEnableInput}

<p>Used at runtime to enable or disable user input processing (e.g. keyboard, mouse, touch) on
a <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a>.</p>
<p>Input is enabled by default.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>enable_input</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### SetPopupFrameCreationListener {#SetPopupFrameCreationListener}

<p>Sets the listener for handling popup frame opened by web content. If no listener is
present, then any new popup frame will be blocked.</p>
<ul>
<li><code>listener</code>: The listener to use. Unregisters any existing listener if null.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='#PopupFrameCreationListener'>PopupFrameCreationListener</a>?</code>
            </td>
        </tr></table>



### SetUrlRequestRewriteRules {#SetUrlRequestRewriteRules}

<p>Supplies a set of <a class='link' href='#fuchsia.web.UrlRequestRewriteRule'>fuchsia.web.UrlRequestRewriteRule</a> to apply on every subsequent URL
request.</p>
<ul>
<li><code>rules</code> are cumulative and applied in order.</li>
<li><code>rules</code> will be validated before being applied. If <code>rules</code> are invalid, the
<a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a> will be closed with <code>ERR_INVALID_ARGS</code>.</li>
<li><a class='link' href='../fuchsia.web.Frame/'>fuchsia.web.Frame</a>/<a class='link' href='../fuchsia.web.Frame/#SetUrlRequestRewriteRules'>SetUrlRequestRewriteRules</a> must not be called again until its
acknowledgement callback has been processed. If this happens, the <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a>
will be closed with <code>ERR_BAD_STATE</code>.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rules</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#UrlRequestRewriteRule'>UrlRequestRewriteRule</a>&gt;[4096]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### SetMediaSessionId {#SetMediaSessionId}

<p>Sets <code>session_id</code> to pass to the <a class='link' href='#fuchsia.media.AudioConsumer'>fuchsia.media.AudioConsumer</a> when playing audio. The
specified value is not applied retroactively to audio streams that were started before this
message is processed. If the caller needs to ensure the value is applied to all streams it
should call this method before <a class='link' href='../fuchsia.web.Frame/'>fuchsia.web.Frame</a>/<a class='link' href='../fuchsia.web.Frame/#GetNavigationController'>GetNavigationController</a>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>session_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



## MessagePort {#MessagePort}
*Defined in [fuchsia.web/frame.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/frame.fidl#217)*

<p>Represents one end of an HTML5 MessageChannel. Can be used to send and exchange Messages with
the peered MessagePort in the Frame's script context. The port is destroyed when either end of
the MessagePort channel is torn down.</p>

### PostMessage {#PostMessage}

<p>Sends a <a class='link' href='#fuchsia.web.WebMessage'>fuchsia.web.WebMessage</a> to the peer. These are processed in order, one at a
time. It is not necessary for the caller to wait for the completion callback before calling
<a class='link' href='../fuchsia.web.MessagePort/'>fuchsia.web.MessagePort</a>/<a class='link' href='../fuchsia.web.MessagePort/#PostMessage'>PostMessage</a> again.</p>
<p>If an error occured, the <a class='link' href='#fuchsia.web.FrameError'>fuchsia.web.FrameError</a> will be set to one of these value:</p>
<ul>
<li><code>BUFFER_NOT_UTF8</code>: The script in <code>message</code>'s <code>data</code> property is not UTF-8 encoded.</li>
<li><code>NO_DATA_IN_MESSAGE</code>: The <code>data</code> property is missing in <code>message</code>.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>message</code></td>
            <td>
                <code><a class='link' href='#WebMessage'>WebMessage</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#MessagePort_PostMessage_Result'>MessagePort_PostMessage_Result</a></code>
            </td>
        </tr></table>

### ReceiveMessage {#ReceiveMessage}

<p>Asynchronously reads the next message from the channel. The client should invoke the
callback when it is ready to process another message. Unreceived messages are buffered
on the sender's side and bounded by its available resources.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>message</code></td>
            <td>
                <code><a class='link' href='#WebMessage'>WebMessage</a></code>
            </td>
        </tr></table>

## PopupFrameCreationListener {#PopupFrameCreationListener}
*Defined in [fuchsia.web/frame.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/frame.fidl#243)*


### OnPopupFrameCreated {#OnPopupFrameCreated}

<p>Called when a <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a> has created a new popup <code>frame</code>. Information about the
popup frame, and how it was created, is provided via <code>info</code>. Additional popup frames are
delivered after the the acknowledgement callback is invoked.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>frame</code></td>
            <td>
                <code><a class='link' href='#Frame'>Frame</a></code>
            </td>
        </tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#PopupFrameCreationInfo'>PopupFrameCreationInfo</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## NavigationEventListener {#NavigationEventListener}
*Defined in [fuchsia.web/navigation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/navigation.fidl#11)*

<p>Interface supplied by the embedder for receiving notifications about navigation events in a
<a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a>.</p>

### OnNavigationStateChanged {#OnNavigationStateChanged}

<p>Called when user-visible navigation state has changed since <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a> creation
or the last acknowledgement callback, whichever occurred last. <code>change</code> will contain all
the differences in navigation state since the last acknowledgement. Any unchanged
properties will be left unset in <code>change</code>.</p>
<p>Implementer must call the acknowledgement callback to receive new navigation events.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>change</code></td>
            <td>
                <code><a class='link' href='#NavigationState'>NavigationState</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## NavigationController {#NavigationController}
*Defined in [fuchsia.web/navigation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/navigation.fidl#31)*

<p>Provides methods for controlling and querying the navigation state of a <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a>.</p>

### LoadUrl {#LoadUrl}

<p>Tells the <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a> to navigate to a <code>url</code>.</p>
<ul>
<li><code>url</code>:    The address to navigate to.</li>
<li><code>params</code>: Additional parameters that affect how the resource will be
loaded (e.g. cookies, HTTP headers, etc.)</li>
</ul>
<p>If an error occured, the <a class='link' href='#fuchsia.web.NavigationControllerError'>fuchsia.web.NavigationControllerError</a> will be set to one of
these values:</p>
<ul>
<li><code>INVALID_URL</code>: The <code>url</code> parameter is invalid.</li>
<li><code>INVALID_HEADER</code>: At least one of the headers in <a class='link' href='../fuchsia.web.LoadUrlParams/'>fuchsia.web.LoadUrlParams</a>/<a class='link' href='../fuchsia.web.LoadUrlParams/#headers'>headers</a>
is invalid.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>url</code></td>
            <td>
                <code>string[65536]</code>
            </td>
        </tr><tr>
            <td><code>params</code></td>
            <td>
                <code><a class='link' href='#LoadUrlParams'>LoadUrlParams</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#NavigationController_LoadUrl_Result'>NavigationController_LoadUrl_Result</a></code>
            </td>
        </tr></table>

### GoBack {#GoBack}

<p>Tells the <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a> to navigate to the previous page in its history, if any.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### GoForward {#GoForward}

<p>Tells the <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a> to navigate to the next page in its history, if any.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Stop {#Stop}

<p>Tells the <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a> to stop the current navigation if a navigation is ongoing.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Reload {#Reload}

<p>Tells the <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a> to reload the current page.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#ReloadType'>ReloadType</a></code>
            </td>
        </tr></table>



### GetVisibleEntry {#GetVisibleEntry}

<p>Returns information for the currently visible content regardless of loading state, or an
empty entry if no content is being displayed.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>entry</code></td>
            <td>
                <code><a class='link' href='#NavigationState'>NavigationState</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Context_GetRemoteDebuggingPort_Response {#Context_GetRemoteDebuggingPort_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>port</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Frame_ExecuteJavaScript_Response {#Frame_ExecuteJavaScript_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Frame_ExecuteJavaScriptNoResult_Response {#Frame_ExecuteJavaScriptNoResult_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Frame_AddBeforeLoadJavaScript_Response {#Frame_AddBeforeLoadJavaScript_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Frame_PostMessage_Response {#Frame_PostMessage_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### MessagePort_PostMessage_Response {#MessagePort_PostMessage_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### NavigationController_LoadUrl_Response {#NavigationController_LoadUrl_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>



## **ENUMS**

### ContextError {#ContextError}
Type: <code>int32</code>

*Defined in [fuchsia.web/context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/context.fidl#9)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>REMOTE_DEBUGGING_PORT_NOT_OPENED</code></td>
            <td><code>1</code></td>
            <td><p>The remote debugging service was not opened.</p>
</td>
        </tr></table>

### ConsoleLogLevel {#ConsoleLogLevel}
Type: <code>int32</code>

*Defined in [fuchsia.web/frame.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/frame.fidl#12)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NONE</code></td>
            <td><code>100</code></td>
            <td><p>No logging.</p>
</td>
        </tr><tr>
            <td><code>DEBUG</code></td>
            <td><code>-1</code></td>
            <td><p>Outputs messages from <code>console.debug()</code> and above levels.</p>
</td>
        </tr><tr>
            <td><code>INFO</code></td>
            <td><code>0</code></td>
            <td><p>Outputs messages from <code>console.log()</code>, <code>console.info()</code> and above levels.</p>
</td>
        </tr><tr>
            <td><code>WARN</code></td>
            <td><code>1</code></td>
            <td><p>Outputs messages from <code>console.warn()</code> and <code>console.error()</code>.</p>
</td>
        </tr><tr>
            <td><code>ERROR</code></td>
            <td><code>2</code></td>
            <td><p>Outputs messages from <code>console.error()</code>.</p>
</td>
        </tr></table>

### FrameError {#FrameError}
Type: <code>int32</code>

*Defined in [fuchsia.web/frame.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/frame.fidl#30)*

<p>Represents the return status of a <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a> method.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INTERNAL_ERROR</code></td>
            <td><code>1</code></td>
            <td><p>An internal error occured.</p>
</td>
        </tr><tr>
            <td><code>BUFFER_NOT_UTF8</code></td>
            <td><code>2</code></td>
            <td><p>The provided buffer is not UTF-8 encoded.</p>
</td>
        </tr><tr>
            <td><code>INVALID_ORIGIN</code></td>
            <td><code>3</code></td>
            <td><p>The Frame's URL does not match any of the origins provided by the caller.</p>
</td>
        </tr><tr>
            <td><code>NO_DATA_IN_MESSAGE</code></td>
            <td><code>4</code></td>
            <td><p>The required <code>data</code> property is missing from a <a class='link' href='#fuchsia.web.WebMessage'>fuchsia.web.WebMessage</a>.</p>
</td>
        </tr></table>

### NavigationControllerError {#NavigationControllerError}
Type: <code>int32</code>

*Defined in [fuchsia.web/navigation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/navigation.fidl#22)*

<p>Represents the return status of a <a class='link' href='#fuchsia.web.NavigationController'>fuchsia.web.NavigationController</a> method.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INVALID_URL</code></td>
            <td><code>1</code></td>
            <td><p>The provided URL is invalid.</p>
</td>
        </tr><tr>
            <td><code>INVALID_HEADER</code></td>
            <td><code>2</code></td>
            <td><p>At least one of the provided headers was invalid.</p>
</td>
        </tr></table>

### ReloadType {#ReloadType}
Type: <code>uint32</code>

*Defined in [fuchsia.web/navigation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/navigation.fidl#104)*

<p>Characterizes the type of reload.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>PARTIAL_CACHE</code></td>
            <td><code>0</code></td>
            <td><p>Reloads the current entry, bypassing the cache for the main resource.</p>
</td>
        </tr><tr>
            <td><code>NO_CACHE</code></td>
            <td><code>1</code></td>
            <td><p>Reloads the current entry, bypassing the cache entirely.</p>
</td>
        </tr></table>

### LoadUrlReason {#LoadUrlReason}
Type: <code>uint32</code>

*Defined in [fuchsia.web/navigation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/navigation.fidl#113)*

<p>Characterizes the origin of a <a class='link' href='../fuchsia.web.NavigationController/'>fuchsia.web.NavigationController</a>/<a class='link' href='../fuchsia.web.NavigationController/#LoadUrl'>LoadUrl</a> request.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>LINK</code></td>
            <td><code>0</code></td>
            <td><p>Navigation was initiated by the user following a link.</p>
</td>
        </tr><tr>
            <td><code>TYPED</code></td>
            <td><code>1</code></td>
            <td><p>Navigation was initiated by a user-provided URL.</p>
</td>
        </tr></table>

### PageType {#PageType}
Type: <code>uint32</code>

*Defined in [fuchsia.web/navigation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/navigation.fidl#122)*

<p>Characterizes the page type in a <a class='link' href='#fuchsia.web.NavigationState'>fuchsia.web.NavigationState</a>.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NORMAL</code></td>
            <td><code>0</code></td>
            <td><p>Regular web page.</p>
</td>
        </tr><tr>
            <td><code>ERROR</code></td>
            <td><code>1</code></td>
            <td><p>Error page.</p>
</td>
        </tr></table>



## **TABLES**

### ContentDirectoryProvider {#ContentDirectoryProvider}


*Defined in [fuchsia.web/context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/context.fidl#46)*

<p>Defines a provider which hosts resources from a <a class='link' href='#fuchsia.io.Directory'>fuchsia.io.Directory</a>. Content can <code>GET</code>
resource files via the provider, but not enumerate directories. Resources can be accessed by
their URLs: <code>fuchsia-dir://&lt;provider-name&gt;/&lt;path/to/resource&gt;</code></p>
<p>By default the MIME types of files are determined automatically by &quot;sniffing&quot; the contents of
the files. No content encoding will be declared, which browsers will interpret as meaning
<code>&quot;text/plain&quot;</code>.</p>
<p>Content type and encoding metadata may optionally be specified explicitly by metadata files,
which reside alongside the file. Metadata is expressed in JSON files, named after the files
they describe with a <code>&quot;._metadata&quot;</code> suffix.</p>
<p>For example, the file <code>&quot;index.html&quot;</code> would have the a metadata file called
<code>&quot;index.html._metadata&quot;</code>, with the following contents:</p>
<pre><code>{
  &quot;charset&quot;: &quot;utf-8&quot;,
  &quot;mime&quot;: &quot;text/html&quot;
}
</code></pre>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string[255]</code>
            </td>
            <td><p>Name of the provider. Must be non-empty and composed solely of alphanumerics, dots, and
dashes.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>directory</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#Directory'>Directory</a></code>
            </td>
            <td><p>Directory containing the files served by this provider.</p>
</td>
        </tr></table>

### CreateContextParams {#CreateContextParams}


*Defined in [fuchsia.web/context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/context.fidl#92)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>service_directory</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#Directory'>Directory</a></code>
            </td>
            <td><p>Service directory to be used by the context. The following services must be present in the
directory:</p>
<ul>
<li><a class='link' href='#fuchsia.accessibility.semantics.SemanticsManager'>fuchsia.accessibility.semantics.SemanticsManager</a></li>
<li><a class='link' href='#fuchsia.deprecatedtimezone.Timezone'>fuchsia.deprecatedtimezone.Timezone</a></li>
<li><a class='link' href='#fuchsia.device.NameProvider'>fuchsia.device.NameProvider</a></li>
<li><a class='link' href='#fuchsia.fonts.Provider'>fuchsia.fonts.Provider</a></li>
<li><a class='link' href='#fuchsia.logger.LogSink'>fuchsia.logger.LogSink</a></li>
<li><a class='link' href='#fuchsia.process.Launcher'>fuchsia.process.Launcher</a></li>
</ul>
<p>The following services must be present in order to present web content in a Scenic view
using <a class='link' href='../fuchsia.web.Frame/'>fuchsia.web.Frame</a>/<a class='link' href='../fuchsia.web.Frame/#CreateView'>CreateView</a>:</p>
<ul>
<li><a class='link' href='#fuchsia.ui.scenic.Scenic'>fuchsia.ui.scenic.Scenic</a></li>
<li><a class='link' href='#fuchsia.ui.input.ImeService'>fuchsia.ui.input.ImeService</a></li>
<li><a class='link' href='#fuchsia.ui.input.ImeVisibilityService'>fuchsia.ui.input.ImeVisibilityService</a></li>
</ul>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>data_directory</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#Directory'>Directory</a></code>
            </td>
            <td><p>Handle to the directory that will contain the <a class='link' href='#fuchsia.web.Context'>fuchsia.web.Context</a>'s persistent data. If
it is left unset, then the created <a class='link' href='#fuchsia.web.Context'>fuchsia.web.Context</a> will be stateless, with all of
its data discarded upon <a class='link' href='#fuchsia.web.Context'>fuchsia.web.Context</a> destruction.</p>
<p>If set, <code>data_directory</code> must not be shared with any other <a class='link' href='#fuchsia.web.Context'>fuchsia.web.Context</a>.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>user_agent_product</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td><p>Optional suffix to append to the UserAgent string, to describe the
embedder's product &amp; version. See the User-Agent HTTP header
specification at https://tools.ietf.org/html/rfc7231#section-5.5.3</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>user_agent_version</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>remote_debugging_port</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>Enables Frames to be created with remote debugging enabled using the DevTools protocol. If
<code>port</code> is 0, then an ephemeral port will be used, which can be queried via the
<a class='link' href='../fuchsia.web.Context/'>fuchsia.web.Context</a>/<a class='link' href='../fuchsia.web.Context/#GetRemoteDebuggingPort'>GetRemoteDebuggingPort</a> API.</p>
</td>
        </tr><tr>
            <td>6</td>
            <td><code>content_directories</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ContentDirectoryProvider'>ContentDirectoryProvider</a>&gt;[100]</code>
            </td>
            <td><p>List of providers whose contents will be served by <code>fuchsia-dir://</code> URLs.</p>
</td>
        </tr><tr>
            <td>7</td>
            <td><code>features</code></td>
            <td>
                <code><a class='link' href='#ContextFeatureFlags'>ContextFeatureFlags</a></code>
            </td>
            <td><p>Optional features that should be enabled for this context. Some features may also require
additional services in <code>service_directory</code>.</p>
</td>
        </tr><tr>
            <td>8</td>
            <td><code>playready_key_system</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td><p>Enables PlayReady CDM for the Context using the specified string as a key system
string. The string should be a reverse domain name, as required by
<a href="https://www.w3.org/TR/encrypted-media/#key-system">EME API</a>. Requires
<a class='link' href='#fuchsia.media.drm.PlayReady'>fuchsia.media.drm.PlayReady</a> service.</p>
</td>
        </tr><tr>
            <td>9</td>
            <td><code>unsafely_treat_insecure_origins_as_secure</code></td>
            <td>
                <code>vector&lt;string&gt;[100]</code>
            </td>
            <td><p>Treat given insecure origins as secure origins. For the definition of secure contexts, see
https://w3c.github.io/webappsec-secure-contexts/ and
https://www.w3.org/TR/powerful-features/#is-origin-trustworthy.
Example value: <code>{&quot;http://a.com&quot;, &quot;http://b.com&quot;}</code>.</p>
</td>
        </tr></table>

### CreateFrameParams {#CreateFrameParams}


*Defined in [fuchsia.web/context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/context.fidl#177)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>enable_remote_debugging</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Set to true to enable remote debugging. The <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a> will be closed with
`ERR_INVALID_ARGS if |remote_debugging_port| was not set in
<a class='link' href='#fuchsia.web.CreateContextParams'>fuchsia.web.CreateContextParams</a>.</p>
</td>
        </tr></table>

### CookieId {#CookieId}


*Defined in [fuchsia.web/cookie.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/cookie.fidl#37)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The name of the cookie. An arbitrary string defined by the website.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>domain</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>Specifies the host that is allowed to receive the cookie.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>path</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>Specifies the URL path prefix which is required to receive the cookie.</p>
</td>
        </tr></table>

### Cookie {#Cookie}


*Defined in [fuchsia.web/cookie.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/cookie.fidl#48)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='#CookieId'>CookieId</a></code>
            </td>
            <td><p>A table with fields to identify a cookie.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The cookie value.</p>
</td>
        </tr></table>

### WebMessage {#WebMessage}


*Defined in [fuchsia.web/frame.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/frame.fidl#193)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td><p>The message payload, encoded as an UTF-8 string. This is a required property.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>incoming_transfer</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#IncomingTransferable'>IncomingTransferable</a>&gt;</code>
            </td>
            <td><p>Optional list of objects transferred into the <a class='link' href='#fuchsia.web.MessagePort'>fuchsia.web.MessagePort</a> from the FIDL
client.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>outgoing_transfer</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#OutgoingTransferable'>OutgoingTransferable</a>&gt;</code>
            </td>
            <td><p>Optional list of objects transferred out of the <a class='link' href='#fuchsia.web.MessagePort'>fuchsia.web.MessagePort</a> to the FIDL
client.</p>
</td>
        </tr></table>

### PopupFrameCreationInfo {#PopupFrameCreationInfo}


*Defined in [fuchsia.web/frame.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/frame.fidl#234)*

<p>Specifies additional information about a newly created popup frame.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>initial_url</code></td>
            <td>
                <code>string[65536]</code>
            </td>
            <td><p>The URL to which the popup frame was initially navigated.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>initiated_by_user</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Set if the popup frame was created in response to UI interaction from the user (e.g. a
link was clicked).</p>
</td>
        </tr></table>

### LoadUrlParams {#LoadUrlParams}


*Defined in [fuchsia.web/navigation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/navigation.fidl#65)*

<p>Additional parameters for modifying the behavior of
<a class='link' href='../fuchsia.web.NavigationController/'>fuchsia.web.NavigationController</a>/<a class='link' href='../fuchsia.web.NavigationController/#LoadUrl'>LoadUrl</a>.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#LoadUrlReason'>LoadUrlReason</a></code>
            </td>
            <td><p>Provides a hint to the browser UI about how <a class='link' href='../fuchsia.web.NavigationController/'>fuchsia.web.NavigationController</a>/<a class='link' href='../fuchsia.web.NavigationController/#LoadUrl'>LoadUrl</a>
was triggered.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>referrer_url</code></td>
            <td>
                <code>string[65536]</code>
            </td>
            <td><p>The URL that linked to the resource being requested.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>was_user_activated</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Should be set to true to propagate user activation to the frame. User activation implies
that the user is interacting with the web frame. It enables some web features that are not
available otherwise. For example, autoplay will work only when this flag is set to true.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>headers</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.net.http/'>fuchsia.net.http</a>/<a class='link' href='../fuchsia.net.http/#Header'>Header</a>&gt;</code>
            </td>
            <td><p>Custom HTTP headers.</p>
</td>
        </tr></table>

### NavigationState {#NavigationState}


*Defined in [fuchsia.web/navigation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/navigation.fidl#83)*

<p>Contains information about the <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a>'s navigation state.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>url</code></td>
            <td>
                <code>string[65536]</code>
            </td>
            <td><p>The page's URL.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>title</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The user-visible page title.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>page_type</code></td>
            <td>
                <code><a class='link' href='#PageType'>PageType</a></code>
            </td>
            <td><p>Indicates whether this was a navigation to an error page.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>can_go_forward</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Indicates if there is a following navigation.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>can_go_back</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Indicates if there is a previous navigation.</p>
</td>
        </tr><tr>
            <td>6</td>
            <td><code>is_main_document_loaded</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Indicates that the main document's statically declared resources have been loaded.</p>
</td>
        </tr></table>

### UrlRequestRewriteRule {#UrlRequestRewriteRule}


*Defined in [fuchsia.web/url_request_rewrite_rules.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/url_request_rewrite_rules.fidl#9)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>hosts_filter</code></td>
            <td>
                <code>vector&lt;string&gt;[4096]</code>
            </td>
            <td><p>Set of hosts to apply the rules to. If not set, the rule will apply to every request,
independent of host.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>schemes_filter</code></td>
            <td>
                <code>vector&lt;string&gt;[4096]</code>
            </td>
            <td><p>Set of schemes to apply the rules to. If not set, the rule will apply to every request,
independent of scheme.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>rewrites</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#UrlRequestRewrite'>UrlRequestRewrite</a>&gt;[4096]</code>
            </td>
            <td><p>URL request rewrites to apply.</p>
</td>
        </tr></table>

### UrlRequestRewriteAddHeaders {#UrlRequestRewriteAddHeaders}


*Defined in [fuchsia.web/url_request_rewrite_rules.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/url_request_rewrite_rules.fidl#41)*

<p>Adds <code>headers</code> to the URL request. If a header is already present in the original URL request,
it will be overwritten.</p>
<ul>
<li><code>headers</code> must be set.</li>
<li>Each <a class='link' href='#fuchsia.net.http.Header'>fuchsia.net.http.Header</a> in <code>headers</code> must have a valid HTTP header name and value,
per <a href="https://tools.ietf.org/html/rfc7230#section-3.2">RFC 7230 section  3.2</a>.</li>
</ul>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>headers</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.net.http/'>fuchsia.net.http</a>/<a class='link' href='../fuchsia.net.http/#Header'>Header</a>&gt;[4096]</code>
            </td>
            <td></td>
        </tr></table>

### UrlRequestRewriteRemoveHeader {#UrlRequestRewriteRemoveHeader}


*Defined in [fuchsia.web/url_request_rewrite_rules.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/url_request_rewrite_rules.fidl#50)*

<p>If <code>query_pattern</code> in the URL query, removes <code>header_name</code> from the list of headers. If
<code>query_pattern</code> is not set, removes <code>header_name</code> from the list of headers unconditionally.</p>
<ul>
<li><code>header_name</code> must be set.</li>
<li><code>header_name</code> must be a valid HTTP header name, per
<a href="https://tools.ietf.org/html/rfc7230#section-3.2">RFC 7230 section 3.2</a>.</li>
</ul>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>query_pattern</code></td>
            <td>
                <code>string[65536]</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>header_name</code></td>
            <td>
                <code>vector&lt;uint8&gt;[4096]</code>
            </td>
            <td></td>
        </tr></table>

### UrlRequestRewriteSubstituteQueryPattern {#UrlRequestRewriteSubstituteQueryPattern}


*Defined in [fuchsia.web/url_request_rewrite_rules.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/url_request_rewrite_rules.fidl#59)*

<p>If <code>pattern</code> is found in the URL request query, replaces it with <code>substitution</code>.</p>
<ul>
<li><code>pattern</code> and <code>substitution</code> must be set.</li>
<li><code>substitution</code> must be a valid
<a href="https://url.spec.whatwg.org/#url-query-string">URL-query string</a>.</li>
</ul>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>pattern</code></td>
            <td>
                <code>string[65536]</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>substitution</code></td>
            <td>
                <code>string[65536]</code>
            </td>
            <td></td>
        </tr></table>

### UrlRequestRewriteReplaceUrl {#UrlRequestRewriteReplaceUrl}


*Defined in [fuchsia.web/url_request_rewrite_rules.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/url_request_rewrite_rules.fidl#69)*

<p>If the URL in the URL request ends with <code>url_ends_with</code>, rewrites the URL to <code>new_url</code>.</p>
<ul>
<li><code>url_ends_with</code> and <code>new_url</code> must be set.</li>
<li><code>url_ends_with</code> must be a valid
<a href="https://url.spec.whatwg.org/#path-relative-url-string">path-relative-URL string</a>.</li>
<li><code>new_url</code> must be a <a href="https://url.spec.whatwg.org/#valid-url-string">valid URL string</a>.</li>
</ul>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>url_ends_with</code></td>
            <td>
                <code>string[65536]</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>new_url</code></td>
            <td>
                <code>string[65536]</code>
            </td>
            <td></td>
        </tr></table>



## **UNIONS**

### Context_GetRemoteDebuggingPort_Result {#Context_GetRemoteDebuggingPort_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Context_GetRemoteDebuggingPort_Response'>Context_GetRemoteDebuggingPort_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ContextError'>ContextError</a></code>
            </td>
            <td></td>
        </tr></table>

### Frame_ExecuteJavaScript_Result {#Frame_ExecuteJavaScript_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Frame_ExecuteJavaScript_Response'>Frame_ExecuteJavaScript_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#FrameError'>FrameError</a></code>
            </td>
            <td></td>
        </tr></table>

### Frame_ExecuteJavaScriptNoResult_Result {#Frame_ExecuteJavaScriptNoResult_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Frame_ExecuteJavaScriptNoResult_Response'>Frame_ExecuteJavaScriptNoResult_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#FrameError'>FrameError</a></code>
            </td>
            <td></td>
        </tr></table>

### Frame_AddBeforeLoadJavaScript_Result {#Frame_AddBeforeLoadJavaScript_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Frame_AddBeforeLoadJavaScript_Response'>Frame_AddBeforeLoadJavaScript_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#FrameError'>FrameError</a></code>
            </td>
            <td></td>
        </tr></table>

### Frame_PostMessage_Result {#Frame_PostMessage_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Frame_PostMessage_Response'>Frame_PostMessage_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#FrameError'>FrameError</a></code>
            </td>
            <td></td>
        </tr></table>

### MessagePort_PostMessage_Result {#MessagePort_PostMessage_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#MessagePort_PostMessage_Response'>MessagePort_PostMessage_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#FrameError'>FrameError</a></code>
            </td>
            <td></td>
        </tr></table>

### NavigationController_LoadUrl_Result {#NavigationController_LoadUrl_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#NavigationController_LoadUrl_Response'>NavigationController_LoadUrl_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#NavigationControllerError'>NavigationControllerError</a></code>
            </td>
            <td></td>
        </tr></table>



## **XUNIONS**

### OutgoingTransferable {#OutgoingTransferable}
*Defined in [fuchsia.web/frame.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/frame.fidl#206)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>message_port</code></td>
            <td>
                <code>request&lt;<a class='link' href='#MessagePort'>MessagePort</a>&gt;</code>
            </td>
            <td></td>
        </tr></table>

### IncomingTransferable {#IncomingTransferable}
*Defined in [fuchsia.web/frame.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/frame.fidl#210)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>message_port</code></td>
            <td>
                <code><a class='link' href='#MessagePort'>MessagePort</a></code>
            </td>
            <td></td>
        </tr></table>

### UrlRequestRewrite {#UrlRequestRewrite}
*Defined in [fuchsia.web/url_request_rewrite_rules.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/url_request_rewrite_rules.fidl#22)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>add_headers</code></td>
            <td>
                <code><a class='link' href='#UrlRequestRewriteAddHeaders'>UrlRequestRewriteAddHeaders</a></code>
            </td>
            <td><p>Adds a set of headers to a URL request.</p>
</td>
        </tr><tr>
            <td><code>remove_header</code></td>
            <td>
                <code><a class='link' href='#UrlRequestRewriteRemoveHeader'>UrlRequestRewriteRemoveHeader</a></code>
            </td>
            <td><p>Removes a header based on the presence of a pattern in the URL query.</p>
</td>
        </tr><tr>
            <td><code>substitute_query_pattern</code></td>
            <td>
                <code><a class='link' href='#UrlRequestRewriteSubstituteQueryPattern'>UrlRequestRewriteSubstituteQueryPattern</a></code>
            </td>
            <td><p>Substitutes a pattern in the URL query.</p>
</td>
        </tr><tr>
            <td><code>replace_url</code></td>
            <td>
                <code><a class='link' href='#UrlRequestRewriteReplaceUrl'>UrlRequestRewriteReplaceUrl</a></code>
            </td>
            <td><p>Replaces a URL if the original URL ends with a pattern.</p>
</td>
        </tr></table>



## **BITS**

### ContextFeatureFlags {#ContextFeatureFlags}
Type: <code>uint64</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>NETWORK</td>
            <td>1</td>
            <td><p>Enables network access. Requires the following services:</p>
<ul>
<li><a class='link' href='#fuchsia.net.NameLookup'>fuchsia.net.NameLookup</a></li>
<li><a class='link' href='#fuchsia.netstack.Netstack'>fuchsia.netstack.Netstack</a></li>
<li><a class='link' href='#fuchsia.posix.socket.Provider'>fuchsia.posix.socket.Provider</a></li>
</ul>
</td>
        </tr><tr>
            <td>AUDIO</td>
            <td>2</td>
            <td><p>Enables audio input and output. Requires <a class='link' href='#fuchsia.media.Audio'>fuchsia.media.Audio</a> and
<a class='link' href='#fuchsia.media.SessionAudioConsumerFactory'>fuchsia.media.SessionAudioConsumerFactory</a> service.</p>
</td>
        </tr><tr>
            <td>VULKAN</td>
            <td>4</td>
            <td><p>Enables GPU-accelerated rendering of the web content. Requires the following services:</p>
<ul>
<li><a class='link' href='#fuchsia.sysmem.Allocator'>fuchsia.sysmem.Allocator</a></li>
<li><a class='link' href='#fuchsia.vulkan.loader.Loader'>fuchsia.vulkan.loader.Loader</a></li>
</ul>
</td>
        </tr><tr>
            <td>HARDWARE_VIDEO_DECODER</td>
            <td>8</td>
            <td><p>Enables hardware video decoding. <code>VULKAN</code> must be enabled as well. Requires
<a class='link' href='#fuchsia.mediacodec.CodecFactory'>fuchsia.mediacodec.CodecFactory</a> service.</p>
</td>
        </tr><tr>
            <td>HARDWARE_VIDEO_DECODER_ONLY</td>
            <td>16</td>
            <td><p>Disables all software video decoders. Videos will be rendered only if they can be decoded
in hardware using <a class='link' href='#fuchsia.mediacodec.CodecFactory'>fuchsia.mediacodec.CodecFactory</a>.
Requires the <a class='link' href='#HARDWARE_VIDEO_DECODER'>HARDWARE_VIDEO_DECODER</a> flag.</p>
</td>
        </tr><tr>
            <td>WIDEVINE_CDM</td>
            <td>32</td>
            <td><p>Enables Widevine CDM modules for EME API. <code>VULKAN</code> feature must be enabled as well.
Requires <a class='link' href='#fuchsia.media.drm.Widevine'>fuchsia.media.drm.Widevine</a> service.</p>
</td>
        </tr><tr>
            <td>HEADLESS</td>
            <td>64</td>
            <td><p>Allows embedders to render web content without graphical output or Scenic.
Not compatible with the <a class='link' href='#VULKAN'>VULKAN</a> flag.</p>
</td>
        </tr></table>



## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/constants.fidl#8">MAX_URL_LENGTH</a></td>
            <td>
                    <code>65536</code>
                </td>
                <td><code>int32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/constants.fidl#12">MAX_URL_SCHEME_NAME_LENGTH</a></td>
            <td>
                    <code>255</code>
                </td>
                <td><code>int32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/constants.fidl#16">MAX_HOST_LENGTH</a></td>
            <td>
                    <code>255</code>
                </td>
                <td><code>int32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/constants.fidl#20">MAX_SCHEME_AND_HOST_LENGTH</a></td>
            <td>
                    <code>513</code>
                </td>
                <td><code>int32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/constants.fidl#24">MAX_HEADERS_COUNT</a></td>
            <td>
                    <code>4096</code>
                </td>
                <td><code>int32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/constants.fidl#27">MAX_RULE_COUNT</a></td>
            <td>
                    <code>4096</code>
                </td>
                <td><code>int32</code></td>
            <td></td>
        </tr>
    
</table>



## **TYPE ALIASES**

<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/constants.fidl#9">Url</a></td>
            <td>
                <code>string</code>[<code><a class='link' href='#MAX_URL_LENGTH'>MAX_URL_LENGTH</a></code>]</td>
            <td></td>
        </tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/constants.fidl#13">UrlSchemeName</a></td>
            <td>
                <code>string</code>[<code><a class='link' href='#MAX_URL_SCHEME_NAME_LENGTH'>MAX_URL_SCHEME_NAME_LENGTH</a></code>]</td>
            <td></td>
        </tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/constants.fidl#17">UrlHostName</a></td>
            <td>
                <code>string</code>[<code><a class='link' href='#MAX_HOST_LENGTH'>MAX_HOST_LENGTH</a></code>]</td>
            <td></td>
        </tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/constants.fidl#21">UrlSchemeAndHostName</a></td>
            <td>
                <code>string</code>[<code><a class='link' href='#MAX_SCHEME_AND_HOST_LENGTH'>MAX_SCHEME_AND_HOST_LENGTH</a></code>]</td>
            <td></td>
        </tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/cookie.fidl#7">CookieName</a></td>
            <td>
                <code>string</code></td>
            <td></td>
        </tr></table>

