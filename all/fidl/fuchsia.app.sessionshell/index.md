Project: /_project.yaml
Book: /_book.yaml

# fuchsia.app.sessionshell


## **PROTOCOLS**

## Context {:#Context}
*Defined in [fuchsia.app.sessionshell/context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.sessionshell/context.fidl#14)*

 An instance of this service is exposed to session shells in their namespace.
 It exposes the base capabilities offered by modular to session shells.

 See also: fuchsia.app.SessionShell

### ConnectToAgent {:#ConnectToAgent}

 Obtains a fuchsia.io.Directory of services from the agent specified in `request.handler`.
 Services are bound to `request.services`. The agent endpoint may close `request.services`
 at its discretion, at which point `request.controller` must be closed by the caller.

 If brokering a connection is successful, keeping `request.controller` open will ensure
 that the agent endpoint is not terminated.

 Failure to provide all required fields in `request` will close the
 Context channel with an ZX_ERR_INVALID_ARGS.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code><a class='link' href='../fuchsia.app/index.html'>fuchsia.app</a>/<a class='link' href='../fuchsia.app/index.html#AgentConnectionRequest'>AgentConnectionRequest</a></code>
            </td>
        </tr></table>



### FocusStory {:#FocusStory}

 Focuses the story given the `id`. The shell can expect:
   * The story's runtime state to transition to RUNNING, observable
     through SessionObserver/WatchStories().
   * The story's `StoryInfo.last_focus_time` to increase.
   * A future call to SessionShell/AttachView(), if there is not already
     a view attached.

 Modular priotizes runtime resources for the focused story.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>string[1024]</code>
            </td>
        </tr></table>



### SetPrioritizedStories {:#SetPrioritizedStories}

 Sets the prioritized stories.  `ids` should include those stories that
 the shell wishes to remain interactive such as ambient UI elements or
 other stories that do not classify as focused but remain important.

 The list is used to prioritize runtime resources.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ids</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr></table>



### TeardownSession {:#TeardownSession}

 Tears down the session. The SessionController channel will close
 immediately.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### WatchStories {:#WatchStories}

 Returns the list of existing stories.  Subsequent calls will wait until
 the list has changed to return.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>stories</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.app.sessionshell/index.html#StorySummary'>StorySummary</a>&gt;</code>
            </td>
        </tr></table>

### WatchOngoingActivities {:#WatchOngoingActivities}

 Immediately returns the list of ongoing activities in the session on the
 first call. On subsequent calls, waits and returns a new list only once
 the list has changed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ongoing_activies</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.app.sessionshell/index.html#OngoingActivityInfo'>OngoingActivityInfo</a>&gt;</code>
            </td>
        </tr></table>

## SessionController {:#SessionController}
*Defined in [fuchsia.app.sessionshell/session_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.sessionshell/session_controller.fidl#11)*

 Allows clients to make changes to the session.

### FocusStory {:#FocusStory}

 Focuses the story given the `id`. The shell can expect:
   * The story's runtime state to transition to RUNNING, observable
     through SessionObserver/WatchStories().
   * The story's `StoryInfo.last_focus_time` to increase.
   * A future call to SessionShell/AttachView(), if there is not already
     a view attached.

 Modular priotizes runtime resources for the focused story.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>string[1024]</code>
            </td>
        </tr></table>



### SetPrioritizedStories {:#SetPrioritizedStories}

 Sets the prioritized stories.  `ids` should include those stories that
 the shell wishes to remain interactive such as ambient UI elements or
 other stories that do not classify as focused but remain important.

 The list is used to prioritize runtime resources.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ids</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr></table>



### TeardownSession {:#TeardownSession}

 Tears down the session. The SessionController channel will close
 immediately.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## SessionObserver {:#SessionObserver}
*Defined in [fuchsia.app.sessionshell/session_observer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.sessionshell/session_observer.fidl#12)*

 Allows clients to observe changes in the session.

### WatchStories {:#WatchStories}

 Returns the list of existing stories.  Subsequent calls will wait until
 the list has changed to return.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>stories</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.app.sessionshell/index.html#StorySummary'>StorySummary</a>&gt;</code>
            </td>
        </tr></table>

### WatchOngoingActivities {:#WatchOngoingActivities}

 Immediately returns the list of ongoing activities in the session on the
 first call. On subsequent calls, waits and returns a new list only once
 the list has changed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ongoing_activies</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.app.sessionshell/index.html#OngoingActivityInfo'>OngoingActivityInfo</a>&gt;</code>
            </td>
        </tr></table>

## SessionShell {:#SessionShell}
*Defined in [fuchsia.app.sessionshell/session_shell.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.sessionshell/session_shell.fidl#14)*


### AttachView {:#AttachView}

 Attaches `view_holder_token` as the view for `story_id`. Session
 shells are expected to compose the view into the session UI. Metadata
 about the story are available through SessionObserver/WatchStories() for the same
 StoryId.

 It is customary for the session shell to display a placeholder before a
 the first call to AttachView() for a given view_id.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_id</code></td>
            <td>
                <code>string[1024]</code>
            </td>
        </tr><tr>
            <td><code>view_holder_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#ViewHolderToken'>ViewHolderToken</a></code>
            </td>
        </tr></table>



### DetachView {:#DetachView}

 Instructs the session shell to detach from the shell UI the view
 for `story_id`.  The view will be closed soon after
 DetachView() returns, or after a timeout is reached.

 If the story identified by `story_id` is being deleted, the
 shell will observe the story's removal in a future call to
 SessionObserver/WatchStories().

 If the session for which this session shell is responsible for is being
 terminated, the shell should expect to be terminated without observing
 individual calls to DetachView() for each story.

 It is customary for the session shell to display a placeholder after a
 call to DetachView().

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_id</code></td>
            <td>
                <code>string[1024]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### HandleFocusStoryRequest {:#HandleFocusStoryRequest}

 Instructs the shell that another client (such as a session controller)
 is requesting a specific story be brought into focus. The shell should
 return true if it will honor the request and false otherwise.

 Returning true has the same behavior as returning false and calling
 SessionController/FocusStory(id).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>string[1024]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>did_focus</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>





## **ENUMS**

### StoryVisibilityMode {:#StoryVisibilityMode}
Type: <code>uint32</code>

*Defined in [fuchsia.app.sessionshell/session_observer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.sessionshell/session_observer.fidl#59)*

 Describes how a story should be displayed, when focused, within the session
 shell.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DEFAULT</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>IMMERSIVE</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### StoryRuntimeState {:#StoryRuntimeState}
Type: <code>uint32</code>

*Defined in [fuchsia.app.sessionshell/session_observer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.sessionshell/session_observer.fidl#82)*

 State of a Story. A story is either running, stopping, or stopped,
 separately on every device of the user. If it's running, it can also be
 focused, but that's tracked in a separate service, cf. FocusProvider in
 focus.fidl.

 State transitions are:
   STOPPED -> RUNNING -> STOPPING -> STOPPED


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>RUNNING</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>STOPPING</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>STOPPED</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### StorySummary {:#StorySummary}


*Defined in [fuchsia.app.sessionshell/session_observer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.sessionshell/session_observer.fidl#24)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>id</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td> The ID, unique to the session and assigned by the framework, for this story.

 NOTE: the value of `id` is different from that provided by session
 controllers through fuchsia.app.sessioncontrol.SessionController.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>runtime_state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.app.sessionshell/index.html#StoryRuntimeState'>StoryRuntimeState</a></code>
            </td>
            <td> Contains the latest runtime state for this story. Shells may opt to use
 this state to, e.g., dim a story's UI while it is not running.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>display_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.app.sessionshell/index.html#StoryDisplayInfo'>StoryDisplayInfo</a></code>
            </td>
            <td> Informs the session shell how to display this story when on screen. See
 StoryDisplayInfo below for details.

 The value can change at any time. Shells are expected to update the
 story's UI accordingly.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>last_focus_time</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> The last time this story was the foreground story in any session shell
 across all devices.
 Updated after a session shell calls SessionController/FocusedStory().
</td>
        </tr></table>

### StoryDisplayInfo {:#StoryDisplayInfo}


*Defined in [fuchsia.app.sessionshell/session_observer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.sessionshell/session_observer.fidl#51)*

 Describes how a story should be displayed within the session
 shell when the story is being displayed on screen. Session shells are
 expected to honor the semantics of this struct.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>mode</code></td>
            <td>
                <code><a class='link' href='../fuchsia.app.sessionshell/index.html#StoryVisibilityMode'>StoryVisibilityMode</a></code>
            </td>
            <td> The expected display mode for the story within the shell. See
 StoryVisibilityMode docs for details.
</td>
        </tr></table>

### OngoingActivityInfo {:#OngoingActivityInfo}


*Defined in [fuchsia.app.sessionshell/session_observer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.sessionshell/session_observer.fidl#69)*

 Information about a single ongoing activity within a story.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>id</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='../fuchsia.app/index.html'>fuchsia.app</a>/<a class='link' href='../fuchsia.app/index.html#OngoingActivityType'>OngoingActivityType</a></code>
            </td>
            <td></td>
        </tr></table>









