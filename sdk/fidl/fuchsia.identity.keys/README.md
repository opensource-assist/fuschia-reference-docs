[TOC]

# fuchsia.identity.keys

 Defines protocols to manage and access key material that is consistent
 across all devices provisioned with a particular identity.

## **PROTOCOLS**

## KeyManager {#KeyManager}
*Defined in [fuchsia.identity.keys/key_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.keys/key_manager.fidl#163)*

 `KeyManager` provides access to key material that is consistent across all
 devices provisioned with the identity that the `KeyManager` was acquired
 from, such as a Fuchsia Persona.

 Acheiving consistency implies synchonization between devices and this
 synchronization is not instantaneous. For some implementations
 synchronization may take many minutes or even longer when devices are
 offline. The `KeyManager` is able to report information about the progress
 of this synchronization via `SynchonizationState`.

### WatchOrCreateKeySingleton {#WatchOrCreateKeySingleton}

 Returns the `KeySingleton` with the name supplied in `properties` or
 creates a new `KeySingleton` if this name does not exist.

 This method follows the hanging get pattern and does not return until
 the response would be different than the previous request for the same
 name. Errors are always returned as soon as they are detected.

 `properties` The properties of the new `KeySingleton`.

 Returns: `properties` The `KeySingletonProperties` supplied at creation,
                       with uid populated.
          `state` The `SychronizationState` for the `KeySingleton`.
          `key` The `Key` for the `KeySingleton`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>properties</code></td>
            <td>
                <code><a class='link' href='#KeySingletonProperties'>KeySingletonProperties</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#KeyManager_WatchOrCreateKeySingleton_Result'>KeyManager_WatchOrCreateKeySingleton_Result</a></code>
            </td>
        </tr></table>

### WatchKeySingleton {#WatchKeySingleton}

 Returns the `KeySingleton` with the specified name.

 Fails with `NOT_FOUND` if the requested name does not exist. This method
 follows the hanging get pattern and does not return until the response
 would be different than the previous request for the same name. Errors
 are always returned as soon as they are detected.

 `name` The name of the requested `KeySingleton`.

 Returns: `properties` The `KeySingletonProperties` supplied at creation,
                       with uid populated.
          `state` The `SychronizationState` for the `KeySingleton`.
          `key` The `Key` for the `KeySingleton`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string[128]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#KeyManager_WatchKeySingleton_Result'>KeyManager_WatchKeySingleton_Result</a></code>
            </td>
        </tr></table>

### DeleteKeySingleton {#DeleteKeySingleton}

 Deletes a previously created `KeySingleton`.

 Fails with `NOT_FOUND` if the requested name does not exist. This method
 returns once the deletion has been recorded locally and this does not
 guarantee that the deletion will be successfully committed.

 `name` The name of the key singleton.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string[128]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#KeyManager_DeleteKeySingleton_Result'>KeyManager_DeleteKeySingleton_Result</a></code>
            </td>
        </tr></table>

### GetOrCreateKeySet {#GetOrCreateKeySet}

 Connects a channel to the `KeySet` with the name supplied in
 `properties` or creates a new `KeySet` containing a single `Key` if this
 name does not exist.

 `properties` The properties of the new `KeySet`.
 `key_set_to_freeze` If this string is the name of another `KeySet` that
                     is in the `LIVE` state, and if this method causes a
                     new `KeySet` to be created, the other `KeySet` will
                     be moved to the `FROZEN` state atomically with the
                     new `KeySet` reaching the `LIVE` state.
 `key_set` The server end of a `KeySet` channel.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>properties</code></td>
            <td>
                <code><a class='link' href='#KeySetProperties'>KeySetProperties</a></code>
            </td>
        </tr><tr>
            <td><code>key_set_to_freeze</code></td>
            <td>
                <code>string[128]?</code>
            </td>
        </tr><tr>
            <td><code>key_set</code></td>
            <td>
                <code>request&lt;<a class='link' href='#KeySet'>KeySet</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#KeyManager_GetOrCreateKeySet_Result'>KeyManager_GetOrCreateKeySet_Result</a></code>
            </td>
        </tr></table>

### GetKeySet {#GetKeySet}

 Connects a channel to a previously created `KeySet`.

 Fails with `NOT_FOUND` if the requested name does not exist.

 `name` The name of the key set.
 `key_set` The server end of a `KeySet` channel.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string[128]</code>
            </td>
        </tr><tr>
            <td><code>key_set</code></td>
            <td>
                <code>request&lt;<a class='link' href='#KeySet'>KeySet</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#KeyManager_GetKeySet_Result'>KeyManager_GetKeySet_Result</a></code>
            </td>
        </tr></table>

### FreezeKeySet {#FreezeKeySet}

 Freezes a previously created `KeySet`.

 Fails with `NOT_FOUND` if the requested name does not exist.  The method
 returns once the freeze has been recorded locally and this does not
 guarantee that the freeze will be successfully committed. If the
 `KeySet` is already in the `PENDING_FROZEN_ADDITION`, `PENDING_FREEZE`,
 or `FROZEN` state this operation has no effect.

 `name` The name of the key set.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string[128]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#KeyManager_FreezeKeySet_Result'>KeyManager_FreezeKeySet_Result</a></code>
            </td>
        </tr></table>

### DeleteKeySet {#DeleteKeySet}

 Deletes a previously created `KeySet`.

 Fails with `NOT_FOUND` if the requested name does not exist. Once the
 deletion has been successfully committed any `KeySet` channels referring
 to it will be closed. The method returns once the deletion has been
 recorded locally and this does not guarantee that the deletion will
 be successfully committed.

 `name` The name of the key set.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string[128]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#KeyManager_DeleteKeySet_Result'>KeyManager_DeleteKeySet_Result</a></code>
            </td>
        </tr></table>

## KeySet {#KeySet}
*Defined in [fuchsia.identity.keys/key_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.keys/key_manager.fidl#363)*

 `KeySet` provides access to a set of keys that is consistent across devices
 provisioned with the identity that it applies to.

 The keys within a key set are typically all used for the same purpose, such
 as encrypting a sensitive dataset. A recent key can be used to encrypt new
 data but older keys remain available to decrypt older data.

 All keys in the set are of the same size and each is identified by a
 monotonically increasing `KeyId` starting at one. A new key is added into
 the set on each rotation event. These rotation events may either occur
 "automatically" or "manually":
 * An automatic rotation occurs when a device's access to the identity is
   remotely revoked (we trust a device that performs its own recovation to
   also securely delete the key material it is holding). The newly added key
   is not supplied to the device whose access was revoked. The account system
   may combine the revocation of multiple devices into a single rotation
   event.
 * A manual rotation occurs when a client calls the `AddKey` method.

 Old keys are deleted from the set automatically to avoid exceeding its
 maximum size, clients may also delete keys using the `DeleteKey` method.

 Optionally, a client may "mark" specific keys in the `KeySet` to track
 its processing of individual keys. The account system will report the
 latest key that has been marked on any device.

 A key set may be frozen, after which no further keys will be added and no
 further mark operations may be performed. Keys may still be deleted from a
 frozen key set.

### WatchSynchronizationState {#WatchSynchronizationState}

 Returns the `SynchronizationState` for the entire `KeySet`. Refer to the
 documentation on `SynchronizationState` for the available states and
 state transitions.

 This method follows the hanging get pattern and does not return until
 the response would be different than the previous request.

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
                <code><a class='link' href='#SynchronizationState'>SynchronizationState</a></code>
            </td>
        </tr></table>

### GetProperties {#GetProperties}

 Returns the `KeySetProperties` for this key set.

 These properties are fixed and will not change through the life of the
 key set.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>properties</code></td>
            <td>
                <code><a class='link' href='#KeySetProperties'>KeySetProperties</a></code>
            </td>
        </tr></table>

### WatchSynchronizedIds {#WatchSynchronizedIds}

 Return a vector of the `KeyId` for all keys in the key set with
 `SynchronizationState == LIVE`.

 The returned vector is ordered by id. This method follows the hanging
 get pattern and does not return until the response would be different
 than the previous request.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#KeySet_WatchSynchronizedIds_Result'>KeySet_WatchSynchronizedIds_Result</a></code>
            </td>
        </tr></table>

### WatchAllIds {#WatchAllIds}

 Return a vector of the `KeyId` for all keys in the key set, whatever
 their `SynchronizationState`.

 The returned vector is ordered by id. This method follows the hanging
 get pattern and does not return until the response would be different
 than the previous request.

 Note: Worst case this vector will be twice the maximum size of the key
       set. Consider a full key set that contains N `LIVE` keys.
       N manual rotations are now performed before the first succeeds.
       Each rotation moves a key from the `LIVE` state to the
       `PENDING_DELETION` state and adds a new key in the
       `PENDING_ADDITION` state.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#KeySet_WatchAllIds_Result'>KeySet_WatchAllIds_Result</a></code>
            </td>
        </tr></table>

### WatchKey {#WatchKey}

 Returns a `Key` from the key set.

 Fails with `NOT_FOUND` if the requested key does not exist. This method
 follows the hanging get pattern and does not return until the response
 would be different than the previous request for this `id`.

 `id` The `KeyId` of the requested key.

 Returns: `key` The requested `Key`.
          `state` The current `SynchronizationState` of the key. Note
                  that keys in `PENDING_ADDITION` are not final: they
                  might never reach other devices and the same `KeyId`
                  might be reused for a different `Key` in the future.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#KeySet_WatchKey_Result'>KeySet_WatchKey_Result</a></code>
            </td>
        </tr></table>

### DeleteKey {#DeleteKey}

 Deletes a `Key` from the key set.

 Fails with `NOT_FOUND` if the requested key does not exist. The method
 returns once the deletion has been recorded locally and this does not
 guarantee that the deletion will be successfully committed.

 `id` The `KeyId` of the requested key.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#KeySet_DeleteKey_Result'>KeySet_DeleteKey_Result</a></code>
            </td>
        </tr></table>

### AddKey {#AddKey}

 Adds a new `Key` to the key set, i.e. performs a manual key rotation.

 The method returns once the addition has been recorded locally and this
 does not guarantee that the addition will be successfully committed.

 Fails with `UNSUPPORTED_OPERATION` if `KeySetProperties.manual_rotation`
 is false or with `FROZEN` if the key set has been frozen.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#KeySet_AddKey_Result'>KeySet_AddKey_Result</a></code>
            </td>
        </tr></table>

### MarkId {#MarkId}

 Performs a "Mark" operation on a key, such that it is eligible to be
 returned by `GetMaxMarkedId`.

 The largest `KeyId` on which a mark operation has been performed is
 synchronized across devices.

 Fails with `FROZEN` if the key set has been frozen.

 `id` The `KeyId` of the requested key. The method will fail with
      NOT_FOUND if this key does not exist.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#KeySet_MarkId_Result'>KeySet_MarkId_Result</a></code>
            </td>
        </tr></table>

### WatchMaxCommittedMarkedId {#WatchMaxCommittedMarkedId}

 Returns the maximum `KeyId` on which `MarkId` has been called and
 successfully commited.

 This method follows the hanging get pattern and does not return until
 the response would be different than the previous request.

 Returns: `id` The largest `KeyId` for which a `MarkId` call has been
               made and successfully committed, or zero if no `MarkId`
               calls have been committed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#KeySet_WatchMaxCommittedMarkedId_Result'>KeySet_WatchMaxCommittedMarkedId_Result</a></code>
            </td>
        </tr></table>

### WatchMaxPendingMarkedId {#WatchMaxPendingMarkedId}

 Returns the maximum `KeyId` on which `MarkId` has been called, even if
 this has not yet been successfully committed.

 This method follows the hanging get pattern and does not return until
 the response would be different than the previous request.

 Returns: `id` The largest `KeyId` for which a `MarkId` call has been
               made, or zero if no `MarkId` calls have been made.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#KeySet_WatchMaxPendingMarkedId_Result'>KeySet_WatchMaxPendingMarkedId_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### KeyManager_WatchOrCreateKeySingleton_Response {#KeyManager_WatchOrCreateKeySingleton_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>properties</code></td>
            <td>
                <code><a class='link' href='#KeySingletonProperties'>KeySingletonProperties</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#SynchronizationState'>SynchronizationState</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>key</code></td>
            <td>
                <code><a class='link' href='#Key'>Key</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### KeyManager_WatchKeySingleton_Response {#KeyManager_WatchKeySingleton_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>properties</code></td>
            <td>
                <code><a class='link' href='#KeySingletonProperties'>KeySingletonProperties</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#SynchronizationState'>SynchronizationState</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>key</code></td>
            <td>
                <code><a class='link' href='#Key'>Key</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### KeyManager_DeleteKeySingleton_Response {#KeyManager_DeleteKeySingleton_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### KeyManager_GetOrCreateKeySet_Response {#KeyManager_GetOrCreateKeySet_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### KeyManager_GetKeySet_Response {#KeyManager_GetKeySet_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### KeyManager_FreezeKeySet_Response {#KeyManager_FreezeKeySet_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### KeyManager_DeleteKeySet_Response {#KeyManager_DeleteKeySet_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### KeySet_WatchSynchronizedIds_Response {#KeySet_WatchSynchronizedIds_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>ids</code></td>
            <td>
                <code>vector&lt;uint32&gt;[64]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### KeySet_WatchAllIds_Response {#KeySet_WatchAllIds_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>ids</code></td>
            <td>
                <code>vector&lt;uint32&gt;[128]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### KeySet_WatchKey_Response {#KeySet_WatchKey_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code><a class='link' href='#Key'>Key</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#SynchronizationState'>SynchronizationState</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### KeySet_DeleteKey_Response {#KeySet_DeleteKey_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### KeySet_AddKey_Response {#KeySet_AddKey_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### KeySet_MarkId_Response {#KeySet_MarkId_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### KeySet_WatchMaxCommittedMarkedId_Response {#KeySet_WatchMaxCommittedMarkedId_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### KeySet_WatchMaxPendingMarkedId_Response {#KeySet_WatchMaxPendingMarkedId_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### Error {#Error}
Type: <code>uint32</code>

*Defined in [fuchsia.identity.keys/key_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.keys/key_manager.fidl#24)*

 Specifies the reason that a `fuchsia.identity.keys` method failed.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>1</code></td>
            <td> Some other problem occurred that cannot be classified using one of the
 more specific statuses. Retry is optional.
</td>
        </tr><tr>
            <td><code>INTERNAL</code></td>
            <td><code>2</code></td>
            <td> An internal error occurred. This usually indicates a bug within the
 account system itself. Retry is optional.
</td>
        </tr><tr>
            <td><code>UNSUPPORTED_OPERATION</code></td>
            <td><code>3</code></td>
            <td> The requested operation is not supported. This generally indicates that
 implementation of a new feature is not yet complete. The request should
 not be retried.
</td>
        </tr><tr>
            <td><code>INVALID_REQUEST</code></td>
            <td><code>4</code></td>
            <td> The request was malformed in some way, such as using an invalid key
 size. The request should not be retried.
</td>
        </tr><tr>
            <td><code>RESOURCE</code></td>
            <td><code>5</code></td>
            <td> A local resource error occurred such as I/O, FIDL, or memory allocation
 failure. Retry, after a delay, is recommended.
</td>
        </tr><tr>
            <td><code>NOT_FOUND</code></td>
            <td><code>7</code></td>
            <td> The requested key or key set is not present.  The request should not be
 retried.
</td>
        </tr><tr>
            <td><code>FROZEN</code></td>
            <td><code>8</code></td>
            <td> The request would require an illegal change to an entry that is in a
 frozen state.
</td>
        </tr></table>

### SynchronizationState {#SynchronizationState}
Type: <code>uint32</code>

*Defined in [fuchsia.identity.keys/key_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.keys/key_manager.fidl#118)*

 Summarizes the sychronization between the device's local state and the
 master definition for some item (such as a `KeySingleton` or `KeySet`) in an
 identity. Depending on the identity and implementation this "master
 definition" might take one of many forms such as the device itself, a
 server, a blockchain, a transparency directory, or a quorum of devices.

 Synchronization follows the state machine illustrated below. Only `KeySet`
 supports the `PENDING_FROZEN_ADDITION`, `PENDING_FREEZE`, and `FROZEN`
 states:
 ```
             +------------------------+                 --\
             |                        |                   |
             |   +----------------+   | [commit           |
             |   | PENDING_FROZEN |   |  success]         |
             |   |   _ADDITION    |---|----------\        \ Present on
             |   +----------------+   |          |        / local device
             |     ^                  | Delete   |        |
             |     | Freeze locally   | locally  |        |
   Add       |     |                  |----------|--\     |
   locally   |  +------------------+  | [commit  |  |     |
   ----------|->| PENDING_ADDITION |  |  fail]   |  |     |
             |  +------------------+  |          |  |     |
             |          |             |          |  |     |
   Add       +----------|-------------+          |  |     |
   remotely             |                        |  |     |
   ----------------+    | [commit success]       |  |     |
                   |    |                        |  |     |  --\
             +-----|----|------------+           |  |     |    |
             |     v    v            |           |  |     |    |
             |  +-----------------+  |           |  |     |    |
   +----------->|     LIVE        |  |           |  |     |    |
   |         |  +-----------------+  |           |  |     |    |
   |         |         | ^           |           |  |     |    |
   |         |  Freeze | | [commit   |           |  |     |    |
   |         | locally | |  fail]    |           |  |     |    |
   |         |         v |           | Delete    |  |     |    |
   |         |  +-----------------+  | Remotely  |  |     |    |
   |         |  | PENDING_FREEZE  |  |-----------|--+     |    |
   |         |  +-----------------+  |           |  |     |    |
   |         |          |            |           |  |     |    |
   |         |          | [commit    |           |  |     |    |
   |         |          |  success]  |           |  |     |    |
   |         |          v            |           |  |     |    |
   |         |  +-----------------+  |           |  |     |    |
   | +--------->|    FROZEN       |<-------------/  |     |    |
   | |       |  +-----------------+  |              |     |    |
   | |       |    ^                  |              |     |    |
   | |       |    | Freeze remotely  |              |     |    |
   | |       |    |                  |              |     |    |
   | |       +----+------------------+              |     |    |
   | |                    |                         |     |    |
   | | [previous state    | Delete                  |   --/    |
   | |  == FROZEN]        | locally                 |          |
   | |                    v            Delete       |          \ Present
   | +----+      +------------------+  remotely     |          / in master
   |      |      | PENDING_DELETION |---------------+          | definition
   |      ^      +------------------+  [commit      |          |
   |     / \              |             success]    |        --/
   +----<   >-------------+                         V
 [else]  \ /   [commit fail]                   +---------+
          v                                    | INVALID |
                                               +---------+
 ```


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>PENDING_ADDITION</code></td>
            <td><code>1</code></td>
            <td> The item is present and not frozen on the current device but has not yet
 been committed into the master definition. Items in this state might not
 reach other devices and might become invalid if committing the addition
 fails.
</td>
        </tr><tr>
            <td><code>PENDING_FROZEN_ADDITION</code></td>
            <td><code>2</code></td>
            <td> The item is present and frozen on the current device but has not yet
 been committed into the master definition. Items in this state might not
 reach other devices and might become invalid if committing the addition
 fails. If committing the item succeeds it will enter the `FROZEN` state
 directly without passing through `LIVE`.
</td>
        </tr><tr>
            <td><code>LIVE</code></td>
            <td><code>3</code></td>
            <td> The item is present and not frozen both on the current device and in the
 master definition of the identity. It should eventually be consistent
 across all devices with access to the identity.
</td>
        </tr><tr>
            <td><code>PENDING_FREEZE</code></td>
            <td><code>4</code></td>
            <td> The item has been frozen on the current device but this operation has
 not yet been committed. Items in this state might return to the `LIVE`
 state if committing the freeze fails.
</td>
        </tr><tr>
            <td><code>FROZEN</code></td>
            <td><code>5</code></td>
            <td> The item is present and frozen both on the current device and in the
 master definition of the identity. Mutations are no longer possible
 but deletions are still allowed.
</td>
        </tr><tr>
            <td><code>PENDING_DELETION</code></td>
            <td><code>6</code></td>
            <td> The item is present in the master definition of the identity, but has
 been deleted from the current device and this deletion has not yet been
 committed. Items in this state might return to the `LIVE` or `FROZEN`
 state if committing the deletion fails.
</td>
        </tr></table>



## **TABLES**

### KeySingletonProperties {#KeySingletonProperties}


*Defined in [fuchsia.identity.keys/key_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.keys/key_manager.fidl#271)*

 Specifies the properties of a `KeySingleton`. These properties are provided
 when the `KeySingleton` is created and do not change during its lifetime.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td> A name of the `KeySingleton`. Unique within the `KeyManager` that
 supplied it at a single point in time.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>uid</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> A numeric identifier for the `KeySingleton` that is unique within the
 `KeyManager` that created it. The same name might be reused for
 different key singletons during the lifetime of a `KeyManager` but these
 will have different `uid` values.

 This field is set by the account system and must not be supplied in
 `KeyManager.CreateKeySingleton`.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>metadata</code></td>
            <td>
                <code>vector&lt;uint8&gt;[128]</code>
            </td>
            <td> Optional metadata associated with the `KeySingleton`. This is supplied
 by the client and is opaque to the account system.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>key_length</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The size of the key material in this `KeySingleton` in bytes. The value
 must be between one and MAX_KEY_LEN inclusive.
</td>
        </tr></table>

### KeySetProperties {#KeySetProperties}


*Defined in [fuchsia.identity.keys/key_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.keys/key_manager.fidl#296)*

 Specifies the properties of a `KeySet`. These properties are provided when
 the `KeySet` is created and do not change during its lifetime.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td> A name of the `KeySet`. Unique within the `KeyManager` that supplied it
 at a single point in time.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>uid</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> A numeric identifier for the `KeySet` that is unique within the
 `KeyManager` that created it. The same name might be reused for
 different key sets during the lifetime of a `KeyManager` but these will
 have different `uid` values.

 This field is set by the account system and must not be supplied in
 `KeyManager.CreateKeySet`.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>metadata</code></td>
            <td>
                <code>vector&lt;uint8&gt;[128]</code>
            </td>
            <td> Optional metadata associated with the `KeySet`. This is supplied by the
 client and is opaque to the account system.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>key_length</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The size of the keys in this `KeySet` in bytes. The value must be
 between one and MAX_KEY_LEN inclusive.
</td>
        </tr><tr>
            <td>5</td>
            <td><code>max_keys</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The maximum number of keys within this `KeySet`. Old keys will be
 automatically deleted to prevent this limit being exceeded. The value
 must be between one and MAX_KEYSET_SIZE inclusive.
</td>
        </tr><tr>
            <td>6</td>
            <td><code>automatic_rotation</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, a new key will be added to this `KeySet` each time a device
 with access to the identity is remotely revoked.
 `automatic_rotation` and `manual_rotation` cannot both be false.
</td>
        </tr><tr>
            <td>7</td>
            <td><code>manual_rotation</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, users of this KeySet may cause new keys to be added by calling
 `KeySet.AddKey`.
 `automatic_rotation` and `manual_rotation` cannot both be false.
</td>
        </tr></table>



## **UNIONS**

### KeyManager_WatchOrCreateKeySingleton_Result {#KeyManager_WatchOrCreateKeySingleton_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#KeyManager_WatchOrCreateKeySingleton_Response'>KeyManager_WatchOrCreateKeySingleton_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### KeyManager_WatchKeySingleton_Result {#KeyManager_WatchKeySingleton_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#KeyManager_WatchKeySingleton_Response'>KeyManager_WatchKeySingleton_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### KeyManager_DeleteKeySingleton_Result {#KeyManager_DeleteKeySingleton_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#KeyManager_DeleteKeySingleton_Response'>KeyManager_DeleteKeySingleton_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### KeyManager_GetOrCreateKeySet_Result {#KeyManager_GetOrCreateKeySet_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#KeyManager_GetOrCreateKeySet_Response'>KeyManager_GetOrCreateKeySet_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### KeyManager_GetKeySet_Result {#KeyManager_GetKeySet_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#KeyManager_GetKeySet_Response'>KeyManager_GetKeySet_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### KeyManager_FreezeKeySet_Result {#KeyManager_FreezeKeySet_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#KeyManager_FreezeKeySet_Response'>KeyManager_FreezeKeySet_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### KeyManager_DeleteKeySet_Result {#KeyManager_DeleteKeySet_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#KeyManager_DeleteKeySet_Response'>KeyManager_DeleteKeySet_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### KeySet_WatchSynchronizedIds_Result {#KeySet_WatchSynchronizedIds_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#KeySet_WatchSynchronizedIds_Response'>KeySet_WatchSynchronizedIds_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### KeySet_WatchAllIds_Result {#KeySet_WatchAllIds_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#KeySet_WatchAllIds_Response'>KeySet_WatchAllIds_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### KeySet_WatchKey_Result {#KeySet_WatchKey_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#KeySet_WatchKey_Response'>KeySet_WatchKey_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### KeySet_DeleteKey_Result {#KeySet_DeleteKey_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#KeySet_DeleteKey_Response'>KeySet_DeleteKey_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### KeySet_AddKey_Result {#KeySet_AddKey_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#KeySet_AddKey_Response'>KeySet_AddKey_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### KeySet_MarkId_Result {#KeySet_MarkId_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#KeySet_MarkId_Response'>KeySet_MarkId_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### KeySet_WatchMaxCommittedMarkedId_Result {#KeySet_WatchMaxCommittedMarkedId_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#KeySet_WatchMaxCommittedMarkedId_Response'>KeySet_WatchMaxCommittedMarkedId_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### KeySet_WatchMaxPendingMarkedId_Result {#KeySet_WatchMaxPendingMarkedId_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#KeySet_WatchMaxPendingMarkedId_Response'>KeySet_WatchMaxPendingMarkedId_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>



## **XUNIONS**

### Key {#Key}
*Defined in [fuchsia.identity.keys/key_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.keys/key_manager.fidl#263)*

 Defines the key material in a `KeySingleton` or each member of a `KeySet`.

 Note: Currently all keys are defined as fixed length arrays of random data
       but we use an xunion to potentially allow more structured key types
       in a future version of the API.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>random_key</code></td>
            <td>
                <code>vector&lt;uint8&gt;[64]</code>
            </td>
            <td> An unstructured random key of the length specified in
 `KeySingletonProperties.key_length` or `KeySetProperties.key_length`.
</td>
        </tr></table>





## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.keys/key_manager.fidl#12">MAX_NAME_LEN</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
            <td> The maximum length of a `KeySingleton` or `KeySet` name, in bytes.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.keys/key_manager.fidl#14">MAX_METADATA_LEN</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
            <td> The maximum length of metadata in a `KeySingleton` or `KeySet`, in bytes.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.keys/key_manager.fidl#16">MAX_KEY_LEN</a></td>
            <td>
                    <code>64</code>
                </td>
                <td><code>uint32</code></td>
            <td> The maximum length of an unstructured random `Key`, in bytes.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.keys/key_manager.fidl#19">MAX_KEYSET_SIZE</a></td>
            <td>
                    <code>64</code>
                </td>
                <td><code>uint32</code></td>
            <td> The maximum number of `Key` objects in a `KeySet`.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.keys/key_manager.fidl#21">TWICE_MAX_KEYSET_SIZE</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
            <td> Two times the maximum number of `Key` objects in a `KeySet`.
</td>
        </tr>
    
</table>

