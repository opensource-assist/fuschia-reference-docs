[TOC]

# fuchsia.factory


## **PROTOCOLS**

## FactoryStoreProvider {#FactoryStoreProvider}
*Defined in [fuchsia.factory/factory.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.factory/factory.fidl#19)*

 This protocol is a base protocol for all providers of factory store
 directories. It exposes a single method to allow clients to establish a
 connection to a directory containing the relevant factory data. All files
 surfaced by a component that implements FactoryStoreProvider (or any
 protocol that depends on it) are expected to be validated for consistency
 before being exposed to clients.

### GetFactoryStore {#GetFactoryStore}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>dir</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#Directory'>Directory</a>&gt;</code>
            </td>
        </tr></table>



## CastCredentialsFactoryStoreProvider {#CastCredentialsFactoryStoreProvider}
*Defined in [fuchsia.factory/factory.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.factory/factory.fidl#27)*

 This protocol exposes a method to connect to a directory containing
 Cast-specific factory data: public certificates and keys for
 authentication with Cast servers.

### GetFactoryStore {#GetFactoryStore}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>dir</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#Directory'>Directory</a>&gt;</code>
            </td>
        </tr></table>



## WidevineFactoryStoreProvider {#WidevineFactoryStoreProvider}
*Defined in [fuchsia.factory/factory.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.factory/factory.fidl#35)*

 This protocol exposes a method to connect to a directory containing
 Widevine-specific factory data: public certificates and keys for
 authentication with Widevine systems.

### GetFactoryStore {#GetFactoryStore}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>dir</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#Directory'>Directory</a>&gt;</code>
            </td>
        </tr></table>



## PlayReadyFactoryStoreProvider {#PlayReadyFactoryStoreProvider}
*Defined in [fuchsia.factory/factory.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.factory/factory.fidl#43)*

 This protocol exposes a method to connect to a directory containing
 PlayReady-specific factory data: public certificates and keys for
 authentication with PlayReady systems.

### GetFactoryStore {#GetFactoryStore}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>dir</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#Directory'>Directory</a>&gt;</code>
            </td>
        </tr></table>



## MiscFactoryStoreProvider {#MiscFactoryStoreProvider}
*Defined in [fuchsia.factory/factory.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.factory/factory.fidl#53)*

 This protocol exposes a method to connect to a directory containing
 miscellaneous factory data such as tuning/calibration files, region-specific
 audio files, factory process metadata files, and more. Any raw files not
 covered by other FactoryStoreProviders or methods in fuchsia.hwinfo will
 appear here.

### GetFactoryStore {#GetFactoryStore}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>dir</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#Directory'>Directory</a>&gt;</code>
            </td>
        </tr></table>

















