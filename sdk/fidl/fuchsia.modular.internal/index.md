Project: /_project.yaml
Book: /_book.yaml

# fuchsia.modular.internal


## **PROTOCOLS**

## BasemgrDebug {:#BasemgrDebug}
*Defined in [fuchsia.modular.internal/basemgr_debug.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.internal/basemgr_debug.fidl#10)*

 A debug interface exposed by `basemgr` to allow developer tools to control
 state within the `basemgr` process.

### RestartSession {:#RestartSession}

 Restarts the current session. If a user was logged in, this will return
 when the same user is logged back in. Otherwise, this will return when
 sessionmgr has been torn down.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### SelectNextSessionShell {:#SelectNextSessionShell}

 Toggles to the next session defined in the basemgr.config file.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### LoginAsGuest {:#LoginAsGuest}

 Logs in as a guest user.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## Sessionmgr {:#Sessionmgr}
*Defined in [fuchsia.modular.internal/sessionmgr.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.internal/sessionmgr.fidl#16)*

 The basemgr application (there is no `Basemgr` service) requests
 an instance of this service in order to launch and display a `Sessionmgr`.

### Initialize {:#Initialize}

 Launches a sessionmgr instance identified by a unique device-local
 `session_id`. The uniqueness of `session_id` must be guaranteed by the
 caller, because `sessionmgr` creates an Environment namespace with the
 given `session_id`, and this will crash if we try to create an
 environment with a pre-existing name, because the services sessionmgr
 tries to access won't be available.


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
                <code><a class='link' href='../fuchsia.modular.auth/index.html'>fuchsia.modular.auth</a>/<a class='link' href='../fuchsia.modular.auth/index.html#Account'>Account</a>?</code>
            </td>
        </tr><tr>
            <td><code>session_shell</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/index.html#AppConfig'>AppConfig</a></code>
            </td>
        </tr><tr>
            <td><code>story_shell</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/index.html#AppConfig'>AppConfig</a></code>
            </td>
        </tr><tr>
            <td><code>use_session_shell_for_story_shell_factory</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>ledger_token_manager</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/index.html'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/index.html#TokenManager'>TokenManager</a>?</code>
            </td>
        </tr><tr>
            <td><code>agent_token_manager</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/index.html'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/index.html#TokenManager'>TokenManager</a>?</code>
            </td>
        </tr><tr>
            <td><code>session_context</code></td>
            <td>
                <code><a class='link' href='#SessionContext'>SessionContext</a></code>
            </td>
        </tr><tr>
            <td><code>view_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#ViewToken'>ViewToken</a></code>
            </td>
        </tr></table>



### SwapSessionShell {:#SwapSessionShell}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>session_shell</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/index.html#AppConfig'>AppConfig</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## SessionContext {:#SessionContext}
*Defined in [fuchsia.modular.internal/sessionmgr.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.internal/sessionmgr.fidl#40)*

 This interface is provided by basemgr to `Sessionmgr`.

### Logout {:#Logout}

 See detailed comments in SessionShellContext.Logout(). Logs out all the
 users in this session, then shut down the sessionmgr process.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Shutdown {:#Shutdown}

 Shut down the sessionmgr process. This method should be called if the
 users of the session should remain logged in. Call Logout() if the intent
 is to also log out the users from the session.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### GetPresentation {:#GetPresentation}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>presentation</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.ui.policy/index.html'>fuchsia.ui.policy</a>/<a class='link' href='../fuchsia.ui.policy/index.html#Presentation'>Presentation</a>&gt;</code>
            </td>
        </tr></table>









## **TABLES**

### StoryData {:#StoryData}


*Defined in [fuchsia.modular.internal/story_data.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.internal/story_data.fidl#12)*

 Metadata and summary information about a single story.  Does not contain the
 data necessary to run a story: see story_model.fidl for that.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>story_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/index.html#StoryInfo'>StoryInfo</a></code>
            </td>
            <td> Metadata available to the SessionShell.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>story_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td> A client-supplied name for this story.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>story_options</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/index.html#StoryOptions'>StoryOptions</a></code>
            </td>
            <td> Story metadata and configuration.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>story_page_id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ledger/index.html'>fuchsia.ledger</a>/<a class='link' href='../fuchsia.ledger/index.html#PageId'>PageId</a></code>
            </td>
            <td> Page id on the user's ledger which stores story information.
</td>
        </tr></table>









