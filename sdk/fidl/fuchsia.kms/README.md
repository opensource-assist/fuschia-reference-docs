[TOC]

# fuchsia.kms


## **PROTOCOLS**

## KeyManager {#KeyManager}
*Defined in [fuchsia.kms/key_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.kms/key_manager.fidl#53)*


### SealData {#SealData}

 Seal data to an encrypted form.

 Seal data to an encrypted form. The sealed data can only be unsealed by the same KMS instance
 by using UnsealData. `plain_text` needs to be less than `MAX_DATA_SIZE` bytes.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>plain_text</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#KeyManager_SealData_Result'>KeyManager_SealData_Result</a></code>
            </td>
        </tr></table>

### UnsealData {#UnsealData}

 Unseal sealed data.

 Unseal data previously sealed by this KMS instance.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>cipher_text</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#KeyManager_UnsealData_Result'>KeyManager_UnsealData_Result</a></code>
            </td>
        </tr></table>

### GenerateAsymmetricKey {#GenerateAsymmetricKey}

 Generate an asymmetric key.

 Generate an asymmetric key using `key_name` as the unique name. `key` is the generated
 asymmetric key interface request. If the `key_name` is not unique, you would get
 `KEY_ALREADY_EXISTS`. The generated key can be used to sign data. The algorithm used for
 generating asymmetric key is `ECDSA_SHA512_P521`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key_name</code></td>
            <td>
                <code>string[32]</code>
            </td>
        </tr><tr>
            <td><code>key</code></td>
            <td>
                <code>request&lt;<a class='link' href='#AsymmetricPrivateKey'>AsymmetricPrivateKey</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#KeyManager_GenerateAsymmetricKey_Result'>KeyManager_GenerateAsymmetricKey_Result</a></code>
            </td>
        </tr></table>

### GenerateAsymmetricKeyWithAlgorithm {#GenerateAsymmetricKeyWithAlgorithm}

 Generate an asymmetric key with a specific algorithm.

 Generate an asymmetric key using `key_name` as the unique name and `key_algorithm` as
 algorithm. `key` is the generated asymmetric key interface request. If the `key_name` is not
 unique, you would get `KEY_ALREADY_EXISTS`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key_name</code></td>
            <td>
                <code>string[32]</code>
            </td>
        </tr><tr>
            <td><code>key_algorithm</code></td>
            <td>
                <code><a class='link' href='#AsymmetricKeyAlgorithm'>AsymmetricKeyAlgorithm</a></code>
            </td>
        </tr><tr>
            <td><code>key</code></td>
            <td>
                <code>request&lt;<a class='link' href='#AsymmetricPrivateKey'>AsymmetricPrivateKey</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#KeyManager_GenerateAsymmetricKeyWithAlgorithm_Result'>KeyManager_GenerateAsymmetricKeyWithAlgorithm_Result</a></code>
            </td>
        </tr></table>

### ImportAsymmetricPrivateKey {#ImportAsymmetricPrivateKey}

 Import an asymmetric private key with a specific algorithm.

 Import an asymmetric private key using `key_name` as the unique name, `key_algorithm` as
 algorithm and `data` as key data. `key` is imported asymmetric key interface request. Key
 data should be in asn.1 encoded DER format. If the `key_name` is not unique, you would get
 `KEY_ALREADY_EXISTS`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr><tr>
            <td><code>key_name</code></td>
            <td>
                <code>string[32]</code>
            </td>
        </tr><tr>
            <td><code>key_algorithm</code></td>
            <td>
                <code><a class='link' href='#AsymmetricKeyAlgorithm'>AsymmetricKeyAlgorithm</a></code>
            </td>
        </tr><tr>
            <td><code>key</code></td>
            <td>
                <code>request&lt;<a class='link' href='#AsymmetricPrivateKey'>AsymmetricPrivateKey</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#KeyManager_ImportAsymmetricPrivateKey_Result'>KeyManager_ImportAsymmetricPrivateKey_Result</a></code>
            </td>
        </tr></table>

### GetAsymmetricPrivateKey {#GetAsymmetricPrivateKey}

 Get an asymmetric private key handle.

 Get an asymmetric private key handle using the `key_name`. If such key is not found, would
 return `KEY_NOT_FOUND`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key_name</code></td>
            <td>
                <code>string[32]</code>
            </td>
        </tr><tr>
            <td><code>key</code></td>
            <td>
                <code>request&lt;<a class='link' href='#AsymmetricPrivateKey'>AsymmetricPrivateKey</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#KeyManager_GetAsymmetricPrivateKey_Result'>KeyManager_GetAsymmetricPrivateKey_Result</a></code>
            </td>
        </tr></table>

### DeleteKey {#DeleteKey}

 Delete a key.

 Delete a key for `key_name`.  For all the current handle to the deleted key, they would
 become invalid and all following requests on those handles would return `KEY_NOT_FOUND`, user
 should close the invalid handles once get `KEY_NOT_FOUND` error.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key_name</code></td>
            <td>
                <code>string[32]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#KeyManager_DeleteKey_Result'>KeyManager_DeleteKey_Result</a></code>
            </td>
        </tr></table>

## Key {#Key}
*Defined in [fuchsia.kms/key_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.kms/key_manager.fidl#114)*


### GetKeyOrigin {#GetKeyOrigin}

 Get the key origin (generated/imported).

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
                <code><a class='link' href='#Key_GetKeyOrigin_Result'>Key_GetKeyOrigin_Result</a></code>
            </td>
        </tr></table>

## AsymmetricPrivateKey {#AsymmetricPrivateKey}
*Defined in [fuchsia.kms/key_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.kms/key_manager.fidl#119)*


### GetKeyOrigin {#GetKeyOrigin}

 Get the key origin (generated/imported).

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
                <code><a class='link' href='#Key_GetKeyOrigin_Result'>Key_GetKeyOrigin_Result</a></code>
            </td>
        </tr></table>

### Sign {#Sign}

 Sign `data` using the current key. `data` needs to be less than `MAX_DATA_SIZE` bytes.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#AsymmetricPrivateKey_Sign_Result'>AsymmetricPrivateKey_Sign_Result</a></code>
            </td>
        </tr></table>

### GetPublicKey {#GetPublicKey}

 Get the DER format public key for the current private key.

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
                <code><a class='link' href='#AsymmetricPrivateKey_GetPublicKey_Result'>AsymmetricPrivateKey_GetPublicKey_Result</a></code>
            </td>
        </tr></table>

### GetKeyAlgorithm {#GetKeyAlgorithm}

 Get the key algorithm.

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
                <code><a class='link' href='#AsymmetricPrivateKey_GetKeyAlgorithm_Result'>AsymmetricPrivateKey_GetKeyAlgorithm_Result</a></code>
            </td>
        </tr></table>

## StatelessKeyManager {#StatelessKeyManager}
*Defined in [fuchsia.kms/key_manager_stateless.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.kms/key_manager_stateless.fidl#11)*


### GetHardwareDerivedKey {#GetHardwareDerivedKey}

 Get a hardware key derived key.

 Get a key derived from hardware root key using | key_info | as info and the trusted app ID
 as salt. This call is deterministic and always returns the same result if given the same
 | key_info | on the same device and would be different across different devices if they have
 different hardware keys.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key_info</code></td>
            <td>
                <code>vector&lt;uint8&gt;[32]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#StatelessKeyManager_GetHardwareDerivedKey_Result'>StatelessKeyManager_GetHardwareDerivedKey_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### KeyManager_SealData_Response {#KeyManager_SealData_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>cipher_text</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### KeyManager_UnsealData_Response {#KeyManager_UnsealData_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>plain_text</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### KeyManager_GenerateAsymmetricKey_Response {#KeyManager_GenerateAsymmetricKey_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### KeyManager_GenerateAsymmetricKeyWithAlgorithm_Response {#KeyManager_GenerateAsymmetricKeyWithAlgorithm_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### KeyManager_ImportAsymmetricPrivateKey_Response {#KeyManager_ImportAsymmetricPrivateKey_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### KeyManager_GetAsymmetricPrivateKey_Response {#KeyManager_GetAsymmetricPrivateKey_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### KeyManager_DeleteKey_Response {#KeyManager_DeleteKey_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Key_GetKeyOrigin_Response {#Key_GetKeyOrigin_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key_origin</code></td>
            <td>
                <code><a class='link' href='#KeyOrigin'>KeyOrigin</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AsymmetricPrivateKey_Sign_Response {#AsymmetricPrivateKey_Sign_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>signature</code></td>
            <td>
                <code><a class='link' href='#Signature'>Signature</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AsymmetricPrivateKey_GetPublicKey_Response {#AsymmetricPrivateKey_GetPublicKey_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>public_key</code></td>
            <td>
                <code><a class='link' href='#PublicKey'>PublicKey</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AsymmetricPrivateKey_GetKeyAlgorithm_Response {#AsymmetricPrivateKey_GetKeyAlgorithm_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key_algorithm</code></td>
            <td>
                <code><a class='link' href='#AsymmetricKeyAlgorithm'>AsymmetricKeyAlgorithm</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Signature {#Signature}
*Defined in [fuchsia.kms/key_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.kms/key_manager.fidl#44)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>bytes</code></td>
            <td>
                <code>vector&lt;uint8&gt;[512]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### PublicKey {#PublicKey}
*Defined in [fuchsia.kms/key_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.kms/key_manager.fidl#48)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>bytes</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StatelessKeyManager_GetHardwareDerivedKey_Response {#StatelessKeyManager_GetHardwareDerivedKey_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>derived_key</code></td>
            <td>
                <code>vector&lt;uint8&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### Error {#Error}
Type: <code>uint32</code>

*Defined in [fuchsia.kms/key_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.kms/key_manager.fidl#12)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INTERNAL_ERROR</code></td>
            <td><code>1</code></td>
            <td> Internal unexpected error.
</td>
        </tr><tr>
            <td><code>KEY_ALREADY_EXISTS</code></td>
            <td><code>2</code></td>
            <td> When trying to create/import a new key however another key with the same name already exists.
</td>
        </tr><tr>
            <td><code>KEY_NOT_FOUND</code></td>
            <td><code>3</code></td>
            <td> When the key you are trying to use is not found.
</td>
        </tr><tr>
            <td><code>PARSE_KEY_ERROR</code></td>
            <td><code>4</code></td>
            <td> When the key material could not be parsed.
</td>
        </tr><tr>
            <td><code>INPUT_TOO_LARGE</code></td>
            <td><code>5</code></td>
            <td> When the size for input data is larger than `MAX_DATA_SIZE`.
</td>
        </tr></table>

### AsymmetricKeyAlgorithm {#AsymmetricKeyAlgorithm}
Type: <code>uint32</code>

*Defined in [fuchsia.kms/key_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.kms/key_manager.fidl#25)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>RSA_SSA_PSS_SHA256_2048</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>RSA_SSA_PSS_SHA256_3072</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>RSA_SSA_PSS_SHA512_4096</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>RSA_SSA_PKCS1_SHA256_2048</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>RSA_SSA_PKCS1_SHA256_3072</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>RSA_SSA_PKCS1_SHA512_4096</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>ECDSA_SHA256_P256</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr><tr>
            <td><code>ECDSA_SHA512_P384</code></td>
            <td><code>8</code></td>
            <td></td>
        </tr><tr>
            <td><code>ECDSA_SHA512_P521</code></td>
            <td><code>9</code></td>
            <td></td>
        </tr></table>

### KeyOrigin {#KeyOrigin}
Type: <code>uint32</code>

*Defined in [fuchsia.kms/key_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.kms/key_manager.fidl#37)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>GENERATED</code></td>
            <td><code>1</code></td>
            <td> The key was generated in this KMS instance.
</td>
        </tr><tr>
            <td><code>IMPORTED</code></td>
            <td><code>2</code></td>
            <td> The key was imported.
</td>
        </tr></table>





## **UNIONS**

### KeyManager_SealData_Result {#KeyManager_SealData_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#KeyManager_SealData_Response'>KeyManager_SealData_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### KeyManager_UnsealData_Result {#KeyManager_UnsealData_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#KeyManager_UnsealData_Response'>KeyManager_UnsealData_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### KeyManager_GenerateAsymmetricKey_Result {#KeyManager_GenerateAsymmetricKey_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#KeyManager_GenerateAsymmetricKey_Response'>KeyManager_GenerateAsymmetricKey_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### KeyManager_GenerateAsymmetricKeyWithAlgorithm_Result {#KeyManager_GenerateAsymmetricKeyWithAlgorithm_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#KeyManager_GenerateAsymmetricKeyWithAlgorithm_Response'>KeyManager_GenerateAsymmetricKeyWithAlgorithm_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### KeyManager_ImportAsymmetricPrivateKey_Result {#KeyManager_ImportAsymmetricPrivateKey_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#KeyManager_ImportAsymmetricPrivateKey_Response'>KeyManager_ImportAsymmetricPrivateKey_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### KeyManager_GetAsymmetricPrivateKey_Result {#KeyManager_GetAsymmetricPrivateKey_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#KeyManager_GetAsymmetricPrivateKey_Response'>KeyManager_GetAsymmetricPrivateKey_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### KeyManager_DeleteKey_Result {#KeyManager_DeleteKey_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#KeyManager_DeleteKey_Response'>KeyManager_DeleteKey_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Key_GetKeyOrigin_Result {#Key_GetKeyOrigin_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Key_GetKeyOrigin_Response'>Key_GetKeyOrigin_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### AsymmetricPrivateKey_Sign_Result {#AsymmetricPrivateKey_Sign_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#AsymmetricPrivateKey_Sign_Response'>AsymmetricPrivateKey_Sign_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### AsymmetricPrivateKey_GetPublicKey_Result {#AsymmetricPrivateKey_GetPublicKey_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#AsymmetricPrivateKey_GetPublicKey_Response'>AsymmetricPrivateKey_GetPublicKey_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### AsymmetricPrivateKey_GetKeyAlgorithm_Result {#AsymmetricPrivateKey_GetKeyAlgorithm_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#AsymmetricPrivateKey_GetKeyAlgorithm_Response'>AsymmetricPrivateKey_GetKeyAlgorithm_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### StatelessKeyManager_GetHardwareDerivedKey_Result {#StatelessKeyManager_GetHardwareDerivedKey_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#StatelessKeyManager_GetHardwareDerivedKey_Response'>StatelessKeyManager_GetHardwareDerivedKey_Response</a></code>
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
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.kms/key_manager.fidl#9">MAX_KEY_NAME_SIZE</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint8</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.kms/key_manager.fidl#10">MAX_DATA_SIZE</a></td>
            <td>
                    <code>65536</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.kms/key_manager_stateless.fidl#7">MAX_HARDWARE_DERIVE_KEY_INFO_SIZE</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint8</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.kms/key_manager_stateless.fidl#8">MAX_HARDWARE_DERIVED_KEY_SIZE</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint8</code></td>
            <td></td>
        </tr>
    
</table>

