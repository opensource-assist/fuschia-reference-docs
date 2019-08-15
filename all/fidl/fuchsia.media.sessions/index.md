Project: /_project.yaml
Book: /_book.yaml

# fuchsia.media.sessions


## **PROTOCOLS**

## Publisher {:#Publisher}
*Defined in [fuchsia.media.sessions/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions/service.fidl#11)*

 `Publisher` publishes media sessions. This allows priviledged processes to
 send media controls to the media session and observe changes in its
 playback state.

### Publish {:#Publish}

 Publishes a session. Returns `session_id` which can be used to
 to identify the session.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>session</code></td>
            <td>
                <code><a class='link' href='#Session'>Session</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>session_id</code></td>
            <td>
                <code>handle&lt;event&gt;</code>
            </td>
        </tr></table>

### PublishRemote {:#PublishRemote}

 Publishes a remote session, whose playback does not originate on this
 device. Returns a `session_id` which can be used to identify the session.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>session</code></td>
            <td>
                <code><a class='link' href='#Session'>Session</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>session_id</code></td>
            <td>
                <code>handle&lt;event&gt;</code>
            </td>
        </tr></table>

## Registry {:#Registry}
*Defined in [fuchsia.media.sessions/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions/service.fidl#48)*

 `Registry` observes the collection of published media sessions
 and vends control handles to them.

### OnActiveSessionChanged {:#OnActiveSessionChanged}

 `OnActiveSessionChanged` is sent on connection and when the
 underlying active session is changed.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>active_session</code></td>
            <td>
                <code><a class='link' href='#ActiveSession'>ActiveSession</a></code>
            </td>
        </tr></table>

### NotifyActiveSessionChangeHandled {:#NotifyActiveSessionChangeHandled}

 Notifies the `Registry` that the active session change events was handled
 and that the client is ready for more. If you want these events, send
 this message on receipt of them. After some amount of events are sent
 without receipts, the client will stop receiving events from the
 `Registry`.

 Never sending this message has no effect other than unsubscribing from
 these events.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### OnSessionsChanged {:#OnSessionsChanged}

 When the set of registered sessions changes, this event is sent. On
 connection the client is caught up to the state of the collection with
 "ADD" events for each existing session.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>sessions_change</code></td>
            <td>
                <code><a class='link' href='#SessionsChange'>SessionsChange</a></code>
            </td>
        </tr></table>

### NotifySessionsChangeHandled {:#NotifySessionsChangeHandled}

 Notifies the `Registry` that the sessions change event was handled
 and that the client is ready for more. If you want these events, send
 this message on receipt of them. After some amount of events are sent
 without receipts, the client will stop receiving events from the
 `Registry`.

 Never sending this message has no effect other than unsubscribing from
 these events.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### ConnectToSessionById {:#ConnectToSessionById}

 Connects to a `Session` for `session_id` if present.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>session_id</code></td>
            <td>
                <code>handle&lt;event&gt;</code>
            </td>
        </tr><tr>
            <td><code>session_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Session'>Session</a>&gt;</code>
            </td>
        </tr></table>



## ReadOnlySession {:#ReadOnlySession}
*Defined in [fuchsia.media.sessions/session.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions/session.fidl#15)*

 `ReadOnlySession` is a handle for media playback, allowing clients to observe
 a playback session.

### OnPlaybackStatusChanged {:#OnPlaybackStatusChanged}

 Sent on first connection and when playback
 status changes.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>playback_status</code></td>
            <td>
                <code><a class='link' href='#PlaybackStatus'>PlaybackStatus</a></code>
            </td>
        </tr></table>

### OnMetadataChanged {:#OnMetadataChanged}

 Sent on first connection and when metadata
 changes.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>media_metadata</code></td>
            <td>
                <code><a class='link' href='../fuchsia.media/index.html'>fuchsia.media</a>/<a class='link' href='../fuchsia.media/index.html#Metadata'>Metadata</a></code>
            </td>
        </tr></table>

### OnMediaImagesChanged {:#OnMediaImagesChanged}

 Sent on first connection if there are images, and when media images
 change. Sends only the image type that has changed: if album
 art changes but not source icon, the source icon is not re-sent.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>media_images</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#MediaImage'>MediaImage</a>&gt;</code>
            </td>
        </tr></table>

### GetMediaImageBitmap {:#GetMediaImageBitmap}

 Returns the bitmap for a given image url. This url is expected to be a
 url the session gave the client in an `OnMediaImagesChanged` event. If
 the minimum size is not available or the url is not recognized, the
 session may return a null image.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>url</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>minimum_size</code></td>
            <td>
                <code><a class='link' href='../fuchsia.math/index.html'>fuchsia.math</a>/<a class='link' href='../fuchsia.math/index.html#Size'>Size</a></code>
            </td>
        </tr><tr>
            <td><code>desired_size</code></td>
            <td>
                <code><a class='link' href='../fuchsia.math/index.html'>fuchsia.math</a>/<a class='link' href='../fuchsia.math/index.html#Size'>Size</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>media_image_bitmap</code></td>
            <td>
                <code><a class='link' href='#MediaImageBitmap'>MediaImageBitmap</a>?</code>
            </td>
        </tr></table>

## Session {:#Session}
*Defined in [fuchsia.media.sessions/session.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions/session.fidl#40)*

 `Session` is a handle for media playback, allowing clients to observe
 and control a media playback session. Unsupported commands are no-ops.
 Consult `PlaybackCapabilities`, sent by `OnPlaybackCapabilities`, to learn
 which commands are supported.

### OnPlaybackStatusChanged {:#OnPlaybackStatusChanged}

 Sent on first connection and when playback
 status changes.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>playback_status</code></td>
            <td>
                <code><a class='link' href='#PlaybackStatus'>PlaybackStatus</a></code>
            </td>
        </tr></table>

### OnMetadataChanged {:#OnMetadataChanged}

 Sent on first connection and when metadata
 changes.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>media_metadata</code></td>
            <td>
                <code><a class='link' href='../fuchsia.media/index.html'>fuchsia.media</a>/<a class='link' href='../fuchsia.media/index.html#Metadata'>Metadata</a></code>
            </td>
        </tr></table>

### OnMediaImagesChanged {:#OnMediaImagesChanged}

 Sent on first connection if there are images, and when media images
 change. Sends only the image type that has changed: if album
 art changes but not source icon, the source icon is not re-sent.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>media_images</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#MediaImage'>MediaImage</a>&gt;</code>
            </td>
        </tr></table>

### GetMediaImageBitmap {:#GetMediaImageBitmap}

 Returns the bitmap for a given image url. This url is expected to be a
 url the session gave the client in an `OnMediaImagesChanged` event. If
 the minimum size is not available or the url is not recognized, the
 session may return a null image.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>url</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>minimum_size</code></td>
            <td>
                <code><a class='link' href='../fuchsia.math/index.html'>fuchsia.math</a>/<a class='link' href='../fuchsia.math/index.html#Size'>Size</a></code>
            </td>
        </tr><tr>
            <td><code>desired_size</code></td>
            <td>
                <code><a class='link' href='../fuchsia.math/index.html'>fuchsia.math</a>/<a class='link' href='../fuchsia.math/index.html#Size'>Size</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>media_image_bitmap</code></td>
            <td>
                <code><a class='link' href='#MediaImageBitmap'>MediaImageBitmap</a>?</code>
            </td>
        </tr></table>

### OnPlaybackCapabilitiesChanged {:#OnPlaybackCapabilitiesChanged}

 Sent on first connection and when supported
 playback capabilities change.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>playback_capabilities</code></td>
            <td>
                <code><a class='link' href='#PlaybackCapabilities'>PlaybackCapabilities</a></code>
            </td>
        </tr></table>

### Play {:#Play}

 Plays media.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Pause {:#Pause}

 Pauses playback and retains position in media

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Stop {:#Stop}

 Stops playback. There is no position or associated media in the stopped
 state.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SeekToPosition {:#SeekToPosition}

 Seeks to a specific position in media. Implementations are free to
 to treat this as a no-op or enter an error state if the position
 is out of bounds. `position` is an offset from the beginning of the media.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>position</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>



### SkipForward {:#SkipForward}

 Skips forward in media. Uses the default skip interval if `skip_amount`
 is 0.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>skip_amount</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>



### SkipReverse {:#SkipReverse}

 Skips in reverse in media. Uses the default skip interval if `skip_amount`
 is 0.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>skip_amount</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>



### NextItem {:#NextItem}

 Changes media to the next item (e.g. next song in playlist).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### PrevItem {:#PrevItem}

 Changes media to the previous item.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SetPlaybackRate {:#SetPlaybackRate}

 Sets the playback rate of the media. This may imply a change of
 playback mode.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>playback_rate</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>



### SetRepeatMode {:#SetRepeatMode}

 Sets repeat mode to any of the supported repeat modes.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>repeat_mode</code></td>
            <td>
                <code><a class='link' href='#RepeatMode'>RepeatMode</a></code>
            </td>
        </tr></table>



### SetShuffleMode {:#SetShuffleMode}

 Sets shuffle mode.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>shuffle_on</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### BindGainControl {:#BindGainControl}

 Binds to the session's gain control for control and notifications.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>gain_control_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.media.audio/index.html'>fuchsia.media.audio</a>/<a class='link' href='../fuchsia.media.audio/index.html#GainControl'>GainControl</a>&gt;</code>
            </td>
        </tr></table>



### ConnectToExtension {:#ConnectToExtension}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>extension</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>channel</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>





## **STRUCTS**

### MediaImage {:#MediaImage}
*Defined in [fuchsia.media.sessions/image.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions/image.fidl#19)*



 An image for playing media.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>image_type</code></td>
            <td>
                <code><a class='link' href='#MediaImageType'>MediaImageType</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>url</code></td>
            <td>
                <code>string</code>
            </td>
            <td> A url the client can use to load the image or request a bitmap from the
 player.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>mime_type</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The mime type of the image if loaded through the given url by the client.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>sizes</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.math/index.html'>fuchsia.math</a>/<a class='link' href='../fuchsia.math/index.html#Size'>Size</a>&gt;</code>
            </td>
            <td> Dimensions in which the image is available.
</td>
            <td>No default</td>
        </tr>
</table>

### MediaImageBitmap {:#MediaImageBitmap}
*Defined in [fuchsia.media.sessions/image.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions/image.fidl#31)*



 An ARGB8888 bitmap image.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>size</code></td>
            <td>
                <code><a class='link' href='../fuchsia.math/index.html'>fuchsia.math</a>/<a class='link' href='../fuchsia.math/index.html#Size'>Size</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>argb8888_pixel_data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SessionsChange {:#SessionsChange}
*Defined in [fuchsia.media.sessions/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions/service.fidl#40)*



 A change to the set of registered sessions.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>session</code></td>
            <td>
                <code><a class='link' href='#SessionEntry'>SessionEntry</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>delta</code></td>
            <td>
                <code><a class='link' href='#SessionDelta'>SessionDelta</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### MediaImageType {:#MediaImageType}
Type: <code>uint32</code>

*Defined in [fuchsia.media.sessions/image.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions/image.fidl#10)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ARTWORK</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>SOURCE_ICON</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### PlaybackState {:#PlaybackState}
Type: <code>uint32</code>

*Defined in [fuchsia.media.sessions/playback_status.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions/playback_status.fidl#28)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>STOPPED</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>PLAYING</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>PAUSED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERROR</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### RepeatMode {:#RepeatMode}
Type: <code>uint32</code>

*Defined in [fuchsia.media.sessions/playback_status.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions/playback_status.fidl#40)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OFF</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>GROUP</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>SINGLE</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### SessionDelta {:#SessionDelta}
Type: <code>uint32</code>

*Defined in [fuchsia.media.sessions/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions/service.fidl#34)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ADDED</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>REMOVED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### PlaybackCapabilities {:#PlaybackCapabilities}


*Defined in [fuchsia.media.sessions/playback_capabilities.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions/playback_capabilities.fidl#35)*

 `PlaybackCapabilities` enumerates the capabilities of the player backing
 the media session, and correspond to the control commands they can execute.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>flags</code></td>
            <td>
                <code><a class='link' href='#PlaybackCapabilityFlags'>PlaybackCapabilityFlags</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>supported_skip_intervals</code></td>
            <td>
                <code>vector&lt;int64&gt;</code>
            </td>
            <td> The intervals on which skipping can be performed in the media.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>supported_playback_rates</code></td>
            <td>
                <code>vector&lt;float32&gt;</code>
            </td>
            <td> The playback rates supported by the media.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>supported_repeat_modes</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#RepeatMode'>RepeatMode</a>&gt;</code>
            </td>
            <td> Supported repeat modes that can be set with `SetRepeatMode()`.
</td>
        </tr><tr>
            <td>5</td>
            <td><code>custom_extensions</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td> A set of names of custom extensions the player advertises.
</td>
        </tr></table>

### PlaybackStatus {:#PlaybackStatus}


*Defined in [fuchsia.media.sessions/playback_status.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions/playback_status.fidl#10)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>duration</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> Total duration of playing media. 0 if not known or not applicable.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>playback_state</code></td>
            <td>
                <code><a class='link' href='#PlaybackState'>PlaybackState</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>playback_function</code></td>
            <td>
                <code><a class='link' href='../fuchsia.media/index.html'>fuchsia.media</a>/<a class='link' href='../fuchsia.media/index.html#TimelineFunction'>TimelineFunction</a></code>
            </td>
            <td> A playback function that describes the position and rate of play through
 the media.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>repeat_mode</code></td>
            <td>
                <code><a class='link' href='#RepeatMode'>RepeatMode</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>shuffle_on</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td>6</td>
            <td><code>has_next_item</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Whether a media item exists after the playing one in queue (e.g. a next
 song in an album or next video in a playlist.)
</td>
        </tr><tr>
            <td>7</td>
            <td><code>has_prev_item</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Whether a media item preceded the playing one in queue.
</td>
        </tr><tr>
            <td>8</td>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Error {:#Error}


*Defined in [fuchsia.media.sessions/playback_status.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions/playback_status.fidl#35)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>code</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>description</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr></table>

### ActiveSession {:#ActiveSession}


*Defined in [fuchsia.media.sessions/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions/service.fidl#22)*

 Describes the session which is currently implementing the active session
 interface.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>session_id</code></td>
            <td>
                <code>handle&lt;event&gt;</code>
            </td>
            <td></td>
        </tr></table>

### SessionEntry {:#SessionEntry}


*Defined in [fuchsia.media.sessions/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions/service.fidl#27)*

 A registered session in the Media Session registry.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>session_id</code></td>
            <td>
                <code>handle&lt;event&gt;</code>
            </td>
            <td> The id of the registered session.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>local</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Whether the session takes place locally on this device.
</td>
        </tr></table>







## **BITS**
### PlaybackCapabilityFlags {:#PlaybackCapabilityFlags}
Type: <code>uint32</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>PLAY</td>
            <td>1</td>
            <td> If set, the player can `Play()`.
</td>
        </tr><tr>
            <td>STOP</td>
            <td>2</td>
            <td> If set, the player can `Stop()`.
</td>
        </tr><tr>
            <td>PAUSE</td>
            <td>4</td>
            <td> If set, the player can `Pause()`.
</td>
        </tr><tr>
            <td>SEEK_TO_POSITION</td>
            <td>8</td>
            <td> If set, the player can `SeekToPosition()`.
</td>
        </tr><tr>
            <td>SKIP_FORWARD</td>
            <td>16</td>
            <td> If set, the player can `SkipForward()` on `supported_skip_intervals`.
</td>
        </tr><tr>
            <td>SKIP_REVERSE</td>
            <td>32</td>
            <td> If set, the player can `SkipReverse()` on `supported_skip_intervals`.
</td>
        </tr><tr>
            <td>SHUFFLE</td>
            <td>64</td>
            <td> The intervals on which skipping can be performed in the media.
</td>
        </tr><tr>
            <td>CHANGE_TO_NEXT_ITEM</td>
            <td>128</td>
            <td></td>
        </tr><tr>
            <td>CHANGE_TO_PREV_ITEM</td>
            <td>256</td>
            <td></td>
        </tr><tr>
            <td>HAS_GAIN_CONTROL</td>
            <td>512</td>
            <td> If set, the player can `BindGainControl()`.
</td>
        </tr><tr>
            <td>PROVIDE_BITMAPS</td>
            <td>1024</td>
            <td> If set, the player can provide bitmaps of its artwork.
</td>
        </tr></table>



