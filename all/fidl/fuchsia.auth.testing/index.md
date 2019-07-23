Project: /_project.yaml
Book: /_book.yaml

# fuchsia.auth.testing


## **PROTOCOLS**

## LegacyAuthCredentialInjector {:#LegacyAuthCredentialInjector}
*Defined in [fuchsia.auth.testing/legacy_auth_credential_injector.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.auth.testing/legacy_auth_credential_injector.fidl#13)*

 This interface is intended as an additional interface implemented by an
 AuthProvider.  It allows a test component to inject persistent credentials
 into the AuthProvider.  This interface is intended as a short term solution
 to enable end-to-end testing only and should not be generally used.

### InjectPersistentCredential {:#InjectPersistentCredential}

 Injects a persistent credential to the AuthProvider.  This API should
 only be called while there is an ongoing call to the AuthProvider's
 GetPersistentCredential method.  Calling this causes
 GetPersistentCredential to return the supplied credential and
 UserProfileInfo.  It additionally stops the UI overlay started by
 AuthProvider as part of the normal process for obtaining the credential.

 `user_profile_info` should be information such as user id expected to
 be returned by the external identity provider when authenticating.
 `credential` should be a persistent credential provided by the external
 identity provider called by the AuthProvider.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>user_profile_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.auth/index.html'>fuchsia.auth</a>/<a class='link' href='../fuchsia.auth/index.html#UserProfileInfo'>UserProfileInfo</a>?</code>
            </td>
        </tr><tr>
            <td><code>credential</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

















