Project: /_project.yaml
Book: /_book.yaml

# fuchsia.feedback


## **PROTOCOLS**

## DataProvider {:#DataProvider}
*Defined in [fuchsia.feedback/data_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.feedback/data_provider.fidl#13)*

 Provides data useful to attach in feedback reports (crash or user feedback).

### GetData {:#GetData}

 Returns all the feedback data except the screenshot, which is provided
 separately.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#DataProvider_GetData_Result'>DataProvider_GetData_Result</a></code>
            </td>
        </tr></table>

### GetScreenshot {:#GetScreenshot}

 Returns an image of the current view encoded in the provided `encoding`.

 `screenshot` may be null if the encoding is not supported, the device
 does not have a display, or there is not enough memory to allocate the
 screenshot image.

 The screenshot is provided separately from the rest of the data as
 callers might want to block on it before changing the view.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>encoding</code></td>
            <td>
                <code><a class='link' href='#ImageEncoding'>ImageEncoding</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>screenshot</code></td>
            <td>
                <code><a class='link' href='#Screenshot'>Screenshot</a>?</code>
            </td>
        </tr></table>



## **STRUCTS**

### DataProvider_GetData_Response {:#DataProvider_GetData_Response}
*Defined in [fuchsia.feedback/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#2)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='#Data'>Data</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Annotation {:#Annotation}
*Defined in [fuchsia.feedback/data_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.feedback/data_provider.fidl#45)*



 An annotation and its plain ASCII string key.
 Annotations are short strings, e.g., the board name or the build version.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Attachment {:#Attachment}
*Defined in [fuchsia.feedback/data_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.feedback/data_provider.fidl#53)*



 An attachment and its plain ASCII string key.
 Attachments are larger objects, e.g., log files. They may be binary or text
 data.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Screenshot {:#Screenshot}
*Defined in [fuchsia.feedback/data_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.feedback/data_provider.fidl#67)*



 An encoded image of the screen.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>image</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>dimensions_in_px</code></td>
            <td>
                <code><a class='link' href='../fuchsia.math/index.html'>fuchsia.math</a>/<a class='link' href='../fuchsia.math/index.html#Size'>Size</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### ImageEncoding {:#ImageEncoding}
Type: <code>uint32</code>

*Defined in [fuchsia.feedback/data_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.feedback/data_provider.fidl#62)*

 The encoding used for the image.

 Today, only PNG is supported, but in the future the screenshot could be
 returned in other encodings if need arises.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>PNG</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### Data {:#Data}


*Defined in [fuchsia.feedback/data_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.feedback/data_provider.fidl#35)*

 Data to attach to feedback reports.

 Clients typically upload the data straight to servers without expecting some
 particular fields. So the data comes in the form of arbitrary key-value pairs
 that clients can directly forward to the servers.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>annotations</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Annotation'>Annotation</a>&gt;[32]</code>
            </td>
            <td> A vector of key-value string pairs. Keys are guaranteed to be unique.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>attachments</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Attachment'>Attachment</a>&gt;[16]</code>
            </td>
            <td> A vector of key-value string-to-VMO pairs. Keys are guaranteed to be unique.
</td>
        </tr></table>



## **UNIONS**

### DataProvider_GetData_Result {:#DataProvider_GetData_Result}
*Defined in [fuchsia.feedback/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#5)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#DataProvider_GetData_Response'>DataProvider_GetData_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>







