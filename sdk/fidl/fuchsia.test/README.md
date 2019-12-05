[TOC]

# fuchsia.test


## **PROTOCOLS**

## RunListener {#RunListener}
*Defined in [fuchsia.test/suite.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.test/suite.fidl#38)*

<p>Listener listens to results from |<code>Suite.Run</code>| request.</p>

### OnTestCaseStarted {#OnTestCaseStarted}

<p>Indicates that an individual test case has started execution and provides
the primary log stream used by this test case.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string[512]</code>
            </td>
        </tr><tr>
            <td><code>primary_log</code></td>
            <td>
                <code>handle&lt;socket&gt;</code>
            </td>
        </tr></table>



### OnTestCaseFinished {#OnTestCaseFinished}

<p>Indicates that an invididual test case has completed and outcome is
available.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string[512]</code>
            </td>
        </tr><tr>
            <td><code>outcome</code></td>
            <td>
                <code><a class='link' href='#Outcome'>Outcome</a></code>
            </td>
        </tr></table>



## Suite {#Suite}
*Defined in [fuchsia.test/suite.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.test/suite.fidl#65)*


### GetTests {#GetTests}

<p>Enumerate the test cases available in this test suite.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>cases</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Case'>Case</a>&gt;</code>
            </td>
        </tr></table>

### Run {#Run}

<p>Run the specified test cases. Results are returned over the results
channel. The Suite is expected to execute tests one at a time in the order
specified. Closing |run_listener| marks end of this call.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>tests</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Invocation'>Invocation</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#RunOptions'>RunOptions</a></code>
            </td>
        </tr><tr>
            <td><code>run_listener</code></td>
            <td>
                <code><a class='link' href='#RunListener'>RunListener</a></code>
            </td>
        </tr></table>







## **ENUMS**

### Status {#Status}
Type: <code>uint32</code>

*Defined in [fuchsia.test/suite.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.test/suite.fidl#17)*

<p>Defines the end state of a test case.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>PASSED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>FAILED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### Case {#Case}


*Defined in [fuchsia.test/suite.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.test/suite.fidl#11)*

<p>Description of a single test case.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string[512]</code>
            </td>
            <td><p>Used to show human readable results.</p>
</td>
        </tr></table>

### Outcome {#Outcome}


*Defined in [fuchsia.test/suite.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.test/suite.fidl#27)*

<p>Represents the results of invoking a single test case.
Should be named 'Result', but this interacts awkwardly with Rust's generated
code.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
            <td></td>
        </tr></table>

### Invocation {#Invocation}


*Defined in [fuchsia.test/suite.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.test/suite.fidl#49)*

<p>Specification of a test to run.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>case</code></td>
            <td>
                <code><a class='link' href='#Case'>Case</a></code>
            </td>
            <td><p>Test case to execute.</p>
</td>
        </tr></table>

### RunOptions {#RunOptions}


*Defined in [fuchsia.test/suite.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.test/suite.fidl#61)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    </table>











## **TYPE ALIASES**

<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.test/suite.fidl#8">Name</a></td>
            <td>
                <code>string</code></td>
            <td><p>Name of a test case.</p>
</td>
        </tr></table>

