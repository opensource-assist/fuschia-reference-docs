[TOC]

# fuchsia.amber


## **PROTOCOLS**

## Control {#Control}
*Defined in [fuchsia.amber/amber.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.amber/amber.fidl#141)*


### DoTest {#DoTest}

 simple no-op that can be used to test the connection

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>input</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>output</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

### AddSrc {#AddSrc}

 Add a TUF source repository.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#SourceConfig'>SourceConfig</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>res</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

### RemoveSrc {#RemoveSrc}

 Remove a TUF source repository. SourceConfigs that were bundled when the
 system was built may be removed, but that funcionality may change in the
 future. See PKG-150.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>res</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>

### ListSrcs {#ListSrcs}

 Get the list of URLs of the current set of sources

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>srcs</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#SourceConfig'>SourceConfig</a>&gt;</code>
            </td>
        </tr></table>

### GetBlob {#GetBlob}

 Get a content blob identified by the given hashed Merkle root.
 This operation is asynchronous and provides no results.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>merkle</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### PackagesActivated {#PackagesActivated}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>merkle</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr></table>



### GetUpdateComplete {#GetUpdateComplete}

 Get an update for the package identified by 'name' which has the
 provided version. If no version is supplied, the latest available
 version of that package will be retrieved. The package data is sent to
 PackageFS which then stores the package in BlobFS. This method returns
 a channel that will provide the ultimate results. The channel will become
 readable when the update is complete. If at that time the User0 signal is
 set on the channel, the result is an error string that may be read from
 the channel, otherwise the result is success, and the new merkleroot can
 be read from the channel.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>version</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr><tr>
            <td><code>merkle</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rplyChan</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>

### CheckForSystemUpdate {#CheckForSystemUpdate}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>res</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

### Login {#Login}

 Log into the source specified by the source id. Returns the oauth2
 device flow code if the source is configured for authentication, or null
 if not.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>sourceId</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device</code></td>
            <td>
                <code><a class='link' href='#DeviceCode'>DeviceCode</a>?</code>
            </td>
        </tr></table>

### SetSrcEnabled {#SetSrcEnabled}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>enabled</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>res</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>

### GC {#GC}

 Trigger a garbage collection.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### PackagesFailed {#PackagesFailed}

 Sent when a blob fails to write, causing one or more package installs to
 permanently fail.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>merkle</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>blob_merkle</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### OpenRepository {#OpenRepository}

 Opens a TUF repository specified by the provided RepositoryConfig.
 The repository will stay open for the life of the OpenedRepository
 channel.

 Packages in the opened repository can be accessed via
 OpenedRepository.GetUpdateComplete, but will not appear in calls to
 the global GetUpdateComplete, above.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.pkg/'>fuchsia.pkg</a>/<a class='link' href='../fuchsia.pkg/#RepositoryConfig'>RepositoryConfig</a></code>
            </td>
        </tr><tr>
            <td><code>repo</code></td>
            <td>
                <code>request&lt;<a class='link' href='#OpenedRepository'>OpenedRepository</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

## OpenedRepository {#OpenedRepository}
*Defined in [fuchsia.amber/amber.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.amber/amber.fidl#200)*


### GetUpdateComplete {#GetUpdateComplete}

 Get an update for the package identified by 'name' which has the
 provided variant. The package data is sent to PackageFS which then
 stores the package in BlobFS. This method provides a FetchResult that
 will send the ultimate results.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>variant</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr><tr>
            <td><code>merkle</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr><tr>
            <td><code>result</code></td>
            <td>
                <code>request&lt;<a class='link' href='#FetchResult'>FetchResult</a>&gt;</code>
            </td>
        </tr></table>



### MerkleFor {#MerkleFor}

 Finds the merkle hash for the package identified by 'name' which has the
 provided variant. Does not install the package or fetch any blobs.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>variant</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>message</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>merkle</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>size</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>

## FetchResult {#FetchResult}
*Defined in [fuchsia.amber/amber.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.amber/amber.fidl#214)*

 A protocol providing results for a OpenedRepository.GetUpdateComplete call.
 Only one event will be sent before the channel is closed.

### OnSuccess {#OnSuccess}

 Sent when the package is successfully installed and available for use.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>merkle</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

### OnError {#OnError}

 Sent when the package fails to install for some reason.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>message</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



## **STRUCTS**

### OAuth2Config {#OAuth2Config}
*Defined in [fuchsia.amber/amber.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.amber/amber.fidl#10)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>clientId</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>clientSecret</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>string</td>
        </tr><tr>
            <td><code>authUrl</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>tokenUrl</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>scopes</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>deviceCodeUrl</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DeviceCode {#DeviceCode}
*Defined in [fuchsia.amber/amber.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.amber/amber.fidl#21)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>userCode</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>verificationUrl</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>expiresIn</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### KeyConfig {#KeyConfig}
*Defined in [fuchsia.amber/amber.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.amber/amber.fidl#27)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>type</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Supported TUF key types. The only supported algorithm is ed25519.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The value of the key encoded in hex.
</td>
            <td>No default</td>
        </tr>
</table>

### TLSClientConfig {#TLSClientConfig}
*Defined in [fuchsia.amber/amber.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.amber/amber.fidl#35)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>insecureSkipVerify</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If insecureSkipTlsVerify is true, TLS will accept any certificate
 provided by the server. This should only be used for testing.
</td>
            <td>false</td>
        </tr><tr>
            <td><code>rootCAs</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td> The set of root certificate authorities that clients use when verifying
 server certificates. If the list is empty, TLS uses the host's root CA
 set.
</td>
            <td>No default</td>
        </tr>
</table>

### TransportConfig {#TransportConfig}
*Defined in [fuchsia.amber/amber.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.amber/amber.fidl#46)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>disableKeepAlives</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, prevent re-use of TCP connections between HTTP requests.
</td>
            <td>false</td>
        </tr><tr>
            <td><code>KeepAlive</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The keep-alive period for an active network connection. A zero value
 means that we use the system default.
</td>
            <td>0</td>
        </tr><tr>
            <td><code>maxIdleConns</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The maximum number of idle (keep-alive) connections across all hosts. A
 zero value means that we use the system default.
</td>
            <td>0</td>
        </tr><tr>
            <td><code>maxIdleConnsPerHost</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The maximum number of idle (keep-alive) connections across for each
 host. A zero value means we use the system default.
</td>
            <td>0</td>
        </tr><tr>
            <td><code>connectTimeout</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The maximum amount of time to wait for a connection to complete in
 milliseconds. A zero value means we use the system default.
</td>
            <td>0</td>
        </tr><tr>
            <td><code>requestTimeout</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The deadline in milliseconds for a request to complete. A zero value
 means that we use the system default.
</td>
            <td>0</td>
        </tr><tr>
            <td><code>idleConnTimeout</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The maximum amount of time in milliseconds an idle (keep-alive)
 connection will remain idle before closing itself. A zero value means
 that we use the system default.
</td>
            <td>0</td>
        </tr><tr>
            <td><code>responseHeaderTimeout</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The amount of time to wait for a server's response headers. A zero value
 means that we use the system default.
</td>
            <td>0</td>
        </tr><tr>
            <td><code>expectContinueTimeout</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The deadline in milliseconds to wait for a server's first response
 headers if the request has an "Expect: 100-continue" header. A zero
 value means that we use the system default.
</td>
            <td>0</td>
        </tr><tr>
            <td><code>tlsHandshakeTimeout</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The deadline in milliseconds to wait for a TLS handshake. Zero means that we use the system
 default.
</td>
            <td>0</td>
        </tr><tr>
            <td><code>tlsClientConfig</code></td>
            <td>
                <code><a class='link' href='#TLSClientConfig'>TLSClientConfig</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StatusConfig {#StatusConfig}
*Defined in [fuchsia.amber/amber.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.amber/amber.fidl#91)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>enabled</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SourceConfig {#SourceConfig}
*Defined in [fuchsia.amber/amber.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.amber/amber.fidl#95)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>string</code>
            </td>
            <td> A unique identifier that distinquishes this source from others.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>repoUrl</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The canonical URL for the TUF repository.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>blobRepoUrl</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Optionally download package blobs from this repository. If not
 specified, blobs will be fetched from `$repoUrl/blobs`.
</td>
            <td>string</td>
        </tr><tr>
            <td><code>rateLimit</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The rate limit indicates the number of requests per rateReriod,
 expressed in milliseconds. A limit or period of zero means there is no
 limit.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>ratePeriod</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The TUF metadata will be refreshed after it is ratePeriod seconds stale.
</td>
            <td>3600</td>
        </tr><tr>
            <td><code>rootKeys</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#KeyConfig'>KeyConfig</a>&gt;</code>
            </td>
            <td> A vector of public keys. These keys must match one of the trusted keys
 known to the system.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>transportConfig</code></td>
            <td>
                <code><a class='link' href='#TransportConfig'>TransportConfig</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>oauth2Config</code></td>
            <td>
                <code><a class='link' href='#OAuth2Config'>OAuth2Config</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>statusConfig</code></td>
            <td>
                <code><a class='link' href='#StatusConfig'>StatusConfig</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>auto</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, the source supports the /auto SSE endpoint for live updates
</td>
            <td>false</td>
        </tr><tr>
            <td><code>blobKey</code></td>
            <td>
                <code><a class='link' href='#BlobEncryptionKey'>BlobEncryptionKey</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### BlobEncryptionKey {#BlobEncryptionKey}
*Defined in [fuchsia.amber/amber.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.amber/amber.fidl#130)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>data</code></td>
            <td>
                <code>uint8[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### Status {#Status}
Type: <code>uint32</code>

*Defined in [fuchsia.amber/amber.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.amber/amber.fidl#134)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OK</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERR</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERR_NOT_FOUND</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>











