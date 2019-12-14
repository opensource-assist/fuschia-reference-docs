[TOC]

# fuchsia.recovery.ui


## **PROTOCOLS**

## FactoryResetCountdown {#FactoryResetCountdown}
*Defined in [fuchsia.recovery.ui/countdown.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.recovery.ui/countdown.fidl#21)*

<p>Protocol to watch for changes when a factory reset countdown is started or
cancelled. An immediate factory reset does not start a countdown.</p>

### Watch {#Watch}

<p>Hanging get that returns when a factory reset is scheduled or a
scheduled factory reset is cancelled. Will return immediately on first
call per connection and then on change after that.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#FactoryResetCountdownState'>FactoryResetCountdownState</a></code>
            </td>
        </tr></table>







## **TABLES**

### FactoryResetCountdownState {#FactoryResetCountdownState}


*Defined in [fuchsia.recovery.ui/countdown.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.recovery.ui/countdown.fidl#11)*

<p>Information provided through the FactoryResetCountdown protocol on the
current factory reset state.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>scheduled_reset_time</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#time'>time</a></code>
            </td>
            <td><p>The time of when factory reset is scheduled to be triggered when a
countdown for factory reset is in progress with respect to the monotonic
clock. This field is left unpopulated if no reset is scheduled.</p>
</td>
        </tr></table>











