[TOC]

# fuchsia.scheduler


## **PROTOCOLS**

## ProfileProvider {#ProfileProvider}
*Defined in [fuchsia.scheduler/profile.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-scheduler/profile.fidl#10)*


### GetProfile {#GetProfile}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>priority</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[64]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr><tr>
            <td><code>profile</code></td>
            <td>
                <code>handle&lt;profile&gt;?</code>
            </td>
        </tr></table>

### GetDeadlineProfile {#GetDeadlineProfile}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>capacity</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>deadline</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>period</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[64]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr><tr>
            <td><code>profile</code></td>
            <td>
                <code>handle&lt;profile&gt;?</code>
            </td>
        </tr></table>

















