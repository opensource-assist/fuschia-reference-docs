Project: /_project.yaml
Book: /_book.yaml

# fuchsia.net.http


## **PROTOCOLS**

## Loader {:#Loader}
*Defined in [fuchsia.net.http/client.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.http/client.fidl#155)*

 An HTTP loader.

 The loader can service many HTTP requests concurrently. The loader tracks all
 the outstanding requests and will cancel them all if the client closes the
 loader interface.

### Fetch {:#Fetch}

 Initiate the given HTTP request, follow redirects, and return the final
 response.

 The loader will follow redirects (up to an implementation-defined limit)
 and return the final response as a reply to this message. To cancel the
 request, either close the loader interface or close the peer to the `event`
 included in the `request`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.http/index.html#Request'>Request</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.http/index.html#Response'>Response</a></code>
            </td>
        </tr></table>

### Start {:#Start}

 Initiate the given HTTP request and return all intermediate responses to
 the given client.

 Unlike `Fetch`, `Start` does not automatically follow all redirects.
 Instead, each individual response along the redirect chain is delivered to
 the `LoaderClient`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.http/index.html#Request'>Request</a></code>
            </td>
        </tr><tr>
            <td><code>client</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.http/index.html#LoaderClient'>LoaderClient</a></code>
            </td>
        </tr></table>



## LoaderClient {:#LoaderClient}
*Defined in [fuchsia.net.http/client.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.http/client.fidl#177)*

 A client interface used with `Loader.Start`.

 Closing the underlying channel will cancel the associated HTTP transaction.

### OnResponse {:#OnResponse}

 Called by the loader when the loader receives an HTTP response.

 If the server has requested a redirect, then `redirect` will be non-null
 and describe the target the server requested. To follow the redirect, reply
 to this message. To not follow the redirect, close the underlying channel.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.http/index.html#Response'>Response</a></code>
            </td>
        </tr><tr>
            <td><code>redirect</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.http/index.html#RedirectTarget'>RedirectTarget</a>?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## **STRUCTS**

### Error {:#Error}
*Defined in [fuchsia.net.http/client.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.http/client.fidl#10)*



 An error occurred during the HTTP transaction.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>code</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The numerical error code.

 These error codes correspond to
 <https://fuchsia.googlesource.com/fuchsia/+/master/garnet/bin/network/net_error_list.h>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>description</code></td>
            <td>
                <code>string?</code>
            </td>
            <td> A textual description of the error in en-US.
</td>
            <td>No default</td>
        </tr>
</table>

### Header {:#Header}
*Defined in [fuchsia.net.http/client.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.http/client.fidl#22)*



 An HTTP header field.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td> The name of the header field.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td> The value of the header field.
</td>
            <td>No default</td>
        </tr>
</table>

### Request {:#Request}
*Defined in [fuchsia.net.http/client.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.http/client.fidl#76)*



 An HTTP request.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>method</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The HTTP method if applicable.
</td>
            <td>GET</td>
        </tr><tr>
            <td><code>url</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td> The URL to load.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>headers</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.net.http/index.html#Header'>Header</a>&gt;?</code>
            </td>
            <td> Additional HTTP request headers.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>body</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.http/index.html#Body'>Body</a>?</code>
            </td>
            <td> The payload for the request body. For HTTP requests, the method must be set
 to "POST" or "PUT". If a buffer is used for the body, a Content-Length
 header will automatically be added.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>event</code></td>
            <td>
                <code>handle&lt;eventpair&gt;?</code>
            </td>
            <td> The loader will cancel the request if the peer for this event is closed.

 When this happens, the loader will send a Response with the appropriate
 error code.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>cache_mode</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.http/index.html#CacheMode'>CacheMode</a></code>
            </td>
            <td> The cache behavior for the request.
</td>
            <td><a class='link' href='../fuchsia.net.http/index.html#DEFAULT'>DEFAULT</a></td>
        </tr><tr>
            <td><code>response_body_mode</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.http/index.html#ResponseBodyMode'>ResponseBodyMode</a></code>
            </td>
            <td> The response body mode.
</td>
            <td><a class='link' href='../fuchsia.net.http/index.html#BUFFER'>BUFFER</a></td>
        </tr>
</table>

### RedirectTarget {:#RedirectTarget}
*Defined in [fuchsia.net.http/client.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.http/client.fidl#109)*



 A description of the redirect the server requested.

 The semantics of an HTTP redirect vary according to the status code use to
 generate the redirect. This structure ensures that the loader and its client
 agree on the interpretation of the redirect response from the server.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>method</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The HTTP method the server suggested for the redirect.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>url</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td> The URL the server suggested for the redirect.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>referrer</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td> The referrer the server suggested for the redirect.
</td>
            <td>No default</td>
        </tr>
</table>

### Response {:#Response}
*Defined in [fuchsia.net.http/client.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.http/client.fidl#121)*



 A response to an HTTP request.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.http/index.html#Error'>Error</a>?</code>
            </td>
            <td> If the response resulted in a network level error, this field will be set.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>body</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.http/index.html#Body'>Body</a>?</code>
            </td>
            <td> The response body.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>url</code></td>
            <td>
                <code>vector&lt;uint8&gt;?</code>
            </td>
            <td> The final URL of the response, after redirects have been followed.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>status_code</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The HTTP status code.

 0 if not applicable.
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
                <code>vector&lt;<a class='link' href='../fuchsia.net.http/index.html#Header'>Header</a>&gt;?</code>
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
        </tr>
</table>



## **ENUMS**

### CacheMode {:#CacheMode}
Type: <code>uint32</code>

*Defined in [fuchsia.net.http/client.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.http/client.fidl#40)*

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

*Defined in [fuchsia.net.http/client.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.http/client.fidl#62)*

 Specify the mechanism used to return the response body.

 Streaming the response can be more efficient if the response body is large
 and can be processed incrementally (e.g., by an image decoder).

 Buffering the response can be more efficient if the response body is in cache
 and the cache entry can be directly mapped into the resulting buffer.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>BUFFER</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>STREAM</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>





## **UNIONS**

### Body {:#Body}
*Defined in [fuchsia.net.http/client.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.http/client.fidl#31)*

 The body of either an HTTP request or an HTTP response.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
            <td> A buffer that will contain the complete request or response body.
</td>
        </tr><tr>
            <td><code>stream</code></td>
            <td>
                <code>handle&lt;socket&gt;</code>
            </td>
            <td> A socket that will contain the streaming request or response body.
</td>
        </tr></table>







