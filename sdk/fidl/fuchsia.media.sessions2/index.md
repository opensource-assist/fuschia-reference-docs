Project: /_project.yaml
Book: /_book.yaml

# fuchsia.media.sessions2


## **PROTOCOLS**

## SessionControl {:#SessionControl}
*Defined in [fuchsia.media.sessions2/discovery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/discovery.fidl#39)*

 A protocol for clients to control sessions and view their status.

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

 Stops playback. The session should close.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Seek {:#Seek}

 Seeks to a specific position in media. Implementations are free to
 enter an error state if the position is out of bounds. `position`
 is an offset from the beginning of the media.

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

 Skips forward in media by the player's default skip amount.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SkipReverse {:#SkipReverse}

 Skips in reverse in media by the player's default skip amount.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



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

 Sets the playback rate of the media. This will not change the
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



### BindVolumeControl {:#BindVolumeControl}

 Binds to the session's volume control for control and notifications.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>volume_control_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.media.audio/index.html'>fuchsia.media.audio</a>/<a class='link' href='../fuchsia.media.audio/index.html#VolumeControl'>VolumeControl</a>&gt;</code>
            </td>
        </tr></table>



## SessionsWatcher {:#SessionsWatcher}
*Defined in [fuchsia.media.sessions2/discovery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/discovery.fidl#80)*

 `SessionsWatcher` watches the collection of published sessions.

### SessionUpdated {:#SessionUpdated}

 Called by the registry service when a session is updated. On first connection,
 this will be called as many times as needed to communicate the state of the
 world.

 `SessionsWatchers` must reply to acknlowledge receipt of the session info delta.
 Delinquent watchers who do not reply will eventually be disconnected.

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

### SessionRemoved {:#SessionRemoved}

 Called by the registry service when a session is removed from the registered
 collection.

 `SessionsWatchers` must reply to acknlowledge receipt of the session removal.
 Delinquent watchers who do not reply will eventually be disconnected.

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

## Discovery {:#Discovery}
*Defined in [fuchsia.media.sessions2/discovery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/discovery.fidl#100)*

 `Discovery` observes the collection of published media sessions
 and connects clients to them.

### WatchSessions {:#WatchSessions}

 Connects a session watcher configured with the given options.

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



### ConnectToSession {:#ConnectToSession}

 Connects to a `SessionControl` for `session_id` if present. Drops the
 given channel otherwise.

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



## PlayerControl {:#PlayerControl}
*Defined in [fuchsia.media.sessions2/player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/player.fidl#22)*

 Controls for a media player.

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

 Stops playback. The session should close.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Seek {:#Seek}

 Seeks to a specific position in media. Implementations are free to
 enter an error state if the position is out of bounds. `position`
 is an offset from the beginning of the media.

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

 Skips forward in media by the player's default skip amount.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SkipReverse {:#SkipReverse}

 Skips in reverse in media by the player's default skip amount.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



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

 Sets the playback rate of the media. This will not change the
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



### BindVolumeControl {:#BindVolumeControl}

 Binds to the session's volume control for control and notifications.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>volume_control_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.media.audio/index.html'>fuchsia.media.audio</a>/<a class='link' href='../fuchsia.media.audio/index.html#VolumeControl'>VolumeControl</a>&gt;</code>
            </td>
        </tr></table>



## Player {:#Player}
*Defined in [fuchsia.media.sessions2/player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/player.fidl#160)*

 `Player` is a handle for a media player. Unsupported commands are
 no-ops.  Consult `PlaybackCapabilities`, sent by to learn which
 commands are supported.

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

 Stops playback. The session should close.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Seek {:#Seek}

 Seeks to a specific position in media. Implementations are free to
 enter an error state if the position is out of bounds. `position`
 is an offset from the beginning of the media.

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

 Skips forward in media by the player's default skip amount.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SkipReverse {:#SkipReverse}

 Skips in reverse in media by the player's default skip amount.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



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

 Sets the playback rate of the media. This will not change the
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



### BindVolumeControl {:#BindVolumeControl}

 Binds to the session's volume control for control and notifications.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>volume_control_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.media.audio/index.html'>fuchsia.media.audio</a>/<a class='link' href='../fuchsia.media.audio/index.html#VolumeControl'>VolumeControl</a>&gt;</code>
            </td>
        </tr></table>



### WatchInfoChange {:#WatchInfoChange}

 Leave hanging to receive a response when the player's
 status changes.

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

## Publisher {:#Publisher}
*Defined in [fuchsia.media.sessions2/publisher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/publisher.fidl#19)*

 `Publisher` publishes media players so they may be discovered and
 controlled by clients who have permission to do so.

### PublishPlayer {:#PublishPlayer}


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



## SessionControl {:#SessionControl}
*Defined in [fuchsia.media.sessions2/discovery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/discovery.fidl#39)*

 A protocol for clients to control sessions and view their status.

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

 Stops playback. The session should close.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Seek {:#Seek}

 Seeks to a specific position in media. Implementations are free to
 enter an error state if the position is out of bounds. `position`
 is an offset from the beginning of the media.

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

 Skips forward in media by the player's default skip amount.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SkipReverse {:#SkipReverse}

 Skips in reverse in media by the player's default skip amount.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



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

 Sets the playback rate of the media. This will not change the
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



### BindVolumeControl {:#BindVolumeControl}

 Binds to the session's volume control for control and notifications.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>volume_control_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.media.audio/index.html'>fuchsia.media.audio</a>/<a class='link' href='../fuchsia.media.audio/index.html#VolumeControl'>VolumeControl</a>&gt;</code>
            </td>
        </tr></table>



## SessionsWatcher {:#SessionsWatcher}
*Defined in [fuchsia.media.sessions2/discovery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/discovery.fidl#80)*

 `SessionsWatcher` watches the collection of published sessions.

### SessionUpdated {:#SessionUpdated}

 Called by the registry service when a session is updated. On first connection,
 this will be called as many times as needed to communicate the state of the
 world.

 `SessionsWatchers` must reply to acknlowledge receipt of the session info delta.
 Delinquent watchers who do not reply will eventually be disconnected.

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

### SessionRemoved {:#SessionRemoved}

 Called by the registry service when a session is removed from the registered
 collection.

 `SessionsWatchers` must reply to acknlowledge receipt of the session removal.
 Delinquent watchers who do not reply will eventually be disconnected.

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

## Discovery {:#Discovery}
*Defined in [fuchsia.media.sessions2/discovery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/discovery.fidl#100)*

 `Discovery` observes the collection of published media sessions
 and connects clients to them.

### WatchSessions {:#WatchSessions}

 Connects a session watcher configured with the given options.

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



### ConnectToSession {:#ConnectToSession}

 Connects to a `SessionControl` for `session_id` if present. Drops the
 given channel otherwise.

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



## PlayerControl {:#PlayerControl}
*Defined in [fuchsia.media.sessions2/player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/player.fidl#22)*

 Controls for a media player.

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

 Stops playback. The session should close.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Seek {:#Seek}

 Seeks to a specific position in media. Implementations are free to
 enter an error state if the position is out of bounds. `position`
 is an offset from the beginning of the media.

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

 Skips forward in media by the player's default skip amount.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SkipReverse {:#SkipReverse}

 Skips in reverse in media by the player's default skip amount.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



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

 Sets the playback rate of the media. This will not change the
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



### BindVolumeControl {:#BindVolumeControl}

 Binds to the session's volume control for control and notifications.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>volume_control_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.media.audio/index.html'>fuchsia.media.audio</a>/<a class='link' href='../fuchsia.media.audio/index.html#VolumeControl'>VolumeControl</a>&gt;</code>
            </td>
        </tr></table>



## Player {:#Player}
*Defined in [fuchsia.media.sessions2/player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/player.fidl#160)*

 `Player` is a handle for a media player. Unsupported commands are
 no-ops.  Consult `PlaybackCapabilities`, sent by to learn which
 commands are supported.

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

 Stops playback. The session should close.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Seek {:#Seek}

 Seeks to a specific position in media. Implementations are free to
 enter an error state if the position is out of bounds. `position`
 is an offset from the beginning of the media.

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

 Skips forward in media by the player's default skip amount.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SkipReverse {:#SkipReverse}

 Skips in reverse in media by the player's default skip amount.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



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

 Sets the playback rate of the media. This will not change the
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



### BindVolumeControl {:#BindVolumeControl}

 Binds to the session's volume control for control and notifications.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>volume_control_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.media.audio/index.html'>fuchsia.media.audio</a>/<a class='link' href='../fuchsia.media.audio/index.html#VolumeControl'>VolumeControl</a>&gt;</code>
            </td>
        </tr></table>



### WatchInfoChange {:#WatchInfoChange}

 Leave hanging to receive a response when the player's
 status changes.

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

## Publisher {:#Publisher}
*Defined in [fuchsia.media.sessions2/publisher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/publisher.fidl#19)*

 `Publisher` publishes media players so they may be discovered and
 controlled by clients who have permission to do so.

### PublishPlayer {:#PublishPlayer}


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





## **STRUCTS**

### ImageSizeVariant {:#ImageSizeVariant}
*Defined in [fuchsia.media.sessions2/images.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/images.fidl#18)*



 A variant of an image at a specific size.


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

### ImageSizeVariant {:#ImageSizeVariant}
*Defined in [fuchsia.media.sessions2/images.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/images.fidl#18)*



 A variant of an image at a specific size.


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

### MediaImageType {:#MediaImageType}
Type: <code>uint32</code>

*Defined in [fuchsia.media.sessions2/images.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/images.fidl#9)*



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

### ContentType {:#ContentType}
Type: <code>uint32</code>

*Defined in [fuchsia.media.sessions2/player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/player.fidl#60)*

 The type of content playing back, which should be set to the largest
 applicable value.


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

### PlayerState {:#PlayerState}
Type: <code>uint32</code>

*Defined in [fuchsia.media.sessions2/player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/player.fidl#86)*

 State of a media player.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>IDLE</code></td>
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
            <td><code>BUFFERING</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERROR</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr></table>

### Error {:#Error}
Type: <code>uint32</code>

*Defined in [fuchsia.media.sessions2/player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/player.fidl#98)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OTHER</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### RepeatMode {:#RepeatMode}
Type: <code>uint32</code>

*Defined in [fuchsia.media.sessions2/player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/player.fidl#103)*

 Modes of repeating playback of the current media.


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

### MediaImageType {:#MediaImageType}
Type: <code>uint32</code>

*Defined in [fuchsia.media.sessions2/images.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/images.fidl#9)*



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

### ContentType {:#ContentType}
Type: <code>uint32</code>

*Defined in [fuchsia.media.sessions2/player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/player.fidl#60)*

 The type of content playing back, which should be set to the largest
 applicable value.


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

### PlayerState {:#PlayerState}
Type: <code>uint32</code>

*Defined in [fuchsia.media.sessions2/player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/player.fidl#86)*

 State of a media player.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>IDLE</code></td>
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
            <td><code>BUFFERING</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERROR</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr></table>

### Error {:#Error}
Type: <code>uint32</code>

*Defined in [fuchsia.media.sessions2/player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/player.fidl#98)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OTHER</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### RepeatMode {:#RepeatMode}
Type: <code>uint32</code>

*Defined in [fuchsia.media.sessions2/player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/player.fidl#103)*

 Modes of repeating playback of the current media.


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



## **TABLES**

### SessionInfoDelta {:#SessionInfoDelta}


*Defined in [fuchsia.media.sessions2/discovery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/discovery.fidl#17)*

 SessionInfoDelta holds a description of a given session. The first
 time a client receives this, it is a state of the world. On successive
 receipts of this table, only the changed fields will be present (this
 property is not recursive; top-level fields if set are snapshots).


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>domain</code></td>
            <td>
                <code>string[1000]</code>
            </td>
            <td> The domain on which the session takes place. A domain identifies a set of
 mutually compatable media targets and sessions; sessions on a domain may
 be played back on targets of the same domain.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>is_local</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Whether the entry point for the media into our device network is the local
 machine; this should be true if this is the device streaming from
 a music service, but false if this machine is just receiving an audio stream
 to act as a speaker.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>is_locally_active</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If this is set, the playback is taking place local to the device.
 Playing on the device speaker is local, playing on a remote speaker
 is not. This is only set when the session is playing back; a paused
 session is not active.
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
                <code><a class='link' href='../fuchsia.media/index.html'>fuchsia.media</a>/<a class='link' href='../fuchsia.media/index.html#Metadata'>Metadata</a></code>
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

### WatchOptions {:#WatchOptions}


*Defined in [fuchsia.media.sessions2/discovery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/discovery.fidl#74)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>only_active</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Watch only the active session. Watches all if not set.
</td>
        </tr></table>

### MediaImage {:#MediaImage}


*Defined in [fuchsia.media.sessions2/images.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/images.fidl#25)*

 An image for playing media.


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
            <td> Available variants of the image.
</td>
        </tr></table>

### PlayerStatus {:#PlayerStatus}


*Defined in [fuchsia.media.sessions2/player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/player.fidl#70)*

 Status of a media player.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>duration</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> Total duration of playing media. Omitted if not known or not applicable.
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
                <code><a class='link' href='../fuchsia.media/index.html'>fuchsia.media</a>/<a class='link' href='../fuchsia.media/index.html#TimelineFunction'>TimelineFunction</a></code>
            </td>
            <td> A playback function that describes the position and rate of
 play through the media as a function of `CLOCK_MONOTONIC`.
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
            <td> The type of content playing back. Omitted if it is not a first class
 category.
</td>
        </tr><tr>
            <td>7</td>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### PlayerCapabilities {:#PlayerCapabilities}


*Defined in [fuchsia.media.sessions2/player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/player.fidl#139)*

 `PlaybackCapabilities` enumerates the capabilities of a media player, and
 corresponds to the control commands it can execute.


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

### PlayerInfoDelta {:#PlayerInfoDelta}


*Defined in [fuchsia.media.sessions2/player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/player.fidl#145)*

 When emitted, fields that have changed should be set.
 The first emission to a new client should be a snapshot.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>local</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Whether the entry point for the media into our device network is the
 local machine; this should be true if this is the device streaming
 from a music service, but false or omitted if this machine is just
 receiving an audio stream to act as a speaker.
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
                <code><a class='link' href='../fuchsia.media/index.html'>fuchsia.media</a>/<a class='link' href='../fuchsia.media/index.html#Metadata'>Metadata</a></code>
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

### PlayerRegistration {:#PlayerRegistration}


*Defined in [fuchsia.media.sessions2/publisher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/publisher.fidl#10)*

 All information required by the media session registry service to
 register a player so that clients may observe its status and control
 it.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>domain</code></td>
            <td>
                <code>string[1000]</code>
            </td>
            <td> The domain on which the player exists. Unset if it is the native
 Fuchsia domain.
</td>
        </tr></table>

### SessionInfoDelta {:#SessionInfoDelta}


*Defined in [fuchsia.media.sessions2/discovery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/discovery.fidl#17)*

 SessionInfoDelta holds a description of a given session. The first
 time a client receives this, it is a state of the world. On successive
 receipts of this table, only the changed fields will be present (this
 property is not recursive; top-level fields if set are snapshots).


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>domain</code></td>
            <td>
                <code>string[1000]</code>
            </td>
            <td> The domain on which the session takes place. A domain identifies a set of
 mutually compatable media targets and sessions; sessions on a domain may
 be played back on targets of the same domain.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>is_local</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Whether the entry point for the media into our device network is the local
 machine; this should be true if this is the device streaming from
 a music service, but false if this machine is just receiving an audio stream
 to act as a speaker.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>is_locally_active</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If this is set, the playback is taking place local to the device.
 Playing on the device speaker is local, playing on a remote speaker
 is not. This is only set when the session is playing back; a paused
 session is not active.
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
                <code><a class='link' href='../fuchsia.media/index.html'>fuchsia.media</a>/<a class='link' href='../fuchsia.media/index.html#Metadata'>Metadata</a></code>
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

### WatchOptions {:#WatchOptions}


*Defined in [fuchsia.media.sessions2/discovery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/discovery.fidl#74)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>only_active</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Watch only the active session. Watches all if not set.
</td>
        </tr></table>

### MediaImage {:#MediaImage}


*Defined in [fuchsia.media.sessions2/images.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/images.fidl#25)*

 An image for playing media.


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
            <td> Available variants of the image.
</td>
        </tr></table>

### PlayerStatus {:#PlayerStatus}


*Defined in [fuchsia.media.sessions2/player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/player.fidl#70)*

 Status of a media player.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>duration</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> Total duration of playing media. Omitted if not known or not applicable.
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
                <code><a class='link' href='../fuchsia.media/index.html'>fuchsia.media</a>/<a class='link' href='../fuchsia.media/index.html#TimelineFunction'>TimelineFunction</a></code>
            </td>
            <td> A playback function that describes the position and rate of
 play through the media as a function of `CLOCK_MONOTONIC`.
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
            <td> The type of content playing back. Omitted if it is not a first class
 category.
</td>
        </tr><tr>
            <td>7</td>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### PlayerCapabilities {:#PlayerCapabilities}


*Defined in [fuchsia.media.sessions2/player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/player.fidl#139)*

 `PlaybackCapabilities` enumerates the capabilities of a media player, and
 corresponds to the control commands it can execute.


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

### PlayerInfoDelta {:#PlayerInfoDelta}


*Defined in [fuchsia.media.sessions2/player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/player.fidl#145)*

 When emitted, fields that have changed should be set.
 The first emission to a new client should be a snapshot.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>local</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Whether the entry point for the media into our device network is the
 local machine; this should be true if this is the device streaming
 from a music service, but false or omitted if this machine is just
 receiving an audio stream to act as a speaker.
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
                <code><a class='link' href='../fuchsia.media/index.html'>fuchsia.media</a>/<a class='link' href='../fuchsia.media/index.html#Metadata'>Metadata</a></code>
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

### PlayerRegistration {:#PlayerRegistration}


*Defined in [fuchsia.media.sessions2/publisher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sessions2/publisher.fidl#10)*

 All information required by the media session registry service to
 register a player so that clients may observe its status and control
 it.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>domain</code></td>
            <td>
                <code>string[1000]</code>
            </td>
            <td> The domain on which the player exists. Unset if it is the native
 Fuchsia domain.
</td>
        </tr></table>







## **BITS**

### PlayerCapabilityFlags {:#PlayerCapabilityFlags}
Type: <code>uint32</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>PLAY</td>
            <td>1</td>
            <td> If set, the player can `Play()`.
</td>
        </tr><tr>
            <td>PAUSE</td>
            <td>4</td>
            <td> If set, the player can `Pause()`.
</td>
        </tr><tr>
            <td>SEEK</td>
            <td>8</td>
            <td> If set, the player can `Seek()`.
</td>
        </tr><tr>
            <td>SKIP_FORWARD</td>
            <td>16</td>
            <td> If set, the player can `SkipForward()`.
</td>
        </tr><tr>
            <td>SKIP_REVERSE</td>
            <td>32</td>
            <td> If set, the player can `SkipReverse()`.
</td>
        </tr><tr>
            <td>SHUFFLE</td>
            <td>64</td>
            <td> If set, the player can shuffle media.
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
            <td>REPEAT_GROUPS</td>
            <td>1024</td>
            <td> If set, the player can repeat groups.
</td>
        </tr><tr>
            <td>REPEAT_SINGLE</td>
            <td>2048</td>
            <td> If set, the player can repeat single media items.
</td>
        </tr></table>

### PlayerCapabilityFlags {:#PlayerCapabilityFlags}
Type: <code>uint32</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>PLAY</td>
            <td>1</td>
            <td> If set, the player can `Play()`.
</td>
        </tr><tr>
            <td>PAUSE</td>
            <td>4</td>
            <td> If set, the player can `Pause()`.
</td>
        </tr><tr>
            <td>SEEK</td>
            <td>8</td>
            <td> If set, the player can `Seek()`.
</td>
        </tr><tr>
            <td>SKIP_FORWARD</td>
            <td>16</td>
            <td> If set, the player can `SkipForward()`.
</td>
        </tr><tr>
            <td>SKIP_REVERSE</td>
            <td>32</td>
            <td> If set, the player can `SkipReverse()`.
</td>
        </tr><tr>
            <td>SHUFFLE</td>
            <td>64</td>
            <td> If set, the player can shuffle media.
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
            <td>REPEAT_GROUPS</td>
            <td>1024</td>
            <td> If set, the player can repeat groups.
</td>
        </tr><tr>
            <td>REPEAT_SINGLE</td>
            <td>2048</td>
            <td> If set, the player can repeat single media items.
</td>
        </tr></table>



