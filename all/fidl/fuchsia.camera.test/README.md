[TOC]

# fuchsia.camera.test


## **PROTOCOLS**

## IspTester {#IspTester}
*Defined in [fuchsia.camera.test/isp.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/camera/test/isp_tester/isp.fidl#30)*

<p>Interface for testing an ISP driver
The sole purpose of this interface is to allow communication
between the ArmIspDevice and the ArmIspDeviceTester.  No other usages
of this interface will be supported!!</p>

### RunTests {#RunTests}

<p>Execute the tests for this device.  Tests will be run on the ISP.
Returns the status from the test.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>report</code></td>
            <td>
                <code><a class='link' href='#TestReport'>TestReport</a></code>
            </td>
        </tr></table>

### CreateStream {#CreateStream}

<p>Acquire a stream from the ISP.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>stream</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.camera2/'>fuchsia.camera2</a>/<a class='link' href='../fuchsia.camera2/#Stream'>Stream</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffers</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sysmem/'>fuchsia.sysmem</a>/<a class='link' href='../fuchsia.sysmem/#BufferCollectionInfo_2'>BufferCollectionInfo_2</a></code>
            </td>
        </tr><tr>
            <td><code>format</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sysmem/'>fuchsia.sysmem</a>/<a class='link' href='../fuchsia.sysmem/#ImageFormat_2'>ImageFormat_2</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### TestReport {#TestReport}
*Defined in [fuchsia.camera.test/isp.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/camera/test/isp_tester/isp.fidl#16)*



<p>Returns the result summary of a test run</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>test_count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Total number of tests</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>success_count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Number of successful tests</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>failure_count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Number of failed tests</p>
</td>
            <td>No default</td>
        </tr>
</table>













