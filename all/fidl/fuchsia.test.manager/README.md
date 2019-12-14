[TOC]

# fuchsia.test.manager


## **PROTOCOLS**

## Harness {#Harness}
*Defined in [fuchsia.test.manager/test_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/test_manager/fidl/test_manager.fidl#15)*

<p>Runs test that implements the <code>fuchsia.test.Suite</code> protocol
(either directly or via a runner adapter). The test must be a
v2 component test.</p>
<p>Designed to be used by run_test_suite to execute v2 tests.</p>

### RunSuite {#RunSuite}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>suite_url</code></td>
            <td>
                <code>string[4096]</code>
            </td>
        </tr><tr>
            <td><code>logger</code></td>
            <td>
                <code>handle&lt;socket&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>outcome</code></td>
            <td>
                <code><a class='link' href='#Outcome'>Outcome</a></code>
            </td>
        </tr></table>





## **ENUMS**

### Outcome {#Outcome}
Type: <code>uint32</code>

*Defined in [fuchsia.test.manager/test_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/test_manager/fidl/test_manager.fidl#20)*

<p>Outcome of running the suite.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>PASSED</code></td>
            <td><code>0</code></td>
            <td><p>All tests in the suite passed.</p>
</td>
        </tr><tr>
            <td><code>FAILED</code></td>
            <td><code>1</code></td>
            <td><p>Some test in the suite failed.</p>
</td>
        </tr><tr>
            <td><code>INCONCLUSIVE</code></td>
            <td><code>2</code></td>
            <td><p>Some test in the suite did not complete and return outcome.</p>
</td>
        </tr><tr>
            <td><code>ERROR</code></td>
            <td><code>3</code></td>
            <td><p>Suite completed with some error, like it crashed or did not implement fuchsia.test.Suite properly.</p>
</td>
        </tr></table>













