Project: /_project.yaml
Book: /_book.yaml

# fuchsia.testing.runner


## **PROTOCOLS**

## TestRunner {:#TestRunner}
*Defined in [fuchsia.testing.runner/test_runner.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.testing.runner/test_runner.fidl#20)*

 This service is included in the Environment of multi-process tests
 that are launched by the test runner harness. Test processes can connect to
 this service to log failures, signal crashes, and signal completion.
 The empty return acknowledges that the connection to TestRunner was
 successful.

### Identify {:#Identify}

 Tells the test runner how to identify this test program.

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

### ReportResult {:#ReportResult}

 Tells the test runner that a paritcular test case finished. May be called
 multiple times.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='../fuchsia.testing.runner/index.html#TestResult'>TestResult</a></code>
            </td>
        </tr></table>



### Fail {:#Fail}

 Tells the test runner that a particular test case failed, with the supplied
 message. May be called multiple times. When `Teardown()` is called, the
 test program ends as a failure.

 `Fail()` is deprecated in favor of `ReportResult`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>log_message</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### Done {:#Done}

 Either this method, `Teardown()` or `WillTerminate()` must be invoked
 before closing the connection to this interface; otherwise the TestRunner
 service will assume that the connection broke due to the test crashing.
 The test runner will send a reply back as an acknowledgement when it starts
 processing this method.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### Teardown {:#Teardown}

 Signals that the test program is complete and the entire test harness
 should be torn down. The test will be declared a failure if `Fail()` was
 ever called, or if `ReportResult()` was ever called where `failed` is true.
 Otherwise the test will be declared successful. The test runner will send a
 reply back as an acknowledgement when it starts processing this method.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### WillTerminate {:#WillTerminate}

 Signals that this process expects to be terminated within the time
 specified. If it is not killed that is a failure. A test that calls this
 should not call `Done()` or `Teardown()`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>withinSeconds</code></td>
            <td>
                <code>float64</code>
            </td>
        </tr></table>



### SetTestPointCount {:#SetTestPointCount}

 Declare how many test points this test is expected to pass to complete.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>count</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>



### PassTestPoint {:#PassTestPoint}

 Signals that a test point has been passed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## TestRunnerStore {:#TestRunnerStore}
*Defined in [fuchsia.testing.runner/test_runner.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.testing.runner/test_runner.fidl#79)*

 This service is included in the Environment of the test runner
 harness, along with TestRunner. This service represents a producer-consumer
 queue that is shared between all of its clients; clients can use it to signal
 events across different processes. Producers can queue values associated to a
 key, and consumers can get values out of the queue (or block until a value is
 available).

 Two example use cases:

 A module testing the persistence of its 'Ledger' between reinflations can use
 this queue to Put() some state and Get() the state in a subsequent run, and
 assert that the ledger data it sees in its subsequent runs matches the state
 saved in previous runs.

 An test agent can Put() a "connected" key when it receives a connection, and
 a test module that requested the agent can Get() that "connected" key to
 assert that it was able to connect to the right agent.

### Put {:#Put}

 This will store `key` with value `value` and respond back. Subsequent
 Put()s to `key` are queued up until they are read by a `Get()`.

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

### Get {:#Get}

 Get() will return the next queued value associated with the `key`. If there
 are no values queued for key, this method will not return until one has
 been Put().

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

### TestResult {:#TestResult}
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













