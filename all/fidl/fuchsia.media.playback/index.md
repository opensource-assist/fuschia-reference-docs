Project: /_project.yaml
Book: /_book.yaml

# fuchsia.media.playback


## **PROTOCOLS**

## Player {:#Player}
*Defined in [fuchsia.media.playback/player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.playback/player.fidl#16)*

 Plays media.

### CreateHttpSource {:#CreateHttpSource}

 Creates a source that reads from a URL.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>http_url</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>headers</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.net.oldhttp/index.html'>fuchsia.net.oldhttp</a>/<a class='link' href='../fuchsia.net.oldhttp/index.html#HttpHeader'>HttpHeader</a>&gt;?</code>
            </td>
        </tr><tr>
            <td><code>source_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Source'>Source</a>&gt;</code>
            </td>
        </tr></table>



### CreateFileSource {:#CreateFileSource}

 Creates a source that reads from a file.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>file_channel</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr><tr>
            <td><code>source_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Source'>Source</a>&gt;</code>
            </td>
        </tr></table>



### CreateReaderSource {:#CreateReaderSource}

 Creates a source that reads from a `SeekingReader`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>seeking_reader</code></td>
            <td>
                <code><a class='link' href='#SeekingReader'>SeekingReader</a></code>
            </td>
        </tr><tr>
            <td><code>source_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Source'>Source</a>&gt;</code>
            </td>
        </tr></table>



### CreateElementarySource {:#CreateElementarySource}

 Creates a source that allows the client to provide independent elementary
 streams to the player. duration_ns, can_pause, can_seek and metadata are
 all included in the SourceStatus and, when the `ElementarySource` is used by
 the player, in the `PlayerStatus` as well. `can_pause` and `can_seek`, when
 false, constrain the capabilities of the player.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>duration_ns</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>can_pause</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>can_seek</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>metadata</code></td>
            <td>
                <code><a class='link' href='../fuchsia.media/index.html'>fuchsia.media</a>/<a class='link' href='../fuchsia.media/index.html#Metadata'>Metadata</a>?</code>
            </td>
        </tr><tr>
            <td><code>source_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ElementarySource'>ElementarySource</a>&gt;</code>
            </td>
        </tr></table>



### SetSource {:#SetSource}

 Sets the source for this player to use. If source is null, the player
 becomes idle.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Source'>Source</a>?</code>
            </td>
        </tr></table>



### TransitionToSource {:#TransitionToSource}

 Transitions to the specified source when playback of the current source
 reaches transition_pts. The new source starts playback at start_pts. If
 a transition is already pending, it will be discarded in favor of the new
 transition.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Source'>Source</a></code>
            </td>
        </tr><tr>
            <td><code>transition_pts</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>start_pts</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>



### CancelSourceTransition {:#CancelSourceTransition}

 Cancels a pending transition, returning the source. If no transition is
 pending, the request channel is closed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>returned_source_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Source'>Source</a>&gt;</code>
            </td>
        </tr></table>



### SetHttpSource {:#SetHttpSource}

 Sets an HTTP URL to read from. The provided headers are added to each
 HTTP request issued to the URL.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>http_url</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>headers</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.net.oldhttp/index.html'>fuchsia.net.oldhttp</a>/<a class='link' href='../fuchsia.net.oldhttp/index.html#HttpHeader'>HttpHeader</a>&gt;?</code>
            </td>
        </tr></table>



### SetFileSource {:#SetFileSource}

 Sets a file channel to read from.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>file_channel</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



### Play {:#Play}

 Starts playback.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Pause {:#Pause}

 Pauses playback.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### OnStatusChanged {:#OnStatusChanged}

 Provides current status immediately after binding and whenever status
 changes thereafter.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>player_status</code></td>
            <td>
                <code><a class='link' href='#PlayerStatus'>PlayerStatus</a></code>
            </td>
        </tr></table>

### Seek {:#Seek}

 Seeks to the specified position, specified in nanoseconds.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>position</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>



### CreateView {:#CreateView}

 Creates a video view.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#ViewToken'>ViewToken</a></code>
            </td>
        </tr></table>



### BindGainControl {:#BindGainControl}

 Binds to the gain control for this player.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>gain_control_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.media.audio/index.html'>fuchsia.media.audio</a>/<a class='link' href='../fuchsia.media.audio/index.html#GainControl'>GainControl</a>&gt;</code>
            </td>
        </tr></table>



### AddBinding {:#AddBinding}

 Adds a new binding to this player.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>player_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Player'>Player</a>&gt;</code>
            </td>
        </tr></table>



## SeekingReader {:#SeekingReader}
*Defined in [fuchsia.media.playback/seeking_reader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.playback/seeking_reader.fidl#11)*


### Describe {:#Describe}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>size</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>can_seek</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

### ReadAt {:#ReadAt}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>position</code></td>
            <td>
                <code>uint64</code>
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
        </tr><tr>
            <td><code>socket</code></td>
            <td>
                <code>handle&lt;socket&gt;?</code>
            </td>
        </tr></table>

## SourceManager {:#SourceManager}
*Defined in [fuchsia.media.playback/source_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.playback/source_manager.fidl#13)*

 Manages sources on behalf of a Player.

### CreateHttpSource {:#CreateHttpSource}

 Creates a source that reads from a URL.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>http_url</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>headers</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.net.oldhttp/index.html'>fuchsia.net.oldhttp</a>/<a class='link' href='../fuchsia.net.oldhttp/index.html#HttpHeader'>HttpHeader</a>&gt;?</code>
            </td>
        </tr><tr>
            <td><code>source_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Source'>Source</a>&gt;</code>
            </td>
        </tr></table>



### CreateFileSource {:#CreateFileSource}

 Creates a source that reads from a file.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>file_channel</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr><tr>
            <td><code>source_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Source'>Source</a>&gt;</code>
            </td>
        </tr></table>



### CreateReaderSource {:#CreateReaderSource}

 Creates a source that reads from a `SeekingReader`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>seeking_reader</code></td>
            <td>
                <code><a class='link' href='#SeekingReader'>SeekingReader</a></code>
            </td>
        </tr><tr>
            <td><code>source_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Source'>Source</a>&gt;</code>
            </td>
        </tr></table>



### CreateElementarySource {:#CreateElementarySource}

 Creates a source that allows the client to provide independent elementary
 streams to the player. duration_ns, can_pause, can_seek and metadata are
 all included in the SourceStatus and, when the `ElementarySource` is used by
 the player, in the `PlayerStatus` as well. `can_pause` and `can_seek`, when
 false, constrain the capabilities of the player.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>duration_ns</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>can_pause</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>can_seek</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>metadata</code></td>
            <td>
                <code><a class='link' href='../fuchsia.media/index.html'>fuchsia.media</a>/<a class='link' href='../fuchsia.media/index.html#Metadata'>Metadata</a>?</code>
            </td>
        </tr><tr>
            <td><code>source_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ElementarySource'>ElementarySource</a>&gt;</code>
            </td>
        </tr></table>



### SetSource {:#SetSource}

 Sets the source for this player to use. If source is null, the player
 becomes idle.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Source'>Source</a>?</code>
            </td>
        </tr></table>



### TransitionToSource {:#TransitionToSource}

 Transitions to the specified source when playback of the current source
 reaches transition_pts. The new source starts playback at start_pts. If
 a transition is already pending, it will be discarded in favor of the new
 transition.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#Source'>Source</a></code>
            </td>
        </tr><tr>
            <td><code>transition_pts</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>start_pts</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>



### CancelSourceTransition {:#CancelSourceTransition}

 Cancels a pending transition, returning the source. If no transition is
 pending, the request channel is closed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>returned_source_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Source'>Source</a>&gt;</code>
            </td>
        </tr></table>



## Source {:#Source}
*Defined in [fuchsia.media.playback/source_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.playback/source_manager.fidl#54)*

 A source of content that may be used by a player.

### OnStatusChanged {:#OnStatusChanged}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>source_status</code></td>
            <td>
                <code><a class='link' href='#SourceStatus'>SourceStatus</a></code>
            </td>
        </tr></table>

## ElementarySource {:#ElementarySource}
*Defined in [fuchsia.media.playback/source_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.playback/source_manager.fidl#61)*

 `Source` variant for providing elementary streams directly to the player.

### OnStatusChanged {:#OnStatusChanged}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>source_status</code></td>
            <td>
                <code><a class='link' href='#SourceStatus'>SourceStatus</a></code>
            </td>
        </tr></table>

### AddStream {:#AddStream}

 Adds an elementary stream. The elementary stream can be removed by
 closing the `SimpleStreamSink`. `ticks_per_second_numerator` and
 `ticks_per_second_denominator` indicate the units that will be used for
 `Streampacket` timestamp values. For nanoseconds units, for example,
 `ticks_per_second_numerator` should be 1000000000 and
 `ticks_per_second_denominator` should be 1. To use units of frames for
 48k audio, `ticks_per_second_numerator` should be 48000 and
 `ticks_per_second_denominator` should be 1.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='../fuchsia.media/index.html'>fuchsia.media</a>/<a class='link' href='../fuchsia.media/index.html#StreamType'>StreamType</a></code>
            </td>
        </tr><tr>
            <td><code>ticks_per_second_numerator</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>ticks_per_second_denominator</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>sink_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.media/index.html'>fuchsia.media</a>/<a class='link' href='../fuchsia.media/index.html#SimpleStreamSink'>SimpleStreamSink</a>&gt;</code>
            </td>
        </tr></table>



### AddBinding {:#AddBinding}

 Adds a new binding to this `ElementarySource`. By using this method,
 the client can obtain an additional channel through which to communicate
 to this `ElementarySource` even after a channel is consumed by a call to
 `SourceManager.SetSource`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>source_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ElementarySource'>ElementarySource</a>&gt;</code>
            </td>
        </tr></table>





## **STRUCTS**

### PlayerStatus {:#PlayerStatus}
*Defined in [fuchsia.media.playback/player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.playback/player.fidl#52)*



 Player status information.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>duration</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> Duration of the content.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>can_pause</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Whether the player can pause.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>can_seek</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Whether the player can seek.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>has_audio</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Whether the source has an audio stream.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>has_video</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Whether the source has a video stream.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>ready</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Indicates whether the player is ready to play. After `SetHttpSource`,
 `SetFileSource` or `SourceManager.SetSource` is called, this value is
 false until the player is fully prepared to play the content from the
 source.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>metadata</code></td>
            <td>
                <code><a class='link' href='../fuchsia.media/index.html'>fuchsia.media</a>/<a class='link' href='../fuchsia.media/index.html#Metadata'>Metadata</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>problem</code></td>
            <td>
                <code><a class='link' href='#Problem'>Problem</a>?</code>
            </td>
            <td> Indicates a problem preventing intended operation.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>audio_connected</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Indicates whether an audio stream is currently connected for rendering.
 This value will be false if `has_audio` is false or if the audio stream
 type isn't supported.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>video_connected</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Indicates whether a video stream is currently connected for rendering.
 This value will be false if `has_video` is false or if the video stream
 type isn't supported.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>video_size</code></td>
            <td>
                <code><a class='link' href='../fuchsia.math/index.html'>fuchsia.math</a>/<a class='link' href='../fuchsia.math/index.html#Size'>Size</a>?</code>
            </td>
            <td> Size of the video currently being produced. This value will be null if
 the video size is currently unknown.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>pixel_aspect_ratio</code></td>
            <td>
                <code><a class='link' href='../fuchsia.math/index.html'>fuchsia.math</a>/<a class='link' href='../fuchsia.math/index.html#Size'>Size</a>?</code>
            </td>
            <td> Relative dimensions of a video pixel. This value will be null if the
 pixel aspect ratio is currently unknown.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>timeline_function</code></td>
            <td>
                <code><a class='link' href='../fuchsia.media/index.html'>fuchsia.media</a>/<a class='link' href='../fuchsia.media/index.html#TimelineFunction'>TimelineFunction</a>?</code>
            </td>
            <td> Function translating local time to presentation time. This value will be
 null if the timeline function is currently undefined.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>end_of_stream</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Indicates whether presentation for all streams has reached end-of-stream.
</td>
            <td>No default</td>
        </tr>
</table>

### Problem {:#Problem}
*Defined in [fuchsia.media.playback/problem.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.playback/problem.fidl#17)*



 Models a problem preventing intended operation.

 A `Problem` is generally surfaced as part of a component's status, probably
 as an optional field. Absence of a `Problem` means that nothing is preventing
 intended operation. When a problem is exposed, the client can take action
 automatically or present relevant UI. If a problem can be resolved by some
 action, the client may take that action automatically or enlist the user
 somehow in the resolution. In either case, the problem goes away when the
 issue that caused it to be exposed is resolved. By design, there is no
 general means of dismissing a problem.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>type</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The type of problem. This is a string for extensibility.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>details</code></td>
            <td>
                <code>string?</code>
            </td>
            <td> Type-dependent details.
</td>
            <td>No default</td>
        </tr>
</table>

### SourceStatus {:#SourceStatus}
*Defined in [fuchsia.media.playback/source_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.playback/source_manager.fidl#97)*



 Source status information.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>duration</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> Duration of the content.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>can_pause</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Whether the source can pause.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>can_seek</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Whether the source can seek.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>has_audio</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Whether the source has an audio stream.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>has_video</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Whether the source has a video stream.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>ready</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Indicates whether the source is ready. A true value signals that the
 content has been probed and there are no known problems with it.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>metadata</code></td>
            <td>
                <code><a class='link' href='../fuchsia.media/index.html'>fuchsia.media</a>/<a class='link' href='../fuchsia.media/index.html#Metadata'>Metadata</a>?</code>
            </td>
            <td> Describes the media.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>problem</code></td>
            <td>
                <code><a class='link' href='#Problem'>Problem</a>?</code>
            </td>
            <td> Indicates a problem preventing intended operation. A null value
 indicates that the source is functioning as intended.
</td>
            <td>No default</td>
        </tr>
</table>













## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.playback/problem.fidl#25">PROBLEM_INTERNAL</a></td>
            <td><code>fuchsia.media.playback.Internal</code></td>
                    <td><code>String</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.playback/problem.fidl#27">PROBLEM_ASSET_NOT_FOUND</a></td>
            <td><code>fuchsia.media.playback.AssetNotFound</code></td>
                    <td><code>String</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.playback/problem.fidl#29">PROBLEM_CONTAINER_NOT_SUPPORTED</a></td>
            <td><code>fuchsia.media.playback.ContainerNotSupported</code></td>
                    <td><code>String</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.playback/problem.fidl#31">PROBLEM_AUDIO_ENCODING_NOT_SUPPORTED</a></td>
            <td><code>fuchsia.media.playback.AudioEncodingNotSupported</code></td>
                    <td><code>String</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.playback/problem.fidl#33">PROBLEM_VIDEO_ENCODING_NOT_SUPPORTED</a></td>
            <td><code>fuchsia.media.playback.VideoEncodingNotSupported</code></td>
                    <td><code>String</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.playback/problem.fidl#35">PROBLEM_CONNECTION_FAILED</a></td>
            <td><code>fuchsia.media.playback.ConnectionFailed</code></td>
                    <td><code>String</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.playback/seeking_reader.fidl#25">UNKNOWN_SIZE</a></td>
            <td>
                    <code>18446744073709551615</code>
                </td>
                <td><code>uint64</code></td>
        </tr>
    
</table>

