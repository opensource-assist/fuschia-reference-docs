[TOC]

# fuchsia.developer.tiles


## **PROTOCOLS**

## Controller {#Controller}
*Defined in [fuchsia.developer.tiles/tiles.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.developer.tiles/tiles.fidl#11)*


### AddTileFromURL {#AddTileFromURL}

<p>Instantiates a component by its URL and adds a tile backed by that component's ViewProvider.
Returns a key for the tile that can be used for resizing or removing the tile, or 0 on failure.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>url</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>allow_focus</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>args</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### AddTileFromViewProvider {#AddTileFromViewProvider}

<p>Adds a tile backed by a view from the view provider.
Returns a key for the tile that can be used for resizing or removing the tile, or 0 on failure.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>url</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>provider</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.app/'>fuchsia.ui.app</a>/<a class='link' href='../fuchsia.ui.app/#ViewProvider'>ViewProvider</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### RemoveTile {#RemoveTile}

<p>Removes the tile with the given key.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### ListTiles {#ListTiles}

<p>Returns a list of tiles.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>keys</code></td>
            <td>
                <code>vector&lt;uint32&gt;</code>
            </td>
        </tr><tr>
            <td><code>urls</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr><tr>
            <td><code>sizes</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.ui.gfx/'>fuchsia.ui.gfx</a>/<a class='link' href='../fuchsia.ui.gfx/#vec3'>vec3</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>focusabilities</code></td>
            <td>
                <code>vector&lt;bool&gt;</code>
            </td>
        </tr></table>

### Quit {#Quit}

<p>Asks the tiles component to quit.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



















