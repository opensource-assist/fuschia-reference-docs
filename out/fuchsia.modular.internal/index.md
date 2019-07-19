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


### Initialize {:#Initialize}


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
                <code><a class='link' href='../fuchsia.modular.internal/index.html#SessionContext'>SessionContext</a></code>
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


### Logout {:#Logout}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Shutdown {:#Shutdown}


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



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>story_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/index.html#StoryInfo'>StoryInfo</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>story_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>story_options</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/index.html#StoryOptions'>StoryOptions</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>story_page_id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ledger/index.html'>fuchsia.ledger</a>/<a class='link' href='../fuchsia.ledger/index.html#PageId'>PageId</a></code>
            </td>
            <td></td>
        </tr></table>









