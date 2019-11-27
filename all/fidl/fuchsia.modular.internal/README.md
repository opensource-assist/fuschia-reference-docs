[TOC]

# fuchsia.modular.internal


## **PROTOCOLS**

## BasemgrDebug {#BasemgrDebug}
*Defined in [fuchsia.modular.internal/basemgr_debug.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.internal/basemgr_debug.fidl#10)*

<p>A debug interface exposed by <code>basemgr</code> to allow developer tools to control
state within the <code>basemgr</code> process.</p>

### RestartSession {#RestartSession}

<p>Restarts the current session. If a user was logged in, this will return
when the same user is logged back in. Otherwise, this will return when
sessionmgr has been torn down.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### SelectNextSessionShell {#SelectNextSessionShell}

<p>Toggles to the next session defined in the basemgr.config file.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### LoginAsGuest {#LoginAsGuest}

<p>Logs in as a guest user.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Shutdown {#Shutdown}

<p>Kills the running instance of basemgr.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## Sessionmgr {#Sessionmgr}
*Defined in [fuchsia.modular.internal/sessionmgr.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.internal/sessionmgr.fidl#16)*

<p>The basemgr application (there is no <code>Basemgr</code> service) requests
an instance of this service in order to launch and display a <code>Sessionmgr</code>.</p>

### Initialize {#Initialize}

<p>Launches a sessionmgr instance identified by a unique device-local
<code>session_id</code>. The uniqueness of <code>session_id</code> must be guaranteed by the
caller, because <code>sessionmgr</code> creates an Environment namespace with the
given <code>session_id</code>, and this will crash if we try to create an
environment with a pre-existing name, because the services sessionmgr
tries to access won't be available.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>session_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>account</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular.auth/'>fuchsia.modular.auth</a>/<a class='link' href='../fuchsia.modular.auth/#Account'>Account</a>?</code>
            </td>
        </tr><tr>
            <td><code>session_shell</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/#AppConfig'>AppConfig</a></code>
            </td>
        </tr><tr>
            <td><code>story_shell</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/#AppConfig'>AppConfig</a></code>
            </td>
        </tr><tr>
            <td><code>use_session_shell_for_story_shell_factory</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>agent_token_manager</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/#TokenManager'>TokenManager</a>?</code>
            </td>
        </tr><tr>
            <td><code>session_context</code></td>
            <td>
                <code><a class='link' href='#SessionContext'>SessionContext</a></code>
            </td>
        </tr><tr>
            <td><code>view_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/#ViewToken'>ViewToken</a></code>
            </td>
        </tr></table>



### SwapSessionShell {#SwapSessionShell}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>session_shell</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/#AppConfig'>AppConfig</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## SessionContext {#SessionContext}
*Defined in [fuchsia.modular.internal/sessionmgr.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.internal/sessionmgr.fidl#39)*

<p>This interface is provided by basemgr to <code>Sessionmgr</code>.</p>

### Logout {#Logout}

<p>See detailed comments in SessionShellContext.Logout(). Logs out all the
users in this session, then shut down the sessionmgr process.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Restart {#Restart}

<p>Restarts the session without logging out the users of the session.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Shutdown {#Shutdown}

<p>Shut down the sessionmgr process. This method should be called if the
users of the session should remain logged in. Call Logout() if the intent
is to also log out the users from the session.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### GetPresentation {#GetPresentation}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>presentation</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.ui.policy/'>fuchsia.ui.policy</a>/<a class='link' href='../fuchsia.ui.policy/#Presentation'>Presentation</a>&gt;</code>
            </td>
        </tr></table>









## **TABLES**

### StoryData {#StoryData}


*Defined in [fuchsia.modular.internal/story_data.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.internal/story_data.fidl#12)*

<p>Metadata and summary information about a single story.  Does not contain the
data necessary to run a story: see story_model.fidl for that.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>story_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/#StoryInfo2'>StoryInfo2</a></code>
            </td>
            <td><p>Metadata available to the SessionShell.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>story_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>A client-supplied name for this story.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>story_options</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/#StoryOptions'>StoryOptions</a></code>
            </td>
            <td><p>Story metadata and configuration.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>story_page_id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ledger/'>fuchsia.ledger</a>/<a class='link' href='../fuchsia.ledger/#PageId'>PageId</a></code>
            </td>
            <td><p>Page id on the user's ledger which stores story information.</p>
</td>
        </tr></table>









