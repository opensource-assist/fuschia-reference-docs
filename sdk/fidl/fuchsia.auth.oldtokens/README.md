[TOC]

# fuchsia.auth.oldtokens


## **PROTOCOLS**

## CredentialsProducer {#CredentialsProducer}
*Defined in [fuchsia.auth.oldtokens/credentials_producer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.auth.oldtokens/credentials_producer.fidl#25)*

 Clients can connect to this protocol to subscribe to changes in the set of
 users linked to this device, as well as the OAuth2 access token associated
 with each.

 This protocol won't be supported on the majority of devices, and shouldn't
 be used without permission from its maintainers.

### GetUpdatedCredentials {#GetUpdatedCredentials}

 Get the set of users linked to this device, and their corresponding access
 tokens. While the connection to the service remains uninterrumpted, the
 method call hangs if it would return the same response as the previous
 time it was called by this client. In other words, if the client already
 has the most up-to-date credentials, the method acts as a hanging get and
 only returns when there's an update to report.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>credentials</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Credential'>Credential</a>&gt;</code>
            </td>
        </tr></table>







## **TABLES**

### Credential {#Credential}


*Defined in [fuchsia.auth.oldtokens/credentials_producer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.auth.oldtokens/credentials_producer.fidl#9)*

 The id of a user linked to this device, alongside the current access token
 to make requests on the user's behalf.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>user_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Opaque id for the user with which this credential is associated. It is
 stable across reconnections to the CredentialsProducer protocol.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>access_token</code></td>
            <td>
                <code>string</code>
            </td>
            <td> OAuth2 access token for this user.
</td>
        </tr></table>









