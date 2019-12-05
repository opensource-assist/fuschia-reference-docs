[TOC]

# fuchsia.cobalt


## **PROTOCOLS**

## LoggerFactory {#LoggerFactory}
*Defined in [fuchsia.cobalt/cobalt.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-cobalt/cobalt.fidl#116)*


### CreateLogger {#CreateLogger}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>profile</code></td>
            <td>
                <code><a class='link' href='#ProjectProfile'>ProjectProfile</a></code>
            </td>
        </tr><tr>
            <td><code>logger</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Logger'>Logger</a>&gt;</code>
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
        </tr></table>

### CreateLoggerSimple {#CreateLoggerSimple}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>profile</code></td>
            <td>
                <code><a class='link' href='#ProjectProfile'>ProjectProfile</a></code>
            </td>
        </tr><tr>
            <td><code>logger</code></td>
            <td>
                <code>request&lt;<a class='link' href='#LoggerSimple'>LoggerSimple</a>&gt;</code>
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
        </tr></table>

### CreateLoggerFromProjectName {#CreateLoggerFromProjectName}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>project_name</code></td>
            <td>
                <code>string[64]</code>
            </td>
        </tr><tr>
            <td><code>release_stage</code></td>
            <td>
                <code><a class='link' href='#ReleaseStage'>ReleaseStage</a></code>
            </td>
        </tr><tr>
            <td><code>logger</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Logger'>Logger</a>&gt;</code>
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
        </tr></table>

### CreateLoggerSimpleFromProjectName {#CreateLoggerSimpleFromProjectName}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>project_name</code></td>
            <td>
                <code>string[64]</code>
            </td>
        </tr><tr>
            <td><code>release_stage</code></td>
            <td>
                <code><a class='link' href='#ReleaseStage'>ReleaseStage</a></code>
            </td>
        </tr><tr>
            <td><code>logger</code></td>
            <td>
                <code>request&lt;<a class='link' href='#LoggerSimple'>LoggerSimple</a>&gt;</code>
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
        </tr></table>

### CreateLoggerFromProjectId {#CreateLoggerFromProjectId}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>project_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>logger</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Logger'>Logger</a>&gt;</code>
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
        </tr></table>

### CreateLoggerSimpleFromProjectId {#CreateLoggerSimpleFromProjectId}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>project_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>logger</code></td>
            <td>
                <code>request&lt;<a class='link' href='#LoggerSimple'>LoggerSimple</a>&gt;</code>
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
        </tr></table>

## LoggerBase {#LoggerBase}
*Defined in [fuchsia.cobalt/cobalt.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-cobalt/cobalt.fidl#249)*

<p>LoggerBase Interface</p>

### LogEvent {#LogEvent}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>metric_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>event_code</code></td>
            <td>
                <code>uint32</code>
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
        </tr></table>

### LogEventCount {#LogEventCount}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>metric_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>event_code</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>component</code></td>
            <td>
                <code>string[64]</code>
            </td>
        </tr><tr>
            <td><code>period_duration_micros</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>count</code></td>
            <td>
                <code>int64</code>
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
        </tr></table>

### LogElapsedTime {#LogElapsedTime}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>metric_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>event_code</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>component</code></td>
            <td>
                <code>string[64]</code>
            </td>
        </tr><tr>
            <td><code>elapsed_micros</code></td>
            <td>
                <code>int64</code>
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
        </tr></table>

### LogFrameRate {#LogFrameRate}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>metric_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>event_code</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>component</code></td>
            <td>
                <code>string[64]</code>
            </td>
        </tr><tr>
            <td><code>fps</code></td>
            <td>
                <code>float32</code>
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
        </tr></table>

### LogMemoryUsage {#LogMemoryUsage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>metric_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>event_code</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>component</code></td>
            <td>
                <code>string[64]</code>
            </td>
        </tr><tr>
            <td><code>bytes</code></td>
            <td>
                <code>int64</code>
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
        </tr></table>

### LogString {#LogString}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>metric_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>s</code></td>
            <td>
                <code>string[256]</code>
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
        </tr></table>

### StartTimer {#StartTimer}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>metric_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>event_code</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>component</code></td>
            <td>
                <code>string[64]</code>
            </td>
        </tr><tr>
            <td><code>timer_id</code></td>
            <td>
                <code>string[64]</code>
            </td>
        </tr><tr>
            <td><code>timestamp</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>timeout_s</code></td>
            <td>
                <code>uint32</code>
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
        </tr></table>

### EndTimer {#EndTimer}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>timer_id</code></td>
            <td>
                <code>string[64]</code>
            </td>
        </tr><tr>
            <td><code>timestamp</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>timeout_s</code></td>
            <td>
                <code>uint32</code>
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
        </tr></table>

## Logger {#Logger}
*Defined in [fuchsia.cobalt/cobalt.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-cobalt/cobalt.fidl#584)*


### LogEvent {#LogEvent}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>metric_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>event_code</code></td>
            <td>
                <code>uint32</code>
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
        </tr></table>

### LogEventCount {#LogEventCount}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>metric_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>event_code</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>component</code></td>
            <td>
                <code>string[64]</code>
            </td>
        </tr><tr>
            <td><code>period_duration_micros</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>count</code></td>
            <td>
                <code>int64</code>
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
        </tr></table>

### LogElapsedTime {#LogElapsedTime}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>metric_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>event_code</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>component</code></td>
            <td>
                <code>string[64]</code>
            </td>
        </tr><tr>
            <td><code>elapsed_micros</code></td>
            <td>
                <code>int64</code>
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
        </tr></table>

### LogFrameRate {#LogFrameRate}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>metric_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>event_code</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>component</code></td>
            <td>
                <code>string[64]</code>
            </td>
        </tr><tr>
            <td><code>fps</code></td>
            <td>
                <code>float32</code>
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
        </tr></table>

### LogMemoryUsage {#LogMemoryUsage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>metric_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>event_code</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>component</code></td>
            <td>
                <code>string[64]</code>
            </td>
        </tr><tr>
            <td><code>bytes</code></td>
            <td>
                <code>int64</code>
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
        </tr></table>

### LogString {#LogString}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>metric_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>s</code></td>
            <td>
                <code>string[256]</code>
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
        </tr></table>

### StartTimer {#StartTimer}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>metric_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>event_code</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>component</code></td>
            <td>
                <code>string[64]</code>
            </td>
        </tr><tr>
            <td><code>timer_id</code></td>
            <td>
                <code>string[64]</code>
            </td>
        </tr><tr>
            <td><code>timestamp</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>timeout_s</code></td>
            <td>
                <code>uint32</code>
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
        </tr></table>

### EndTimer {#EndTimer}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>timer_id</code></td>
            <td>
                <code>string[64]</code>
            </td>
        </tr><tr>
            <td><code>timestamp</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>timeout_s</code></td>
            <td>
                <code>uint32</code>
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
        </tr></table>

### LogIntHistogram {#LogIntHistogram}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>metric_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>event_code</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>component</code></td>
            <td>
                <code>string[64]</code>
            </td>
        </tr><tr>
            <td><code>histogram</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#HistogramBucket'>HistogramBucket</a>&gt;[500]</code>
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
        </tr></table>

### LogCustomEvent {#LogCustomEvent}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>metric_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>event_values</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#CustomEventValue'>CustomEventValue</a>&gt;</code>
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
        </tr></table>

### LogCobaltEvent {#LogCobaltEvent}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>event</code></td>
            <td>
                <code><a class='link' href='#CobaltEvent'>CobaltEvent</a></code>
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
        </tr></table>

### LogCobaltEvents {#LogCobaltEvents}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>events</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#CobaltEvent'>CobaltEvent</a>&gt;[64]</code>
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
        </tr></table>

## LoggerSimple {#LoggerSimple}
*Defined in [fuchsia.cobalt/cobalt.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-cobalt/cobalt.fidl#654)*

<p>LoggerSimple Interface</p>

### LogEvent {#LogEvent}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>metric_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>event_code</code></td>
            <td>
                <code>uint32</code>
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
        </tr></table>

### LogEventCount {#LogEventCount}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>metric_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>event_code</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>component</code></td>
            <td>
                <code>string[64]</code>
            </td>
        </tr><tr>
            <td><code>period_duration_micros</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>count</code></td>
            <td>
                <code>int64</code>
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
        </tr></table>

### LogElapsedTime {#LogElapsedTime}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>metric_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>event_code</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>component</code></td>
            <td>
                <code>string[64]</code>
            </td>
        </tr><tr>
            <td><code>elapsed_micros</code></td>
            <td>
                <code>int64</code>
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
        </tr></table>

### LogFrameRate {#LogFrameRate}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>metric_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>event_code</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>component</code></td>
            <td>
                <code>string[64]</code>
            </td>
        </tr><tr>
            <td><code>fps</code></td>
            <td>
                <code>float32</code>
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
        </tr></table>

### LogMemoryUsage {#LogMemoryUsage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>metric_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>event_code</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>component</code></td>
            <td>
                <code>string[64]</code>
            </td>
        </tr><tr>
            <td><code>bytes</code></td>
            <td>
                <code>int64</code>
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
        </tr></table>

### LogString {#LogString}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>metric_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>s</code></td>
            <td>
                <code>string[256]</code>
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
        </tr></table>

### StartTimer {#StartTimer}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>metric_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>event_code</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>component</code></td>
            <td>
                <code>string[64]</code>
            </td>
        </tr><tr>
            <td><code>timer_id</code></td>
            <td>
                <code>string[64]</code>
            </td>
        </tr><tr>
            <td><code>timestamp</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>timeout_s</code></td>
            <td>
                <code>uint32</code>
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
        </tr></table>

### EndTimer {#EndTimer}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>timer_id</code></td>
            <td>
                <code>string[64]</code>
            </td>
        </tr><tr>
            <td><code>timestamp</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>timeout_s</code></td>
            <td>
                <code>uint32</code>
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
        </tr></table>

### LogIntHistogram {#LogIntHistogram}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>metric_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>event_code</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>component</code></td>
            <td>
                <code>string[64]</code>
            </td>
        </tr><tr>
            <td><code>bucket_indices</code></td>
            <td>
                <code>vector&lt;uint32&gt;[500]</code>
            </td>
        </tr><tr>
            <td><code>bucket_counts</code></td>
            <td>
                <code>vector&lt;uint64&gt;[500]</code>
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
        </tr></table>

## SystemDataUpdater {#SystemDataUpdater}
*Defined in [fuchsia.cobalt/cobalt.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-cobalt/cobalt.fidl#689)*


### SetExperimentState {#SetExperimentState}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>experiments</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Experiment'>Experiment</a>&gt;</code>
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
        </tr></table>

### SetChannel {#SetChannel}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>current_channel</code></td>
            <td>
                <code>string[256]</code>
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
        </tr></table>

## Controller {#Controller}
*Defined in [fuchsia.cobalt/cobalt_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-cobalt/cobalt_controller.fidl#11)*


### RequestSendSoon {#RequestSendSoon}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>success</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

### BlockUntilEmpty {#BlockUntilEmpty}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>max_wait_seconds</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### GetNumSendAttempts {#GetNumSendAttempts}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>num</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### GetFailedSendAttempts {#GetFailedSendAttempts}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>num</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### GetNumObservationsAdded {#GetNumObservationsAdded}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>num_obs</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### GenerateAggregatedObservations {#GenerateAggregatedObservations}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>day_index</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>report_ids</code></td>
            <td>
                <code>vector&lt;uint32&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>num_obs</code></td>
            <td>
                <code>vector&lt;uint64&gt;</code>
            </td>
        </tr></table>



## **STRUCTS**

### ProjectProfile {#ProjectProfile}
*Defined in [fuchsia.cobalt/cobalt.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-cobalt/cobalt.fidl#104)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>release_stage</code></td>
            <td>
                <code><a class='link' href='#ReleaseStage'>ReleaseStage</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### CustomEventValue {#CustomEventValue}
*Defined in [fuchsia.cobalt/cobalt.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-cobalt/cobalt.fidl#490)*



<p>Logger Interface</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>dimension_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#Value'>Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### HistogramBucket {#HistogramBucket}
*Defined in [fuchsia.cobalt/cobalt.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-cobalt/cobalt.fidl#507)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>index</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>count</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### CountEvent {#CountEvent}
*Defined in [fuchsia.cobalt/cobalt.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-cobalt/cobalt.fidl#518)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>period_duration_micros</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>count</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Event {#Event}
*Defined in [fuchsia.cobalt/cobalt.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-cobalt/cobalt.fidl#528)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### CobaltEvent {#CobaltEvent}
*Defined in [fuchsia.cobalt/cobalt.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-cobalt/cobalt.fidl#560)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>metric_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>event_codes</code></td>
            <td>
                <code>vector&lt;uint32&gt;[5]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>component</code></td>
            <td>
                <code>string[64]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>payload</code></td>
            <td>
                <code><a class='link' href='#EventPayload'>EventPayload</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Experiment {#Experiment}
*Defined in [fuchsia.cobalt/cobalt.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-cobalt/cobalt.fidl#678)*



<p>SystemProfileUpdater Interface</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>experiment_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>arm_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### Status {#Status}
Type: <code>int32</code>

*Defined in [fuchsia.cobalt/cobalt.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-cobalt/cobalt.fidl#69)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OK</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVALID_ARGUMENTS</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>EVENT_TOO_BIG</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>BUFFER_FULL</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>INTERNAL_ERROR</code></td>
            <td><code>-1</code></td>
            <td></td>
        </tr></table>

### ReleaseStage {#ReleaseStage}
Type: <code>int32</code>

*Defined in [fuchsia.cobalt/cobalt.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-cobalt/cobalt.fidl#89)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>GA</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>DOGFOOD</code></td>
            <td><code>10</code></td>
            <td></td>
        </tr><tr>
            <td><code>FISHFOOD</code></td>
            <td><code>20</code></td>
            <td></td>
        </tr><tr>
            <td><code>DEBUG</code></td>
            <td><code>99</code></td>
            <td></td>
        </tr></table>





## **UNIONS**

### Value {#Value}
*Defined in [fuchsia.cobalt/cobalt.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-cobalt/cobalt.fidl#499)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>string_value</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>int_value</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>double_value</code></td>
            <td>
                <code>float64</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>index_value</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr></table>

### EventPayload {#EventPayload}
*Defined in [fuchsia.cobalt/cobalt.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-cobalt/cobalt.fidl#532)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>event</code></td>
            <td>
                <code><a class='link' href='#Event'>Event</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>event_count</code></td>
            <td>
                <code><a class='link' href='#CountEvent'>CountEvent</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>elapsed_micros</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>fps</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>memory_bytes_used</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>string_event</code></td>
            <td>
                <code>string[256]</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>int_histogram</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#HistogramBucket'>HistogramBucket</a>&gt;[500]</code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-cobalt/cobalt.fidl#41">MAX_BYTES_PER_EVENT</a></td>
            <td>
                    <code>102400</code>
                </td>
                <td><code>int64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-cobalt/cobalt.fidl#44">MAX_HISTOGRAM_BUCKETS</a></td>
            <td>
                    <code>500</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-cobalt/cobalt.fidl#48">MAX_BATCHED_EVENTS</a></td>
            <td>
                    <code>64</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-cobalt/cobalt.fidl#51">MAX_COMPONENT_LENGTH</a></td>
            <td>
                    <code>64</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-cobalt/cobalt.fidl#54">MAX_PROJECT_NAME_LENGTH</a></td>
            <td>
                    <code>64</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-cobalt/cobalt.fidl#57">MAX_TIMER_ID_LENGTH</a></td>
            <td>
                    <code>64</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-cobalt/cobalt.fidl#60">MAX_STRING_EVENT_SIZE</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-cobalt/cobalt.fidl#63">MAX_EVENT_CODE_COUNT</a></td>
            <td>
                    <code>5</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-cobalt/cobalt.fidl#66">MAX_CHANNEL_NAME_LENGTH</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    
</table>



