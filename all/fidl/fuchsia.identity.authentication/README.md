[TOC]

# fuchsia.identity.authentication

<p>Defines the protocols used to enroll and interact with user
authentication mechanisms.</p>
<p>New authentication mechanisms may be added to the system by implementing the
server side of one or more of these protocols, the core identity system will
act as the client.</p>

## **PROTOCOLS**

## StorageUnlockMechanism {#StorageUnlockMechanism}
*Defined in [fuchsia.identity.authentication/mechanisms.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.authentication/mechanisms.fidl#16)*

<p>A stateless interface serving an authentication mechanism capable of
supplying pre-key material for use with storage unlock. Clients are
responsible for managing and persisting enrollments. Enrollment
data created during registration must be provided back during
authentication.</p>
<p>NOTE: This protocol may not be discoverable in the future.</p>

### Authenticate {#Authenticate}

<p>Interactively requests the user to authenticate against any of the
provided enrollments.</p>
<p><code>enrollments</code>      A list of enrollments that will be accepted.</p>
<p>Returns: <code>attempt</code> An <code>AttemptedEvent</code> where the <code>enrollment_id</code> refers
to one of the provided enrollments, and the optional
<code>updated_enrollment_data</code> indicates that the
enrollment with said id must also be updated if the
attempt is successful.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>enrollments</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Enrollment'>Enrollment</a>&gt;[16]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#StorageUnlockMechanism_Authenticate_Result'>StorageUnlockMechanism_Authenticate_Result</a></code>
            </td>
        </tr></table>

### Enroll {#Enroll}

<p>Interactively run the enrollment flow for a single enrollment.</p>
<p>Returns: <code>enrollment_data</code> Data associated with this enrollment,
to be provided during authentication in
the future.
<code>prekey_material</code> The the pre-key material that will be
produced by successfully authenticating
against this enrollment.</p>

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
                <code><a class='link' href='#StorageUnlockMechanism_Enroll_Result'>StorageUnlockMechanism_Enroll_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Enrollment {#Enrollment}
*Defined in [fuchsia.identity.authentication/common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.authentication/common.fidl#64)*



<p>Enrollments allow some authentication mechanisms to produce authentication
events. An enrollment must first be created in order to be authenticated
against. Both creation and authentication may involve user interaction.
An enrollment is typically tied to a user controlled authentication factor,
such as a fingerprint, a password or a security key.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='#EnrollmentId'>EnrollmentId</a></code>
            </td>
            <td><p>A unique identifier associated with the enrollment.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='#EnrollmentData'>EnrollmentData</a></code>
            </td>
            <td><p>Data associated with the enrollment.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### PositiveEvent {#PositiveEvent}
*Defined in [fuchsia.identity.authentication/common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.authentication/common.fidl#97)*



<p>An authentication event is a statement which an authentication mechanism
makes about the presence and/or engagement of an account owner, and thus
affecting the entity's authentication state. The effect of an event depends
on the properties of the authentication mechanism which created it.
A positive authentication event may contribute to an increase in
authentication state.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>timestamp</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#time'>time</a></code>
            </td>
            <td><p>The time on <code>ZX_CLOCK_UTC</code> when the event completed.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### NegativeEvent {#NegativeEvent}
*Defined in [fuchsia.identity.authentication/common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.authentication/common.fidl#109)*



<p>A negative authentication event may contribute to a decrease in
authentication state.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>timestamp</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#time'>time</a></code>
            </td>
            <td><p>The time on <code>ZX_CLOCK_UTC</code> when the event completed.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### AttemptedEvent {#AttemptedEvent}
*Defined in [fuchsia.identity.authentication/common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.authentication/common.fidl#120)*



<p>A attempted authentication event may contribute to an increase in
authentication state if and only if the pre-key material is correct.
Otherwise, it does not affect the authentication state.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>timestamp</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#time'>time</a></code>
            </td>
            <td><p>The time on <code>ZX_CLOCK_UTC</code> when the event completed.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>enrollment_id</code></td>
            <td>
                <code><a class='link' href='#EnrollmentId'>EnrollmentId</a></code>
            </td>
            <td><p>The id of the enrollment used to produce this attempt.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>updated_enrollment_data</code></td>
            <td>
                <code><a class='link' href='#EnrollmentData'>EnrollmentData</a></code>
            </td>
            <td><p>Enrollment data which should should replace the old enrollment data upon
successful authentication. This field is only populated if a
change in enrollment data is required.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>prekey_material</code></td>
            <td>
                <code><a class='link' href='#PrekeyMaterial'>PrekeyMaterial</a></code>
            </td>
            <td><p>Pre-key material produced during the authentication attempt.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### StorageUnlockMechanism_Authenticate_Response {#StorageUnlockMechanism_Authenticate_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>attempt</code></td>
            <td>
                <code><a class='link' href='#AttemptedEvent'>AttemptedEvent</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StorageUnlockMechanism_Enroll_Response {#StorageUnlockMechanism_Enroll_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>enrollment_data</code></td>
            <td>
                <code><a class='link' href='#EnrollmentData'>EnrollmentData</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>prekey_material</code></td>
            <td>
                <code><a class='link' href='#PrekeyMaterial'>PrekeyMaterial</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### Error {#Error}
Type: <code>uint32</code>

*Defined in [fuchsia.identity.authentication/common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.authentication/common.fidl#16)*

<p>Specifies the reason that a fuchsia.identity.authentication method failed.</p>


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
component implementing the authentication mechanism. Retry is optional.</p>
</td>
        </tr><tr>
            <td><code>UNSUPPORTED_OPERATION</code></td>
            <td><code>3</code></td>
            <td><p>The requested operation is not supported. This generally indicates that
implementation of a new feature is not yet complete. The request should
not be retried.</p>
</td>
        </tr><tr>
            <td><code>INVALID_AUTH_CONTEXT</code></td>
            <td><code>4</code></td>
            <td><p>An invalid or non-functional <code>AuthenticationContextProvider</code> was
provided. Retrying is unlikely to correct this error.</p>
</td>
        </tr><tr>
            <td><code>INVALID_REQUEST</code></td>
            <td><code>5</code></td>
            <td><p>The request was malformed in some way, such as supplying duplicate
enrollment entries. The request should not be retried.</p>
</td>
        </tr><tr>
            <td><code>INVALID_DATA_FORMAT</code></td>
            <td><code>6</code></td>
            <td><p>Data supplied with the request was malformed in some way, such as
supplying corrupted enrollment data. The request should not be retried.</p>
</td>
        </tr><tr>
            <td><code>RESOURCE</code></td>
            <td><code>7</code></td>
            <td><p>A local resource error occurred such as I/O, FIDL, or memory allocation
failure. Retry, after a delay, is recommended.</p>
</td>
        </tr><tr>
            <td><code>ABORTED</code></td>
            <td><code>8</code></td>
            <td><p>An interactive authentication operation was cancelled by the user.</p>
</td>
        </tr></table>





## **UNIONS**

### StorageUnlockMechanism_Authenticate_Result {#StorageUnlockMechanism_Authenticate_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#StorageUnlockMechanism_Authenticate_Response'>StorageUnlockMechanism_Authenticate_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### StorageUnlockMechanism_Enroll_Result {#StorageUnlockMechanism_Enroll_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#StorageUnlockMechanism_Enroll_Response'>StorageUnlockMechanism_Enroll_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="PREKEY_MATERIAL_MAX_SIZE">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.authentication/common.fidl#10">PREKEY_MATERIAL_MAX_SIZE</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maxium size of the prekey material in bytes.</p>
</td>
        </tr>
    <tr id="ENROLLMENT_DATA_MAX_SIZE">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.authentication/common.fidl#13">ENROLLMENT_DATA_MAX_SIZE</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maxium size of enrollment data in bytes.</p>
</td>
        </tr>
    <tr id="MAX_ENROLLMENTS">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.authentication/common.fidl#56">MAX_ENROLLMENTS</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum number of active enrollments per authentication mechanism and
account.</p>
</td>
        </tr>
    
</table>



## **TYPE ALIASES**

<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr id="EnrollmentId">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.authentication/common.fidl#77">EnrollmentId</a></td>
            <td>
                <code>uint64</code></td>
            <td><p>A unique identifier for an <code>Enrollment</code> within an account and an
authentication mechanism.</p>
</td>
        </tr><tr id="EnrollmentData">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.authentication/common.fidl#83">EnrollmentData</a></td>
            <td>
                <code>vector</code>[<code><a class='link' href='#ENROLLMENT_DATA_MAX_SIZE'>ENROLLMENT_DATA_MAX_SIZE</a></code>]</td>
            <td><p>Arbitrary opaque data associated with an authentication enrollment, created
and subsequently read by the authentication mechanism that produced the
enrollment. It is meaningful only to the authenticator, and opaque to its
clients.</p>
</td>
        </tr><tr id="PrekeyMaterial">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.identity.authentication/common.fidl#88">PrekeyMaterial</a></td>
            <td>
                <code>vector</code>[<code><a class='link' href='#PREKEY_MATERIAL_MAX_SIZE'>PREKEY_MATERIAL_MAX_SIZE</a></code>]</td>
            <td><p>Pseudo-random data associated with an enrollment of an authentication
mechanism capable of storage unlock. It is reproduced only upon
successful authentication against that enrollment.</p>
</td>
        </tr></table>

