Project: /_project.yaml
Book: /_book.yaml

# fuchsia.update


## **PROTOCOLS**

## Manager {:#Manager}
*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#8)*


### CheckNow {:#CheckNow}

 Immediately check for an update.
  `options`:  Did a user initiate this request? (`USER_INITIATED`) This changes
              some parameters about aggressiveness of retries and throttling.
  `monitor`:  An interface on which to receive the status events for this update check.
               It's only valid for a single update check, after that it won't receive any
               more events.

  -> Was the update check successfully started (state machine in a proper state
     to do so).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#Options'>Options</a></code>
            </td>
        </tr><tr>
            <td><code>monitor</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Monitor'>Monitor</a>&gt;?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#CheckStartedResult'>CheckStartedResult</a></code>
            </td>
        </tr></table>

### GetState {:#GetState}

 Get the current state of the Manager (is an update available, is it currently
 checking for an update, etc).

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
                <code><a class='link' href='#State'>State</a></code>
            </td>
        </tr></table>

### AddMonitor {:#AddMonitor}

 Get all status events, for all update checks (interactive and background).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>monitor</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Monitor'>Monitor</a>&gt;</code>
            </td>
        </tr></table>



## Monitor {:#Monitor}
*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#31)*

 Receiver of updates for either an individual update check, or to continuously
 receive updates for all checks.

### OnState {:#OnState}

 Receive the current state as it changes.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#State'>State</a></code>
            </td>
        </tr></table>





## **ENUMS**

### Initiator {:#Initiator}
Type: <code>uint32</code>

*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#46)*

 Who or what initiated the update check.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>USER</code></td>
            <td><code>0</code></td>
            <td> The update check was initiated by an interactive user, or the user is
 otherwise blocked and waiting for the result of this update check.
</td>
        </tr><tr>
            <td><code>SERVICE</code></td>
            <td><code>1</code></td>
            <td> The update check was initiated by a service, in the background.
</td>
        </tr></table>

### ManagerState {:#ManagerState}
Type: <code>uint32</code>

*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#82)*

 ```
 The various states that the manager can be in.

     +----------------------+
 --->|         IDLE         |<--------------------------------+
 |   +----------------------+                                 |
 |              |               +----------------------+      |
 |              |<--------------|   UPDATE_AVAILABLE   |      |
 |              |               +----------------------+      |
 |              v                       ^                     |
 |   +----------------------+           |                     |
 |<--| CHECKING_FOR_UPDATES |-----------------+               |
 |   +----------------------+                 |               |
 |              v                             |               |
 |   +----------------------+                 |               |
 |   |  PERFORMING_UPDATE   |---------------->|               |
 |   +----------------------+                 |               |
 |              v                             |               |
 |   +----------------------+                 |               |
 |   |  WAITING_FOR_REBOOT  |---------------->|               |
 |   +----------------------+                 |               |
 |              v                             v               |
 |   +----------------------+     +----------------------+    |
 +---|  FINALIZING_UPDATE   |---->|  ENCOUNTERED_ERROR   |----+
     +----------------------+     +----------------------+

 ```


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>IDLE</code></td>
            <td><code>0</code></td>
            <td> The Manager is currently idle (in between updates).

 Next states:
 * `CHECKING_FOR_UPDATES`
</td>
        </tr><tr>
            <td><code>CHECKING_FOR_UPDATES</code></td>
            <td><code>1</code></td>
            <td> The Manager is currently checking for an update.

 Next states:
 * `IDLE` update is not available
 * `UPDATE_AVAILABLE` update is available but not allowed by policy
 * `PERFORMING_UPDATE` update is available and allowed by policy
 * `ENCOUNTERED_ERROR` on error
</td>
        </tr><tr>
            <td><code>UPDATE_AVAILABLE</code></td>
            <td><code>2</code></td>
            <td> The Manager has found an available update but is not allowed to update
 due to policy.

 Next states:
 * `CHECKING_FOR_UPDATES` when CheckNow() is called or a background update starts
</td>
        </tr><tr>
            <td><code>PERFORMING_UPDATE</code></td>
            <td><code>3</code></td>
            <td> The Manager has started the available update.

 Next states:
 * `WAITING_FOR_REBOOT` on success
 * `ENCOUNTERED_ERROR` on error
</td>
        </tr><tr>
            <td><code>WAITING_FOR_REBOOT</code></td>
            <td><code>4</code></td>
            <td> The update has been performed, and the device is waiting to be rebooted.

 Next states:
 * `FINALIZING_UPDATE` after device reboot
 * `ENCOUNTERED_ERROR` on error
</td>
        </tr><tr>
            <td><code>FINALIZING_UPDATE</code></td>
            <td><code>5</code></td>
            <td> The update is being finalized after reboot.

 Next states:
 * `IDLE` on success
 * `ENCOUNTERED_ERROR` on error
</td>
        </tr><tr>
            <td><code>ENCOUNTERED_ERROR</code></td>
            <td><code>6</code></td>
            <td> The Manager is reporting to Omaha that an error has occurred during the
 update.

 Next states:
 * `IDLE`
</td>
        </tr></table>

### CheckStartedResult {:#CheckStartedResult}
Type: <code>uint32</code>

*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#128)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>STARTED</code></td>
            <td><code>0</code></td>
            <td> The update check has been started.
</td>
        </tr><tr>
            <td><code>IN_PROGRESS</code></td>
            <td><code>1</code></td>
            <td> The update check was not started, as an update is already in progress, `monitor` is
 attached to that update and will immediately get a OnState() call on current state.
</td>
        </tr><tr>
            <td><code>THROTTLED</code></td>
            <td><code>2</code></td>
            <td> The update check was not started, because too many requests to check have
 been made in a short period of time.
</td>
        </tr></table>



## **TABLES**

### Options {:#Options}


*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#40)*

 Configuration options for an update attempt (this is common with the Fuchsia
  OTA Interface v2)


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>initiator</code></td>
            <td>
                <code><a class='link' href='#Initiator'>Initiator</a></code>
            </td>
            <td> What initiated this update attempt.
</td>
        </tr></table>

### State {:#State}


*Defined in [fuchsia.update/update.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.update/update.fidl#139)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#ManagerState'>ManagerState</a></code>
            </td>
            <td> The current state of the Manager. Always present.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>version_available</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The version available from Omaha. Will be present in `UPDATE_AVAILABLE` or starting
 from `PERFORMING_UPDATE`.
</td>
        </tr></table>









