[TOC]

# fuchsia.tts


## **PROTOCOLS**

## TtsService {#TtsService}
*Defined in [fuchsia.tts/tts.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.tts/tts.fidl#8)*


### Say {#Say}

<p>Speak the string of words provided.  Return the provided token to the
caller when the speaking has finished.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>words</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>token</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>token</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

















