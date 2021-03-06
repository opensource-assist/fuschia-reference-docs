[TOC]

# fuchsia.modular.storymodel








## **TABLES**

### StoryModel {#StoryModel}


*Defined in [fuchsia.modular.storymodel/story_model.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.storymodel/story_model.fidl#14)*

<p>IMPORTANT: StoryModel must only contain field types that are cloneable.</p>
<p>The <code>StoryModel</code> FIDL table is used to represent the state of a story.
<code>sessionmgr</code> keeps a separate <code>StoryModel</code> in memory for each running story,
and also persists changes to it onto storage.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>The name of the story, set at story create time.</p>
<p>Always set. Immutable.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>runtime_state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/#StoryState'>StoryState</a></code>
            </td>
            <td><p>An enum describing if the story is RUNNING, STOPPING, STOPPED.</p>
<p>Always set. Defaults to StoryState::STOPPED.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>visibility_state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/#StoryVisibilityState'>StoryVisibilityState</a></code>
            </td>
            <td><p>An enum describing how the story should be displayed, when focused,
in the StoryShell.</p>
<p>Always set. Defaults to StoryVisibilityState::DEFAULT.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>modules</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ModuleModel'>ModuleModel</a>&gt;[128]</code>
            </td>
            <td><p>A list of modules present in the story.</p>
<p>Always set. Defaults to an empty list.</p>
</td>
        </tr></table>

### ModuleModel {#ModuleModel}


*Defined in [fuchsia.modular.storymodel/story_model.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.storymodel/story_model.fidl#37)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>The name of the module, set by the client that requested creation
of the module. The name uniquely identifies this module within
the story.</p>
<p>Always set. Immutable.</p>
</td>
        </tr></table>



## **UNIONS**

### StoryModelMutation {#StoryModelMutation}
*Defined in [fuchsia.modular.storymodel/story_model_mutation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.storymodel/story_model_mutation.fidl#16)*

<p>The <code>StoryModelMutation</code> union represents the set of all possible low-level mutations to data
for a single story. A vector of mutations represent mutations that are to be applied to the
model in a single transaction.</p>
<p>This structured is used internally in <code>sessionmgr</code> and is not exposed to any clients outside
that process. Clients will typically construct these indirectly using convenience methods on the
<code>StoryMutator</code> class.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>set_visibility_state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/#StoryVisibilityState'>StoryVisibilityState</a></code>
            </td>
            <td><p>Sets the value of <code>StoryModel.visibility_state</code>.</p>
</td>
        </tr><tr>
            <td><code>set_runtime_state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/#StoryState'>StoryState</a></code>
            </td>
            <td><p>Sets the value of <code>StoryModel.runtime_state</code>.</p>
</td>
        </tr></table>







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="MAX_STORY_NAME_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.storymodel/constants.fidl#7">MAX_STORY_NAME_LENGTH</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="MAX_MODULES_PER_STORY">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.storymodel/constants.fidl#9">MAX_MODULES_PER_STORY</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="MAX_MODULE_NAME_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.storymodel/constants.fidl#10">MAX_MODULE_NAME_LENGTH</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    
</table>



