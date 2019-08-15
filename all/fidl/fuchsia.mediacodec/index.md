Project: /_project.yaml
Book: /_book.yaml

# fuchsia.mediacodec


## **PROTOCOLS**

## CodecFactory {:#CodecFactory}
*Defined in [fuchsia.mediacodec/codec_factory.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.mediacodec/codec_factory.fidl#222)*


### OnCodecList {:#OnCodecList}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>codecs</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#CodecDescription'>CodecDescription</a>&gt;</code>
            </td>
        </tr></table>

### CreateDecoder {:#CreateDecoder}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>decoder_params</code></td>
            <td>
                <code><a class='link' href='#CreateDecoder_Params'>CreateDecoder_Params</a></code>
            </td>
        </tr><tr>
            <td><code>decoder</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.media/index.html'>fuchsia.media</a>/<a class='link' href='../fuchsia.media/index.html#StreamProcessor'>StreamProcessor</a>&gt;</code>
            </td>
        </tr></table>



### CreateEncoder {:#CreateEncoder}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>encoder_params</code></td>
            <td>
                <code><a class='link' href='#CreateEncoder_Params'>CreateEncoder_Params</a></code>
            </td>
        </tr><tr>
            <td><code>encoder</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.media/index.html'>fuchsia.media</a>/<a class='link' href='../fuchsia.media/index.html#StreamProcessor'>StreamProcessor</a>&gt;</code>
            </td>
        </tr></table>





## **STRUCTS**

### CodecDescription {:#CodecDescription}
*Defined in [fuchsia.mediacodec/codec_factory.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.mediacodec/codec_factory.fidl#187)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>codec_type</code></td>
            <td>
                <code><a class='link' href='#CodecType'>CodecType</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>mime_type</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>can_stream_bytes_input</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>true</td>
        </tr><tr>
            <td><code>can_find_start</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>true</td>
        </tr><tr>
            <td><code>can_re_sync</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>true</td>
        </tr><tr>
            <td><code>will_report_all_detected_errors</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>true</td>
        </tr><tr>
            <td><code>is_hw</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>true</td>
        </tr><tr>
            <td><code>split_header_handling</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>true</td>
        </tr>
</table>



## **ENUMS**

### CodecType {:#CodecType}
Type: <code>uint32</code>

*Defined in [fuchsia.mediacodec/codec_factory.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.mediacodec/codec_factory.fidl#182)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DECODER</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>ENCODER</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### CreateDecoder_Params {:#CreateDecoder_Params}


*Defined in [fuchsia.mediacodec/codec_factory.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.mediacodec/codec_factory.fidl#14)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>input_details</code></td>
            <td>
                <code><a class='link' href='../fuchsia.media/index.html'>fuchsia.media</a>/<a class='link' href='../fuchsia.media/index.html#FormatDetails'>FormatDetails</a></code>
            </td>
            <td> Input mime type for a decoder.

 The recognized mime types for now:
 video/h264
 video/vp9
 audio/aac
   input_details.oob_bytes must be an AudioSpecificConfig() as defined
   by AAC spec.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>promise_separate_access_units_on_input</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> This must be true in order for the client to be permitted to put a
 timestamp on an input packet, which is in turn required to get any
 timestamps on any output packets.

 It is always legal to provide separate Access Units (henceforth AUs) to a
 decoder, but this boolean must be true for a decoder to accept and
 propagate timestamp values.

 This must be true when creating a video encoder, or the CodecFactory
 channel will close.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>require_can_stream_bytes_input</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Require that the selected codec be capable of accepting input where
 AUs are not separated into separate packets.

 This does not imply that the decoder can find the start of the first AU;
 for that see require_can_find_start.  This does not imply that the decoder
 can re-sync on its own if the stream data is damaged; for that see
 require_can_re_sync.

 If both promise_separate_access_units_on_input and
 require_can_stream_bytes_input are true, the CodecFactory channel will
 close.

 If this is false, the client must feed separate AUs on the fuchsia.ui.input.  This
 must be false for a video encoder, and if true the CodecFactory channel
 will close.

 Unless a client demands a decoder capable of taking concatenated AUs
 (require_can_stream_bytes_input true), the client must feed a decoder
 separate AUs.  This means the client cannot have parts of two separate AUs
 in the same packet, unless require_can_stream_bytes_input is true.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>require_can_find_start</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> A decoder is allowed to be capable of streaming bytes but not capable of
 searching for the start of the first usable AU.  To require both, set both
 require_can_stream_bytes_input and require_can_find_start.  Setting
 require_can_find_start without require_can_stream_bytes_input is invalid.

 With require_can_stream_bytes_input true but require_can_find_start false,
 the client must start the first packet with the start of an AU, but can
 send a stream of bytes after that.
</td>
        </tr><tr>
            <td>5</td>
            <td><code>require_can_re_sync</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> On problematic input data, all decoders are expected to at least be able to
 close the channel rather than getting stuck in a failed and/or broken
 state.

 A decoder returned from a request with require_can_re_sync is potentially
 able to handle damaged input without closing the Codec channel.  Such a
 Codec is encouraged, but not required, to also satisfy requirements of
 require_report_all_detected_errors.
</td>
        </tr><tr>
            <td>6</td>
            <td><code>require_report_all_detected_errors</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Sometimes a client would rather fail an overall use of a decoder than fail
 to notice data corruption.  For such scenarios, the client can specify
 require_report_all_detected_errors.  For any codec returned from a
 request with require_report_all_detected_errors set, on detection of
 any input data corruption the codec will report in one or more of these
 ways:
   * closing the Codec channel
   * OnStreamFailed()
   * error_detected_before
   * error_detected_during

 If false, a codec may silently skip past corrupted input data.

 No decoder can detect all corruption, because some corruption can look like
 valid stream data.  This requirement is only to request a codec that
 is written to attempt to detect _and report_ input stream corruption.

 This flag is not intended to be 100% bulletproof.  If a client needs robust
 assurance that _all_ detectable stream corruption is _always_ detected,
 this flag is not enough of a guarantee to achieve that.  Since some stream
 corruption is inherently non-detectable in any case, such a client should
 consider using stronger techniques upstream to ensure that corruption can
 be detected with the needed probability very close to 1.

 This flag being true doesn't imply anything about whether the codec will
 discard damaged data vs. producing corresponding damaged output.  Only that
 the codec will set error_detected_* bools to true when appropriate.

 Regardless of this setting, not all timestamp_ish values provided on input
 are guaranteed to show up on output.
</td>
        </tr><tr>
            <td>7</td>
            <td><code>require_hw</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, require that the returned codec is HW-accelerated.
</td>
        </tr><tr>
            <td>8</td>
            <td><code>permit_lack_of_split_header_handling</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> permit_lack_of_split_header_handling

 This field is a temporary field that will be going away.

 TODO(dustingreen): Remove this field once we're down to zero codecs with
 problems handling split headers.

 By default, a Codec instance is required to handle "split headers", meaning
 that a client is allowed to deliver parts of an AU one byte at a time,
 including parts near the beginning of the AU, and the codec is required to
 tolerate and handle that properly.  However, unfortunately not all codecs
 properly support split headers.  If a client is willing to permit such a
 codec to be used, the client can set this to true.  Clients are not
 encouraged to set this, but setting it may be necessary to find a codec for
 some formats _for now_.  If a client sets this to true, the client should
 deliver data of each AU with many contiguous non-split bytes from the start
 of each AU.  The client is not strictly required to deliver one AU at a
 time, only to ensure that either all the AU bytes are in a single packet or
 that many bytes at the start of each AU are in a single packet.

 The specification for how a client should use this and how a client should
 behave if setting this to true is intentionally vague, because lack of
 support for header splitting is not ideal, and is expected to be
 temporary, and all codecs should handle split headers in the long run.
 The main intent of this field is to avoid giving an innocent client using
 default value of false here a codec that can't properly handle split
 headers.  This is not an attempt at a mechanism to fully work around a
 codec that doesn't handle split headers.
</td>
        </tr></table>

### CreateEncoder_Params {:#CreateEncoder_Params}


*Defined in [fuchsia.mediacodec/codec_factory.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.mediacodec/codec_factory.fidl#168)*

 Parameters used to request an encoder.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>input_details</code></td>
            <td>
                <code><a class='link' href='../fuchsia.media/index.html'>fuchsia.media</a>/<a class='link' href='../fuchsia.media/index.html#FormatDetails'>FormatDetails</a></code>
            </td>
            <td> The format of the uncompressed input data.

 This field should be a raw mime_type (e.g. 'video/raw') and uncompressed
 format details for the encoder to use when reading buffers.

 To be elibigible an encoder must support the input format.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>require_hw</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, require that the returned codec is HW-accelerated.
</td>
        </tr></table>









