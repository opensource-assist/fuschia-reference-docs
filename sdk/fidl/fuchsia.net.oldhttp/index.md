Project: /_project.yaml
Book: /_book.yaml

# fuchsia.net.oldhttp


## **PROTOCOLS**

## HttpService {:#HttpService}
*Defined in [fuchsia.net.oldhttp/http_service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.oldhttp/http_service.fidl#8)*


### CreateURLLoader {:#CreateURLLoader}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>loader</code></td>
            <td>
                <code>request&lt;<a class='link' href='#URLLoader'>URLLoader</a>&gt;</code>
            </td>
        </tr></table>



## URLLoader {:#URLLoader}
*Defined in [fuchsia.net.oldhttp/url_loader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.oldhttp/url_loader.fidl#21)*


### Start {:#Start}

 Loads the given `request`, asynchronously producing `response`. Consult
 `response` to determine if the request resulted in an error, was
 redirected, or has a response body to be consumed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code><a class='link' href='#URLRequest'>URLRequest</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#URLResponse'>URLResponse</a></code>
            </td>
        </tr></table>

### FollowRedirect {:#FollowRedirect}

 If the request passed to `Start` had `auto_follow_redirects` set to false,
 then upon receiving an URLResponse with a non-NULL `redirect_url` field,
 `FollowRedirect` may be called to load the URL indicated by the redirect.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#URLResponse'>URLResponse</a></code>
            </td>
        </tr></table>

### QueryStatus {:#QueryStatus}

 Query status about the URLLoader.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#URLLoaderStatus'>URLLoaderStatus</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### HttpError {:#HttpError}
*Defined in [fuchsia.net.oldhttp/http_error.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.oldhttp/http_error.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>code</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>description</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### HttpHeader {:#HttpHeader}
*Defined in [fuchsia.net.oldhttp/http_header.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.oldhttp/http_header.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### URLLoaderStatus {:#URLLoaderStatus}
*Defined in [fuchsia.net.oldhttp/url_loader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.oldhttp/url_loader.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#HttpError'>HttpError</a>?</code>
            </td>
            <td> If the loader has failed due to a network level error, this field will be
 set.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>is_loading</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Set to true if the URLLoader is still working. Set to false once an error
 is encountered or the response body is completely copied to the response
 body stream.
</td>
            <td>No default</td>
        </tr>
</table>

### URLRequest {:#URLRequest}
*Defined in [fuchsia.net.oldhttp/url_request.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.oldhttp/url_request.fidl#35)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>url</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The URL to load.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>method</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The HTTP method if applicable.
</td>
            <td>GET</td>
        </tr><tr>
            <td><code>headers</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#HttpHeader'>HttpHeader</a>&gt;?</code>
            </td>
            <td> Additional HTTP request headers.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>body</code></td>
            <td>
                <code><a class='link' href='#URLBody'>URLBody</a>?</code>
            </td>
            <td> The payload for the request body. For HTTP requests, the method must be set
 to "POST" or "PUT". If a buffer is used for the body, a Content-Length
 header will automatically be added.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>response_body_buffer_size</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The buffer size of the socket returned in URLResponse's `body` member.
 A value of 0 indicates that the default buffer size should be used.  This
 value is just a suggestion. The URLLoader may choose to ignore this value.
</td>
            <td>0</td>
        </tr><tr>
            <td><code>auto_follow_redirects</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If set to true, then redirects will be automatically followed. Otherwise,
 when a redirect is encounterd, FollowRedirect must be called to proceed.
</td>
            <td>false</td>
        </tr><tr>
            <td><code>cache_mode</code></td>
            <td>
                <code><a class='link' href='#CacheMode'>CacheMode</a></code>
            </td>
            <td> The cache behavior for the request.
</td>
            <td><a class='link' href='#DEFAULT'>DEFAULT</a></td>
        </tr><tr>
            <td><code>response_body_mode</code></td>
            <td>
                <code><a class='link' href='#ResponseBodyMode'>ResponseBodyMode</a></code>
            </td>
            <td> The response body mode.
</td>
            <td><a class='link' href='#STREAM'>STREAM</a></td>
        </tr>
</table>

### URLResponse {:#URLResponse}
*Defined in [fuchsia.net.oldhttp/url_response.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.oldhttp/url_response.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#HttpError'>HttpError</a>?</code>
            </td>
            <td> If the response resulted in a network level error, this field will be set.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>body</code></td>
            <td>
                <code><a class='link' href='#URLBody'>URLBody</a>?</code>
            </td>
            <td> The response body.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>url</code></td>
            <td>
                <code>string?</code>
            </td>
            <td> The final URL of the response, after redirects have been followed.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>status_code</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The HTTP status code. 0 if not applicable.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>status_line</code></td>
            <td>
                <code>string?</code>
            </td>
            <td> The HTTP status line.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>headers</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#HttpHeader'>HttpHeader</a>&gt;?</code>
            </td>
            <td> The HTTP response headers.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>mime_type</code></td>
            <td>
                <code>string?</code>
            </td>
            <td> The MIME type of the response body.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>charset</code></td>
            <td>
                <code>string?</code>
            </td>
            <td> The character set of the response body.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>redirect_method</code></td>
            <td>
                <code>string?</code>
            </td>
            <td> These fields are set to non-NULL if this response corresponds to a
 redirect.  Call the `FollowRedirect` method on the URLLoader instance to
 follow this redirect.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>redirect_url</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>redirect_referrer</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### CacheMode {:#CacheMode}
Type: <code>uint32</code>

*Defined in [fuchsia.net.oldhttp/url_request.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.oldhttp/url_request.fidl#8)*

 Specify the cache behavior of the request.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DEFAULT</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>BYPASS_CACHE</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>ONLY_FROM_CACHE</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### ResponseBodyMode {:#ResponseBodyMode}
Type: <code>uint32</code>

*Defined in [fuchsia.net.oldhttp/url_request.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.oldhttp/url_request.fidl#24)*

 Specify the mechanism used to return the response body.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>BUFFER</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>STREAM</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>BUFFER_OR_STREAM</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>





## **UNIONS**

### URLBody {:#URLBody}
*Defined in [fuchsia.net.oldhttp/url_body.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.oldhttp/url_body.fidl#9)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>stream</code></td>
            <td>
                <code>handle&lt;socket&gt;</code>
            </td>
            <td> A socket that will contain the streaming request or response body.
</td>
        </tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
            <td> A shared buffer that will contain the complete request or response body.
</td>
        </tr></table>







