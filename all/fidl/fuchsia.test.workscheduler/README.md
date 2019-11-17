[TOC]

# fuchsia.test.workscheduler


## **PROTOCOLS**

## WorkSchedulerDispatchReporter {#WorkSchedulerDispatchReporter}
*Defined in [fuchsia.test.workscheduler/fuchsia.test.workscheduler.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/component_manager/tests/fidl/fuchsia.test.workscheduler.fidl#21)*

<p>A protocol used in testing by a component instance to report that work has been dispatched.</p>
<p>For example:</p>
<ul>
<li><code>integration-test</code> hosts <code>work-scheduler</code>, starts <code>client</code>.</li>
<li><code>client --- WorkScheduler.ScheduleWork(work_id, ...) --&gt; work-scheduler</code></li>
<li><code>client &lt;-- Worker.DoWork(work_id) --------------------&gt; work-scheduler</code></li>
<li><code>client --- WorkSchedulerDispatchReporter(work_id) ------&gt; integration-test</code></li>
</ul>
<p>This protocol enables <code>integration-test</code> to confirm that the <code>DoWork</code> invocation reached
<code>client</code>.</p>

### OnDoWorkCalled {#OnDoWorkCalled}

<p>Report that <code>WorkScheduler.DoWork(work_id)</code> was successfully invoked on a component.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>work_id</code></td>
            <td>
                <code>string[100]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>















