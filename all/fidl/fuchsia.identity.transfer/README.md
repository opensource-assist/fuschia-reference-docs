[TOC]

# fuchsia.identity.transfer


## **PROTOCOLS**

## AccountManagerPeer {#AccountManagerPeer}
*Defined in [fuchsia.identity.transfer/account_transfer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/identity/fidl/account_transfer.fidl#17)*

<p>The control protocol used by two AccountManager components on different
devices to exchange information.</p>
<p>Note: this is a sensitive interface and connections should only be created
between AccountManagers on remotely attested devices.  No components on
the same device should connect over this protocol.</p>

### ReceiveAccount {#ReceiveAccount}

<p>Requests an account transfer.
<code>lifetime</code> The lifetime that the transferred account should have
on the target device.
<code>account_transfer</code> The server end of an <code>AccountTransfer</code> channel.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>lifetime</code></td>
            <td>
                <code><a class='link' href='../fuchsia.identity.account/'>fuchsia.identity.account</a>/<a class='link' href='../fuchsia.identity.account/#Lifetime'>Lifetime</a></code>
            </td>
        </tr><tr>
            <td><code>account_transfer</code></td>
            <td>
                <code>request&lt;<a class='link' href='#AccountTransfer'>AccountTransfer</a>&gt;</code>
            </td>
        </tr></table>



## AccountTransfer {#AccountTransfer}
*Defined in [fuchsia.identity.transfer/account_transfer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/identity/fidl/account_transfer.fidl#37)*

<p>The control channel through which AccountManager components on different
devices communicate to execute an account transfer.</p>
<p>When an account needs to be transferred, the source device should request
an <code>AccountTransfer</code> connection using the <code>ReceiveAccount</code> method on the
<code>AccountManagerPeer</code> exposed by the target device.
Once the target device is ready, it sends an <code>OnTransferReady</code> containing
a <code>target_key</code>.
The source device should then encrypt the account using the <code>target_key</code>
and complete the transfer with <code>CompleteAccountTransfer</code>.
Once the account transfer is complete, the channel is closed.</p>

### OnTransferReady {#OnTransferReady}

<p>This event is sent once by the target device when it has completed
preparing to receive an account.  The event contains a <code>target_key</code>
which should be used to encrypt the account data sent through
<code>CompleteAccountTransfer</code>.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>target_key</code></td>
            <td>
                <code><a class='link' href='../fuchsia.kms/'>fuchsia.kms</a>/<a class='link' href='../fuchsia.kms/#PublicKey'>PublicKey</a></code>
            </td>
        </tr></table>

### CompleteAccountTransfer {#CompleteAccountTransfer}

<p>Completes the account transfer by sending the transfered data.
The data is opaque to the AccountManager binary, and should be
supplied and encrypted by the account handler on the source device
using the <code>target_key</code> received through <code>OnTransferReady</code>.</p>
<p>If the account is already present on the target device this fails
with UNSUPPORTED_OPERATION.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>encrypted_account_data</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#AccountTransfer_CompleteAccountTransfer_Result'>AccountTransfer_CompleteAccountTransfer_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### AccountTransfer_CompleteAccountTransfer_Response {#AccountTransfer_CompleteAccountTransfer_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>







## **UNIONS**

### AccountTransfer_CompleteAccountTransfer_Result {#AccountTransfer_CompleteAccountTransfer_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#AccountTransfer_CompleteAccountTransfer_Response'>AccountTransfer_CompleteAccountTransfer_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.identity.account/'>fuchsia.identity.account</a>/<a class='link' href='../fuchsia.identity.account/#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>







