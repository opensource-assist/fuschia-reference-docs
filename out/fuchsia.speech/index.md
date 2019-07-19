Project: /_project.yaml
Book: /_book.yaml

# fuchsia.speech


## **PROTOCOLS**

## SpeechToText {:#SpeechToText}
*Defined in [fuchsia.speech/speech_to_text.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.speech/speech_to_text.fidl#8)*


### BeginCapture {:#BeginCapture}

 Starts capturing speech from the microphone.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>transcription_listener</code></td>
            <td>
                <code><a class='link' href='../fuchsia.speech/index.html#TranscriptionListener'>TranscriptionListener</a></code>
            </td>
        </tr></table>



### ListenForHotword {:#ListenForHotword}

 Begins hotword detection. Detected hotword utterances are reported on the
 given listener.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>hotword_listener</code></td>
            <td>
                <code><a class='link' href='../fuchsia.speech/index.html#HotwordListener'>HotwordListener</a></code>
            </td>
        </tr></table>



## TranscriptionListener {:#TranscriptionListener}
*Defined in [fuchsia.speech/speech_to_text.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.speech/speech_to_text.fidl#21)*

 Represents an active transcription session. Either side may close this
 interface to indicate that transcription should stop. If the transcription is
 unexpectedly closed before `OnReady` is called, the implementer should treat
 it as an error (in such cases, `OnError` is called).

### OnReady {:#OnReady}

 Indicates that capture has begun. Prior to this, parts of the system may
 not have been initialized and audio may have been dropped. No calls to
 `OnTranscriptUpdate` will occur before `OnReady` is called.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### OnTranscriptUpdate {:#OnTranscriptUpdate}

 Receives updated transcripts. Each call receives the most likely
 transcription of the entire utterance at that time. Previously transcribed
 text may mutate in response to later input.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>spoken_text</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### OnSpeechLevelUpdate {:#OnSpeechLevelUpdate}

 Provides periodic updates on the user's speech signal power, when the
 microphone is open and streaming to the backend.
 `speech_level` is instantaneous speech power, in decibels (negative).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>speech_level</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>



### OnError {:#OnError}

 An error occurred before or during transcription. Depending on the nature
 of the error, this may occur before `OnReady` is called, and `OnReady` may
 never be called. This binding will be closed immediately after sending this
 message.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## HotwordListener {:#HotwordListener}
*Defined in [fuchsia.speech/speech_to_text.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.speech/speech_to_text.fidl#46)*

 Listens for hotwords. Each detected hotword utterance triggers `OnHotword`.
 Closure of this handle by the speech service indicates an error.

### OnReady {:#OnReady}

 Indicates that capture has begun. Prior to this, parts of the system may
 not have been initialized and audio may have been dropped. No calls to
 `OnHotword` will occur before `OnReady` is called.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### OnHotword {:#OnHotword}

 Called for each detected hotword utterance.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

















