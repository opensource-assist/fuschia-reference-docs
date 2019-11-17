[TOC]

# fuchsia.net.http


## **PROTOCOLS**

## Loader {#Loader}
*Defined in [fuchsia.net.http/client.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.http/client.fidl#155)*

<p>An HTTP loader.</p>
<p>The loader can service many HTTP requests concurrently. The loader tracks all
the outstanding requests and will cancel them all if the client closes the
loader interface.</p>

### Fetch {#Fetch}

<p>Initiate the given HTTP request, follow redirects, and return the final
response.</p>
<p>The loader will follow redirects (up to an implementation-defined limit)
and return the final response as a reply to this message. To cancel the
request, either close the loader interface or close the peer to the <code>event</code>
included in the <code>request</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code><a class='link' href='#Request'>Request</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Response'>Response</a></code>
            </td>
        </tr></table>

### Start {#Start}

<p>Initiate the given HTTP request and return all intermediate responses to
the given client.</p>
<p>Unlike <code>Fetch</code>, <code>Start</code> does not automatically follow all redirects.
Instead, each individual response along the redirect chain is delivered to
the <code>LoaderClient</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code><a class='link' href='#Request'>Request</a></code>
            </td>
        </tr><tr>
            <td><code>client</code></td>
            <td>
                <code><a class='link' href='#LoaderClient'>LoaderClient</a></code>
            </td>
        </tr></table>



## LoaderClient {#LoaderClient}
*Defined in [fuchsia.net.http/client.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.http/client.fidl#177)*

<p>A client interface used with <code>Loader.Start</code>.</p>
<p>Closing the underlying channel will cancel the associated HTTP transaction.</p>

### OnResponse {#OnResponse}

<p>Called by the loader when the loader receives an HTTP response.</p>
<p>If the server has requested a redirect, then <code>redirect</code> will be non-null
and describe the target the server requested. To follow the redirect, reply
to this message. To not follow the redirect, close the underlying channel.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Response'>Response</a></code>
            </td>
        </tr><tr>
            <td><code>redirect</code></td>
            <td>
                <code><a class='link' href='#RedirectTarget'>RedirectTarget</a>?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## **STRUCTS**

### Error {#Error}
*Defined in [fuchsia.net.http/client.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.http/client.fidl#10)*



<p>An error occurred during the HTTP transaction.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>code</code></td>
            <td>
                <code>int32</code>
            </td>
            <td><p>The numerical error code.</p>
<p>These error codes correspond to
<a href="https://fuchsia.googlesource.com/fuchsia/+/master/garnet/bin/network/net_error_list.h">https://fuchsia.googlesource.com/fuchsia/+/master/garnet/bin/network/net_error_list.h</a></p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>description</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>A textual description of the error in en-US.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### Header {#Header}
*Defined in [fuchsia.net.http/client.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.http/client.fidl#22)*



<p>An HTTP header field.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td><p>The name of the header field.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td><p>The value of the header field.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### Request {#Request}
*Defined in [fuchsia.net.http/client.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.http/client.fidl#76)*



<p>An HTTP request.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>method</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The HTTP method if applicable.</p>
</td>
            <td>GET</td>
        </tr><tr>
            <td><code>url</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td><p>The URL to load.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>headers</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Header'>Header</a>&gt;?</code>
            </td>
            <td><p>Additional HTTP request headers.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>body</code></td>
            <td>
                <code><a class='link' href='#Body'>Body</a>?</code>
            </td>
            <td><p>The payload for the request body. For HTTP requests, the method must be set
to &quot;POST&quot; or &quot;PUT&quot;. If a buffer is used for the body, a Content-Length
header will automatically be added.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>event</code></td>
            <td>
                <code>handle&lt;eventpair&gt;?</code>
            </td>
            <td><p>The loader will cancel the request if the peer for this event is closed.</p>
<p>When this happens, the loader will send a Response with the appropriate
error code.</p>
</td>
            <td>No default</td>
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
            <td><a class='link' href='#ResponseBodyMode.BUFFER'>ResponseBodyMode.BUFFER</a></td>
        </tr>
</table>

### RedirectTarget {#RedirectTarget}
*Defined in [fuchsia.net.http/client.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.http/client.fidl#109)*



<p>A description of the redirect the server requested.</p>
<p>The semantics of an HTTP redirect vary according to the status code use to
generate the redirect. This structure ensures that the loader and its client
agree on the interpretation of the redirect response from the server.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>method</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The HTTP method the server suggested for the redirect.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>url</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td><p>The URL the server suggested for the redirect.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>referrer</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td><p>The referrer the server suggested for the redirect.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### Response {#Response}
*Defined in [fuchsia.net.http/client.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.http/client.fidl#121)*



<p>A response to an HTTP request.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
            <td><p>If the response resulted in a network level error, this field will be set.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>body</code></td>
            <td>
                <code><a class='link' href='#Body'>Body</a>?</code>
            </td>
            <td><p>The response body.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>url</code></td>
            <td>
                <code>vector&lt;uint8&gt;?</code>
            </td>
            <td><p>The final URL of the response, after redirects have been followed.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>status_code</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>The HTTP status code.</p>
<p>0 if not applicable.</p>
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
                <code>vector&lt;<a class='link' href='#Header'>Header</a>&gt;?</code>
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
        </tr>
</table>



## **ENUMS**

### CacheMode {#CacheMode}
Type: <code>uint32</code>

*Defined in [fuchsia.net.http/client.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.http/client.fidl#40)*

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

*Defined in [fuchsia.net.http/client.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.http/client.fidl#62)*

<p>Specify the mechanism used to return the response body.</p>
<p>Streaming the response can be more efficient if the response body is large
and can be processed incrementally (e.g., by an image decoder).</p>
<p>Buffering the response can be more efficient if the response body is in cache
and the cache entry can be directly mapped into the resulting buffer.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>BUFFER</code></td>
            <td><code>0</code></td>
            <td><p>The complete response body should be returned in the <code>buffer</code> field of
the response body.</p>
<p>The loader MAY abort the transation if the buffer size exceeds an
implementation-defined limit.</p>
</td>
        </tr><tr>
            <td><code>STREAM</code></td>
            <td><code>1</code></td>
            <td><p>The response body should be streamed through the <code>stream</code> field of the
response body.</p>
</td>
        </tr></table>





## **UNIONS**

### Body {#Body}
*Defined in [fuchsia.net.http/client.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.http/client.fidl#31)*

<p>The body of either an HTTP request or an HTTP response.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td><p>A buffer that will contain the complete request or response body.</p>
</td>
        </tr><tr>
            <td><code>stream</code></td>
            <td>
                <code>handle&lt;socket&gt;</code>
            </td>
            <td><p>A socket that will contain the streaming request or response body.</p>
</td>
        </tr></table>







