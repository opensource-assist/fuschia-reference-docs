[TOC]

# fuchsia.media.sounds


## **PROTOCOLS**

## Player {#Player}
*Defined in [fuchsia.media.sounds/sound_player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sounds/sound_player.fidl#13)*

<p>Allows clients to play fire-and-forget sounds.</p>

### AddSoundFromFile {#AddSoundFromFile}

<p>Adds a sound to the collection maintained for the client, reading the sound from a file.
If <code>id</code> identifies an existing sound in the collection, the service will close the
connection.</p>
<p>Currently, only PCM WAV files are supported.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>file_channel</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Player_AddSoundFromFile_Result'>Player_AddSoundFromFile_Result</a></code>
            </td>
        </tr></table>

### AddSoundBuffer {#AddSoundBuffer}

<p>Adds a sound, in the form of a buffer containing raw PCM samples, to the collection
maintained for the client. The service will retain a handle to the buffer's VMO until the
sound is removed and is no longer playing or until the connection is closed.</p>
<p>If <code>id</code> identifies an existing sound in the collection, the service will close the
connection.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
        </tr><tr>
            <td><code>stream_type</code></td>
            <td>
                <code><a class='link' href='../fuchsia.media/'>fuchsia.media</a>/<a class='link' href='../fuchsia.media/#AudioStreamType'>AudioStreamType</a></code>
            </td>
        </tr></table>



### RemoveSound {#RemoveSound}

<p>Removes a sound from the collection maintained for the client. A sound can be removed even
if a <code>PlaySound</code> method is pending for that sound.</p>
<p>If <code>id</code> doesn't identify an existing sound in the collection, the service will do nothing.
This is tolerated so that clients don't have to wait for the response from
<code>AddSoundFromFile</code> before playing and removing the sound.</p>
<p>Removing an unneeded sound frees the resources associated with that sound, principally
the VMO required to store the uncompressed sound.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### PlaySound {#PlaySound}

<p>Plays the existing sound identified by <code>id</code> using a renderer with usage <code>usage</code>. The
sound is played as soon as possible. The reply is sent when the sound is finished playing.
If <code>id</code> doesn't identify an existing sound in the collection, the method return
<code>PlaySoundError.NO_SUCH_SOUND</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>usage</code></td>
            <td>
                <code><a class='link' href='../fuchsia.media/'>fuchsia.media</a>/<a class='link' href='../fuchsia.media/#AudioRenderUsage'>AudioRenderUsage</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Player_PlaySound_Result'>Player_PlaySound_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Player_AddSoundFromFile_Response {#Player_AddSoundFromFile_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Player_PlaySound_Response {#Player_PlaySound_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>



## **ENUMS**

### PlaySoundError {#PlaySoundError}
Type: <code>uint32</code>

*Defined in [fuchsia.media.sounds/sound_player.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.sounds/sound_player.fidl#48)*

<p>Error type for <code>Player.PlaySound</code>.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NO_SUCH_SOUND</code></td>
            <td><code>1</code></td>
            <td><p>The <code>id</code> passed to <code>PlaySound</code> is not recognized.</p>
</td>
        </tr></table>





## **UNIONS**

### Player_AddSoundFromFile_Result {#Player_AddSoundFromFile_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Player_AddSoundFromFile_Response'>Player_AddSoundFromFile_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### Player_PlaySound_Result {#Player_PlaySound_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Player_PlaySound_Response'>Player_PlaySound_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#PlaySoundError'>PlaySoundError</a></code>
            </td>
            <td></td>
        </tr></table>









