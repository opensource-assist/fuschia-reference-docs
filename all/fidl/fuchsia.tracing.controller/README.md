[TOC]

# fuchsia.tracing.controller


## **PROTOCOLS**

## Controller {#Controller}
*Defined in [fuchsia.tracing.controller/trace_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.tracing.controller/trace_controller.fidl#23)*


### StartTracing {#StartTracing}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#TraceOptions'>TraceOptions</a></code>
            </td>
        </tr><tr>
            <td><code>output</code></td>
            <td>
                <code>handle&lt;socket&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### StopTracing {#StopTracing}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### GetProviders {#GetProviders}

<p>Return the set of registered providers.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>providers</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ProviderInfo'>ProviderInfo</a>&gt;[100]</code>
            </td>
        </tr></table>

### GetKnownCategories {#GetKnownCategories}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>categories</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#KnownCategory'>KnownCategory</a>&gt;</code>
            </td>
        </tr></table>



## **STRUCTS**

### KnownCategory {#KnownCategory}
*Defined in [fuchsia.tracing.controller/trace_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.tracing.controller/trace_controller.fidl#57)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>description</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### BufferingMode {#BufferingMode}
Type: <code>uint8</code>

*Defined in [fuchsia.tracing.controller/trace_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.tracing.controller/trace_controller.fidl#63)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ONESHOT</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>CIRCULAR</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>STREAMING</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### ProviderSpec {#ProviderSpec}


*Defined in [fuchsia.tracing.controller/trace_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.tracing.controller/trace_controller.fidl#70)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>buffer_size_megabytes_hint</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr></table>

### TraceOptions {#TraceOptions}


*Defined in [fuchsia.tracing.controller/trace_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.tracing.controller/trace_controller.fidl#76)*

<p>Provides options for the trace.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>categories</code></td>
            <td>
                <code>vector&lt;string&gt;[100]</code>
            </td>
            <td><p>The trace categories to record, or an empty array for all.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>buffer_size_megabytes_hint</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Suggested size of trace buffer which each provider should receive.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>start_timeout_milliseconds</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Acknowledge start request after at most <code>start_timeout_milliseconds</code>.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>buffering_mode</code></td>
            <td>
                <code><a class='link' href='#BufferingMode'>BufferingMode</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>provider_specs</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ProviderSpec'>ProviderSpec</a>&gt;[100]</code>
            </td>
            <td><p>Overrides for particular providers.</p>
</td>
        </tr></table>

### ProviderInfo {#ProviderInfo}


*Defined in [fuchsia.tracing.controller/trace_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.tracing.controller/trace_controller.fidl#96)*

<p>Result of |GetProviders|.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>The provider's ID, assigned by trace-manager.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>pid</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#koid'>koid</a></code>
            </td>
            <td><p>The provider's pid.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>name</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td><p>The name of the provider.</p>
</td>
        </tr></table>









## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="MAX_NUM_PROVIDERS">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.tracing.controller/trace_controller.fidl#10">MAX_NUM_PROVIDERS</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum number of providers supported.</p>
</td>
        </tr>
    <tr id="MAX_PROVIDER_NAME_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.tracing.controller/trace_controller.fidl#13">MAX_PROVIDER_NAME_LENGTH</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum length of a provider's name.</p>
</td>
        </tr>
    <tr id="MAX_NUM_CATEGORIES">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.tracing.controller/trace_controller.fidl#16">MAX_NUM_CATEGORIES</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum number of categories supported.</p>
</td>
        </tr>
    <tr id="MAX_CATEGORY_NAME_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.tracing.controller/trace_controller.fidl#19">MAX_CATEGORY_NAME_LENGTH</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum length of a category name.</p>
</td>
        </tr>
    
</table>



