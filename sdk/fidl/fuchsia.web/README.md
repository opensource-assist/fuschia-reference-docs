[TOC]

# fuchsia.web


## **PROTOCOLS**

## ContextProvider {#ContextProvider}
*Defined in [fuchsia.web/context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/context.fidl#17)*

 The top-level service interface which allows for the creation of Context resources.

### Create {#Create}

 Creates a new browser <a class='link' href='#fuchsia.web.Context'>fuchsia.web.Context</a> whose state is wholly independent and
 isolated from other Contexts.

 - `context`: An interface request which will receive a bound <a class='link' href='#fuchsia.web.Context'>fuchsia.web.Context</a>
   service.

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
*Defined in [fuchsia.web/context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/context.fidl#145)*

 Manages browsing state (e.g. LocalStorage, cookies, etc) associated with a set of
 <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a>.

### CreateFrame {#CreateFrame}

 Creates a new <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a> under this <a class='link' href='#fuchsia.web.Context'>fuchsia.web.Context</a>. Destruction of a
 <a class='link' href='#fuchsia.web.Context'>fuchsia.web.Context</a> triggers the destruction of all of its associated
 <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a>. <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a> can be transferred to another component but
 cannot be shared across multiple components.

 - `frame`: An interface request that will be bound to the created <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a>.

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

 Similar to <a class='link' href='../fuchsia.web.Context/'>fuchsia.web.Context</a>/<a class='link' href='../fuchsia.web.Context/#CreateFrame'>CreateFrame</a>, with extra parameters.

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

 Used to observe cookies for sites hosted under this Context.

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

 Waits until debugging is available on one or more Frames, and returns the DevTools port
 number. Multiple calls may be queued to received the port number.

 If an error occured, the <a class='link' href='#fuchsia.web.ContextError'>fuchsia.web.ContextError</a> will be set to this value:
 - `REMOTE_DEBUGGING_PORT_NOT_OPENED`: |remote_debugging_port| was not set in
   <a class='link' href='#fuchsia.web.CreateContextParams'>fuchsia.web.CreateContextParams</a> or the remote debugging service failed to start.

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

 Provides methods for monitoring and accessing browser cookie state.

### ObserveCookieChanges {#ObserveCookieChanges}

 Observe changes to all cookies named `name` that would be sent in a request to `url`.

 If neither `url` nor `name` are set then all cookies are observed. If only `url` is set
 then all cookies for that URL are observed. If both are set then only cookies matching both
 fields are observed.

 |changes| iterates over a stream of cookie changes. Additions or updates are expressed as
 complete cookies, while deletions are expressed as cookies with no `value` set.

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

 Returns a list of Cookies, optionally limited to those matching `url`, and optionally
 `name`. `cookies` iterates over the matching cookies, including their `value`s.

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

 Used to iterator over a set of cookies, or a stream of changes to cookies.

### GetNext {#GetNext}

 Fetches the next batch of cookies, or of changes to cookies.

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

 The debug service which allows to enable the DevTools service on Contexts.

### EnableDevTools {#EnableDevTools}

 Enables the DevTools service on every subsequent Context creation and
 and delivers subsequent DevTools events to the supplied `listener`.
 The callback indicates when the WebEngine is in a debuggable state.
 Events will be sent to every `listener` registered with this method.

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

 Interface used to observe DevTools service availability events.

### OnContextDevToolsAvailable {#OnContextDevToolsAvailable}

 Called when the DevTools service is available on a new Context.

 `listener`: Channel over which DevTools events for the new Context will
             be delivered. This channel will disconnect when the Context
             is detroyed.

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

 Interface supplied by the debugging component to observe the DevTools
 service opening event.

### OnHttpPortOpen {#OnHttpPortOpen}

 Called when the DevTools service starts accepting TCP connections on
 `port`. `port` will remain open until the Context is destroyed.

 `port`: The port used by the service.

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

 Creates a new view using the specified `view_token`. Caller should pass the other end of
 the token to <a class='link' href='../fuchsia.ui.gfx.ViewHolderArgs/'>fuchsia.ui.gfx.ViewHolderArgs</a>/<a class='link' href='../fuchsia.ui.gfx.ViewHolderArgs/#token'>token</a> to attach the new view to a view tree.

 - `view_token`: Token for the new view.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/#ViewToken'>ViewToken</a></code>
            </td>
        </tr></table>



### GetMediaPlayer {#GetMediaPlayer}

 Returns a <a class='link' href='#fuchsia.media.sessions2.Player'>fuchsia.media.sessions2.Player</a> interface through which media (i.e.
 video/audio) playback in the frame may be observed, and/or controlled. Only one
 <a class='link' href='#fuchsia.media.sessions2.Player'>fuchsia.media.sessions2.Player</a> may be active at a time, for each <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a>.

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

 Returns an interface through which the <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a> may be navigated to a desired
 URL, reloaded, etc.

 - `controller`: An asynchronous interface request for the <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a>'s
 <a class='link' href='#fuchsia.web.NavigationController'>fuchsia.web.NavigationController</a>.

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

 Executes a UTF-8 encoded `script` in the <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a> if the
 <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a>'s URL has an origin which matches entries in `origins`.

 At least one `origins` entry must be specified. If a wildcard `"*"` is specified in
 `origins`, then the script will be evaluated unconditionally.

 Returns the result of executing `script`, as a JSON-encoded string.

 Note that scripts share the same execution context as the document,
 meaning that document may modify variables, classes, or objects set by
 the script in arbitrary or unpredictable ways.

 If an error occured, the FrameError will be set to one of these values:
 - `BUFFER_NOT_UTF8`: `script` is not UTF-8 encoded.
 - `INVALID_ORIGIN`: The <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a>'s current URL does not match any of the
    values in `origins` or `origins` is an empty vector.

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

 Variant of <a class='link' href='../fuchsia.web.Frame/'>fuchsia.web.Frame</a>/<a class='link' href='../fuchsia.web.Frame/#ExecuteJavaScript'>ExecuteJavaScript</a> which executes the supplied script
 without returning a result.

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

 Executes a UTF-8 encoded `script` for every subsequent page load where the
 <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a>'s URL has an origin reflected in `origins`. The script is executed
 early, prior to the execution of the document's scripts.

 Scripts are identified by a client-managed identifier `id`. Any script previously injected
 using the same `id` will be replaced.

 The order in which multiple bindings are executed is the same as the order in which the
 bindings were added. If a script is added which clobbers an existing script of the same
 `id`, the previous script's precedence in the injection order will be preserved.

 At least one `origins` entry must be specified. If a wildcard `"*"` is specified in
 `origins`, then the script will be evaluated unconditionally.

 If an error occured, the <a class='link' href='#fuchsia.web.FrameError'>fuchsia.web.FrameError</a> will be set to one of these values:
 - `BUFFER_NOT_UTF8`: `script` is not UTF-8 encoded.
 - `INVALID_ORIGIN`: `origins` is an empty vector.

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

 Removes a previously added JavaScript snippet identified by `id`. This is a no-op if there
 is no JavaScript snippet identified by `id`.

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

 Posts a message to the frame's onMessage handler.

 `target_origin` restricts message delivery to the specified origin. If `target_origin` is
 `"*"`, then the message will be sent to the document regardless of its origin.
 See the
 [https://html.spec.whatwg.org/multipage/web-messaging.html#posting-messages](HTML spec)
 section 9.4.3 for more details on how the target origin policy is applied.

 If an error occured, the <a class='link' href='#fuchsia.web.FrameError'>fuchsia.web.FrameError</a> will be set to one of these values:
 - `INTERNAL_ERROR`: The WebEngine failed to create a message pipe.
 - `BUFFER_NOT_UTF8`: The script in `message`'s `data` property is not UTF-8 encoded.
 - `INVALID_ORIGIN`: `origins` is an empty vector.
 - `NO_DATA_IN_MESSAGE`: The `data` property is missing in `message`.

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

 Sets the listener for handling page navigation events.

 - `listener`: The observer to use. Unregisters any existing listener is null.

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

 If set to a value other than <a class='link' href='../fuchsia.web.ConsoleLogLevel/'>fuchsia.web.ConsoleLogLevel</a>/<a class='link' href='../fuchsia.web.ConsoleLogLevel/#NONE'>NONE</a>, allows web content to
 log messages to the system logger using the console APIs (`debug()`, `log()`, `info()`,
 `warn()` and `error()`).

 When logged to the system logger:
 - `debug()`, `log()` and `info()` logs are logged with
   <a class='link' href='../fuchsia.logger.LogLevelFilter/'>fuchsia.logger.LogLevelFilter</a>/<a class='link' href='../fuchsia.logger.LogLevelFilter/#INFO'>INFO</a> severity level.
 - `warn()` logs are logged with <a class='link' href='../fuchsia.logger.LogLevelFilter/'>fuchsia.logger.LogLevelFilter</a>/<a class='link' href='../fuchsia.logger.LogLevelFilter/#INFO'>INFO</a> severity level.
 - `error()` logs are logged with <a class='link' href='../fuchsia.logger.LogLevelFilter/'>fuchsia.logger.LogLevelFilter</a>/<a class='link' href='../fuchsia.logger.LogLevelFilter/#INFO'>INFO</a> severity level.

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

 Used at runtime to enable or disable user input processing (e.g. keyboard, mouse, touch) on
 a <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a>.

 Input is enabled by default.

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

 Sets the listener for handling popup frame opened by web content. If no listener is
 present, then any new popup frame will be blocked.

 - `listener`: The listener to use. Unregisters any existing listener if null.

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

 Supplies a set of <a class='link' href='#fuchsia.web.UrlRequestRewriteRule'>fuchsia.web.UrlRequestRewriteRule</a> to apply on every subsequent URL
 request.
 - `rules` are cumulative and applied in order.
 - `rules` will be validated before being applied. If `rules` are invalid, the
   <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a> will be closed with `ERR_INVALID_ARGS`.
 - <a class='link' href='../fuchsia.web.Frame/'>fuchsia.web.Frame</a>/<a class='link' href='../fuchsia.web.Frame/#SetUrlRequestRewriteRules'>SetUrlRequestRewriteRules</a> must not be called again until its
   acknowledgement callback has been processed. If this happens, the <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a>
   will be closed with `ERR_BAD_STATE`.

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

## MessagePort {#MessagePort}
*Defined in [fuchsia.web/frame.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/frame.fidl#199)*

 Represents one end of an HTML5 MessageChannel. Can be used to send and exchange Messages with
 the peered MessagePort in the Frame's script context. The port is destroyed when either end of
 the MessagePort channel is torn down.

### PostMessage {#PostMessage}

 Sends a <a class='link' href='#fuchsia.web.WebMessage'>fuchsia.web.WebMessage</a> to the peer. These are processed in order, one at a
 time. It is not necessary for the caller to wait for the completion callback before calling
 <a class='link' href='../fuchsia.web.MessagePort/'>fuchsia.web.MessagePort</a>/<a class='link' href='../fuchsia.web.MessagePort/#PostMessage'>PostMessage</a> again.

 If an error occured, the <a class='link' href='#fuchsia.web.FrameError'>fuchsia.web.FrameError</a> will be set to one of these value:
 - `BUFFER_NOT_UTF8`: The script in `message`'s `data` property is not UTF-8 encoded.
 - `NO_DATA_IN_MESSAGE`: The `data` property is missing in `message`.

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

 Asynchronously reads the next message from the channel. The client should invoke the
 callback when it is ready to process another message. Unreceived messages are buffered
 on the sender's side and bounded by its available resources.

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
*Defined in [fuchsia.web/frame.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/frame.fidl#225)*


### OnPopupFrameCreated {#OnPopupFrameCreated}

 Called when a <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a> has created a new popup `frame`. Information about the
 popup frame, and how it was created, is provided via `info`. Additional popup frames are
 delivered after the the acknowledgement callback is invoked.

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

 Interface supplied by the embedder for receiving notifications about navigation events in a
 <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a>.

### OnNavigationStateChanged {#OnNavigationStateChanged}

 Called when user-visible navigation state has changed since <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a> creation
 or the last acknowledgement callback, whichever occurred last. `change` will contain all
 the differences in navigation state since the last acknowledgement. Any unchanged
 properties will be left unset in `change`.

 Implementer must call the acknowledgement callback to receive new navigation events.

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

 Provides methods for controlling and querying the navigation state of a <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a>.

### LoadUrl {#LoadUrl}

 Tells the <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a> to navigate to a `url`.

 - `url`:    The address to navigate to.
 - `params`: Additional parameters that affect how the resource will be
   loaded (e.g. cookies, HTTP headers, etc.)

 If an error occured, the <a class='link' href='#fuchsia.web.NavigationControllerError'>fuchsia.web.NavigationControllerError</a> will be set to one of
 these values:
 - `INVALID_URL`: The `url` parameter is invalid.
 - `INVALID_HEADER`: At least one of the headers in <a class='link' href='../fuchsia.web.LoadUrlParams/'>fuchsia.web.LoadUrlParams</a>/<a class='link' href='../fuchsia.web.LoadUrlParams/#headers'>headers</a>
   is invalid.

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

 Tells the <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a> to navigate to the previous page in its history, if any.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### GoForward {#GoForward}

 Tells the <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a> to navigate to the next page in its history, if any.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Stop {#Stop}

 Tells the <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a> to stop the current navigation if a navigation is ongoing.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Reload {#Reload}

 Tells the <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a> to reload the current page.

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

 Returns information for the currently visible content regardless of loading state, or an
 empty entry if no content is being displayed.

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
            <td> The remote debugging service was not opened.
</td>
        </tr></table>

### ConsoleLogLevel {#ConsoleLogLevel}
Type: <code>int32</code>

*Defined in [fuchsia.web/frame.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/frame.fidl#12)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NONE</code></td>
            <td><code>100</code></td>
            <td> No logging.
</td>
        </tr><tr>
            <td><code>DEBUG</code></td>
            <td><code>-1</code></td>
            <td> Outputs messages from `console.debug()` and above levels.
</td>
        </tr><tr>
            <td><code>INFO</code></td>
            <td><code>0</code></td>
            <td> Outputs messages from `console.log()`, `console.info()` and above levels.
</td>
        </tr><tr>
            <td><code>WARN</code></td>
            <td><code>1</code></td>
            <td> Outputs messages from `console.warn()` and `console.error()`.
</td>
        </tr><tr>
            <td><code>ERROR</code></td>
            <td><code>2</code></td>
            <td> Outputs messages from `console.error()`.
</td>
        </tr></table>

### FrameError {#FrameError}
Type: <code>int32</code>

*Defined in [fuchsia.web/frame.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/frame.fidl#30)*

 Represents the return status of a <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a> method.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INTERNAL_ERROR</code></td>
            <td><code>1</code></td>
            <td> An internal error occured.
</td>
        </tr><tr>
            <td><code>BUFFER_NOT_UTF8</code></td>
            <td><code>2</code></td>
            <td> The provided buffer is not UTF-8 encoded.
</td>
        </tr><tr>
            <td><code>INVALID_ORIGIN</code></td>
            <td><code>3</code></td>
            <td> The Frame's URL does not match any of the origins provided by the caller.
</td>
        </tr><tr>
            <td><code>NO_DATA_IN_MESSAGE</code></td>
            <td><code>4</code></td>
            <td> The required `data` property is missing from a <a class='link' href='#fuchsia.web.WebMessage'>fuchsia.web.WebMessage</a>.
</td>
        </tr></table>

### NavigationControllerError {#NavigationControllerError}
Type: <code>int32</code>

*Defined in [fuchsia.web/navigation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/navigation.fidl#22)*

 Represents the return status of a <a class='link' href='#fuchsia.web.NavigationController'>fuchsia.web.NavigationController</a> method.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INVALID_URL</code></td>
            <td><code>1</code></td>
            <td> The provided URL is invalid.
</td>
        </tr><tr>
            <td><code>INVALID_HEADER</code></td>
            <td><code>2</code></td>
            <td> At least one of the provided headers was invalid.
</td>
        </tr></table>

### ReloadType {#ReloadType}
Type: <code>uint32</code>

*Defined in [fuchsia.web/navigation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/navigation.fidl#104)*

 Characterizes the type of reload.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>PARTIAL_CACHE</code></td>
            <td><code>0</code></td>
            <td> Reloads the current entry, bypassing the cache for the main resource.
</td>
        </tr><tr>
            <td><code>NO_CACHE</code></td>
            <td><code>1</code></td>
            <td> Reloads the current entry, bypassing the cache entirely.
</td>
        </tr></table>

### LoadUrlReason {#LoadUrlReason}
Type: <code>uint32</code>

*Defined in [fuchsia.web/navigation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/navigation.fidl#113)*

 Characterizes the origin of a <a class='link' href='../fuchsia.web.NavigationController/'>fuchsia.web.NavigationController</a>/<a class='link' href='../fuchsia.web.NavigationController/#LoadUrl'>LoadUrl</a> request.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>LINK</code></td>
            <td><code>0</code></td>
            <td> Navigation was initiated by the user following a link.
</td>
        </tr><tr>
            <td><code>TYPED</code></td>
            <td><code>1</code></td>
            <td> Navigation was initiated by a user-provided URL.
</td>
        </tr></table>

### PageType {#PageType}
Type: <code>uint32</code>

*Defined in [fuchsia.web/navigation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/navigation.fidl#122)*

 Characterizes the page type in a <a class='link' href='#fuchsia.web.NavigationState'>fuchsia.web.NavigationState</a>.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NORMAL</code></td>
            <td><code>0</code></td>
            <td> Regular web page.
</td>
        </tr><tr>
            <td><code>ERROR</code></td>
            <td><code>1</code></td>
            <td> Error page.
</td>
        </tr></table>



## **TABLES**

### ContentDirectoryProvider {#ContentDirectoryProvider}


*Defined in [fuchsia.web/context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/context.fidl#46)*

 Defines a provider which hosts resources from a <a class='link' href='#fuchsia.io.Directory'>fuchsia.io.Directory</a>. Content can `GET`
 resource files via the provider, but not enumerate directories. Resources can be accessed by
 their URLs: `fuchsia-dir://<provider-name>/<path/to/resource>`

 By default the MIME types of files are determined automatically by "sniffing" the contents of
 the files. No content encoding will be declared, which browsers will interpret as meaning
 `"text/plain"`.

 Content type and encoding metadata may optionally be specified explicitly by metadata files,
 which reside alongside the file. Metadata is expressed in JSON files, named after the files
 they describe with a `"._metadata"` suffix.

 For example, the file `"index.html"` would have the a metadata file called
 `"index.html._metadata"`, with the following contents:
 ```
 {
   "charset": "utf-8",
   "mime": "text/html"
 }
 ```


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string[255]</code>
            </td>
            <td> Name of the provider. Must be non-empty and composed solely of alphanumerics, dots, and
 dashes.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>directory</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#Directory'>Directory</a></code>
            </td>
            <td> Directory containing the files served by this provider.
</td>
        </tr></table>

### CreateContextParams {#CreateContextParams}


*Defined in [fuchsia.web/context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/context.fidl#87)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>service_directory</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#Directory'>Directory</a></code>
            </td>
            <td> Service directory to be used by the context. The following services must be present in the
 directory:
 - <a class='link' href='#fuchsia.deprecatedtimezone.Timezone'>fuchsia.deprecatedtimezone.Timezone</a>
 - <a class='link' href='#fuchsia.device.NameProvider'>fuchsia.device.NameProvider</a>
 - <a class='link' href='#fuchsia.fonts.Provider'>fuchsia.fonts.Provider</a>
 - <a class='link' href='#fuchsia.logger.LogSink'>fuchsia.logger.LogSink</a>
 - <a class='link' href='#fuchsia.process.Launcher'>fuchsia.process.Launcher</a>

 The following services must be present in order to present web content in a Scenic view
 using <a class='link' href='../fuchsia.web.Frame/'>fuchsia.web.Frame</a>/<a class='link' href='../fuchsia.web.Frame/#CreateView'>CreateView</a>:
 - <a class='link' href='#fuchsia.ui.scenic.Scenic'>fuchsia.ui.scenic.Scenic</a>
 - <a class='link' href='#fuchsia.ui.input.ImeService'>fuchsia.ui.input.ImeService</a>
 - <a class='link' href='#fuchsia.ui.input.ImeVisibilityService'>fuchsia.ui.input.ImeVisibilityService</a>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>data_directory</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#Directory'>Directory</a></code>
            </td>
            <td> Handle to the directory that will contain the <a class='link' href='#fuchsia.web.Context'>fuchsia.web.Context</a>'s persistent data. If
 it is left unset, then the created <a class='link' href='#fuchsia.web.Context'>fuchsia.web.Context</a> will be stateless, with all of
 its data discarded upon <a class='link' href='#fuchsia.web.Context'>fuchsia.web.Context</a> destruction.

 If set, `data_directory` must not be shared with any other <a class='link' href='#fuchsia.web.Context'>fuchsia.web.Context</a>.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>user_agent_product</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td> Optional suffix to append to the UserAgent string, to describe the
 embedder's product & version. See the User-Agent HTTP header
 specification at https://tools.ietf.org/html/rfc7231#section-5.5.3
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
            <td> Enables Frames to be created with remote debugging enabled using the DevTools protocol. If
 `port` is 0, then an ephemeral port will be used, which can be queried via the
 <a class='link' href='../fuchsia.web.Context/'>fuchsia.web.Context</a>/<a class='link' href='../fuchsia.web.Context/#GetRemoteDebuggingPort'>GetRemoteDebuggingPort</a> API.
</td>
        </tr><tr>
            <td>6</td>
            <td><code>content_directories</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ContentDirectoryProvider'>ContentDirectoryProvider</a>&gt;[100]</code>
            </td>
            <td> List of providers whose contents will be served by `fuchsia-dir://` URLs.
</td>
        </tr><tr>
            <td>7</td>
            <td><code>features</code></td>
            <td>
                <code><a class='link' href='#ContextFeatureFlags'>ContextFeatureFlags</a></code>
            </td>
            <td> Optional features that should be enabled for this context. Some features may also require
 additional services in `service_directory`.
</td>
        </tr><tr>
            <td>8</td>
            <td><code>playready_key_system</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td> Enables PlayReady CDM for the Context using the specified string as a key system
 string. The string should be a reverse domain name, as required by
 [EME API](https://www.w3.org/TR/encrypted-media/#key-system). Requires
 <a class='link' href='#fuchsia.media.drm.PlayReady'>fuchsia.media.drm.PlayReady</a> service.
</td>
        </tr><tr>
            <td>9</td>
            <td><code>unsafely_treat_insecure_origins_as_secure</code></td>
            <td>
                <code>vector&lt;string&gt;[100]</code>
            </td>
            <td> Treat given insecure origins as secure origins. For the definition of secure contexts, see
 https://w3c.github.io/webappsec-secure-contexts/ and
 https://www.w3.org/TR/powerful-features/#is-origin-trustworthy.
 Example value: `{"http://a.com", "http://b.com"}`.
</td>
        </tr></table>

### CreateFrameParams {#CreateFrameParams}


*Defined in [fuchsia.web/context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/context.fidl#171)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>enable_remote_debugging</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Set to true to enable remote debugging. The <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a> will be closed with
 `ERR_INVALID_ARGS if |remote_debugging_port| was not set in
 <a class='link' href='#fuchsia.web.CreateContextParams'>fuchsia.web.CreateContextParams</a>.
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
            <td> The name of the cookie. An arbitrary string defined by the website.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>domain</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Specifies the host that is allowed to receive the cookie.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>path</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Specifies the URL path prefix which is required to receive the cookie.
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
            <td> A table with fields to identify a cookie.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The cookie value.
</td>
        </tr></table>

### WebMessage {#WebMessage}


*Defined in [fuchsia.web/frame.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/frame.fidl#175)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td> The message payload, encoded as an UTF-8 string. This is a required property.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>incoming_transfer</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#IncomingTransferable'>IncomingTransferable</a>&gt;</code>
            </td>
            <td> Optional list of objects transferred into the <a class='link' href='#fuchsia.web.MessagePort'>fuchsia.web.MessagePort</a> from the FIDL
 client.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>outgoing_transfer</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#OutgoingTransferable'>OutgoingTransferable</a>&gt;</code>
            </td>
            <td> Optional list of objects transferred out of the <a class='link' href='#fuchsia.web.MessagePort'>fuchsia.web.MessagePort</a> to the FIDL
 client.
</td>
        </tr></table>

### PopupFrameCreationInfo {#PopupFrameCreationInfo}


*Defined in [fuchsia.web/frame.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/frame.fidl#216)*

 Specifies additional information about a newly created popup frame.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>initial_url</code></td>
            <td>
                <code>string[65536]</code>
            </td>
            <td> The URL to which the popup frame was initially navigated.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>initiated_by_user</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Set if the popup frame was created in response to UI interaction from the user (e.g. a
 link was clicked).
</td>
        </tr></table>

### LoadUrlParams {#LoadUrlParams}


*Defined in [fuchsia.web/navigation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/navigation.fidl#65)*

 Additional parameters for modifying the behavior of
 <a class='link' href='../fuchsia.web.NavigationController/'>fuchsia.web.NavigationController</a>/<a class='link' href='../fuchsia.web.NavigationController/#LoadUrl'>LoadUrl</a>.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#LoadUrlReason'>LoadUrlReason</a></code>
            </td>
            <td> Provides a hint to the browser UI about how <a class='link' href='../fuchsia.web.NavigationController/'>fuchsia.web.NavigationController</a>/<a class='link' href='../fuchsia.web.NavigationController/#LoadUrl'>LoadUrl</a>
 was triggered.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>referrer_url</code></td>
            <td>
                <code>string[65536]</code>
            </td>
            <td> The URL that linked to the resource being requested.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>was_user_activated</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Should be set to true to propagate user activation to the frame. User activation implies
 that the user is interacting with the web frame. It enables some web features that are not
 available otherwise. For example, autoplay will work only when this flag is set to true.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>headers</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.net.http/'>fuchsia.net.http</a>/<a class='link' href='../fuchsia.net.http/#Header'>Header</a>&gt;</code>
            </td>
            <td> Custom HTTP headers.
</td>
        </tr></table>

### NavigationState {#NavigationState}


*Defined in [fuchsia.web/navigation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/navigation.fidl#83)*

 Contains information about the <a class='link' href='#fuchsia.web.Frame'>fuchsia.web.Frame</a>'s navigation state.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>url</code></td>
            <td>
                <code>string[65536]</code>
            </td>
            <td> The page's URL.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>title</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The user-visible page title.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>page_type</code></td>
            <td>
                <code><a class='link' href='#PageType'>PageType</a></code>
            </td>
            <td> Indicates whether this was a navigation to an error page.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>can_go_forward</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Indicates if there is a following navigation.
</td>
        </tr><tr>
            <td>5</td>
            <td><code>can_go_back</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Indicates if there is a previous navigation.
</td>
        </tr><tr>
            <td>6</td>
            <td><code>is_main_document_loaded</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Indicates that the main document's statically declared resources have been loaded.
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
            <td> Set of hosts to apply the rules to. If not set, the rule will apply to every request,
 independent of host.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>schemes_filter</code></td>
            <td>
                <code>vector&lt;string&gt;[4096]</code>
            </td>
            <td> Set of schemes to apply the rules to. If not set, the rule will apply to every request,
 independent of scheme.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>rewrites</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#UrlRequestRewrite'>UrlRequestRewrite</a>&gt;[4096]</code>
            </td>
            <td> URL request rewrites to apply.
</td>
        </tr></table>

### UrlRequestRewriteAddHeaders {#UrlRequestRewriteAddHeaders}


*Defined in [fuchsia.web/url_request_rewrite_rules.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/url_request_rewrite_rules.fidl#41)*

 Adds `headers` to the URL request. If a header is already present in the original URL request,
 it will be overwritten.
 - `headers` must be set.
 - Each <a class='link' href='#fuchsia.net.http.Header'>fuchsia.net.http.Header</a> in `headers` must have a valid HTTP header name and value,
   per [RFC 7230 section  3.2](https://tools.ietf.org/html/rfc7230#section-3.2).


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

 If `query_pattern` in the URL query, removes `header_name` from the list of headers. If
 `query_pattern` is not set, removes `header_name` from the list of headers unconditionally.
 - `header_name` must be set.
 - `header_name` must be a valid HTTP header name, per
   [RFC 7230 section 3.2](https://tools.ietf.org/html/rfc7230#section-3.2).


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

 If `pattern` is found in the URL request query, replaces it with `substitution`.
 - `pattern` and `substitution` must be set.
 - `substitution` must be a valid
   [URL-query string](https://url.spec.whatwg.org/#url-query-string).


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

 If the URL in the URL request ends with `url_ends_with`, rewrites the URL to `new_url`.
 - `url_ends_with` and `new_url` must be set.
 - `url_ends_with` must be a valid
   [path-relative-URL string](https://url.spec.whatwg.org/#path-relative-url-string).
 - `new_url` must be a [valid URL string](https://url.spec.whatwg.org/#valid-url-string).


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
*Defined in [fuchsia.web/frame.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/frame.fidl#188)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>message_port</code></td>
            <td>
                <code>request&lt;<a class='link' href='#MessagePort'>MessagePort</a>&gt;</code>
            </td>
            <td></td>
        </tr></table>

### IncomingTransferable {#IncomingTransferable}
*Defined in [fuchsia.web/frame.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/frame.fidl#192)*


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
            <td> Adds a set of headers to a URL request.
</td>
        </tr><tr>
            <td><code>remove_header</code></td>
            <td>
                <code><a class='link' href='#UrlRequestRewriteRemoveHeader'>UrlRequestRewriteRemoveHeader</a></code>
            </td>
            <td> Removes a header based on the presence of a pattern in the URL query.
</td>
        </tr><tr>
            <td><code>substitute_query_pattern</code></td>
            <td>
                <code><a class='link' href='#UrlRequestRewriteSubstituteQueryPattern'>UrlRequestRewriteSubstituteQueryPattern</a></code>
            </td>
            <td> Substitutes a pattern in the URL query.
</td>
        </tr><tr>
            <td><code>replace_url</code></td>
            <td>
                <code><a class='link' href='#UrlRequestRewriteReplaceUrl'>UrlRequestRewriteReplaceUrl</a></code>
            </td>
            <td> Replaces a URL if the original URL ends with a pattern.
</td>
        </tr></table>



## **BITS**

### ContextFeatureFlags {#ContextFeatureFlags}
Type: <code>uint64</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>NETWORK</td>
            <td>1</td>
            <td> Enables network access. Requires the following services:
 - <a class='link' href='#fuchsia.net.NameLookup'>fuchsia.net.NameLookup</a>
 - <a class='link' href='#fuchsia.netstack.Netstack'>fuchsia.netstack.Netstack</a>
 - <a class='link' href='#fuchsia.posix.socket.Provider'>fuchsia.posix.socket.Provider</a>
</td>
        </tr><tr>
            <td>AUDIO</td>
            <td>2</td>
            <td> Enables audio input and output. Requires <a class='link' href='#fuchsia.media.Audio'>fuchsia.media.Audio</a> service.
</td>
        </tr><tr>
            <td>VULKAN</td>
            <td>4</td>
            <td> Enables GPU-accelerated rendering of the web content. Requires the following services:
 - <a class='link' href='#fuchsia.sysmem.Allocator'>fuchsia.sysmem.Allocator</a>
 - <a class='link' href='#fuchsia.vulkan.loader.Loader'>fuchsia.vulkan.loader.Loader</a>
</td>
        </tr><tr>
            <td>HARDWARE_VIDEO_DECODER</td>
            <td>8</td>
            <td> Enables hardware video decoding. `VULKAN` must be enabled as well. Requires
 <a class='link' href='#fuchsia.mediacodec.CodecFactory'>fuchsia.mediacodec.CodecFactory</a> service.
</td>
        </tr><tr>
            <td>HARDWARE_VIDEO_DECODER_ONLY</td>
            <td>16</td>
            <td> Disables all software video decoders. Videos will be rendered only if they can be decoded
 in hardware using <a class='link' href='#fuchsia.mediacodec.CodecFactory'>fuchsia.mediacodec.CodecFactory</a>.
 Requires the <a class='link' href='#HARDWARE_VIDEO_DECODER'>HARDWARE_VIDEO_DECODER</a> flag.
</td>
        </tr><tr>
            <td>WIDEVINE_CDM</td>
            <td>32</td>
            <td> Enables Widevine CDM modules for EME API. `VULKAN` feature must be enabled as well.
 Requires <a class='link' href='#fuchsia.media.drm.Widevine'>fuchsia.media.drm.Widevine</a> service.
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

