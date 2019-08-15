Project: /_project.yaml
Book: /_book.yaml

# fuchsia.skia.skottie


## **PROTOCOLS**

## Player {:#Player}
*Defined in [fuchsia.skia.skottie/skottie_loader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/ui/skottie_viewer/skottie_loader.fidl#25)*


### Seek {:#Seek}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>t</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>



### Play {:#Play}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Pause {:#Pause}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## Loader {:#Loader}
*Defined in [fuchsia.skia.skottie/skottie_loader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/ui/skottie_viewer/skottie_loader.fidl#37)*


### Load {:#Load}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>payload</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
        </tr><tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#Options'>Options</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr><tr>
            <td><code>player</code></td>
            <td>
                <code><a class='link' href='#Player'>Player</a>?</code>
            </td>
        </tr></table>



## **STRUCTS**

### Status {:#Status}
*Defined in [fuchsia.skia.skottie/skottie_loader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/ui/skottie_viewer/skottie_loader.fidl#10)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>error</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>message</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>duration</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Options {:#Options}
*Defined in [fuchsia.skia.skottie/skottie_loader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/ui/skottie_viewer/skottie_loader.fidl#17)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>background_color</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>loop</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>autoplay</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>













