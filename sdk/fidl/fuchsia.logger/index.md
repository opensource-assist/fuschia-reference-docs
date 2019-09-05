Project: /_project.yaml
Book: /_book.yaml

# fuchsia.logger


## **PROTOCOLS**

## Log {:#Log}
*Defined in [fuchsia.logger/logger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-logger/logger.fidl#65)*


### Listen {:#Listen}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>log_listener</code></td>
            <td>
                <code><a class='link' href='#LogListener'>LogListener</a></code>
            </td>
        </tr><tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#LogFilterOptions'>LogFilterOptions</a>?</code>
            </td>
        </tr></table>



### DumpLogs {:#DumpLogs}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>log_listener</code></td>
            <td>
                <code><a class='link' href='#LogListener'>LogListener</a></code>
            </td>
        </tr><tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#LogFilterOptions'>LogFilterOptions</a>?</code>
            </td>
        </tr></table>



## LogSink {:#LogSink}
*Defined in [fuchsia.logger/logger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-logger/logger.fidl#78)*


### Connect {:#Connect}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>socket</code></td>
            <td>
                <code>handle&lt;socket&gt;</code>
            </td>
        </tr></table>



## LogListener {:#LogListener}
*Defined in [fuchsia.logger/logger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-logger/logger.fidl#85)*


### Log {:#Log}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>log</code></td>
            <td>
                <code><a class='link' href='#LogMessage'>LogMessage</a></code>
            </td>
        </tr></table>



### LogMany {:#LogMany}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>log</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#LogMessage'>LogMessage</a>&gt;</code>
            </td>
        </tr></table>



### Done {:#Done}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## Log {:#Log}
*Defined in [fuchsia.logger/logger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-logger/logger.fidl#65)*


### Listen {:#Listen}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>log_listener</code></td>
            <td>
                <code><a class='link' href='#LogListener'>LogListener</a></code>
            </td>
        </tr><tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#LogFilterOptions'>LogFilterOptions</a>?</code>
            </td>
        </tr></table>



### DumpLogs {:#DumpLogs}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>log_listener</code></td>
            <td>
                <code><a class='link' href='#LogListener'>LogListener</a></code>
            </td>
        </tr><tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#LogFilterOptions'>LogFilterOptions</a>?</code>
            </td>
        </tr></table>



## LogSink {:#LogSink}
*Defined in [fuchsia.logger/logger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-logger/logger.fidl#78)*


### Connect {:#Connect}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>socket</code></td>
            <td>
                <code>handle&lt;socket&gt;</code>
            </td>
        </tr></table>



## LogListener {:#LogListener}
*Defined in [fuchsia.logger/logger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-logger/logger.fidl#85)*


### Log {:#Log}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>log</code></td>
            <td>
                <code><a class='link' href='#LogMessage'>LogMessage</a></code>
            </td>
        </tr></table>



### LogMany {:#LogMany}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>log</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#LogMessage'>LogMessage</a>&gt;</code>
            </td>
        </tr></table>



### Done {:#Done}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>





## **STRUCTS**

### LogFilterOptions {:#LogFilterOptions}
*Defined in [fuchsia.logger/logger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-logger/logger.fidl#23)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>filter_by_pid</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>pid</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>filter_by_tid</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>tid</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>verbosity</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>min_severity</code></td>
            <td>
                <code><a class='link' href='#LogLevelFilter'>LogLevelFilter</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>tags</code></td>
            <td>
                <code>vector&lt;string&gt;[5]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### LogMessage {:#LogMessage}
*Defined in [fuchsia.logger/logger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-logger/logger.fidl#47)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>pid</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>tid</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>time</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>severity</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>dropped_logs</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>tags</code></td>
            <td>
                <code>vector&lt;string&gt;[5]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>msg</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### LogFilterOptions {:#LogFilterOptions}
*Defined in [fuchsia.logger/logger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-logger/logger.fidl#23)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>filter_by_pid</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>pid</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>filter_by_tid</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>tid</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>verbosity</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>min_severity</code></td>
            <td>
                <code><a class='link' href='#LogLevelFilter'>LogLevelFilter</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>tags</code></td>
            <td>
                <code>vector&lt;string&gt;[5]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### LogMessage {:#LogMessage}
*Defined in [fuchsia.logger/logger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-logger/logger.fidl#47)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>pid</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>tid</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>time</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>severity</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>dropped_logs</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>tags</code></td>
            <td>
                <code>vector&lt;string&gt;[5]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>msg</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### LogLevelFilter {:#LogLevelFilter}
Type: <code>int8</code>

*Defined in [fuchsia.logger/logger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-logger/logger.fidl#9)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NONE</code></td>
            <td><code>-1</code></td>
            <td></td>
        </tr><tr>
            <td><code>INFO</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>WARN</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERROR</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>FATAL</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### LogLevelFilter {:#LogLevelFilter}
Type: <code>int8</code>

*Defined in [fuchsia.logger/logger.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-logger/logger.fidl#9)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NONE</code></td>
            <td><code>-1</code></td>
            <td></td>
        </tr><tr>
            <td><code>INFO</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>WARN</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERROR</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>FATAL</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>











## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-logger/logger.fidl#18">MAX_TAGS</a></td>
            <td>
                    <code>5</code>
                </td>
                <td><code>uint8</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-logger/logger.fidl#21">MAX_TAG_LEN_BYTES</a></td>
            <td>
                    <code>63</code>
                </td>
                <td><code>uint8</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-logger/logger.fidl#45">MAX_TAGS_PER_LOG_MESSAGE</a></td>
            <td>
                    <code>5</code>
                </td>
                <td><code>uint8</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-logger/logger.fidl#83">MAX_LOG_MANY_SIZE_BYTES</a></td>
            <td>
                    <code>16384</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-logger/logger.fidl#18">MAX_TAGS</a></td>
            <td>
                    <code>5</code>
                </td>
                <td><code>uint8</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-logger/logger.fidl#21">MAX_TAG_LEN_BYTES</a></td>
            <td>
                    <code>63</code>
                </td>
                <td><code>uint8</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-logger/logger.fidl#45">MAX_TAGS_PER_LOG_MESSAGE</a></td>
            <td>
                    <code>5</code>
                </td>
                <td><code>uint8</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-logger/logger.fidl#83">MAX_LOG_MANY_SIZE_BYTES</a></td>
            <td>
                    <code>16384</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    
</table>

