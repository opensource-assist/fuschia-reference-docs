[TOC]

# fuchsia.ledger.internal


## **PROTOCOLS**

## LedgerRepositoryFactory {#LedgerRepositoryFactory}
*Defined in [fuchsia.ledger.internal/internal.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger.internal/internal.fidl#14)*


### Sync {#Sync}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### GetRepository {#GetRepository}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>repository_directory</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr><tr>
            <td><code>cloud_provider</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ledger.cloud/'>fuchsia.ledger.cloud</a>/<a class='link' href='../fuchsia.ledger.cloud/#CloudProvider'>CloudProvider</a>?</code>
            </td>
        </tr><tr>
            <td><code>user_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>repository</code></td>
            <td>
                <code>request&lt;<a class='link' href='#LedgerRepository'>LedgerRepository</a>&gt;</code>
            </td>
        </tr></table>



## LedgerController {#LedgerController}
*Defined in [fuchsia.ledger.internal/internal.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger.internal/internal.fidl#44)*


### Terminate {#Terminate}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## LedgerRepository {#LedgerRepository}
*Defined in [fuchsia.ledger.internal/internal.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/fidl/fuchsia.ledger.internal/internal.fidl#49)*


### Sync {#Sync}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### GetLedger {#GetLedger}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ledger_name</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr><tr>
            <td><code>ledger</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.ledger/'>fuchsia.ledger</a>/<a class='link' href='../fuchsia.ledger/#Ledger'>Ledger</a>&gt;</code>
            </td>
        </tr></table>



### Duplicate {#Duplicate}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ledger_repository</code></td>
            <td>
                <code>request&lt;<a class='link' href='#LedgerRepository'>LedgerRepository</a>&gt;</code>
            </td>
        </tr></table>



### SetSyncStateWatcher {#SetSyncStateWatcher}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ledger/'>fuchsia.ledger</a>/<a class='link' href='../fuchsia.ledger/#SyncWatcher'>SyncWatcher</a></code>
            </td>
        </tr></table>



### DiskCleanUp {#DiskCleanUp}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Close {#Close}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



















