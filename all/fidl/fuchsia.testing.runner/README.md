[TOC]

# fuchsia.testing.runner


## **PROTOCOLS**

## TestRunner {#TestRunner}
*Defined in [fuchsia.testing.runner/test_runner.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.testing.runner/test_runner.fidl#20)*

<p>This service is included in the Environment of multi-process tests
that are launched by the test runner harness. Test processes can connect to
this service to log failures, signal crashes, and signal completion.
The empty return acknowledges that the connection to TestRunner was
successful.</p>

### Identify {#Identify}

<p>Tells the test runner how to identify this test program.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>program_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### ReportResult {#ReportResult}

<p>Tells the test runner that a paritcular test case finished. May be called
multiple times.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#TestResult'>TestResult</a></code>
            </td>
        </tr></table>



### Fail {#Fail}

<p>Tells the test runner that a particular test case failed, with the supplied
message. May be called multiple times. When <code>Teardown()</code> is called, the
test program ends as a failure.</p>
<p><code>Fail()</code> is deprecated in favor of <code>ReportResult</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>log_message</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### Done {#Done}

<p>Either this method, <code>Teardown()</code> or <code>WillTerminate()</code> must be invoked
before closing the connection to this interface; otherwise the TestRunner
service will assume that the connection broke due to the test crashing.
The test runner will send a reply back as an acknowledgement when it starts
processing this method.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### Teardown {#Teardown}

<p>Signals that the test program is complete and the entire test harness
should be torn down. The test will be declared a failure if <code>Fail()</code> was
ever called, or if <code>ReportResult()</code> was ever called where <code>failed</code> is true.
Otherwise the test will be declared successful. The test runner will send a
reply back as an acknowledgement when it starts processing this method.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### WillTerminate {#WillTerminate}

<p>Signals that this process expects to be terminated within the time
specified. If it is not killed that is a failure. A test that calls this
should not call <code>Done()</code> or <code>Teardown()</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>withinSeconds</code></td>
            <td>
                <code>float64</code>
            </td>
        </tr></table>



### SetTestPointCount {#SetTestPointCount}

<p>Declare how many test points this test is expected to pass to complete.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>count</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>



### PassTestPoint {#PassTestPoint}

<p>Signals that a test point has been passed.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## TestRunnerStore {#TestRunnerStore}
*Defined in [fuchsia.testing.runner/test_runner.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.testing.runner/test_runner.fidl#79)*

<p>This service is included in the Environment of the test runner
harness, along with TestRunner. This service represents a producer-consumer
queue that is shared between all of its clients; clients can use it to signal
events across different processes. Producers can queue values associated to a
key, and consumers can get values out of the queue (or block until a value is
available).</p>
<p>Two example use cases:</p>
<p>A module testing the persistence of its 'Ledger' between reinflations can use
this queue to Put() some state and Get() the state in a subsequent run, and
assert that the ledger data it sees in its subsequent runs matches the state
saved in previous runs.</p>
<p>An test agent can Put() a &quot;connected&quot; key when it receives a connection, and
a test module that requested the agent can Get() that &quot;connected&quot; key to
assert that it was able to connect to the right agent.</p>

### Put {#Put}

<p>This will store <code>key</code> with value <code>value</code> and respond back. Subsequent
Put()s to <code>key</code> are queued up until they are read by a <code>Get()</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### Get {#Get}

<p>Get() will return the next queued value associated with the <code>key</code>. If there
are no values queued for key, this method will not return until one has
been Put().</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



## **STRUCTS**

### TestResult {#TestResult}
*Defined in [fuchsia.testing.runner/test_runner.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.testing.runner/test_runner.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>elapsed</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>failed</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>message</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>















