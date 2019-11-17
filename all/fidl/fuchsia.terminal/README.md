[TOC]

# fuchsia.terminal


## **PROTOCOLS**

## Profiles {#Profiles}
*Defined in [fuchsia.terminal/profiles.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.terminal/profiles.fidl#28)*

<p>A service which provides profile information for the terminal.</p>

### GetProfileList {#GetProfileList}

<p>Returns the list of [ProfileEntry] objects.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>profile_list</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ProfileEntry'>ProfileEntry</a>&gt;[24]</code>
            </td>
        </tr></table>

### SetDefault {#SetDefault}

<p>Sets the profile with the given id as the default.</p>
<p>This method can fail if a profile with the given id does not exist.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>string[36]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Profiles_SetDefault_Result'>Profiles_SetDefault_Result</a></code>
            </td>
        </tr></table>

### OnProfileListUpdated {#OnProfileListUpdated}

<p>Event which is triggered when the list of profiles have been updated.</p>
<p>Note: this method will not be called if properties of an individual
profile are updated.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>profile_entries</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ProfileEntry'>ProfileEntry</a>&gt;[24]</code>
            </td>
        </tr></table>

### GetProfile {#GetProfile}

<p>Returns the profile with the given [id].</p>
<p>If there is no profile with the given [name] an error will be returned.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>string[36]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Profiles_GetProfile_Result'>Profiles_GetProfile_Result</a></code>
            </td>
        </tr></table>

### UpdateProfile {#UpdateProfile}

<p>Updates the profile with the given id.</p>
<p>This method will fail if a profile with the given id does not already
exist. A Profile must be created with a call to [CreateProfile].</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>string[36]</code>
            </td>
        </tr><tr>
            <td><code>profile</code></td>
            <td>
                <code><a class='link' href='#Profile'>Profile</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Profiles_UpdateProfile_Result'>Profiles_UpdateProfile_Result</a></code>
            </td>
        </tr></table>

### CreateNew {#CreateNew}

<p>Creates a new profile.</p>
<p>After the profile is created it can be updated with a call to [Update].</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>string[36]</code>
            </td>
        </tr><tr>
            <td><code>profile</code></td>
            <td>
                <code><a class='link' href='#Profile'>Profile</a></code>
            </td>
        </tr></table>

### Delete {#Delete}

<p>Deletes the profile with the given id.</p>
<p>If no profile with [id] exists this method does nothing. If the
default profile is deleted then a new profile will be set as the
default. However, which profile is chosen as the new profile is not
defined and it is up to the implementor to choose. The new default
profile can be retrieved by listening for the OnProfileListUpdated
event.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>string[36]</code>
            </td>
        </tr></table>



### OnProfileUpdated {#OnProfileUpdated}

<p>Triggered when a given profile is updated.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>string[36]</code>
            </td>
        </tr><tr>
            <td><code>profile</code></td>
            <td>
                <code><a class='link' href='#Profile'>Profile</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Profiles_SetDefault_Response {#Profiles_SetDefault_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Profiles_GetProfile_Response {#Profiles_GetProfile_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>profile</code></td>
            <td>
                <code><a class='link' href='#Profile'>Profile</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Profiles_UpdateProfile_Response {#Profiles_UpdateProfile_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### ProfileEntry {#ProfileEntry}
*Defined in [fuchsia.terminal/profiles.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.terminal/profiles.fidl#76)*



<p>The [ProfileEntry] is a readonly value which represents
a profile that has been saved.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>string[36]</code>
            </td>
            <td><p>A unique identifier for this profile represented as a UUID V4 string.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td><p>The user visible name of the profile.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>is_default</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Indicates if this is the users chosen default profile.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### Cursor {#Cursor}
*Defined in [fuchsia.terminal/profiles.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.terminal/profiles.fidl#125)*



<p>A description of the terminal's cursor.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>color</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.types/'>fuchsia.ui.types</a>/<a class='link' href='../fuchsia.ui.types/#ColorRgb'>ColorRgb</a></code>
            </td>
            <td><p>The color to render the cursor.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>style</code></td>
            <td>
                <code><a class='link' href='#CursorStyle'>CursorStyle</a></code>
            </td>
            <td><p>The cursors style.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>blink</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>whether the cursor should blink or not.</p>
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### ProfileError {#ProfileError}
Type: <code>uint32</code>

*Defined in [fuchsia.terminal/profiles.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.terminal/profiles.fidl#18)*

<p>Common error code used across different settings.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NOT_FOUND</code></td>
            <td><code>1</code></td>
            <td><p>Indicates that the requested profile does not exist.</p>
</td>
        </tr><tr>
            <td><code>NAME_ALREADY_EXISTS</code></td>
            <td><code>2</code></td>
            <td><p>Indicates that the profile with a given name already exists.</p>
</td>
        </tr></table>

### CursorStyle {#CursorStyle}
Type: <code>uint32</code>

*Defined in [fuchsia.terminal/profiles.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.terminal/profiles.fidl#137)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>BLOCK</code></td>
            <td><code>1</code></td>
            <td><p>Renders the terminal's cursor as a block.</p>
</td>
        </tr><tr>
            <td><code>UNDERLINE</code></td>
            <td><code>2</code></td>
            <td><p>Renders the terminal's cursor as a single underline.</p>
</td>
        </tr><tr>
            <td><code>VERTICAL_BAR</code></td>
            <td><code>3</code></td>
            <td><p>Renders the terminal's cursor as a single vertical bar.</p>
</td>
        </tr></table>



## **TABLES**

### Profile {#Profile}


*Defined in [fuchsia.terminal/profiles.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.terminal/profiles.fidl#89)*

<p>A table representing the values stored in the profile.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td><p>The visible name for this profile.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>font_family</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts/'>fuchsia.fonts</a>/<a class='link' href='../fuchsia.fonts/#FamilyName'>FamilyName</a></code>
            </td>
            <td><p>The font family used in text rendering.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>point_size</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The point size to render text.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>background_color</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.types/'>fuchsia.ui.types</a>/<a class='link' href='../fuchsia.ui.types/#ColorRgb'>ColorRgb</a></code>
            </td>
            <td><p>The color to render the background;</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>foreground_color</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.types/'>fuchsia.ui.types</a>/<a class='link' href='../fuchsia.ui.types/#ColorRgb'>ColorRgb</a></code>
            </td>
            <td><p>The normal text color.</p>
</td>
        </tr><tr>
            <td>6</td>
            <td><code>bold_color</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.types/'>fuchsia.ui.types</a>/<a class='link' href='../fuchsia.ui.types/#ColorRgb'>ColorRgb</a></code>
            </td>
            <td><p>A color used to render bold text.</p>
</td>
        </tr><tr>
            <td>7</td>
            <td><code>selected_background_color</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.types/'>fuchsia.ui.types</a>/<a class='link' href='../fuchsia.ui.types/#ColorRgb'>ColorRgb</a></code>
            </td>
            <td><p>The color of the selected text.</p>
</td>
        </tr><tr>
            <td>8</td>
            <td><code>selected_foreground_color</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.types/'>fuchsia.ui.types</a>/<a class='link' href='../fuchsia.ui.types/#ColorRgb'>ColorRgb</a></code>
            </td>
            <td><p>The color of the selected text.</p>
</td>
        </tr><tr>
            <td>9</td>
            <td><code>use_bright_for_bold</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>If true, bold characters will use the bright color variant as well.</p>
</td>
        </tr><tr>
            <td>10</td>
            <td><code>ansi_colors</code></td>
            <td>
                <code>[16]</code>
            </td>
            <td></td>
        </tr><tr>
            <td>11</td>
            <td><code>cursor</code></td>
            <td>
                <code><a class='link' href='#Cursor'>Cursor</a></code>
            </td>
            <td><p>A struct representing the cursor.</p>
</td>
        </tr></table>



## **UNIONS**

### Profiles_SetDefault_Result {#Profiles_SetDefault_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Profiles_SetDefault_Response'>Profiles_SetDefault_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ProfileError'>ProfileError</a></code>
            </td>
            <td></td>
        </tr></table>

### Profiles_GetProfile_Result {#Profiles_GetProfile_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Profiles_GetProfile_Response'>Profiles_GetProfile_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ProfileError'>ProfileError</a></code>
            </td>
            <td></td>
        </tr></table>

### Profiles_UpdateProfile_Result {#Profiles_UpdateProfile_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Profiles_UpdateProfile_Response'>Profiles_UpdateProfile_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ProfileError'>ProfileError</a></code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.terminal/profiles.fidl#10">MAX_PROFILE_NAME_LENGTH</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>int32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.terminal/profiles.fidl#11">MAX_ALLOWED_PROFILES</a></td>
            <td>
                    <code>24</code>
                </td>
                <td><code>int32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.terminal/profiles.fidl#12">MAX_ID_LENGTH</a></td>
            <td>
                    <code>36</code>
                </td>
                <td><code>int32</code></td>
            <td></td>
        </tr>
    
</table>

