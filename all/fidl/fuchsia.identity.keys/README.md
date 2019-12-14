[TOC]

# fuchsia.identity.keys

<p>Defines protocols to manage and access key material that is consistent
across all devices provisioned with a particular identity.</p>
<p>Acheiving consistency implies synchonization between devices and this
synchronization is not instantaneous. For some implementations
synchronization may take many minutes, or even longer when devices are
offline. The library provides information about the progress of the
sychronization.</p>

## **PROTOCOLS**

## KeyManager {#KeyManager}
*Defined in [fuchsia.identity.keys/key_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.keys/key_manager.fidl#169)*

<p><code>KeyManager</code> provides access to key material that is consistent across all
devices provisioned with the identity that the <code>KeyManager</code> was acquired
from, such as a Fuchsia Persona.</p>
<p>Acheiving consistency implies synchonization between devices and this
synchronization is not instantaneous. For some implementations
synchronization may take many minutes or even longer when devices are
offline. The <code>KeyManager</code> is able to report information about the progress
of this synchronization via <code>SynchonizationState</code>.</p>

### WatchOrCreateKeySingleton {#WatchOrCreateKeySingleton}

<p>Returns the <code>KeySingleton</code> with the name supplied in <code>properties</code> or
creates a new <code>KeySingleton</code> if this name does not exist.</p>
<p>This method follows the hanging get pattern and does not return until
the response would be different than the previous request for the same
name. Errors are always returned as soon as they are detected.</p>
<p><code>properties</code> The properties of the new <code>KeySingleton</code>.</p>
<p>Returns: <code>properties</code> The <code>KeySingletonProperties</code> supplied at creation,
with uid populated.
<code>state</code> The <code>SychronizationState</code> for the <code>KeySingleton</code>.
<code>key</code> The <code>Key</code> for the <code>KeySingleton</code>.</p>

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

<p>Returns the <code>KeySingleton</code> with the specified name.</p>
<p>Fails with <code>NOT_FOUND</code> if the requested name does not exist. This method
follows the hanging get pattern and does not return until the response
would be different than the previous request for the same name. Errors
are always returned as soon as they are detected.</p>
<p><code>name</code> The name of the requested <code>KeySingleton</code>.</p>
<p>Returns: <code>properties</code> The <code>KeySingletonProperties</code> supplied at creation,
with uid populated.
<code>state</code> The <code>SychronizationState</code> for the <code>KeySingleton</code>.
<code>key</code> The <code>Key</code> for the <code>KeySingleton</code>.</p>

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

<p>Deletes a previously created <code>KeySingleton</code>.</p>
<p>Fails with <code>NOT_FOUND</code> if the requested name does not exist. This method
returns once the deletion has been recorded locally and this does not
guarantee that the deletion will be successfully committed.</p>
<p><code>name</code> The name of the key singleton.</p>

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

<p>Connects a channel to the <code>KeySet</code> with the name supplied in
<code>properties</code> or creates a new <code>KeySet</code> containing a single <code>Key</code> if this
name does not exist.</p>
<p><code>properties</code> The properties of the new <code>KeySet</code>.
<code>key_set_to_freeze</code> If this string is the name of another <code>KeySet</code> that
is in the <code>LIVE</code> state, and if this method causes a
new <code>KeySet</code> to be created, the other <code>KeySet</code> will
be moved to the <code>FROZEN</code> state atomically with the
new <code>KeySet</code> reaching the <code>LIVE</code> state.
<code>key_set</code> The server end of a <code>KeySet</code> channel.</p>

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

<p>Connects a channel to a previously created <code>KeySet</code>.</p>
<p>Fails with <code>NOT_FOUND</code> if the requested name does not exist.</p>
<p><code>name</code> The name of the key set.
<code>key_set</code> The server end of a <code>KeySet</code> channel.</p>

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

<p>Freezes a previously created <code>KeySet</code>.</p>
<p>Fails with <code>NOT_FOUND</code> if the requested name does not exist.  The method
returns once the freeze has been recorded locally and this does not
guarantee that the freeze will be successfully committed. If the
<code>KeySet</code> is already in the <code>PENDING_FROZEN_ADDITION</code>, <code>PENDING_FREEZE</code>,
or <code>FROZEN</code> state this operation has no effect.</p>
<p><code>name</code> The name of the key set.</p>

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

<p>Deletes a previously created <code>KeySet</code>.</p>
<p>Fails with <code>NOT_FOUND</code> if the requested name does not exist. Once the
deletion has been successfully committed any <code>KeySet</code> channels referring
to it will be closed. The method returns once the deletion has been
recorded locally and this does not guarantee that the deletion will
be successfully committed.</p>
<p><code>name</code> The name of the key set.</p>

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
*Defined in [fuchsia.identity.keys/key_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.keys/key_manager.fidl#369)*

<p><code>KeySet</code> provides access to a set of keys that is consistent across devices
provisioned with the identity that it applies to.</p>
<p>The keys within a key set are typically all used for the same purpose, such
as encrypting a sensitive dataset. A recent key can be used to encrypt new
data but older keys remain available to decrypt older data.</p>
<p>All keys in the set are of the same size and each is identified by a
monotonically increasing <code>KeyId</code> starting at one. A new key is added into
the set on each rotation event. These rotation events may either occur
&quot;automatically&quot; or &quot;manually&quot;:</p>
<ul>
<li>An automatic rotation occurs when a device's access to the identity is
remotely revoked (we trust a device that performs its own recovation to
also securely delete the key material it is holding). The newly added key
is not supplied to the device whose access was revoked. The account system
may combine the revocation of multiple devices into a single rotation
event.</li>
<li>A manual rotation occurs when a client calls the <code>AddKey</code> method.</li>
</ul>
<p>Old keys are deleted from the set automatically to avoid exceeding its
maximum size, clients may also delete keys using the <code>DeleteKey</code> method.</p>
<p>Optionally, a client may &quot;mark&quot; specific keys in the <code>KeySet</code> to track
its processing of individual keys. The account system will report the
latest key that has been marked on any device.</p>
<p>A key set may be frozen, after which no further keys will be added and no
further mark operations may be performed. Keys may still be deleted from a
frozen key set.</p>

### WatchSynchronizationState {#WatchSynchronizationState}

<p>Returns the <code>SynchronizationState</code> for the entire <code>KeySet</code>. Refer to the
documentation on <code>SynchronizationState</code> for the available states and
state transitions.</p>
<p>This method follows the hanging get pattern and does not return until
the response would be different than the previous request.</p>

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

<p>Returns the <code>KeySetProperties</code> for this key set.</p>
<p>These properties are fixed and will not change through the life of the
key set.</p>

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

<p>Return a vector of the <code>KeyId</code> for all keys in the key set with
<code>SynchronizationState == LIVE</code>.</p>
<p>The returned vector is ordered by id. This method follows the hanging
get pattern and does not return until the response would be different
than the previous request.</p>

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

<p>Return a vector of the <code>KeyId</code> for all keys in the key set, whatever
their <code>SynchronizationState</code>.</p>
<p>The returned vector is ordered by id. This method follows the hanging
get pattern and does not return until the response would be different
than the previous request.</p>
<p>Note: Worst case this vector will be twice the maximum size of the key
set. Consider a full key set that contains N <code>LIVE</code> keys.
N manual rotations are now performed before the first succeeds.
Each rotation moves a key from the <code>LIVE</code> state to the
<code>PENDING_DELETION</code> state and adds a new key in the
<code>PENDING_ADDITION</code> state.</p>

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

<p>Returns a <code>Key</code> from the key set.</p>
<p>Fails with <code>NOT_FOUND</code> if the requested key does not exist. This method
follows the hanging get pattern and does not return until the response
would be different than the previous request for this <code>id</code>.</p>
<p><code>id</code> The <code>KeyId</code> of the requested key.</p>
<p>Returns: <code>key</code> The requested <code>Key</code>.
<code>state</code> The current <code>SynchronizationState</code> of the key. Note
that keys in <code>PENDING_ADDITION</code> are not final: they
might never reach other devices and the same <code>KeyId</code>
might be reused for a different <code>Key</code> in the future.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='#KeyId'>KeyId</a></code>
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

<p>Deletes a <code>Key</code> from the key set.</p>
<p>Fails with <code>NOT_FOUND</code> if the requested key does not exist. The method
returns once the deletion has been recorded locally and this does not
guarantee that the deletion will be successfully committed.</p>
<p><code>id</code> The <code>KeyId</code> of the requested key.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='#KeyId'>KeyId</a></code>
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

<p>Adds a new <code>Key</code> to the key set, i.e. performs a manual key rotation.</p>
<p>The method returns once the addition has been recorded locally and this
does not guarantee that the addition will be successfully committed.</p>
<p>Fails with <code>UNSUPPORTED_OPERATION</code> if <code>KeySetProperties.manual_rotation</code>
is false or with <code>FROZEN</code> if the key set has been frozen.</p>

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

<p>Performs a &quot;Mark&quot; operation on a key, such that it is eligible to be
returned by <code>GetMaxMarkedId</code>.</p>
<p>The largest <code>KeyId</code> on which a mark operation has been performed is
synchronized across devices.</p>
<p>Fails with <code>FROZEN</code> if the key set has been frozen.</p>
<p><code>id</code> The <code>KeyId</code> of the requested key. The method will fail with
NOT_FOUND if this key does not exist.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='#KeyId'>KeyId</a></code>
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

<p>Returns the maximum <code>KeyId</code> on which <code>MarkId</code> has been called and
successfully commited.</p>
<p>This method follows the hanging get pattern and does not return until
the response would be different than the previous request.</p>
<p>Returns: <code>id</code> The largest <code>KeyId</code> for which a <code>MarkId</code> call has been
made and successfully committed, or zero if no <code>MarkId</code>
calls have been committed.</p>

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

<p>Returns the maximum <code>KeyId</code> on which <code>MarkId</code> has been called, even if
this has not yet been successfully committed.</p>
<p>This method follows the hanging get pattern and does not return until
the response would be different than the previous request.</p>
<p>Returns: <code>id</code> The largest <code>KeyId</code> for which a <code>MarkId</code> call has been
made, or zero if no <code>MarkId</code> calls have been made.</p>

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
                <code><a class='link' href='#KeyId'>KeyId</a></code>
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
                <code><a class='link' href='#KeyId'>KeyId</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### Error {#Error}
Type: <code>uint32</code>

*Defined in [fuchsia.identity.keys/key_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.keys/key_manager.fidl#30)*

<p>Specifies the reason that a <code>fuchsia.identity.keys</code> method failed.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>1</code></td>
            <td><p>Some other problem occurred that cannot be classified using one of the
more specific statuses. Retry is optional.</p>
</td>
        </tr><tr>
            <td><code>INTERNAL</code></td>
            <td><code>2</code></td>
            <td><p>An internal error occurred. This usually indicates a bug within the
account system itself. Retry is optional.</p>
</td>
        </tr><tr>
            <td><code>UNSUPPORTED_OPERATION</code></td>
            <td><code>3</code></td>
            <td><p>The requested operation is not supported. This generally indicates that
implementation of a new feature is not yet complete. The request should
not be retried.</p>
</td>
        </tr><tr>
            <td><code>INVALID_REQUEST</code></td>
            <td><code>4</code></td>
            <td><p>The request was malformed in some way, such as using an invalid key
size. The request should not be retried.</p>
</td>
        </tr><tr>
            <td><code>RESOURCE</code></td>
            <td><code>5</code></td>
            <td><p>A local resource error occurred such as I/O, FIDL, or memory allocation
failure. Retry, after a delay, is recommended.</p>
</td>
        </tr><tr>
            <td><code>NOT_FOUND</code></td>
            <td><code>7</code></td>
            <td><p>The requested key or key set is not present.  The request should not be
retried.</p>
</td>
        </tr><tr>
            <td><code>FROZEN</code></td>
            <td><code>8</code></td>
            <td><p>The request would require an illegal change to an entry that is in a
frozen state.</p>
</td>
        </tr></table>

### SynchronizationState {#SynchronizationState}
Type: <code>uint32</code>

*Defined in [fuchsia.identity.keys/key_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.keys/key_manager.fidl#124)*

<p>Summarizes the sychronization between the device's local state and the
master definition for some item (such as a <code>KeySingleton</code> or <code>KeySet</code>) in an
identity. Depending on the identity and implementation this &quot;master
definition&quot; might take one of many forms such as the device itself, a
server, a blockchain, a transparency directory, or a quorum of devices.</p>
<p>Synchronization follows the state machine illustrated below. Only <code>KeySet</code>
supports the <code>PENDING_FROZEN_ADDITION</code>, <code>PENDING_FREEZE</code>, and <code>FROZEN</code>
states:</p>
<pre><code>            +------------------------+                 --\
            |                        |                   |
            |   +----------------+   | [commit           |
            |   | PENDING_FROZEN |   |  success]         |
            |   |   _ADDITION    |---|----------\        \ Present on
            |   +----------------+   |          |        / local device
            |     ^                  | Delete   |        |
            |     | Freeze locally   | locally  |        |
  Add       |     |                  |----------|--\     |
  locally   |  +------------------+  | [commit  |  |     |
  ----------|-&gt;| PENDING_ADDITION |  |  fail]   |  |     |
            |  +------------------+  |          |  |     |
            |          |             |          |  |     |
  Add       +----------|-------------+          |  |     |
  remotely             |                        |  |     |
  ----------------+    | [commit success]       |  |     |
                  |    |                        |  |     |  --\
            +-----|----|------------+           |  |     |    |
            |     v    v            |           |  |     |    |
            |  +-----------------+  |           |  |     |    |
  +-----------&gt;|     LIVE        |  |           |  |     |    |
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
  | +---------&gt;|    FROZEN       |&lt;-------------/  |     |    |
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
  +----&lt;   &gt;-------------+                         V
[else]  \ /   [commit fail]                   +---------+
         v                                    | INVALID |
                                              +---------+
</code></pre>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>PENDING_ADDITION</code></td>
            <td><code>1</code></td>
            <td><p>The item is present and not frozen on the current device but has not yet
been committed into the master definition. Items in this state might not
reach other devices and might become invalid if committing the addition
fails.</p>
</td>
        </tr><tr>
            <td><code>PENDING_FROZEN_ADDITION</code></td>
            <td><code>2</code></td>
            <td><p>The item is present and frozen on the current device but has not yet
been committed into the master definition. Items in this state might not
reach other devices and might become invalid if committing the addition
fails. If committing the item succeeds it will enter the <code>FROZEN</code> state
directly without passing through <code>LIVE</code>.</p>
</td>
        </tr><tr>
            <td><code>LIVE</code></td>
            <td><code>3</code></td>
            <td><p>The item is present and not frozen both on the current device and in the
master definition of the identity. It should eventually be consistent
across all devices with access to the identity.</p>
</td>
        </tr><tr>
            <td><code>PENDING_FREEZE</code></td>
            <td><code>4</code></td>
            <td><p>The item has been frozen on the current device but this operation has
not yet been committed. Items in this state might return to the <code>LIVE</code>
state if committing the freeze fails.</p>
</td>
        </tr><tr>
            <td><code>FROZEN</code></td>
            <td><code>5</code></td>
            <td><p>The item is present and frozen both on the current device and in the
master definition of the identity. Mutations are no longer possible
but deletions are still allowed.</p>
</td>
        </tr><tr>
            <td><code>PENDING_DELETION</code></td>
            <td><code>6</code></td>
            <td><p>The item is present in the master definition of the identity, but has
been deleted from the current device and this deletion has not yet been
committed. Items in this state might return to the <code>LIVE</code> or <code>FROZEN</code>
state if committing the deletion fails.</p>
</td>
        </tr></table>



## **TABLES**

### KeySingletonProperties {#KeySingletonProperties}


*Defined in [fuchsia.identity.keys/key_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.keys/key_manager.fidl#277)*

<p>Specifies the properties of a <code>KeySingleton</code>. These properties are provided
when the <code>KeySingleton</code> is created and do not change during its lifetime.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td><p>A name of the <code>KeySingleton</code>. Unique within the <code>KeyManager</code> that
supplied it at a single point in time.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>uid</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>A numeric identifier for the <code>KeySingleton</code> that is unique within the
<code>KeyManager</code> that created it. The same name might be reused for
different key singletons during the lifetime of a <code>KeyManager</code> but these
will have different <code>uid</code> values.</p>
<p>This field is set by the account system and must not be supplied in
<code>KeyManager.CreateKeySingleton</code>.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>metadata</code></td>
            <td>
                <code>vector&lt;uint8&gt;[128]</code>
            </td>
            <td><p>Optional metadata associated with the <code>KeySingleton</code>. This is supplied
by the client and is opaque to the account system.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>key_length</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>The size of the key material in this <code>KeySingleton</code> in bytes. The value
must be between one and MAX_KEY_LEN inclusive.</p>
</td>
        </tr></table>

### KeySetProperties {#KeySetProperties}


*Defined in [fuchsia.identity.keys/key_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.keys/key_manager.fidl#302)*

<p>Specifies the properties of a <code>KeySet</code>. These properties are provided when
the <code>KeySet</code> is created and do not change during its lifetime.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td><p>A name of the <code>KeySet</code>. Unique within the <code>KeyManager</code> that supplied it
at a single point in time.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>uid</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>A numeric identifier for the <code>KeySet</code> that is unique within the
<code>KeyManager</code> that created it. The same name might be reused for
different key sets during the lifetime of a <code>KeyManager</code> but these will
have different <code>uid</code> values.</p>
<p>This field is set by the account system and must not be supplied in
<code>KeyManager.CreateKeySet</code>.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>metadata</code></td>
            <td>
                <code>vector&lt;uint8&gt;[128]</code>
            </td>
            <td><p>Optional metadata associated with the <code>KeySet</code>. This is supplied by the
client and is opaque to the account system.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>key_length</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>The size of the keys in this <code>KeySet</code> in bytes. The value must be
between one and MAX_KEY_LEN inclusive.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>max_keys</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>The maximum number of keys within this <code>KeySet</code>. Old keys will be
automatically deleted to prevent this limit being exceeded. The value
must be between one and MAX_KEYSET_SIZE inclusive.</p>
</td>
        </tr><tr>
            <td>6</td>
            <td><code>automatic_rotation</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>If true, a new key will be added to this <code>KeySet</code> each time a device
with access to the identity is remotely revoked.
<code>automatic_rotation</code> and <code>manual_rotation</code> cannot both be false.</p>
</td>
        </tr><tr>
            <td>7</td>
            <td><code>manual_rotation</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>If true, users of this KeySet may cause new keys to be added by calling
<code>KeySet.AddKey</code>.
<code>automatic_rotation</code> and <code>manual_rotation</code> cannot both be false.</p>
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
*Defined in [fuchsia.identity.keys/key_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.keys/key_manager.fidl#269)*

<p>Defines the key material in a <code>KeySingleton</code> or each member of a <code>KeySet</code>.</p>
<p>Note: Currently all keys are defined as fixed length arrays of random data
but we use an xunion to potentially allow more structured key types
in a future version of the API.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>random_key</code></td>
            <td>
                <code>vector&lt;uint8&gt;[64]</code>
            </td>
            <td><p>An unstructured random key of the length specified in
<code>KeySingletonProperties.key_length</code> or <code>KeySetProperties.key_length</code>.</p>
</td>
        </tr></table>





## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="MAX_NAME_LEN">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.keys/key_manager.fidl#18">MAX_NAME_LEN</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum length of a <code>KeySingleton</code> or <code>KeySet</code> name, in bytes.</p>
</td>
        </tr>
    <tr id="MAX_METADATA_LEN">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.keys/key_manager.fidl#20">MAX_METADATA_LEN</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum length of metadata in a <code>KeySingleton</code> or <code>KeySet</code>, in bytes.</p>
</td>
        </tr>
    <tr id="MAX_KEY_LEN">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.keys/key_manager.fidl#22">MAX_KEY_LEN</a></td>
            <td>
                    <code>64</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum length of an unstructured random <code>Key</code>, in bytes.</p>
</td>
        </tr>
    <tr id="MAX_KEYSET_SIZE">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.keys/key_manager.fidl#25">MAX_KEYSET_SIZE</a></td>
            <td>
                    <code>64</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum number of <code>Key</code> objects in a <code>KeySet</code>.</p>
</td>
        </tr>
    <tr id="TWICE_MAX_KEYSET_SIZE">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.keys/key_manager.fidl#27">TWICE_MAX_KEYSET_SIZE</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Two times the maximum number of <code>Key</code> objects in a <code>KeySet</code>.</p>
</td>
        </tr>
    
</table>



## **TYPE ALIASES**

<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr id="KeyId">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.keys/key_manager.fidl#15">KeyId</a></td>
            <td>
                <code>uint32</code></td>
            <td></td>
        </tr></table>

