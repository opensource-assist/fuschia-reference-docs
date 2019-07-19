Project: /_project.yaml
Book: /_book.yaml

# fuchsia.web


## **PROTOCOLS**

## ContextProvider {:#ContextProvider}
*Defined in [fuchsia.web/context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/context.fidl#19)*

 The top-level service interface which allows for the creation of
 Context resources.

### Create {:#Create}

 Creates a new browser Context whose state is wholly independent and
 isolated from other Contexts.

 `context`: An interface request which will receive a bound Context
            service.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>params</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#CreateContextParams'>CreateContextParams</a></code>
            </td>
        </tr><tr>
            <td><code>context</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.web/index.html#Context'>Context</a>&gt;</code>
            </td>
        </tr></table>



## Context {:#Context}
*Defined in [fuchsia.web/context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/context.fidl#58)*

 Manages browsing state (e.g. LocalStorage, cookies, etc) associated with
 a set of Frames.

### CreateFrame {:#CreateFrame}

 Creates a new frame under this Context. Destruction of a Context
 triggers the destruction of all of its associated Frames. Frames can be
 transferred to another component but cannot be shared across multiple
 components.

 `frame`: An interface request that will be bound to the created Frame.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>frame</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.web/index.html#Frame'>Frame</a>&gt;</code>
            </td>
        </tr></table>



### GetCookieManager {:#GetCookieManager}

 Used to observe cookies for sites hosted under this Context.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>manager</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.web/index.html#CookieManager'>CookieManager</a>&gt;</code>
            </td>
        </tr></table>



### GetRemoteDebuggingPort {:#GetRemoteDebuggingPort}

 Returns the port used for remote debugging.
 The ContextError will be set to REMOTE_DEBUGGING_PORT_NOT_OPENED if
 |remote_debugging_port| was not set in CreateContextParams or the
 remote debugging service failed to start.

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
                <code><a class='link' href='../fuchsia.web/index.html#Context_GetRemoteDebuggingPort_Result'>Context_GetRemoteDebuggingPort_Result</a></code>
            </td>
        </tr></table>

## CookieManager {:#CookieManager}
*Defined in [fuchsia.web/cookie.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/cookie.fidl#10)*

 Provides methods for monitoring and accessing browser cookie state.

### StartObservingChanges {:#StartObservingChanges}

 Observe changes to all cookies named `name` that would be sent in a
 request to `url`.
 `url` may be un-set to observe changes across all URLs,
 Similarly, `name` may be un-set to observe changes across all cookie
 names.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>url</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr><tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#CookieChangeListener'>CookieChangeListener</a></code>
            </td>
        </tr></table>



### GetCookies {:#GetCookies}

 Returns a list of Cookies whose CookieIds match `ids`.
 Entries in `cookies` will be omitted for any CookieIds which can't be
 found.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ids</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.web/index.html#CookieId'>CookieId</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>cookies</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.web/index.html#Cookie'>Cookie</a>&gt;</code>
            </td>
        </tr></table>

## CookieChangeListener {:#CookieChangeListener}
*Defined in [fuchsia.web/cookie.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/cookie.fidl#28)*

 Receives notifications about changes in a context's cookie store.

### OnCookieChanged {:#OnCookieChanged}

 Notifies the observer whenever cookies are added, changed, or removed
 for observed URLs. `changes` is populated with information about the
 cookies that were changed, and how they were changed.
 Cookies' data can be accessed by calling GetCookie() with the CookieId.
 Future cookie change events will be buffered until the acknowledgement
 callback is invoked.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>changes</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.web/index.html#CookieChangeEvent'>CookieChangeEvent</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## Debug {:#Debug}
*Defined in [fuchsia.web/debug.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/debug.fidl#9)*

 The debug service which allows to enable the DevTools service on Contexts.

### EnableDevTools {:#EnableDevTools}

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
                <code><a class='link' href='../fuchsia.web/index.html#DevToolsListener'>DevToolsListener</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## DevToolsListener {:#DevToolsListener}
*Defined in [fuchsia.web/debug.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/debug.fidl#18)*

 Interface used to observe DevTools service availability events.

### OnContextDevToolsAvailable {:#OnContextDevToolsAvailable}

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
                <code>request&lt;<a class='link' href='../fuchsia.web/index.html#DevToolsPerContextListener'>DevToolsPerContextListener</a>&gt;</code>
            </td>
        </tr></table>



## DevToolsPerContextListener {:#DevToolsPerContextListener}
*Defined in [fuchsia.web/debug.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/debug.fidl#29)*

 Interface supplied by the debugging component to observe the DevTools
 service opening event.

### OnHttpPortOpen {:#OnHttpPortOpen}

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



## Frame {:#Frame}
*Defined in [fuchsia.web/frame.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/frame.fidl#49)*


### CreateView {:#CreateView}

 Creates a new view using the specified `view_token`. Caller should pass
 the other end of the token to CreateViewHolderCmd() to attach the new
 view to a the view tree.

 `view_token`: Token for the new view.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#ViewToken'>ViewToken</a></code>
            </td>
        </tr></table>



### GetMediaSession {:#GetMediaSession}

 Returns a Session interface through which media (i.e. video/audio)
 playback in the frame may be observed, and/or controlled. Only one
 media Session may be active at a time, for each Frame.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>session</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.media.sessions/index.html'>fuchsia.media.sessions</a>/<a class='link' href='../fuchsia.media.sessions/index.html#Session'>Session</a>&gt;</code>
            </td>
        </tr></table>



### GetNavigationController {:#GetNavigationController}

 Returns an interface through which the frame may be navigated to
 a desired URL, reloaded, etc.

 `controller`: An asynchronous interface request for the Frame's
 NavigationController.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>controller</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.web/index.html#NavigationController'>NavigationController</a>&gt;</code>
            </td>
        </tr></table>



### ExecuteJavaScript {:#ExecuteJavaScript}

 Executes a UTF-8 encoded `script` in the frame if the frame's URL has
 an origin which matches entries in `origins`.
 At least one `origins` entry must be specified.
 If a wildcard "*" is specified in `origins`, then the script will be
 evaluated unconditionally.

 Returns the result of executing |script|, as a JSON-encoded string.

 Note that scripts share the same execution context as the document,
 meaning that document may modify variables, classes, or objects set by
 the script in arbitrary or unpredictable ways.

 If an error occured, the FrameError will be set to one of these values:
 BUFFER_NOT_UTF8: `script` is not UTF-8 encoded.
 INVALID_ORIGIN: The Frame's current URL does not match any of the
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
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#Frame_ExecuteJavaScript_Result'>Frame_ExecuteJavaScript_Result</a></code>
            </td>
        </tr></table>

### ExecuteJavaScriptNoResult {:#ExecuteJavaScriptNoResult}

 Variant of ExecuteJavaScript() which executes the supplied script
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
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#Frame_ExecuteJavaScriptNoResult_Result'>Frame_ExecuteJavaScriptNoResult_Result</a></code>
            </td>
        </tr></table>

### AddBeforeLoadJavaScript {:#AddBeforeLoadJavaScript}

 Executes a UTF-8 encoded `script` for every subsequent page load where
 the frame's URL has an origin reflected in `origins`. The script is
 executed early, prior to the execution of the document's scripts.

 Scripts are identified by a client-managed identifier `id`. Any
 script previously injected using the same `id` will be replaced.

 The order in which multiple bindings are executed is the same as the
 order in which the bindings were Added. If a script is added which
 clobbers an existing script of the same `id`, the previous script's
 precedence in the injection order will be preserved.

 At least one `origins` entry must be specified.
 If a wildcard "*" is specified in `origins`, then the script will be
 evaluated for all documents.

 If an error occured, the FrameError will be set to one of these values:
 BUFFER_NOT_UTF8: `script` is not UTF-8 encoded.
 INVALID_ORIGIN: `origins` is an empty vector.

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
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#Frame_AddBeforeLoadJavaScript_Result'>Frame_AddBeforeLoadJavaScript_Result</a></code>
            </td>
        </tr></table>

### RemoveBeforeLoadJavaScript {:#RemoveBeforeLoadJavaScript}

 Removes a previously added JavaScript snippet identified by `id`.
 This is a no-op if there is no JavaScript snippet identified by `id`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### PostMessage {:#PostMessage}

 Posts a message to the frame's onMessage handler.

 `target_origin` restricts message delivery to the specified origin.
 If `target_origin` is "*", then the message will be sent to the
 document regardless of its origin.
 See html.spec.whatwg.org/multipage/web-messaging.html sect. 9.4.3
 for more details on how the target origin policy is applied.

 If an error occured, the FrameError will be set to one of these values:
 INTERNAL_ERROR: The WebEngine failed to create a message pipe.
 BUFFER_NOT_UTF8: The script in `message`'s `data` property is not
                  UTF-8 encoded.
 INVALID_ORIGIN: `origins` is an empty vector.
 NO_DATA_IN_MESSAGE: The `data` property is missing in `message`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>target_origin</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>message</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#WebMessage'>WebMessage</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#Frame_PostMessage_Result'>Frame_PostMessage_Result</a></code>
            </td>
        </tr></table>

### SetNavigationEventListener {:#SetNavigationEventListener}

 Sets the listener for handling page navigation events.

 `listener`: The observer to use. Unregisters any existing listener if
             null.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#NavigationEventListener'>NavigationEventListener</a>?</code>
            </td>
        </tr></table>



### SetJavaScriptLogLevel {:#SetJavaScriptLogLevel}

 If set to a value other than NONE, allows web content to log messages
 to the system logger using the console APIs (debug(), log(), info(),
 warn() and error()).
 When logged to the system logger:
 * debug(), log() and info() logs are logged with LogLevelFilter.INFO
   severity level.
 * warn() logs are logged with LogLevelFilter.WARN severity level.
 * error() logs are logged with LogLevelFilter.ERROR severity level.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>level</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#ConsoleLogLevel'>ConsoleLogLevel</a></code>
            </td>
        </tr></table>



### SetEnableInput {:#SetEnableInput}

 Used at runtime to enable or disable user input processing
 (e.g. keyboard, mouse, touch) on a Frame.
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



### SetAdditionalHeadersProvider {:#SetAdditionalHeadersProvider}

 Sets additional headers on all HTTP requests, except for top-frame
 navigations initiated via LoadUrl(). The callback must be processed
 before the first call to NavigationController.LoadUrl(). The underlying
 channel for `provider` must remain open for the entirety of the Frame
 lifetime.
 Invalid usage will result in closure of the Frame channel with
 ERR_INVALID_ARGS.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>provider</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#AdditionalHeadersProvider'>AdditionalHeadersProvider</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## AdditionalHeadersProvider {:#AdditionalHeadersProvider}
*Defined in [fuchsia.web/frame.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/frame.fidl#180)*


### GetHeaders {:#GetHeaders}

 Returns a set of `headers` to include in network requests. The returned
 `headers` may be cached and applied to further network requests until
 `expiry`. If `expiry` is in the past then `headers` should be used once
 but not cached.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>headers</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.net.http/index.html'>fuchsia.net.http</a>/<a class='link' href='../fuchsia.net.http/index.html#Header'>Header</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>expiry</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>

## MessagePort {:#MessagePort}
*Defined in [fuchsia.web/frame.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/frame.fidl#214)*

 Represents one end of an HTML5 MessageChannel. Can be used to send
 and exchange Messages with the peered MessagePort in the Frame's script
 context. The port is destroyed when either end of the MessagePort channel
 is torn down.

### PostMessage {:#PostMessage}

 Sends a WebMessage to the peer. These are processed in order, one at a
 time. It is not necessary for the caller to wait for the completion
 callback before calling PostMessage() again.

 If an error occured, the FrameError will be set to this value:
 BUFFER_NOT_UTF8: The script in `message`'s `data` property is not
                  UTF-8 encoded.
 NO_DATA_IN_MESSAGE: The `data` property is missing in `message`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>message</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#WebMessage'>WebMessage</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#MessagePort_PostMessage_Result'>MessagePort_PostMessage_Result</a></code>
            </td>
        </tr></table>

### ReceiveMessage {:#ReceiveMessage}

 Asynchronously reads the next message from the channel.
 The client should invoke the callback when it is ready to process
 another message.
 Unreceived messages are buffered on the sender's side and bounded
 by its available resources.

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
                <code><a class='link' href='../fuchsia.web/index.html#WebMessage'>WebMessage</a></code>
            </td>
        </tr></table>

## NavigationEventListener {:#NavigationEventListener}
*Defined in [fuchsia.web/navigation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/navigation.fidl#11)*

 Interface supplied by the embedder for receiving notifications about
 navigation events in a Frame.

### OnNavigationStateChanged {:#OnNavigationStateChanged}

 Called when user-visible navigation state has changed since Frame
 creation or the last acknowledgement callback, whichever occurred last.
 `change` will contain all the differences in navigation state since the
 last acknowledgement. Any unchanged properties will be left unset in
 `change`.
 Implementer must call the acknowledgement callback to receive new
 navigation events.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>change</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#NavigationState'>NavigationState</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## NavigationController {:#NavigationController}
*Defined in [fuchsia.web/navigation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/navigation.fidl#30)*

 Provides methods for controlling and querying the navigation state
 of a Frame.

### LoadUrl {:#LoadUrl}

 Tells the Frame to navigate to a `url`.

 `url`:    The address to navigate to.
 `params`: Additional parameters that affect how the resource will be
           loaded (e.g. cookies, HTTP headers, etc.)

 If an error occured, the NavigationControllerError will be set:
 INVALID_URL: The `url` parameter is invalid.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>url</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>params</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#LoadUrlParams'>LoadUrlParams</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#NavigationController_LoadUrl_Result'>NavigationController_LoadUrl_Result</a></code>
            </td>
        </tr></table>

### GoBack {:#GoBack}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### GoForward {:#GoForward}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Stop {:#Stop}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Reload {:#Reload}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#ReloadType'>ReloadType</a></code>
            </td>
        </tr></table>



### GetVisibleEntry {:#GetVisibleEntry}

 Returns information for the currently visible content regardless of
 loading state, or an empty entry if no content is being displayed.

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
                <code><a class='link' href='../fuchsia.web/index.html#NavigationState'>NavigationState</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Context_GetRemoteDebuggingPort_Response {:#Context_GetRemoteDebuggingPort_Response}
*Defined in [fuchsia.web/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#5)*





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

### Frame_ExecuteJavaScript_Response {:#Frame_ExecuteJavaScript_Response}
*Defined in [fuchsia.web/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#24)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Frame_ExecuteJavaScriptNoResult_Response {:#Frame_ExecuteJavaScriptNoResult_Response}
*Defined in [fuchsia.web/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#31)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Frame_AddBeforeLoadJavaScript_Response {:#Frame_AddBeforeLoadJavaScript_Response}
*Defined in [fuchsia.web/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#38)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Frame_PostMessage_Response {:#Frame_PostMessage_Response}
*Defined in [fuchsia.web/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#46)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### MessagePort_PostMessage_Response {:#MessagePort_PostMessage_Response}
*Defined in [fuchsia.web/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#60)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### NavigationController_LoadUrl_Response {:#NavigationController_LoadUrl_Response}
*Defined in [fuchsia.web/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#71)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>



## **ENUMS**

### ContextError {:#ContextError}
Type: <code>int32</code>

*Defined in [fuchsia.web/context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/context.fidl#9)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>REMOTE_DEBUGGING_PORT_NOT_OPENED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### CookieChangeType {:#CookieChangeType}
Type: <code>uint32</code>

*Defined in [fuchsia.web/cookie.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/cookie.fidl#57)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ADDED</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>MODIFIED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>DELETED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### ConsoleLogLevel {:#ConsoleLogLevel}
Type: <code>int32</code>

*Defined in [fuchsia.web/frame.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/frame.fidl#16)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NONE</code></td>
            <td><code>100</code></td>
            <td></td>
        </tr><tr>
            <td><code>DEBUG</code></td>
            <td><code>-1</code></td>
            <td></td>
        </tr><tr>
            <td><code>INFO</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>WARN</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERROR</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### FrameError {:#FrameError}
Type: <code>int32</code>

*Defined in [fuchsia.web/frame.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/frame.fidl#34)*

 Represents the return status of a Frame method.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INTERNAL_ERROR</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>BUFFER_NOT_UTF8</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVALID_ORIGIN</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>NO_DATA_IN_MESSAGE</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr></table>

### NavigationControllerError {:#NavigationControllerError}
Type: <code>int32</code>

*Defined in [fuchsia.web/navigation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/navigation.fidl#23)*

 Represents the return status of a NavigationController method.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INVALID_URL</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### ReloadType {:#ReloadType}
Type: <code>uint32</code>

*Defined in [fuchsia.web/navigation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/navigation.fidl#96)*

 Characterizes the type of reload.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>PARTIAL_CACHE</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>NO_CACHE</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### LoadUrlReason {:#LoadUrlReason}
Type: <code>uint32</code>

*Defined in [fuchsia.web/navigation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/navigation.fidl#105)*

 Characterizes the origin of a LoadUrl request.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>LINK</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>TYPED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### PageType {:#PageType}
Type: <code>uint32</code>

*Defined in [fuchsia.web/navigation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/navigation.fidl#114)*

 Characterizes the page type in a NavigationState.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NORMAL</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERROR</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### CreateContextParams {:#CreateContextParams}


*Defined in [fuchsia.web/context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/context.fidl#28)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>service_directory</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io/index.html'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/index.html#Directory'>Directory</a></code>
            </td>
            <td> Service directory to be used by the context.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>data_directory</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io/index.html'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/index.html#Directory'>Directory</a></code>
            </td>
            <td> Handle to the directory that will contain the Context's
 persistent data. If it is left unset, then the created Context will be
 stateless, with all of its data discarded upon Context destruction.
 If set, `data_directory` must not be shared with any other Context.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>user_agent_product</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Optional suffix to append to the UserAgent string, to describe the
 embedder's product & version. See the User-Agent HTTP header
 specification at https://tools.ietf.org/html/rfc7231#section-5.5.3
</td>
        </tr><tr>
            <td>4</td>
            <td><code>user_agent_version</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>remote_debugging_port</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td> Port to be used for remote debugging for connection via the DevTools
 protocol. Setting this to 0 will make the Context use an ephemeral
 port, which can be then queried via the
 Context.GetRemoteDebuggingPort() API.
 This is only for testing purposes and should not be set in production
 code.
</td>
        </tr></table>

### CookieId {:#CookieId}


*Defined in [fuchsia.web/cookie.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/cookie.fidl#38)*



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

### Cookie {:#Cookie}


*Defined in [fuchsia.web/cookie.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/cookie.fidl#49)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#CookieId'>CookieId</a></code>
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

### CookieChangeEvent {:#CookieChangeEvent}


*Defined in [fuchsia.web/cookie.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/cookie.fidl#63)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#CookieId'>CookieId</a></code>
            </td>
            <td> The identity of the cookie which was changed.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#CookieChangeType'>CookieChangeType</a></code>
            </td>
            <td> Describes what type of change caused the CookieChangeEvent to be
 published.
</td>
        </tr></table>

### WebMessage {:#WebMessage}


*Defined in [fuchsia.web/frame.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/frame.fidl#188)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
            <td> The message payload, encoded as an UTF-8 string. This is a required
 property.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>incoming_transfer</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.web/index.html#IncomingTransferable'>IncomingTransferable</a>&gt;</code>
            </td>
            <td> Optional list of objects transferred into the MessagePort from the FIDL
 client.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>outgoing_transfer</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.web/index.html#OutgoingTransferable'>OutgoingTransferable</a>&gt;</code>
            </td>
            <td> Optional list of objects transferred out of the MessagePort to the FIDL
 client.
</td>
        </tr></table>

### LoadUrlParams {:#LoadUrlParams}


*Defined in [fuchsia.web/navigation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/navigation.fidl#56)*

 Additional parameters for modifying the behavior of LoadUrl().


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#LoadUrlReason'>LoadUrlReason</a></code>
            </td>
            <td> Provides a hint to the browser UI about how LoadUrl was triggered.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>referrer_url</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The URL that linked to the resource being requested.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>was_user_activated</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Should be set to true to propagate user activation to the frame. User
 activation implies that the user is interacting with the web frame. It
 enables some web features that are not available otherwise. For example
 autoplay will work only when this flag is set to true.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>headers</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.net.http/index.html'>fuchsia.net.http</a>/<a class='link' href='../fuchsia.net.http/index.html#Header'>Header</a>&gt;</code>
            </td>
            <td> Custom HTTP headers.
</td>
        </tr></table>

### NavigationState {:#NavigationState}


*Defined in [fuchsia.web/navigation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/navigation.fidl#74)*

 Contains information about the Frame's navigation state.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>url</code></td>
            <td>
                <code>string</code>
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
                <code><a class='link' href='../fuchsia.web/index.html#PageType'>PageType</a></code>
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
            <td> Indicates that the main document's statically declared resources have
 been loaded.
</td>
        </tr></table>



## **UNIONS**

### Context_GetRemoteDebuggingPort_Result {:#Context_GetRemoteDebuggingPort_Result}
*Defined in [fuchsia.web/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#8)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#Context_GetRemoteDebuggingPort_Response'>Context_GetRemoteDebuggingPort_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#ContextError'>ContextError</a></code>
            </td>
            <td></td>
        </tr></table>

### Frame_ExecuteJavaScript_Result {:#Frame_ExecuteJavaScript_Result}
*Defined in [fuchsia.web/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#27)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#Frame_ExecuteJavaScript_Response'>Frame_ExecuteJavaScript_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#FrameError'>FrameError</a></code>
            </td>
            <td></td>
        </tr></table>

### Frame_ExecuteJavaScriptNoResult_Result {:#Frame_ExecuteJavaScriptNoResult_Result}
*Defined in [fuchsia.web/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#34)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#Frame_ExecuteJavaScriptNoResult_Response'>Frame_ExecuteJavaScriptNoResult_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#FrameError'>FrameError</a></code>
            </td>
            <td></td>
        </tr></table>

### Frame_AddBeforeLoadJavaScript_Result {:#Frame_AddBeforeLoadJavaScript_Result}
*Defined in [fuchsia.web/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#41)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#Frame_AddBeforeLoadJavaScript_Response'>Frame_AddBeforeLoadJavaScript_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#FrameError'>FrameError</a></code>
            </td>
            <td></td>
        </tr></table>

### Frame_PostMessage_Result {:#Frame_PostMessage_Result}
*Defined in [fuchsia.web/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#49)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#Frame_PostMessage_Response'>Frame_PostMessage_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#FrameError'>FrameError</a></code>
            </td>
            <td></td>
        </tr></table>

### MessagePort_PostMessage_Result {:#MessagePort_PostMessage_Result}
*Defined in [fuchsia.web/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#63)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#MessagePort_PostMessage_Response'>MessagePort_PostMessage_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#FrameError'>FrameError</a></code>
            </td>
            <td></td>
        </tr></table>

### NavigationController_LoadUrl_Result {:#NavigationController_LoadUrl_Result}
*Defined in [fuchsia.web/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#74)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#NavigationController_LoadUrl_Response'>NavigationController_LoadUrl_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#NavigationControllerError'>NavigationControllerError</a></code>
            </td>
            <td></td>
        </tr></table>



## **XUNIONS**

### OutgoingTransferable {:#OutgoingTransferable}
*Defined in [fuchsia.web/frame.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/frame.fidl#202)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>message_port</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.web/index.html#MessagePort'>MessagePort</a>&gt;</code>
            </td>
            <td></td>
        </tr></table>

### IncomingTransferable {:#IncomingTransferable}
*Defined in [fuchsia.web/frame.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.web/frame.fidl#206)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>message_port</code></td>
            <td>
                <code><a class='link' href='../fuchsia.web/index.html#MessagePort'>MessagePort</a></code>
            </td>
            <td></td>
        </tr></table>





