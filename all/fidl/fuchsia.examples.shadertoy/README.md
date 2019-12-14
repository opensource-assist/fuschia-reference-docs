[TOC]

# fuchsia.examples.shadertoy


## **PROTOCOLS**

## Shadertoy {#Shadertoy}
*Defined in [fuchsia.examples.shadertoy/shadertoy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ui/examples/shadertoy/service/services/shadertoy.fidl#24)*


### SetPaused {#SetPaused}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>paused</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### SetShaderCode {#SetShaderCode}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>glsl</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>successful</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

### SetResolution {#SetResolution}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>width</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### SetMouse {#SetMouse}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>i_mouse</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/'>fuchsia.ui.gfx</a>/<a class='link' href='../fuchsia.ui.gfx/#vec4'>vec4</a></code>
            </td>
        </tr></table>



### SetImage {#SetImage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>channel</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>image_pipe</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.images/'>fuchsia.images</a>/<a class='link' href='../fuchsia.images/#ImagePipe'>ImagePipe</a>&gt;</code>
            </td>
        </tr></table>



## ShadertoyFactory {#ShadertoyFactory}
*Defined in [fuchsia.examples.shadertoy/shadertoy_factory.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ui/examples/shadertoy/service/services/shadertoy_factory.fidl#12)*


### NewImagePipeShadertoy {#NewImagePipeShadertoy}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>toy</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Shadertoy'>Shadertoy</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>image_pipe</code></td>
            <td>
                <code><a class='link' href='../fuchsia.images/'>fuchsia.images</a>/<a class='link' href='../fuchsia.images/#ImagePipe'>ImagePipe</a></code>
            </td>
        </tr></table>



### NewViewShadertoy {#NewViewShadertoy}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>toy</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Shadertoy'>Shadertoy</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>view_token</code></td>
            <td>
                <code>handle&lt;eventpair&gt;</code>
            </td>
        </tr><tr>
            <td><code>handle_input_events</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



















