Project: /_project.yaml
Book: /_book.yaml

# fuchsia.modular.storymodel








## **TABLES**

### StoryModel {:#StoryModel}


*Defined in [fuchsia.modular.storymodel/story_model.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.storymodel/story_model.fidl#14)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>runtime_state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/index.html#StoryState'>StoryState</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>visibility_state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/index.html#StoryVisibilityState'>StoryVisibilityState</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>modules</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.modular.storymodel/index.html#ModuleModel'>ModuleModel</a>&gt;[128]</code>
            </td>
            <td></td>
        </tr></table>

### ModuleModel {:#ModuleModel}


*Defined in [fuchsia.modular.storymodel/story_model.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.storymodel/story_model.fidl#37)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td></td>
        </tr></table>



## **UNIONS**

### StoryModelMutation {:#StoryModelMutation}
*Defined in [fuchsia.modular.storymodel/story_model_mutation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.storymodel/story_model_mutation.fidl#16)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>set_visibility_state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/index.html#StoryVisibilityState'>StoryVisibilityState</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_runtime_state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/index.html#StoryState'>StoryState</a></code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.storymodel/constants.fidl#7">MAX_STORY_NAME_LENGTH</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.storymodel/constants.fidl#9">MAX_MODULES_PER_STORY</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.modular.storymodel/constants.fidl#10">MAX_MODULE_NAME_LENGTH</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    
</table>

