[TOC]

# fuchsia.castauth


## **PROTOCOLS**

## CastKeySigner {#CastKeySigner}
*Defined in [fuchsia.castauth/cast_auth.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.castauth/cast_auth.fidl#26)*

<p>This FIDL interface is used to sign with hardware Cast key.
It is intended for short-term use only and will not be supported on all
devices. It will eventually be replaced by an attestation service.</p>

### SignHash {#SignHash}

<p>Use Cast key to sign a hash value.</p>
<p>The input is hash value.
The return value is the error code or the signature if the operation
succeeds. The signature algorithm is RSA-2048-PKCS1.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>hash</code></td>
            <td>
                <code><a class='link' href='#Asn1EncodedHash'>Asn1EncodedHash</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#CastKeySigner_SignHash_Result'>CastKeySigner_SignHash_Result</a></code>
            </td>
        </tr></table>

### GetCertificateChain {#GetCertificateChain}

<p>Get the Cast certificate chain.</p>
<p>The return value is the error code or the certificate chain if
the operation succeeds. The chain contains Cast key cert,
one or more intermediate CA certs and root CA cert.</p>

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
                <code><a class='link' href='#CastKeySigner_GetCertificateChain_Result'>CastKeySigner_GetCertificateChain_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### CastKeySigner_SignHash_Response {#CastKeySigner_SignHash_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>signature</code></td>
            <td>
                <code>uint8[256]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### CastKeySigner_GetCertificateChain_Response {#CastKeySigner_GetCertificateChain_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>cert_chain</code></td>
            <td>
                <code>vector&lt;vector&gt;[16]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### ErrorCode {#ErrorCode}
Type: <code>uint32</code>

*Defined in [fuchsia.castauth/cast_auth.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.castauth/cast_auth.fidl#15)*

<p>Error codes for CastKeySigner operations.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>FILE_NOT_FOUND</code></td>
            <td><code>1</code></td>
            <td><p>Key/cert not found in storage.</p>
</td>
        </tr><tr>
            <td><code>CRYPTO_ERROR</code></td>
            <td><code>2</code></td>
            <td><p>Error occurred during signing operation.</p>
</td>
        </tr></table>





## **UNIONS**

### CastKeySigner_SignHash_Result {#CastKeySigner_SignHash_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#CastKeySigner_SignHash_Response'>CastKeySigner_SignHash_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ErrorCode'>ErrorCode</a></code>
            </td>
            <td></td>
        </tr></table>

### CastKeySigner_GetCertificateChain_Result {#CastKeySigner_GetCertificateChain_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#CastKeySigner_GetCertificateChain_Response'>CastKeySigner_GetCertificateChain_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ErrorCode'>ErrorCode</a></code>
            </td>
            <td></td>
        </tr></table>

### Asn1EncodedHash {#Asn1EncodedHash}
*Defined in [fuchsia.castauth/cast_auth.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.castauth/cast_auth.fidl#9)*

<p>Input hash to be signed by Cast key.
It must be ASN1-encoded SHA1 or SHA256 hash, with sizes 35 or 51 bytes.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>sha1</code></td>
            <td>
                <code>uint8[35]</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>sha256</code></td>
            <td>
                <code>uint8[51]</code>
            </td>
            <td></td>
        </tr></table>







