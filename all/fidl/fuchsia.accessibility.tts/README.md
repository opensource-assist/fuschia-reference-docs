[TOC]

# fuchsia.accessibility.tts


## **PROTOCOLS**

## Engine {#Engine}
*Defined in [fuchsia.accessibility.tts/tts.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.tts/tts.fidl#43)*

<p>An interface to produce speech output.
Assistive technology use an Engine to start producing speech output and
set configuration parameters that control the speech.
TODO(MI4-2452): Implement pause, stop and resume.</p>

### Enqueue {#Enqueue}

<p>Enqueues  an utterance to be spoken. Speech is not started until Speak
is called.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>utterance</code></td>
            <td>
                <code><a class='link' href='#Utterance'>Utterance</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Engine_Enqueue_Result'>Engine_Enqueue_Result</a></code>
            </td>
        </tr></table>

### Speak {#Speak}

<p>Speaks all enqueued utterances. The method returns the value when they
are all finished playing.</p>

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
                <code><a class='link' href='#Engine_Speak_Result'>Engine_Speak_Result</a></code>
            </td>
        </tr></table>

### Cancel {#Cancel}

<p>Cancels current speech and also empties the queue.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## TtsManager {#TtsManager}
*Defined in [fuchsia.accessibility.tts/tts_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.tts/tts_manager.fidl#12)*

<p>An interface to manage TTS for assistive technology.</p>
<p>The TTS Manager offers assistive technology a way to open a TTS engine to
start producing speech output.</p>

### OpenEngine {#OpenEngine}

<p>A speaker is an assistive technology that wants to produce speech
output. Only one speaker is allowed to have an open connection to the
engine at a time. If already in use, BUSY error is returned.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>engine_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Engine'>Engine</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#TtsManager_OpenEngine_Result'>TtsManager_OpenEngine_Result</a></code>
            </td>
        </tr></table>

## EngineRegistry {#EngineRegistry}
*Defined in [fuchsia.accessibility.tts/tts_registration.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.tts/tts_registration.fidl#9)*

<p>An interface for TTS Engines provide speech output.</p>

### RegisterEngine {#RegisterEngine}

<p>A TTS engine registers itself to start listening for incoming speech
output requests through |engine|.
At the moment, only one TTS Engine can be registered at a time.
This registry owners the first engine to register itself.
If an engine crashes and wants to register again, calling this method
will restart the connection. An error is returned if another engine is
already registered.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>engine</code></td>
            <td>
                <code><a class='link' href='#Engine'>Engine</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#EngineRegistry_RegisterEngine_Result'>EngineRegistry_RegisterEngine_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Engine_Enqueue_Response {#Engine_Enqueue_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Engine_Speak_Response {#Engine_Speak_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### TtsManager_OpenEngine_Response {#TtsManager_OpenEngine_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### EngineRegistry_RegisterEngine_Response {#EngineRegistry_RegisterEngine_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>



## **ENUMS**

### Error {#Error}
Type: <code>uint32</code>

*Defined in [fuchsia.accessibility.tts/tts.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.tts/tts.fidl#10)*

<p>Error codes for TTS operations.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NOT_IMPLEMENTED</code></td>
            <td><code>1</code></td>
            <td><p>The underlying TTS engine does not support this operation.</p>
</td>
        </tr><tr>
            <td><code>OUT_OF_RANGE</code></td>
            <td><code>2</code></td>
            <td><p>The value is out of range for a particular TTS parameter.</p>
</td>
        </tr><tr>
            <td><code>BAD_STATE</code></td>
            <td><code>3</code></td>
            <td><p>The operation is impossible to be completed.</p>
</td>
        </tr><tr>
            <td><code>BUSY</code></td>
            <td><code>4</code></td>
            <td><p>This operation can not be completed because the TTS service is in use.</p>
</td>
        </tr></table>



## **TABLES**

### VoiceParameters {#VoiceParameters}


*Defined in [fuchsia.accessibility.tts/tts.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.tts/tts.fidl#23)*

<p>Parameters of a voice.
TODO(MI4-2453): Add extra voice parameters such as speech rate and  pitch.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>language</code></td>
            <td>
                <code><a class='link' href='../fuchsia.intl/'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/#LocaleId'>LocaleId</a></code>
            </td>
            <td><p>The current selected language.</p>
</td>
        </tr></table>

### Utterance {#Utterance}


*Defined in [fuchsia.accessibility.tts/tts.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.tts/tts.fidl#29)*

<p>An utterance holds information about its message and how it should be spoken.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>message</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The message to be spoken.
Clients should pay attention to the FIDL maximum size for a message,
splitting when necessary into several utterances.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>params</code></td>
            <td>
                <code><a class='link' href='#VoiceParameters'>VoiceParameters</a></code>
            </td>
            <td><p>Parameters that control the speech output.</p>
</td>
        </tr></table>



## **UNIONS**

### Engine_Enqueue_Result {#Engine_Enqueue_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Engine_Enqueue_Response'>Engine_Enqueue_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Engine_Speak_Result {#Engine_Speak_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Engine_Speak_Response'>Engine_Speak_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### TtsManager_OpenEngine_Result {#TtsManager_OpenEngine_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#TtsManager_OpenEngine_Response'>TtsManager_OpenEngine_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### EngineRegistry_RegisterEngine_Result {#EngineRegistry_RegisterEngine_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#EngineRegistry_RegisterEngine_Response'>EngineRegistry_RegisterEngine_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>







