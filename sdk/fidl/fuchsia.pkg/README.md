[TOC]

# fuchsia.pkg


## **PROTOCOLS**

## PackageResolverAdmin {#PackageResolverAdmin}
*Defined in [fuchsia.pkg/admin.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/admin.fidl#9)*

<p>Configures a package resolver.</p>

### SetExperimentState {#SetExperimentState}

<p>Sets an experiment toggle to a specific state (on or off).</p>
<p>Experiment states are not persisted and apply only while the resolver
is running.</p>
<ul>
<li>request <code>experiment_id</code> the experiment to enable or disable.</li>
<li>request <code>state</code> the state the experimnet should be set to.</li>
</ul>
<ul>
<li>error a zx.status value indicating success or failure.
Fails with `ZX_ERR_INVALID_ARGS if the experiment is unknown
to the resolver.</li>
</ul>

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

## PackageCache {#PackageCache}
*Defined in [fuchsia.pkg/cache.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/cache.fidl#15)*

<p>Manages the system package cache.</p>
<p>This interface is intended to be implemented by the package manager component and used by
package resolver components.</p>

### Get {#Get}

<p>Gets the package directory if it is present on the local system. If it is not, the
<code>missing_blobs</code> iterator will provide all the blobs in the package that are missing from
the system, and the ability to write those blobs to blobfs. If all the missing blobs are
downloaded and written to by the client, the <code>dir</code> directory will be resolved. This method
will return <code>ZX_OK</code> when the package has been fully resolved, or an error if the client
closes <code>needed_blobs</code> or <code>dir</code> handle before the package has been resolved.</p>
<p>Arguments:</p>
<ul>
<li><code>meta_far_blob</code> is the blob info for the package's meta.far.</li>
<li><code>selectors</code> are the package selectors (TODO: link to docs).</li>
<li><code>needed_blobs</code> is an iterator over all the blobs in the package that
are not present on the system.</li>
<li><code>dir</code> is an optional request for a directory that will be resolved when the package has
been successfully cached.</li>
</ul>
<p>Return Values:</p>
<ul>
<li><code>ZX_OK</code> if the package was successfully cached.</li>
<li><code>ZX_ERR_UNAVAILABLE</code> if the client closed <code>needed_blobs</code> or <code>dir</code> handles before the
all the missing blobs were downloaded to the system.</li>
</ul>

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
                <code>request&lt;<a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#Directory'>Directory</a>&gt;?</code>
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

### Open {#Open}

<p>Opens the package, or error out if it is not present on the local system.</p>
<p>Arguments:</p>
<ul>
<li><code>meta_far_blob_id</code> is the blob id for the package's meta.far.</li>
<li><code>selectors</code> are the package selectors (TODO: link to docs).</li>
<li><code>dir</code> is a request for a directory that will be resolved when the package has been
successfully cached.</li>
</ul>
<p>Return Values:</p>
<ul>
<li><code>ZX_OK</code> if the package was successfully opened.</li>
<li><code>ZX_ERR_NOT_FOUND</code> if the package does not exist.</li>
</ul>

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
                <code>request&lt;<a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#Directory'>Directory</a>&gt;</code>
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

## NeededBlobs {#NeededBlobs}
*Defined in [fuchsia.pkg/cache.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/cache.fidl#63)*

<p>The <code>NeededBlobs</code> is an abstract interface that is provided by a <code>PackageCache</code> to the
<code>PackageResolver</code> to fetch one or more blobs that are not present on the local system for a
given package.</p>

### GetMissingBlobs {#GetMissingBlobs}

<p>Returns a vector of blobs that are not present on the system that must be downloaded and
written to blobfs with the <code>Open</code> method before a package can be resolved. This method
should continue to be called until it returns an empty vector. This signifies all the
missing blobs have been successfully downloaded.</p>

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

### Open {#Open}

<p>Open a blob for writing.</p>
<p>Arguments:</p>
<ul>
<li><code>blob_id</code> is the blob id describing this blob.</li>
<li><code>file</code> resolves to an opened writable file must be truncated to the correct size by the
caller.</li>
</ul>
<p>Return Values:</p>
<ul>
<li><code>ZX_OK</code> if successful.</li>
<li><code>ZX_ERR_ACCESS_DENIED</code> if the package does not contain this blob.</li>
<li><code>ZX_ERR_IO</code> if there is some other unspecified error during I/O.</li>
<li><code>ZX_ERR_NO_SPACE</code> if there is no space available to store the package.</li>
</ul>

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
                <code>request&lt;<a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#File'>File</a>&gt;</code>
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

## FontResolver {#FontResolver}
*Defined in [fuchsia.pkg/font_resolver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/font_resolver.fidl#19)*

<p>Resolves font packages from a registry.</p>
<p>This interface is intended to be implemented by package resolver components, and used
exclusively by fuchsia.fonts.Provider.</p>
<p>DEPRECATED. This is an interim solution, and will be revisited when Component Framework v2
becomes available and allows non-component packages and easier directory routing.</p>

### Resolve {#Resolve}

<p>Populates or updates the cache of a font package, fetching it if it is not present on the
local system.</p>
<ul>
<li>request <code>package_url</code> The package URL of a font package.</li>
<li>request <code>update_policy</code> Freshness and caching policies to be used when the
<code>FontResolver</code> is fetching packages.</li>
<li>request <code>directory_request</code> Request for a directory that will be resolved when the package
has been successfully cached. The directory should contain a single file, corresponding to
the asset filename. The client should retain the directory handle for as long as needed to
prevent the package from being evicted from cache.</li>
</ul>
<ul>
<li>response <code>status</code> Outcome of the request.
<ul>
<li><code>ZX_OK</code> if the package was successfully opened.</li>
<li><code>ZX_ERR_ACCESS_DENIED</code> if the resolver does not have permission to fetch a package blob.</li>
<li><code>ZX_ERR_IO</code> if there is some other unspecified error during I/O.</li>
<li><code>ZX_ERR_NOT_FOUND</code> if the font package or a package blob does not exist, or is not known
to be a font package.</li>
<li><code>ZX_ERR_NO_SPACE</code> if there is no space available to store the package.</li>
<li><code>ZX_ERR_UNAVAILABLE</code> if the resolver is currently unable to fetch a package blob.</li>
</ul>
</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>package_url</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>update_policy</code></td>
            <td>
                <code><a class='link' href='#UpdatePolicy'>UpdatePolicy</a></code>
            </td>
        </tr><tr>
            <td><code>directory_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#Directory'>Directory</a>&gt;</code>
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

## RepositoryManager {#RepositoryManager}
*Defined in [fuchsia.pkg/repo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/repo.fidl#14)*

<p>Manages package repositories.</p>
<p>This interface is intended to be implemented by package resolver components, and used by
repository administration tools.</p>

### Add {#Add}

<p>Add a repository. This will overwrite the repository if it already exists.</p>
<p>Arguments:</p>
<ul>
<li><code>repo</code> is repository to add to the resolver.</li>
</ul>
<p>Return Values:</p>
<ul>
<li><code>ZX_OK</code> if the repository was added.</li>
<li><code>ZX_ERR_ACCESS_DENIED</code> if editing repositories is permanently disabled.</li>
<li><code>ZX_ERR_ALREADY_EXISTS</code> if the repository already exists.</li>
<li><code>ZX_ERR_INVALID_ARGS</code> if the repository is malformed.</li>
</ul>

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

### Remove {#Remove}

<p>Remove a repository.</p>
<p>Removing a repository will prevent future packages from being cached from this repository,
but in-flight downloads may not be interrupted.</p>
<p>Arguments:</p>
<ul>
<li><code>repo_url</code> is the URL of the repository we want to remove.</li>
</ul>
<p>Return Values:</p>
<ul>
<li><code>ZX_OK</code> if the repository was removed.</li>
<li><code>ZX_ERR_ACCESS_DENIED</code> if editing repositories is permanently disabled or the
<code>repo_url</code> matches a static repository.</li>
<li><code>ZX_ERR_INVALID_ARGS</code> if the <code>repo_url</code> is malformed.</li>
<li><code>ZX_ERR_NOT_FOUND</code> if the repository does not exist.</li>
</ul>

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

### AddMirror {#AddMirror}

<p>Add a mirror to a repository. This will overwrite the mirror if it already exists.</p>
<p>Arguments:</p>
<ul>
<li><code>repo_url</code> is repository that corresponds with this mirror.</li>
<li><code>mirror_url</code> is mirror URL to add to the resolver.</li>
</ul>
<p>Return Values:</p>
<ul>
<li><code>ZX_OK</code> if the mirror was removed.</li>
<li><code>ZX_ERR_ALREADY_EXISTS</code> if the mirror for this repository already exists.</li>
<li><code>ZX_ERR_INVALID_ARGS</code> if the <code>repo_url</code> or the <code>mirror</code> is malformed.</li>
<li><code>ZX_ERR_NOT_FOUND</code> if the repository does not exist.</li>
</ul>

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

### RemoveMirror {#RemoveMirror}

<p>Remove a mirror from a repository.</p>
<p>Removing a mirror will prevent future packages from being cached from that mirror, but
in-flight downloads may not be interrupted.</p>
<p>Arguments:</p>
<ul>
<li><code>repo_url</code> the URL of the mirror's repository.</li>
<li><code>mirror_url</code> the URL of the mirror we want to remove.</li>
</ul>
<p>Return Values:</p>
<ul>
<li><code>ZX_OK</code> if the mirror was removed.</li>
<li><code>ZX_ERR_INVALID_ARGS</code> if the <code>repo_url</code> or the <code>mirror_url</code> is malformed.</li>
<li><code>ZX_ERR_NOT_FOUND</code> if the repository or mirror does not exist.</li>
</ul>

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

### List {#List}

<p>Return an iterator over all repositories.</p>
<p>Arguments:
<code>iterator</code> is a request for an iterator.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>iterator</code></td>
            <td>
                <code>request&lt;<a class='link' href='#RepositoryIterator'>RepositoryIterator</a>&gt;</code>
            </td>
        </tr></table>



## RepositoryIterator {#RepositoryIterator}
*Defined in [fuchsia.pkg/repo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/repo.fidl#132)*

<p>The iterator over all the repositories defined in a <code>PackageResolver</code>.</p>

### Next {#Next}

<p>Advance the iterator and return the next batch of repositories.</p>
<p>Return Values:</p>
<ul>
<li>a vector of <code>RepositoryConfig</code> repositories. Will return an empty vector when there are
no more repositories.</li>
</ul>

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

## PackageResolver {#PackageResolver}
*Defined in [fuchsia.pkg/resolver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/resolver.fidl#15)*

<p>Resolves packages from a registry.</p>
<p>This interface is intended to be implemented by package resolver components, and used by
repository administration tools.</p>

### Resolve {#Resolve}

<p>Populates or updates the cache of a package with the given selectors as specified by the
update policy.</p>
<p>Ensures that a package is on the local filesystem.</p>
<p>Arguments:</p>
<ul>
<li><code>package_url</code> The package URL for a package (TODO: link to docs).</li>
<li><code>selectors</code> are the package selectors (TODO: link to docs).</li>
<li><code>dir</code> is a request for a directory that will be resolved when the package has been
successfully cached.</li>
</ul>
<p>Return Values:</p>
<ul>
<li><code>ZX_OK</code> if the package was successfully opened.</li>
<li><code>ZX_ERR_ACCESS_DENIED</code> if the resolver does not have permission to fetch a package blob.</li>
<li><code>ZX_ERR_IO</code> if there is some other unspecified error during I/O.</li>
<li><code>ZX_ERR_NOT_FOUND</code> if the package or a package blob does not exist.</li>
<li><code>ZX_ERR_NO_SPACE</code> if there is no space available to store the package.</li>
<li><code>ZX_ERR_UNAVAILABLE</code> if the resolver is currently unable to fetch a package blob.</li>
</ul>

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
                <code>request&lt;<a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#Directory'>Directory</a>&gt;</code>
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

### BlobId {#BlobId}
*Defined in [fuchsia.pkg/common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/common.fidl#9)*



<p>BlobId is a content-addressed merkle root that describes an artifact that is tracked by the
packaging system.</p>


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

### BlobInfo {#BlobInfo}
*Defined in [fuchsia.pkg/common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/common.fidl#15)*



<p>BlobInfo is a tuple of the content-addressed merkle root for an artifact, along with that
artifact's length in bytes.</p>


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

### UpdatePolicy {#UpdatePolicy}
*Defined in [fuchsia.pkg/resolver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/resolver.fidl#44)*



<p>The <code>UpdatePolicy</code> provides different policies to be used when the <code>PackageResolver</code> is
fetching packages.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>fetch_if_absent</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Should the resolver fetch the package if it is not present on the local system.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>allow_old_versions</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Should the resolver allow old versions of the package to be used.</p>
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### ExperimentToggle {#ExperimentToggle}
Type: <code>uint64</code>

*Defined in [fuchsia.pkg/admin.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/admin.fidl#24)*

<p>List of known experiment toggles</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>LIGHTBULB</code></td>
            <td><code>0</code></td>
            <td><p>Does nothing, but visible in inspect.</p>
</td>
        </tr><tr>
            <td><code>DOWNLOAD_BLOB</code></td>
            <td><code>1</code></td>
            <td><p>Perform blob downloading in the package resolver instead of amber.</p>
</td>
        </tr><tr>
            <td><code>RUST_TUF</code></td>
            <td><code>2</code></td>
            <td><p>Resolve package merkle roots using rust-tuf instead of amber.</p>
</td>
        </tr></table>



## **TABLES**

### RepositoryConfig {#RepositoryConfig}


*Defined in [fuchsia.pkg/repo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/repo.fidl#79)*

<p>Describes the configuration necessary to connect to a repository and it's mirrors.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>repo_url</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>A fuchsia-pkg URL identifying the repository. Required.</p>
<p>Example: fuchsia-pkg://example.com/</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>root_keys</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#RepositoryKeyConfig'>RepositoryKeyConfig</a>&gt;</code>
            </td>
            <td><p>A vector of public keys. Required.</p>
<p>These keys must match one of the trusted keys known to the system.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>mirrors</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#MirrorConfig'>MirrorConfig</a>&gt;</code>
            </td>
            <td><p>The repository mirrors that serve the package contents. Required.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>update_package_url</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The package URL of the system update package. Optional.</p>
<p>Only used for the fuchsia-pkg://fuchsia.com/ repo.</p>
</td>
        </tr></table>

### MirrorConfig {#MirrorConfig}


*Defined in [fuchsia.pkg/repo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/repo.fidl#116)*

<p>Describes the configuration necessary to connect to a mirror.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>mirror_url</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The base URL of the TUF metadata on this mirror. Required.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>subscribe</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Whether or not to automatically monitor the mirror for updates. Required.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>blob_key</code></td>
            <td>
                <code><a class='link' href='#RepositoryBlobKey'>RepositoryBlobKey</a></code>
            </td>
            <td><p>The private (or symmetric) key used to decrypt blobs fetched from this mirror. Optional.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>blob_mirror_url</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The URL where blobs from this mirror should be fetched.  Optional.
Defaults to <code>mirror_url + &quot;/blobs&quot;</code>.</p>
</td>
        </tr></table>





## **XUNIONS**

### RepositoryKeyConfig {#RepositoryKeyConfig}
*Defined in [fuchsia.pkg/repo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/repo.fidl#102)*

<p>Describes the keys used by the repository to authenticate it's packages.</p>
<p>The only supported algorithm at the moment is ed25519.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>ed25519_key</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td><p>The raw ed25519 public key as binary data.</p>
</td>
        </tr></table>

### RepositoryBlobKey {#RepositoryBlobKey}
*Defined in [fuchsia.pkg/repo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg/repo.fidl#110)*

<p>Describes a key used to decrypt blobs.</p>
<p>The only supported algorithm at the moment is aes.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>aes_key</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td><p>A raw aes key as binary data.</p>
</td>
        </tr></table>







