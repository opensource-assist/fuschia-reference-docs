[TOC]

# fuchsia.identity.prototype


## **PROTOCOLS**

## PrototypeAccountTransferControl {#PrototypeAccountTransferControl}
*Defined in [fuchsia.identity.prototype/account_transfer_prototype.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/identity/fidl/account_transfer_prototype.fidl#17)*

 A temporary control interface exposed by Account Manager for prototyping.
 Once the functionality is ready to be brought out of prototype stage this
 protocol will be removed and its methods will be moved to the
 AccountManager interface.  This interface is intended only for use by
 development tools to manually initiate an account transfer, and should
 generally not be used.

### TransferAccount {#TransferAccount}

 Provisions an account on the current device onto another device.

 `account_id` The local id of the account to transfer.
 `target_device` The device on which the account should be provisioned,
                 identified using an Overnet NodeId.
 `target_lifetime` The lifetime the account should have on the target
                   device

 Returns successfully if the account is provisioned on the remote device
 successfully.  Fails with an UNSUPPORTED_OPERATION error if the account
 is already present on the remote device.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>account_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>target_device</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/'>fuchsia.overnet.protocol</a>/<a class='link' href='../fuchsia.overnet.protocol/#NodeId'>NodeId</a></code>
            </td>
        </tr><tr>
            <td><code>target_lifetime</code></td>
            <td>
                <code><a class='link' href='../fuchsia.identity.account/'>fuchsia.identity.account</a>/<a class='link' href='../fuchsia.identity.account/#Lifetime'>Lifetime</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#PrototypeAccountTransferControl_TransferAccount_Result'>PrototypeAccountTransferControl_TransferAccount_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### PrototypeAccountTransferControl_TransferAccount_Response {#PrototypeAccountTransferControl_TransferAccount_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>







## **UNIONS**

### PrototypeAccountTransferControl_TransferAccount_Result {#PrototypeAccountTransferControl_TransferAccount_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#PrototypeAccountTransferControl_TransferAccount_Response'>PrototypeAccountTransferControl_TransferAccount_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.identity.account/'>fuchsia.identity.account</a>/<a class='link' href='../fuchsia.identity.account/#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>







