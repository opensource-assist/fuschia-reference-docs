[TOC]

# fuchsia.media.sessions2


## **PROTOCOLS**

## SessionControl {#SessionControl}
*Defined in [fuchsia.media.sessions2/discovery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/discovery.fidl#39)*

<p>A protocol for clients to control sessions and view their status.</p>

### Play {#Play}

<p>Plays media.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Pause {#Pause}

<p>Pauses playback and retains position in media</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Stop {#Stop}

<p>Stops playback. The session should close.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Seek {#Seek}

<p>Seeks to a specific position in media. Implementations are free to
enter an error state if the position is out of bounds. <code>position</code>
is an offset from the beginning of the media.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>position</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>



### SkipForward {#SkipForward}

<p>Skips forward in media by the player's default skip amount.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SkipReverse {#SkipReverse}

<p>Skips in reverse in media by the player's default skip amount.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### NextItem {#NextItem}

<p>Changes media to the next item (e.g. next song in playlist).</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### PrevItem {#PrevItem}

<p>Changes media to the previous item.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SetPlaybackRate {#SetPlaybackRate}

<p>Sets the playback rate of the media. This will not change the
playback mode.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>playback_rate</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>



### SetRepeatMode {#SetRepeatMode}

<p>Sets repeat mode to any of the supported repeat modes.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>repeat_mode</code></td>
            <td>
                <code><a class='link' href='#RepeatMode'>RepeatMode</a></code>
            </td>
        </tr></table>



### SetShuffleMode {#SetShuffleMode}

<p>Sets shuffle mode.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>shuffle_on</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### BindVolumeControl {#BindVolumeControl}

<p>Binds to the session's volume control for control and notifications.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>volume_control_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.media.audio/'>fuchsia.media.audio</a>/<a class='link' href='../fuchsia.media.audio/#VolumeControl'>VolumeControl</a>&gt;</code>
            </td>
        </tr></table>



## SessionsWatcher {#SessionsWatcher}
*Defined in [fuchsia.media.sessions2/discovery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/discovery.fidl#76)*

<p><code>SessionsWatcher</code> watches the collection of published sessions.</p>

### SessionUpdated {#SessionUpdated}

<p>Called by the registry service when a session is updated. On first connection,
this will be called as many times as needed to communicate the state of the
world.</p>
<p><code>SessionsWatchers</code> must reply to acknlowledge receipt of the session info delta.
Delinquent watchers who do not reply will eventually be disconnected.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>session_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>session_info_delta</code></td>
            <td>
                <code><a class='link' href='#SessionInfoDelta'>SessionInfoDelta</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### SessionRemoved {#SessionRemoved}

<p>Called by the registry service when a session is removed from the registered
collection.</p>
<p><code>SessionsWatchers</code> must reply to acknlowledge receipt of the session removal.
Delinquent watchers who do not reply will eventually be disconnected.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>session_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## Discovery {#Discovery}
*Defined in [fuchsia.media.sessions2/discovery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/discovery.fidl#96)*

<p><code>Discovery</code> observes the collection of published media sessions
and connects clients to them.</p>

### WatchSessions {#WatchSessions}

<p>Connects a session watcher configured with the given options.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watch_options</code></td>
            <td>
                <code><a class='link' href='#WatchOptions'>WatchOptions</a></code>
            </td>
        </tr><tr>
            <td><code>session_watcher</code></td>
            <td>
                <code><a class='link' href='#SessionsWatcher'>SessionsWatcher</a></code>
            </td>
        </tr></table>



### ConnectToSession {#ConnectToSession}

<p>Connects to a <code>SessionControl</code> for <code>session_id</code> if present. Drops the
given channel otherwise.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>session_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>session_control_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#SessionControl'>SessionControl</a>&gt;</code>
            </td>
        </tr></table>



## PlayerControl {#PlayerControl}
*Defined in [fuchsia.media.sessions2/player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/player.fidl#22)*

<p>Controls for a media player.</p>

### Play {#Play}

<p>Plays media.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Pause {#Pause}

<p>Pauses playback and retains position in media</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Stop {#Stop}

<p>Stops playback. The session should close.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Seek {#Seek}

<p>Seeks to a specific position in media. Implementations are free to
enter an error state if the position is out of bounds. <code>position</code>
is an offset from the beginning of the media.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>position</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>



### SkipForward {#SkipForward}

<p>Skips forward in media by the player's default skip amount.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SkipReverse {#SkipReverse}

<p>Skips in reverse in media by the player's default skip amount.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### NextItem {#NextItem}

<p>Changes media to the next item (e.g. next song in playlist).</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### PrevItem {#PrevItem}

<p>Changes media to the previous item.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SetPlaybackRate {#SetPlaybackRate}

<p>Sets the playback rate of the media. This will not change the
playback mode.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>playback_rate</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>



### SetRepeatMode {#SetRepeatMode}

<p>Sets repeat mode to any of the supported repeat modes.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>repeat_mode</code></td>
            <td>
                <code><a class='link' href='#RepeatMode'>RepeatMode</a></code>
            </td>
        </tr></table>



### SetShuffleMode {#SetShuffleMode}

<p>Sets shuffle mode.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>shuffle_on</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### BindVolumeControl {#BindVolumeControl}

<p>Binds to the session's volume control for control and notifications.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>volume_control_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.media.audio/'>fuchsia.media.audio</a>/<a class='link' href='../fuchsia.media.audio/#VolumeControl'>VolumeControl</a>&gt;</code>
            </td>
        </tr></table>



## Player {#Player}
*Defined in [fuchsia.media.sessions2/player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/player.fidl#155)*

<p><code>Player</code> is a handle for a media player. Unsupported commands are
no-ops.  Consult <code>PlaybackCapabilities</code>, sent by to learn which
commands are supported.</p>

### Play {#Play}

<p>Plays media.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Pause {#Pause}

<p>Pauses playback and retains position in media</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Stop {#Stop}

<p>Stops playback. The session should close.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Seek {#Seek}

<p>Seeks to a specific position in media. Implementations are free to
enter an error state if the position is out of bounds. <code>position</code>
is an offset from the beginning of the media.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>position</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>



### SkipForward {#SkipForward}

<p>Skips forward in media by the player's default skip amount.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SkipReverse {#SkipReverse}

<p>Skips in reverse in media by the player's default skip amount.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### NextItem {#NextItem}

<p>Changes media to the next item (e.g. next song in playlist).</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### PrevItem {#PrevItem}

<p>Changes media to the previous item.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SetPlaybackRate {#SetPlaybackRate}

<p>Sets the playback rate of the media. This will not change the
playback mode.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>playback_rate</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>



### SetRepeatMode {#SetRepeatMode}

<p>Sets repeat mode to any of the supported repeat modes.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>repeat_mode</code></td>
            <td>
                <code><a class='link' href='#RepeatMode'>RepeatMode</a></code>
            </td>
        </tr></table>



### SetShuffleMode {#SetShuffleMode}

<p>Sets shuffle mode.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>shuffle_on</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### BindVolumeControl {#BindVolumeControl}

<p>Binds to the session's volume control for control and notifications.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>volume_control_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.media.audio/'>fuchsia.media.audio</a>/<a class='link' href='../fuchsia.media.audio/#VolumeControl'>VolumeControl</a>&gt;</code>
            </td>
        </tr></table>



### WatchInfoChange {#WatchInfoChange}

<p>Leave hanging to receive a response when the player's
status changes.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>player_info_delta</code></td>
            <td>
                <code><a class='link' href='#PlayerInfoDelta'>PlayerInfoDelta</a></code>
            </td>
        </tr></table>

## Publisher {#Publisher}
*Defined in [fuchsia.media.sessions2/publisher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/publisher.fidl#19)*

<p><code>Publisher</code> publishes media players so they may be discovered and
controlled by clients who have permission to do so.</p>

### PublishPlayer {#PublishPlayer}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>player</code></td>
            <td>
                <code><a class='link' href='#Player'>Player</a></code>
            </td>
        </tr><tr>
            <td><code>registration</code></td>
            <td>
                <code><a class='link' href='#PlayerRegistration'>PlayerRegistration</a></code>
            </td>
        </tr></table>



### Publish {#Publish}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>player</code></td>
            <td>
                <code><a class='link' href='#Player'>Player</a></code>
            </td>
        </tr><tr>
            <td><code>registration</code></td>
            <td>
                <code><a class='link' href='#PlayerRegistration'>PlayerRegistration</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>session_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



## **STRUCTS**

### ImageSizeVariant {#ImageSizeVariant}
*Defined in [fuchsia.media.sessions2/images.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/images.fidl#18)*



<p>A variant of an image at a specific size.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>url</code></td>
            <td>
                <code>string[1000]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>width</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### MediaImageType {#MediaImageType}
Type: <code>uint32</code>

*Defined in [fuchsia.media.sessions2/images.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/images.fidl#9)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ARTWORK</code></td>
            <td><code>0</code></td>
            <td><p>Artwork for the playing media.</p>
</td>
        </tr><tr>
            <td><code>SOURCE_ICON</code></td>
            <td><code>1</code></td>
            <td><p>An icon for the source of the playing media (e.g. the player or
streaming service).</p>
</td>
        </tr></table>

### ContentType {#ContentType}
Type: <code>uint32</code>

*Defined in [fuchsia.media.sessions2/player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/player.fidl#55)*

<p>The type of content playing back, which should be set to the largest
applicable value.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OTHER</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>AUDIO</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>VIDEO</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>MUSIC</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>TV_SHOW</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>MOVIE</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr></table>

### PlayerState {#PlayerState}
Type: <code>uint32</code>

*Defined in [fuchsia.media.sessions2/player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/player.fidl#81)*

<p>State of a media player.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>IDLE</code></td>
            <td><code>0</code></td>
            <td><p>The initial state of a session if there is no associated media.</p>
</td>
        </tr><tr>
            <td><code>PLAYING</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>PAUSED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>BUFFERING</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERROR</code></td>
            <td><code>4</code></td>
            <td><p>The player cannot recover from this state and will close.</p>
</td>
        </tr></table>

### Error {#Error}
Type: <code>uint32</code>

*Defined in [fuchsia.media.sessions2/player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/player.fidl#93)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OTHER</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### RepeatMode {#RepeatMode}
Type: <code>uint32</code>

*Defined in [fuchsia.media.sessions2/player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/player.fidl#98)*

<p>Modes of repeating playback of the current media.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OFF</code></td>
            <td><code>0</code></td>
            <td><p>No repeat.</p>
</td>
        </tr><tr>
            <td><code>GROUP</code></td>
            <td><code>1</code></td>
            <td><p>Repeat the relevant group of media (e.g. playlist).</p>
</td>
        </tr><tr>
            <td><code>SINGLE</code></td>
            <td><code>2</code></td>
            <td><p>Repeat the currently playing media.</p>
</td>
        </tr></table>



## **TABLES**

### SessionInfoDelta {#SessionInfoDelta}


*Defined in [fuchsia.media.sessions2/discovery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/discovery.fidl#17)*

<p>SessionInfoDelta holds a description of a given session. The first
time a client receives this, it is a state of the world. On successive
receipts of this table, only the changed fields will be present (this
property is not recursive; top-level fields if set are snapshots).</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>domain</code></td>
            <td>
                <code>string[1000]</code>
            </td>
            <td><p>The domain on which the session takes place. A domain identifies a set of
mutually compatable media targets and sessions; sessions on a domain may
be played back on targets of the same domain.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>is_local</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Whether the entry point for the media into our device network is the local
machine; this should be true if this is the device streaming from
a music service, but false if this machine is just receiving an audio stream
to act as a speaker.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>is_locally_active</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>If this is set, the playback is taking place local to the device.
Playing on the device speaker is local, playing on a remote speaker
is not. This is only set when the session is playing back; a paused
session is not active.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>player_status</code></td>
            <td>
                <code><a class='link' href='#PlayerStatus'>PlayerStatus</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>metadata</code></td>
            <td>
                <code><a class='link' href='../fuchsia.media/'>fuchsia.media</a>/<a class='link' href='../fuchsia.media/#Metadata'>Metadata</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>6</td>
            <td><code>media_images</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#MediaImage'>MediaImage</a>&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td>7</td>
            <td><code>player_capabilities</code></td>
            <td>
                <code><a class='link' href='#PlayerCapabilities'>PlayerCapabilities</a></code>
            </td>
            <td></td>
        </tr></table>

### WatchOptions {#WatchOptions}


*Defined in [fuchsia.media.sessions2/discovery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/discovery.fidl#70)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>only_active</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Watch only the active session. Watches all if not set.</p>
</td>
        </tr></table>

### MediaImage {#MediaImage}


*Defined in [fuchsia.media.sessions2/images.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/images.fidl#25)*

<p>An image for playing media.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>image_type</code></td>
            <td>
                <code><a class='link' href='#MediaImageType'>MediaImageType</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>sizes</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ImageSizeVariant'>ImageSizeVariant</a>&gt;[16]</code>
            </td>
            <td><p>Available variants of the image.</p>
</td>
        </tr></table>

### PlayerStatus {#PlayerStatus}


*Defined in [fuchsia.media.sessions2/player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/player.fidl#65)*

<p>Status of a media player.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>duration</code></td>
            <td>
                <code>int64</code>
            </td>
            <td><p>Total duration of playing media. Omitted if not known or not applicable.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>player_state</code></td>
            <td>
                <code><a class='link' href='#PlayerState'>PlayerState</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>timeline_function</code></td>
            <td>
                <code><a class='link' href='../fuchsia.media/'>fuchsia.media</a>/<a class='link' href='../fuchsia.media/#TimelineFunction'>TimelineFunction</a></code>
            </td>
            <td><p>A playback function that describes the position and rate of
play through the media as a function of <code>CLOCK_MONOTONIC</code>.</p>
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
            <td><code>content_type</code></td>
            <td>
                <code><a class='link' href='#ContentType'>ContentType</a></code>
            </td>
            <td><p>The type of content playing back. Omitted if it is not a first class
category.</p>
</td>
        </tr><tr>
            <td>7</td>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### PlayerCapabilities {#PlayerCapabilities}


*Defined in [fuchsia.media.sessions2/player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/player.fidl#134)*

<p><code>PlaybackCapabilities</code> enumerates the capabilities of a media player, and
corresponds to the control commands it can execute.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>flags</code></td>
            <td>
                <code><a class='link' href='#PlayerCapabilityFlags'>PlayerCapabilityFlags</a></code>
            </td>
            <td></td>
        </tr></table>

### PlayerInfoDelta {#PlayerInfoDelta}


*Defined in [fuchsia.media.sessions2/player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/player.fidl#140)*

<p>When emitted, fields that have changed should be set.
The first emission to a new client should be a snapshot.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>local</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Whether the entry point for the media into our device network is the
local machine; this should be true if this is the device streaming
from a music service, but false or omitted if this machine is just
receiving an audio stream to act as a speaker.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>player_status</code></td>
            <td>
                <code><a class='link' href='#PlayerStatus'>PlayerStatus</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>metadata</code></td>
            <td>
                <code><a class='link' href='../fuchsia.media/'>fuchsia.media</a>/<a class='link' href='../fuchsia.media/#Metadata'>Metadata</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>media_images</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#MediaImage'>MediaImage</a>&gt;[16]</code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>player_capabilities</code></td>
            <td>
                <code><a class='link' href='#PlayerCapabilities'>PlayerCapabilities</a></code>
            </td>
            <td></td>
        </tr></table>

### PlayerRegistration {#PlayerRegistration}


*Defined in [fuchsia.media.sessions2/publisher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/publisher.fidl#10)*

<p>All information required by the media session registry service to
register a player so that clients may observe its status and control
it.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>domain</code></td>
            <td>
                <code>string[1000]</code>
            </td>
            <td><p>The domain on which the player exists. Unset if it is the native
Fuchsia domain.</p>
</td>
        </tr></table>







## **BITS**

### PlayerCapabilityFlags {#PlayerCapabilityFlags}
Type: <code>uint32</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>PLAY</td>
            <td>1</td>
            <td><p>If set, the player can <code>Play()</code>.</p>
</td>
        </tr><tr>
            <td>PAUSE</td>
            <td>4</td>
            <td><p>If set, the player can <code>Pause()</code>.</p>
</td>
        </tr><tr>
            <td>SEEK</td>
            <td>8</td>
            <td><p>If set, the player can <code>Seek()</code>.</p>
</td>
        </tr><tr>
            <td>SKIP_FORWARD</td>
            <td>16</td>
            <td><p>If set, the player can <code>SkipForward()</code>.</p>
</td>
        </tr><tr>
            <td>SKIP_REVERSE</td>
            <td>32</td>
            <td><p>If set, the player can <code>SkipReverse()</code>.</p>
</td>
        </tr><tr>
            <td>SHUFFLE</td>
            <td>64</td>
            <td><p>If set, the player can shuffle media.</p>
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
            <td><p>If set, the player can <code>BindGainControl()</code>.</p>
</td>
        </tr><tr>
            <td>REPEAT_GROUPS</td>
            <td>1024</td>
            <td><p>If set, the player can repeat groups.</p>
</td>
        </tr><tr>
            <td>REPEAT_SINGLE</td>
            <td>2048</td>
            <td><p>If set, the player can repeat single media items.</p>
</td>
        </tr></table>



