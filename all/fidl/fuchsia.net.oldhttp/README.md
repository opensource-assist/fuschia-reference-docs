[TOC]

# fuchsia.net.oldhttp


## **PROTOCOLS**

## HttpService {#HttpService}
*Defined in [fuchsia.net.oldhttp/http_service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.oldhttp/http_service.fidl#8)*


### CreateURLLoader {#CreateURLLoader}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>loader</code></td>
            <td>
                <code>request&lt;<a class='link' href='#URLLoader'>URLLoader</a>&gt;</code>
            </td>
        </tr></table>



## URLLoader {#URLLoader}
*Defined in [fuchsia.net.oldhttp/url_loader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.oldhttp/url_loader.fidl#21)*


### Start {#Start}

<p>Loads the given <code>request</code>, asynchronously producing <code>response</code>. Consult
<code>response</code> to determine if the request resulted in an error, was
redirected, or has a response body to be consumed.</p>

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

### FollowRedirect {#FollowRedirect}

<p>If the request passed to <code>Start</code> had <code>auto_follow_redirects</code> set to false,
then upon receiving an URLResponse with a non-NULL <code>redirect_url</code> field,
<code>FollowRedirect</code> may be called to load the URL indicated by the redirect.</p>

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

### QueryStatus {#QueryStatus}

<p>Query status about the URLLoader.</p>

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

### HttpError {#HttpError}
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

### HttpHeader {#HttpHeader}
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

### URLLoaderStatus {#URLLoaderStatus}
*Defined in [fuchsia.net.oldhttp/url_loader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.oldhttp/url_loader.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#HttpError'>HttpError</a>?</code>
            </td>
            <td><p>If the loader has failed due to a network level error, this field will be
set.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>is_loading</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Set to true if the URLLoader is still working. Set to false once an error
is encountered or the response body is completely copied to the response
body stream.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### URLRequest {#URLRequest}
*Defined in [fuchsia.net.oldhttp/url_request.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.oldhttp/url_request.fidl#35)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>url</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The URL to load.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>method</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The HTTP method if applicable.</p>
</td>
            <td>GET</td>
        </tr><tr>
            <td><code>headers</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#HttpHeader'>HttpHeader</a>&gt;?</code>
            </td>
            <td><p>Additional HTTP request headers.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>body</code></td>
            <td>
                <code><a class='link' href='#URLBody'>URLBody</a>?</code>
            </td>
            <td><p>The payload for the request body. For HTTP requests, the method must be set
to &quot;POST&quot; or &quot;PUT&quot;. If a buffer is used for the body, a Content-Length
header will automatically be added.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>response_body_buffer_size</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>The buffer size of the socket returned in URLResponse's <code>body</code> member.
A value of 0 indicates that the default buffer size should be used.  This
value is just a suggestion. The URLLoader may choose to ignore this value.</p>
</td>
            <td>0</td>
        </tr><tr>
            <td><code>auto_follow_redirects</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>If set to true, then redirects will be automatically followed. Otherwise,
when a redirect is encounterd, FollowRedirect must be called to proceed.</p>
</td>
            <td>false</td>
        </tr><tr>
            <td><code>cache_mode</code></td>
            <td>
                <code><a class='link' href='#CacheMode'>CacheMode</a></code>
            </td>
            <td><p>The cache behavior for the request.</p>
</td>
            <td><a class='link' href='#CacheMode.DEFAULT'>CacheMode.DEFAULT</a></td>
        </tr><tr>
            <td><code>response_body_mode</code></td>
            <td>
                <code><a class='link' href='#ResponseBodyMode'>ResponseBodyMode</a></code>
            </td>
            <td><p>The response body mode.</p>
</td>
            <td><a class='link' href='#ResponseBodyMode.STREAM'>ResponseBodyMode.STREAM</a></td>
        </tr>
</table>

### URLResponse {#URLResponse}
*Defined in [fuchsia.net.oldhttp/url_response.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.oldhttp/url_response.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#HttpError'>HttpError</a>?</code>
            </td>
            <td><p>If the response resulted in a network level error, this field will be set.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>body</code></td>
            <td>
                <code><a class='link' href='#URLBody'>URLBody</a>?</code>
            </td>
            <td><p>The response body.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>url</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>The final URL of the response, after redirects have been followed.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>status_code</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>The HTTP status code. 0 if not applicable.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>status_line</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>The HTTP status line.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>headers</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#HttpHeader'>HttpHeader</a>&gt;?</code>
            </td>
            <td><p>The HTTP response headers.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>mime_type</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>The MIME type of the response body.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>charset</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>The character set of the response body.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>redirect_method</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>These fields are set to non-NULL if this response corresponds to a
redirect.  Call the <code>FollowRedirect</code> method on the URLLoader instance to
follow this redirect.</p>
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

### CacheMode {#CacheMode}
Type: <code>uint32</code>

*Defined in [fuchsia.net.oldhttp/url_request.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.oldhttp/url_request.fidl#8)*

<p>Specify the cache behavior of the request.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DEFAULT</code></td>
            <td><code>0</code></td>
            <td><p>Default behavior.</p>
</td>
        </tr><tr>
            <td><code>BYPASS_CACHE</code></td>
            <td><code>1</code></td>
            <td><p>The HTTP request will bypass the local cache and will have a
'Cache-Control: nocache' header added in that causes any proxy servers
to also not satisfy the request from their cache.  This has the effect
of forcing a full end-to-end fetch.</p>
</td>
        </tr><tr>
            <td><code>ONLY_FROM_CACHE</code></td>
            <td><code>2</code></td>
            <td><p>The HTTP request will fail if it cannot serve the requested resource
from the cache (or some equivalent local store).</p>
</td>
        </tr></table>

### ResponseBodyMode {#ResponseBodyMode}
Type: <code>uint32</code>

*Defined in [fuchsia.net.oldhttp/url_request.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.oldhttp/url_request.fidl#24)*

<p>Specify the mechanism used to return the response body.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>BUFFER</code></td>
            <td><code>0</code></td>
            <td><p>The complete response body should be returned in the <code>buffer</code> field of
the response body.</p>
</td>
        </tr><tr>
            <td><code>STREAM</code></td>
            <td><code>1</code></td>
            <td><p>The response body should be streamed through the <code>stream</code> field of the
response body.</p>
</td>
        </tr><tr>
            <td><code>BUFFER_OR_STREAM</code></td>
            <td><code>2</code></td>
            <td><p>The response body may be returned as a buffer or stream.</p>
</td>
        </tr></table>





## **UNIONS**

### URLBody {#URLBody}
*Defined in [fuchsia.net.oldhttp/url_body.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.oldhttp/url_body.fidl#9)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>stream</code></td>
            <td>
                <code>handle&lt;socket&gt;</code>
            </td>
            <td><p>A socket that will contain the streaming request or response body.</p>
</td>
        </tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td><p>A shared buffer that will contain the complete request or response body.</p>
</td>
        </tr></table>







