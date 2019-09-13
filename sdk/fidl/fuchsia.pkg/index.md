Project: /_project.yaml
Book: /_book.yaml

# fuchsia.pkg


## **PROTOCOLS**

## PackageResolverAdmin {:#PackageResolverAdmin}
*Defined in [fuchsia.pkg/admin.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/admin.fidl#9)*

 Configures a package resolver.

### SetExperimentState {:#SetExperimentState}

 Sets an experiment toggle to a specific state (on or off).

 Experiment states are not persisted and apply only while the resolver
 is running.

 + request `experiment_id` the experiment to enable or disable.
 + request `state` the state the experimnet should be set to.
 * error a zx.status value indicating success or failure.
     Fails with `ZX_ERR_INVALID_ARGS if the experiment is unknown
     to the resolver.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>experiment_id</code></td>
            <td>
                <code><a class='link' href='#ExperimentToggle'>ExperimentToggle</a></code>
            </td>
        </tr><tr>
            <td><code>state</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## PackageCache {:#PackageCache}
*Defined in [fuchsia.pkg/cache.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/cache.fidl#15)*

 Manages the system package cache.

 This interface is intended to be implemented by the package manager component and used by
 package resolver components.

### Get {:#Get}

 Gets the package directory if it is present on the local system. If it is not, the
 `missing_blobs` iterator will provide all the blobs in the package that are missing from
 the system, and the ability to write those blobs to blobfs. If all the missing blobs are
 downloaded and written to by the client, the `dir` directory will be resolved. This method
 will return `ZX_OK` when the package has been fully resolved, or an error if the client
 closes `needed_blobs` or `dir` handle before the package has been resolved.

 Arguments:
 * `meta_far_blob` is the blob info for the package's meta.far.
 * `selectors` are the package selectors (TODO: link to docs).
 * `needed_blobs` is an iterator over all the blobs in the package that
   are not present on the system.
 * `dir` is an optional request for a directory that will be resolved when the package has
   been successfully cached.

 Return Values:
 * `ZX_OK` if the package was successfully cached.
 * `ZX_ERR_UNAVAILABLE` if the client closed `needed_blobs` or `dir` handles before the
   all the missing blobs were downloaded to the system.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>meta_far_blob</code></td>
            <td>
                <code><a class='link' href='#BlobInfo'>BlobInfo</a></code>
            </td>
        </tr><tr>
            <td><code>selectors</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr><tr>
            <td><code>needed_blobs</code></td>
            <td>
                <code>request&lt;<a class='link' href='#NeededBlobs'>NeededBlobs</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>dir</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.io/index.html'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/index.html#Directory'>Directory</a>&gt;?</code>
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
        </tr></table>

### Open {:#Open}

 Opens the package, or error out if it is not present on the local system.

 Arguments:
 * `meta_far_blob_id` is the blob id for the package's meta.far.
 * `selectors` are the package selectors (TODO: link to docs).
 * `dir` is a request for a directory that will be resolved when the package has been
   successfully cached.

 Return Values:
 * `ZX_OK` if the package was successfully opened.
 * `ZX_ERR_NOT_FOUND` if the package does not exist.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>meta_far_blob_id</code></td>
            <td>
                <code><a class='link' href='#BlobId'>BlobId</a></code>
            </td>
        </tr><tr>
            <td><code>selectors</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr><tr>
            <td><code>dir</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.io/index.html'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/index.html#Directory'>Directory</a>&gt;</code>
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
        </tr></table>

## NeededBlobs {:#NeededBlobs}
*Defined in [fuchsia.pkg/cache.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/cache.fidl#63)*

 The `NeededBlobs` is an abstract interface that is provided by a `PackageCache` to the
 `PackageResolver` to fetch one or more blobs that are not present on the local system for a
 given package.

### GetMissingBlobs {:#GetMissingBlobs}

 Returns a vector of blobs that are not present on the system that must be downloaded and
 written to blobfs with the `Open` method before a package can be resolved. This method
 should continue to be called until it returns an empty vector. This signifies all the
 missing blobs have been successfully downloaded.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>blobs</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#BlobInfo'>BlobInfo</a>&gt;</code>
            </td>
        </tr></table>

### Open {:#Open}

 Open a blob for writing.

 Arguments:
 * `blob_id` is the blob id describing this blob.
 * `file` resolves to an opened writable file must be truncated to the correct size by the
   caller.

 Return Values:
 * `ZX_OK` if successful.
 * `ZX_ERR_ACCESS_DENIED` if the package does not contain this blob.
 * `ZX_ERR_IO` if there is some other unspecified error during I/O.
 * `ZX_ERR_NO_SPACE` if there is no space available to store the package.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>blob_id</code></td>
            <td>
                <code><a class='link' href='#BlobId'>BlobId</a></code>
            </td>
        </tr><tr>
            <td><code>file</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.io/index.html'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/index.html#File'>File</a>&gt;</code>
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
        </tr></table>

## FontResolver {:#FontResolver}
*Defined in [fuchsia.pkg/font_resolver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/font_resolver.fidl#19)*

 Resolves font packages from a registry.

 This interface is intended to be implemented by package resolver components, and used
 exclusively by fuchsia.fonts.Provider.

 DEPRECATED. This is an interim solution, and will be revisited when Component Framework v2
 becomes available and allows non-component packages and easier directory routing.

### Resolve {:#Resolve}

 Populates or updates the cache of a font package, fetching it if it is not present on the
 local system.

 + request `package_url` The package URL of a font package.
 + request `directory_request` Request for a directory that will be resolved when the package
   has been successfully cached. The directory should contain a single file, corresponding to
   the asset filename. The client should retain the directory handle for as long as needed to
   prevent the package from being evicted from cache.

 - response `status` Outcome of the request.
   * `ZX_OK` if the package was successfully opened.
   * `ZX_ERR_ACCESS_DENIED` if the resolver does not have permission to fetch a package blob.
   * `ZX_ERR_IO` if there is some other unspecified error during I/O.
   * `ZX_ERR_NOT_FOUND` if the font package or a package blob does not exist, or is not known
     to be a font package.
   * `ZX_ERR_NO_SPACE` if there is no space available to store the package.
   * `ZX_ERR_UNAVAILABLE` if the resolver is currently unable to fetch a package blob.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>package_url</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>directory_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.io/index.html'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/index.html#Directory'>Directory</a>&gt;</code>
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
        </tr></table>

## RepositoryManager {:#RepositoryManager}
*Defined in [fuchsia.pkg/repo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/repo.fidl#14)*

 Manages package repositories.

 This interface is intended to be implemented by package resolver components, and used by
 repository administration tools.

### Add {:#Add}

 Add a repository. This will overwrite the repository if it already exists.

 Arguments:
 * `repo` is repository to add to the resolver.

 Return Values:
 * `ZX_OK` if the repository was added.
 * `ZX_ERR_ALREADY_EXISTS` if the repository already exists.
 * `ZX_ERR_INVALID_ARGS` if the repository is malformed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>repo</code></td>
            <td>
                <code><a class='link' href='#RepositoryConfig'>RepositoryConfig</a></code>
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
        </tr></table>

### Remove {:#Remove}

 Remove a repository.

 Removing a repository will prevent future packages from being cached from this repository,
 but in-flight downloads may not be interrupted.

 Arguments:
 * `repo_url` is the URL of the repository we want to remove.

 Return Values:
 * Returns `ZX_OK` if the repository was removed.
 * Returns `ZX_ERR_INVALID_ARGS` if the `repo_url` is malformed.
 * Returns `ZX_ERR_NOT_FOUND` if the repository does not exist.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>repo_url</code></td>
            <td>
                <code>string</code>
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
        </tr></table>

### AddMirror {:#AddMirror}

 Add a mirror to a repository. This will overwrite the mirror if it already exists.

 Arguments:
 * `repo_url` is repository that corresponds with this mirror.
 * `mirror_url` is mirror URL to add to the resolver.

 Return Values:
 * `ZX_OK` if the mirror was removed.
 * `ZX_ERR_ALREADY_EXISTS` if the mirror for this repository already exists.
 * `ZX_ERR_INVALID_ARGS` if the `repo_url` or the `mirror` is malformed.
 * `ZX_ERR_NOT_FOUND` if the repository does not exist.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>repo_url</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>mirror</code></td>
            <td>
                <code><a class='link' href='#MirrorConfig'>MirrorConfig</a></code>
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
        </tr></table>

### RemoveMirror {:#RemoveMirror}

 Remove a mirror from a repository.

 Removing a mirror will prevent future packages from being cached from that mirror, but
 in-flight downloads may not be interrupted.

 Arguments:
 * `repo_url` the URL of the mirror's repository.
 * `mirror_url` the URL of the mirror we want to remove.

 Return Values:
 * `ZX_OK` if the mirror was removed.
 * `ZX_ERR_INVALID_ARGS` if the `repo_url` or the `mirror_url` is malformed.
 * `ZX_ERR_NOT_FOUND` if the repository or mirror does not exist.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>repo_url</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>mirror_url</code></td>
            <td>
                <code>string</code>
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
        </tr></table>

### List {:#List}

 Return an iterator over all repositories.

 Arguments:
 `iterator` is a request for an iterator.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>iterator</code></td>
            <td>
                <code>request&lt;<a class='link' href='#RepositoryIterator'>RepositoryIterator</a>&gt;</code>
            </td>
        </tr></table>



## RepositoryIterator {:#RepositoryIterator}
*Defined in [fuchsia.pkg/repo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/repo.fidl#129)*

 The iterator over all the repositories defined in a `PackageResolver`.

### Next {:#Next}

 Advance the iterator and return the next batch of repositories.

 Return Values:
 * a vector of `RepositoryConfig` repositories. Will return an empty vector when there are
   no more repositories.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>repos</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#RepositoryConfig'>RepositoryConfig</a>&gt;</code>
            </td>
        </tr></table>

## PackageResolver {:#PackageResolver}
*Defined in [fuchsia.pkg/resolver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/resolver.fidl#15)*

 Resolves packages from a registry.

 This interface is intended to be implemented by package resolver components, and used by
 repository administration tools.

### Resolve {:#Resolve}

 Populates or updates the cache of a package with the given selectors as specified by the
 update policy.

 Ensures that a package is on the local filesystem.

 Arguments:
 * `package_url` The package URL for a package (TODO: link to docs).
 * `selectors` are the package selectors (TODO: link to docs).
 * `dir` is a request for a directory that will be resolved when the package has been
   successfully cached.

 Return Values:
 * `ZX_OK` if the package was successfully opened.
 * `ZX_ERR_ACCESS_DENIED` if the resolver does not have permission to fetch a package blob.
 * `ZX_ERR_IO` if there is some other unspecified error during I/O.
 * `ZX_ERR_NOT_FOUND` if the package or a package blob does not exist.
 * `ZX_ERR_NO_SPACE` if there is no space available to store the package.
 * `ZX_ERR_UNAVAILABLE` if the resolver is currently unable to fetch a package blob.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>package_url</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>selectors</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr><tr>
            <td><code>update_policy</code></td>
            <td>
                <code><a class='link' href='#UpdatePolicy'>UpdatePolicy</a></code>
            </td>
        </tr><tr>
            <td><code>dir</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.io/index.html'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/index.html#Directory'>Directory</a>&gt;</code>
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
        </tr></table>

## SystemBlobAdmin {:#SystemBlobAdmin}
*Defined in [fuchsia.pkg/system_blob_admin.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/system_blob_admin.fidl#10)*

 Administrates the critical system blobs on the system.

### ReleaseRetainedBlobs {:#ReleaseRetainedBlobs}

 Allows blobs from old system versions to be garbage collected. The current system blobs
 will not be collected.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### RetainBlobs {:#RetainBlobs}

 Adds the blobs listed in the `retention_index` blob to the retention list. This should be
 called during a system upgrade with the new system blob in order to make sure they are not
 garbage collected before the upgrade completes.

 Arguments:
 * `retention_index` is the blob id for a list of blobs to retain.

 Return Values:
 * `ZX_OK` if the blobs were successfully retained.
 * `ZX_ERR_IO` if there is some other unspecified error during I/O.
 * `ZX_ERR_NOT_FOUND` if the `retention_index` could not be found on the local system.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>retention_index</code></td>
            <td>
                <code><a class='link' href='#BlobId'>BlobId</a></code>
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
        </tr></table>



## **STRUCTS**

### BlobId {:#BlobId}
*Defined in [fuchsia.pkg/common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/common.fidl#9)*



 BlobId is a content-addressed merkle root that describes an artifact that is tracked by the
 packaging system.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>merkle_root</code></td>
            <td>
                <code>uint8[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### BlobInfo {:#BlobInfo}
*Defined in [fuchsia.pkg/common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/common.fidl#15)*



 BlobInfo is a tuple of the content-addressed merkle root for an artifact, along with that
 artifact's length in bytes.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>blob_id</code></td>
            <td>
                <code><a class='link' href='#BlobId'>BlobId</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>length</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### UpdatePolicy {:#UpdatePolicy}
*Defined in [fuchsia.pkg/resolver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/resolver.fidl#44)*



 The `UpdatePolicy` provides different policies to be used when the `PackageResolver` is
 fetching packages.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>fetch_if_absent</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Should the resolver fetch the package if it is not present on the local system.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>allow_old_versions</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Should the resolver allow old versions of the package to be used.
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### ExperimentToggle {:#ExperimentToggle}
Type: <code>uint64</code>

*Defined in [fuchsia.pkg/admin.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/admin.fidl#24)*

 List of known experiment toggles


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>LIGHTBULB</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>DOWNLOAD_BLOB</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### RepositoryConfig {:#RepositoryConfig}


*Defined in [fuchsia.pkg/repo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/repo.fidl#76)*

 Describes the configuration necessary to connect to a repository and it's mirrors.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>repo_url</code></td>
            <td>
                <code>string</code>
            </td>
            <td> A fuchsia-pkg URL identifying the repository. Required.

 Example: fuchsia-pkg://example.com/
</td>
        </tr><tr>
            <td>2</td>
            <td><code>root_keys</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#RepositoryKeyConfig'>RepositoryKeyConfig</a>&gt;</code>
            </td>
            <td> A vector of public keys. Required.

 These keys must match one of the trusted keys known to the system.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>mirrors</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#MirrorConfig'>MirrorConfig</a>&gt;</code>
            </td>
            <td> The repository mirrors that serve the package contents. Required.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>update_package_url</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The package URL of the system update package. Optional.

 Only used for the fuchsia-pkg://fuchsia.com/ repo.
</td>
        </tr></table>

### MirrorConfig {:#MirrorConfig}


*Defined in [fuchsia.pkg/repo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/repo.fidl#113)*

 Describes the configuration necessary to connect to a mirror.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>mirror_url</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The base URL of the TUF metadata on this mirror. Required.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>subscribe</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Whether or not to automatically monitor the mirror for updates. Required.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>blob_key</code></td>
            <td>
                <code><a class='link' href='#RepositoryBlobKey'>RepositoryBlobKey</a></code>
            </td>
            <td> The private (or symmetric) key used to decrypt blobs fetched from this mirror. Optional.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>blob_mirror_url</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The URL where blobs from this mirror should be fetched.  Optional.
 Defaults to `mirror_url + "/blobs"`.
</td>
        </tr></table>





## **XUNIONS**

### RepositoryKeyConfig {:#RepositoryKeyConfig}
*Defined in [fuchsia.pkg/repo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/repo.fidl#99)*

 Describes the keys used by the repository to authenticate it's packages.

 The only supported algorithm at the moment is ed25519.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>ed25519_key</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td> The raw ed25519 public key as binary data.
</td>
        </tr></table>

### RepositoryBlobKey {:#RepositoryBlobKey}
*Defined in [fuchsia.pkg/repo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/repo.fidl#107)*

 Describes a key used to decrypt blobs.

 The only supported algorithm at the moment is aes.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>aes_key</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td> A raw aes key as binary data.
</td>
        </tr></table>





