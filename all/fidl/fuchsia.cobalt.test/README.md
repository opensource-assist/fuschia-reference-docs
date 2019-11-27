[TOC]

# fuchsia.cobalt.test


## **PROTOCOLS**

## LoggerQuerier {#LoggerQuerier}
*Defined in [fuchsia.cobalt.test/query.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.cobalt.test/query.test.fidl#33)*

<p>LoggerQuerier provides a way to query mock cobalt services to check that
clients of cobalt are logging events as expected.</p>

### WatchLogs {#WatchLogs}

<p>Returns the <em>first</em> N events that were logged for the logger with the
given <code>project_id</code> and a <code>more</code> flag indicating whether there were
more than N events logged. There is no way to retrieve events logged
after the first N events.</p>
<p>Returns an error if a Logger for the given <code>project_id</code> has not been
created through a request to the LoggerFactory protocol.</p>
<p>Repeated calls to WatchLogs for a given LogMethod will block until new
events are logged with that method, enabling tests to synchronize
without sleeps or timeouts.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>project_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>method</code></td>
            <td>
                <code><a class='link' href='#LogMethod'>LogMethod</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#LoggerQuerier_WatchLogs_Result'>LoggerQuerier_WatchLogs_Result</a></code>
            </td>
        </tr></table>

### ResetLogger {#ResetLogger}

<p>Clear all logged events by logging <code>method</code> for the logger with the
given <code>project_id</code>.</p>
<p>This is a no-op if a logger for the given <code>project_id</code> does not exist.
Notably, it does <em>not</em> create a new logger with <code>project_id</code> if one
does not already exist.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>project_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>method</code></td>
            <td>
                <code><a class='link' href='#LogMethod'>LogMethod</a></code>
            </td>
        </tr></table>





## **STRUCTS**

### LoggerQuerier_WatchLogs_Response {#LoggerQuerier_WatchLogs_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>events</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.cobalt/'>fuchsia.cobalt</a>/<a class='link' href='../fuchsia.cobalt/#CobaltEvent'>CobaltEvent</a>&gt;[64]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>more</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### LogMethod {#LogMethod}
Type: <code>uint32</code>

*Defined in [fuchsia.cobalt.test/query.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.cobalt.test/query.test.fidl#13)*

<p>This is currently not exhaustive.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>LOG_EVENT</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>LOG_EVENT_COUNT</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>LOG_ELAPSED_TIME</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>LOG_FRAME_RATE</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>LOG_MEMORY_USAGE</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>LOG_STRING</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>LOG_INT_HISTOGRAM</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr><tr>
            <td><code>LOG_COBALT_EVENT</code></td>
            <td><code>8</code></td>
            <td></td>
        </tr><tr>
            <td><code>LOG_COBALT_EVENTS</code></td>
            <td><code>9</code></td>
            <td></td>
        </tr></table>

### QueryError {#QueryError}
Type: <code>uint32</code>

*Defined in [fuchsia.cobalt.test/query.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.cobalt.test/query.test.fidl#25)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>LOGGER_NOT_FOUND</code></td>
            <td><code>0</code></td>
            <td><p>The logger required to complete the current query could not be found.</p>
</td>
        </tr></table>





## **UNIONS**

### LoggerQuerier_WatchLogs_Result {#LoggerQuerier_WatchLogs_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#LoggerQuerier_WatchLogs_Response'>LoggerQuerier_WatchLogs_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#QueryError'>QueryError</a></code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.cobalt.test/query.test.fidl#10">MAX_QUERY_LENGTH</a></td>
            <td>
                    <code>64</code>
                </td>
                <td><code>uint16</code></td>
            <td><p>Maximum number of events returned by a query.</p>
</td>
        </tr>
    
</table>

