[TOC]

# fuchsia.test


## **PROTOCOLS**

## RunListener {#RunListener}
*Defined in [fuchsia.test/suite.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.test/suite.fidl#38)*

 Listener listens to results from |`Suite.Run`| request.

### OnTestCaseStarted {#OnTestCaseStarted}

 Indicates that an individual test case has started execution and provides
 the primary log stream used by this test case.

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

 Indicates that an invididual test case has completed and outcome is
 available.

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

 Enumerate the test cases available in this test suite.

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

 Run the specified test cases. Results are returned over the results
 channel. The Suite is expected to execute tests one at a time in the order
 specified. Closing |run_listener| marks end of this call.

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

 Defines the end state of a test case.


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

 Description of a single test case.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string[512]</code>
            </td>
            <td> Used to show human readable results.
</td>
        </tr></table>

### Outcome {#Outcome}


*Defined in [fuchsia.test/suite.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.test/suite.fidl#27)*

 Represents the results of invoking a single test case.
 Should be named 'Result', but this interacts awkwardly with Rust's generated
 code.


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

 Specification of a test to run.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>case</code></td>
            <td>
                <code><a class='link' href='#Case'>Case</a></code>
            </td>
            <td> Test case to execute.
</td>
        </tr></table>

### RunOptions {#RunOptions}


*Defined in [fuchsia.test/suite.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.test/suite.fidl#61)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    </table>









