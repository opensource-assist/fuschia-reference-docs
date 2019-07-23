Project: /_project.yaml
Book: /_book.yaml

# fuchsia.app.sessioncontrol


## **PROTOCOLS**

## SessionController {:#SessionController}
*Defined in [fuchsia.app.sessioncontrol/session_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.sessioncontrol/session_controller.fidl#14)*

 Sessions contain a model describing the set of stories and modules contained within.
 SessionController allows clients to mutate and observe the session's model. Observed changes
 may originate from other local clients, or from the same session running on a different device.

### GetStoryController {:#GetStoryController}

 Requests a story controller for the story identified by `id`. `id` may be any
 client-supplied value. A previously unused `id`, or one identifying a story that has been
 deleted (using DeleteStory()) will create a new story record.

 `id`s are scoped to the requesting client's Component URL: two different clients
 which use the same `id` will be controlling different story instances.

 In some system configurations, the results of mutating a story's state are durable across
 reboots and devices.

 `request` is closed if control cannot be granted, or when DeleteStory() is called for the
 same `id` on any device.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>string[1024]</code>
            </td>
        </tr><tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.app.sessioncontrol/index.html#StoryController'>StoryController</a>&gt;</code>
            </td>
        </tr></table>



### DeleteStory {:#DeleteStory}

 Permanently deletes the story identified by `id`. Any StoryControllers
 obtained through GetStoryController() will be closed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>string[1024]</code>
            </td>
        </tr></table>



### WatchStories {:#WatchStories}

 Immediately returns the list of existing stories on the first call. On
 subsequent calls, waits and returns the list of stories only once the
 list has changed.

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
                <code>vector&lt;<a class='link' href='../fuchsia.app.sessioncontrol/index.html#StoryInfo'>StoryInfo</a>&gt;</code>
            </td>
        </tr></table>

## StoryController {:#StoryController}
*Defined in [fuchsia.app.sessioncontrol/story_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.sessioncontrol/story_controller.fidl#35)*

 Allows clients to alter the model of the story for a specific story. Acquired through
 SessionController/ObtainStoryController().

 Not all method calls are guaranteed to result in equivalent and observable side-effects due to
 the potential for cross-device conflict resolution to alter the committed session model prior
 to observation of that model's new state.

 Any invalid calls to methods on StoryController result in the StoryController channel closing
 with ZX_ERR_INVALID_ARGS.

### AddModule {:#AddModule}

 Assigns the module identified by `id` to handle `intent`. Modules within a story are
 a set: calling AddModule() with the same `id` updates the module in place, while calling
 with new `id` results in a brand new module. Callers wishing to add a new module on every
 call should assign a GUID for `id`.

 `intent` describes both the module to add, either explicitly through `intent.handler` or
 indirectly through `intent.action`, as well as the module's input model. The latest
 `intent` is always delivered to modules through their fuchsia.app.module.IntentHandler
 service, either during the module's initialization or during its execution, depending on
 the lifecycle state of the module.

 At least one of `intent.handler` or `intent.action` are required.  `composition`, if not
 provided, uses the default (`composition.arrangement` is set to SurfaceArrangement.NONE).

 Returns Error.ERR_NO_MODULE_FOUND on error.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>string[1024]</code>
            </td>
        </tr><tr>
            <td><code>intent</code></td>
            <td>
                <code><a class='link' href='../fuchsia.app/index.html'>fuchsia.app</a>/<a class='link' href='../fuchsia.app/index.html#Intent'>Intent</a></code>
            </td>
        </tr><tr>
            <td><code>composition</code></td>
            <td>
                <code><a class='link' href='../fuchsia.app.sessioncontrol/index.html#ModuleCompositionSettings'>ModuleCompositionSettings</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='../fuchsia.app.sessioncontrol/index.html#StoryController_AddModule_Result'>StoryController_AddModule_Result</a></code>
            </td>
        </tr></table>

### RemoveModule {:#RemoveModule}

 Permanently removes the module identified by `id`. Calling for a module that doesn't exist,
 or was already removed either by this agent or by an agent on another device, is a no-op.

 Returns Error.ERR_MODULE_ID_NOT_FOUND on error.

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
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='../fuchsia.app.sessioncontrol/index.html#StoryController_RemoveModule_Result'>StoryController_RemoveModule_Result</a></code>
            </td>
        </tr></table>

### FocusModule {:#FocusModule}

 Instructs the story shell to bring this module into focus. Calling for a non-existent
 module is a no-op.

 Returns Error.ERR_MODULE_ID_NOT_FOUND on error.

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
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='../fuchsia.app.sessioncontrol/index.html#StoryController_FocusModule_Result'>StoryController_FocusModule_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### StoryController_AddModule_Response {:#StoryController_AddModule_Response}
*Defined in [fuchsia.app.sessioncontrol/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#6)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### StoryController_RemoveModule_Response {:#StoryController_RemoveModule_Response}
*Defined in [fuchsia.app.sessioncontrol/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#13)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### StoryController_FocusModule_Response {:#StoryController_FocusModule_Response}
*Defined in [fuchsia.app.sessioncontrol/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#20)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>



## **ENUMS**

### Error {:#Error}
Type: <code>uint32</code>

*Defined in [fuchsia.app.sessioncontrol/story_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.sessioncontrol/story_controller.fidl#17)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ERR_NO_MODULE_FOUND</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERR_MODULE_ID_NOT_FOUND</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### StoryInfo {:#StoryInfo}


*Defined in [fuchsia.app.sessioncontrol/session_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.sessioncontrol/session_controller.fidl#42)*

 Metadata about a single Story.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>id</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td> The ID of the story as supplied to SessionController/GetStoryController().
</td>
        </tr><tr>
            <td>2</td>
            <td><code>is_focused</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> True if the story is currently focused on this device.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>last_focus_time</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> The timestamp at which this story was most recently focused across all
 devices. If unset, the story has never been focused.
</td>
        </tr></table>

### ModuleCompositionSettings {:#ModuleCompositionSettings}


*Defined in [fuchsia.app.sessioncontrol/story_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.sessioncontrol/story_controller.fidl#70)*

 Describes preferences to the story shell for how a module's UI should be laid out relative to
 other modules in the same story.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>placeholder</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>relative_to</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td> Specifies the module relative to which the instruction in `relation` applies. `relative_to`
 must identify a module previously added through calls to StoryController/AddModule()
 and not since removed.
</td>
        </tr></table>



## **UNIONS**

### StoryController_AddModule_Result {:#StoryController_AddModule_Result}
*Defined in [fuchsia.app.sessioncontrol/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#9)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.app.sessioncontrol/index.html#StoryController_AddModule_Response'>StoryController_AddModule_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.app.sessioncontrol/index.html#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### StoryController_RemoveModule_Result {:#StoryController_RemoveModule_Result}
*Defined in [fuchsia.app.sessioncontrol/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#16)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.app.sessioncontrol/index.html#StoryController_RemoveModule_Response'>StoryController_RemoveModule_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.app.sessioncontrol/index.html#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### StoryController_FocusModule_Result {:#StoryController_FocusModule_Result}
*Defined in [fuchsia.app.sessioncontrol/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#23)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.app.sessioncontrol/index.html#StoryController_FocusModule_Response'>StoryController_FocusModule_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.app.sessioncontrol/index.html#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.sessioncontrol/story_controller.fidl#15">MODULE_ID_MAX_LENGTH</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    
</table>

