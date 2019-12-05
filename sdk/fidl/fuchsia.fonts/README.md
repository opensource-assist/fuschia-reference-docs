[TOC]

# fuchsia.fonts


## **PROTOCOLS**

## FontSetEventListener {#FontSetEventListener}
*Defined in [fuchsia.fonts/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/events.fidl#10)*

<p>Protocol for listening to possible events that may occur in the <code>Provider</code>'s set of fonts.</p>
<p>Register a listener using <a class='link' href='#Provider.RegisterFontSetEventListener'>Provider.RegisterFontSetEventListener</a>.</p>

### OnFontSetUpdated {#OnFontSetUpdated}

<p>The set of fonts available in the <code>Provider</code> has changed. See
<a class='link' href='#FontSetUpdatedEvent'>FontSetUpdatedEvent</a>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>event</code></td>
            <td>
                <code><a class='link' href='#FontSetUpdatedEvent'>FontSetUpdatedEvent</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## Provider {#Provider}
*Defined in [fuchsia.fonts/font_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/font_provider.fidl#109)*

<p>Provider of digital font files and metadata.</p>
<p>TODO(I18N-12): Remove deprecated methods and move to provider.fidl.</p>

### GetFont {#GetFont}

<p>Deprecated. See <code>GetTypeface</code>.</p>
<p>Returns font that matches specified <code>request</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code><a class='link' href='#Request'>Request</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Response'>Response</a>?</code>
            </td>
        </tr></table>

### GetFamilyInfo {#GetFamilyInfo}

<p>Deprecated. See <code>GetFontFamilyInfo</code>.</p>
<p>Returns information for the specified font family or null if there is
no family with the specified name. This function respects family name
aliases and ignores case, so request for &quot;robotoSLAB&quot; will return
FamilyInfo for &quot;Roboto Slab&quot;.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>family</code></td>
            <td>
                <code>string[128]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>family_info</code></td>
            <td>
                <code><a class='link' href='#FamilyInfo'>FamilyInfo</a>?</code>
            </td>
        </tr></table>

### GetTypeface {#GetTypeface}

<p>Returns a typeface that matches the specified <code>request</code>, or an empty table if no matching
face is found. (The latter is more likely to happen if <code>TypefaceRequestFlags.EXACT_FAMILY</code>
is used to disable fallbacks.)</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code><a class='link' href='#TypefaceRequest'>TypefaceRequest</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#TypefaceResponse'>TypefaceResponse</a></code>
            </td>
        </tr></table>

### GetFontFamilyInfo {#GetFontFamilyInfo}

<p>Returns information for the specified font family, or an empty table if there is no family
with the specified name.</p>
<p>This function respects family name aliases and ignores case. For example, &quot;RobotoSlab&quot; is an
alias for the canonical name &quot;Roboto Slab&quot;. A request for &quot;robotoSLAB&quot; would return the
<code>FontFamilyInfo</code> for &quot;Roboto Slab&quot; due to the case-insensitivity and alias resolution.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>family</code></td>
            <td>
                <code><a class='link' href='#FamilyName'>FamilyName</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>family_info</code></td>
            <td>
                <code><a class='link' href='#FontFamilyInfo'>FontFamilyInfo</a></code>
            </td>
        </tr></table>

### RegisterFontSetEventListener {#RegisterFontSetEventListener}

<p>Register a listener to be notified when the set of available fonts or mappings has changed.
A client can register as many listeners as it wishes.</p>
<p>To unregister, close the channel.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='#FontSetEventListener'>FontSetEventListener</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## **STRUCTS**

### Request {#Request}
*Defined in [fuchsia.fonts/font_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/font_provider.fidl#34)*



<p>Deprecated. See <code>FaceRequest</code>.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>family</code></td>
            <td>
                <code>string[128]?</code>
            </td>
            <td><p>Desired font family name, e.g. &quot;Roboto&quot;. Font family search is
case-insensitive. In case when there is no specified family or the
specified family doesn't have glyph for the requested <code>character</code> then
a font from another family may be returned. This behavior can be disabled
using <code>REQUEST_FLAG_NO_FALLBACK</code>.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>weight</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>For example, 400 is normal, 700 is bold.</p>
</td>
            <td>400</td>
        </tr><tr>
            <td><code>width</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Numeric values matching OS/2 &amp; Windows Metrics usWidthClass table.
https://www.microsoft.com/typography/otspec/os2.htm
For example, 5 is normal.</p>
</td>
            <td>5</td>
        </tr><tr>
            <td><code>slant</code></td>
            <td>
                <code><a class='link' href='#Slant'>Slant</a></code>
            </td>
            <td></td>
            <td><a class='link' href='#Slant.UPRIGHT'>Slant.UPRIGHT</a></td>
        </tr><tr>
            <td><code>language</code></td>
            <td>
                <code>vector&lt;string&gt;[8]?</code>
            </td>
            <td><p>BCP47 language tags in order of preference. See
https://tools.ietf.org/html/bcp47 .</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>character</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Codepoint for the character that must be present in the returned font or 0.
Caller that specify this field are expected to extract character set from
the result and cache it in order to avoid calling the API more than
necessary.</p>
</td>
            <td>0</td>
        </tr><tr>
            <td><code>fallback_group</code></td>
            <td>
                <code><a class='link' href='#FallbackGroup'>FallbackGroup</a></code>
            </td>
            <td><p>Fallback group preference. Caller can leave this field set to NONE. In
that case the font provider will use fallback group of the specified font
family.</p>
</td>
            <td><a class='link' href='#FallbackGroup.NONE'>FallbackGroup.NONE</a></td>
        </tr><tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>0</td>
        </tr>
</table>

### Response {#Response}
*Defined in [fuchsia.fonts/font_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/font_provider.fidl#70)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>buffer_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Buffer identifier for the buffer. Responses with the same buffer_id are
guaranteed to contain the same data in the buffer. Clients may use this
value to detect if they already have the font cached in parsed form.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>font_index</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Font index within <code>buffer</code>. Used for font formats that may contain more
than one font per file, e.g. TTC (TrueType Collection).</p>
</td>
            <td>No default</td>
        </tr>
</table>

### Style {#Style}
*Defined in [fuchsia.fonts/font_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/font_provider.fidl#85)*



<p>Deprecated.
See <code>Style2</code>.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>weight</code></td>
            <td>
                <code>uint32</code>
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
            <td><code>slant</code></td>
            <td>
                <code><a class='link' href='#Slant'>Slant</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FamilyInfo {#FamilyInfo}
*Defined in [fuchsia.fonts/font_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/font_provider.fidl#94)*



<p>Deprecated. See <code>FontFamilyInfo</code>.</p>
<p>Information about font family that can be requested using GetFamilyInfo().</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td><p>Canonical font family name. Note that this may be different from the
value passed to GetFamilyInfo() because GetFamilyInfo() also resolves
font aliases and ignores case. For example GetFamilyInfo(&quot;robotoslab&quot;)
will FamilyInfo.name = &quot;Robot Slab&quot;.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>styles</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Style'>Style</a>&gt;[300]</code>
            </td>
            <td><p>Unordered list of all available styles in the family.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### FamilyName {#FamilyName}
*Defined in [fuchsia.fonts/provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/provider.fidl#25)*



<p>The name of a family of fonts.</p>
<p>Examples: &quot;Roboto&quot;, &quot;Noto Serif&quot;.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td><p>The characters that make up the name.</p>
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### FallbackGroup {#FallbackGroup}
Type: <code>uint32</code>

*Defined in [fuchsia.fonts/font_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/font_provider.fidl#13)*

<p>Deprecated. See <code>GenericFontFamily</code>.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NONE</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>SERIF</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>SANS_SERIF</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>MONOSPACE</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>CURSIVE</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>FANTASY</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr></table>

### CacheMissPolicy {#CacheMissPolicy}
Type: <code>uint32</code>

*Defined in [fuchsia.fonts/provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/provider.fidl#44)*

<p>Options for what the font server should do if the client requests a typeface that is not yet
cached.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>BLOCK_UNTIL_DOWNLOADED</code></td>
            <td><code>1</code></td>
            <td><p>The server will attempt to load the uncached typeface before providing a response. This is
the <em>default</em> behavior.</p>
<p>This option is not recommended for synchronous clients that block rendering while waiting
for a font.</p>
</td>
        </tr><tr>
            <td><code>RETURN_EMPTY_RESPONSE</code></td>
            <td><code>2</code></td>
            <td><p>The server will tell the client that the uncached typeface is unavailable, by returning an
empty <a class='link' href='#TypefaceResponse'>TypefaceResponse</a>. The uncached typeface may be downloaded
asynchronously to be available for future requests.</p>
<p>This is similar to <code>font-display: block</code> in CSS.</p>
</td>
        </tr><tr>
            <td><code>RETURN_FALLBACK</code></td>
            <td><code>3</code></td>
            <td><p>The server will attempt to provide a cached fallback typeface (if allowed by the fallback
restrictions in <a class='link' href='#TypefaceRequestFlags'>TypefaceRequestFlags</a>). The uncached typeface may be
downloaded asynchronously to be available for future requests.</p>
<p>This is similar to <code>font-display: swap</code> in CSS.</p>
</td>
        </tr></table>

### Slant {#Slant}
Type: <code>uint32</code>

*Defined in [fuchsia.fonts/styles.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/styles.fidl#21)*

<p>The type of slant of a type face.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UPRIGHT</code></td>
            <td><code>1</code></td>
            <td><p>The default; upright glyphs.</p>
</td>
        </tr><tr>
            <td><code>ITALIC</code></td>
            <td><code>2</code></td>
            <td><p>Specially designed, slanted and slightly calligraphic glyphs.</p>
</td>
        </tr><tr>
            <td><code>OBLIQUE</code></td>
            <td><code>3</code></td>
            <td><p>Skewed glyphs. Oblique usually means an geometric transformation of the upright variant,
rather than a custom-designed variant.</p>
</td>
        </tr></table>

### Width {#Width}
Type: <code>uint32</code>

*Defined in [fuchsia.fonts/styles.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/styles.fidl#34)*

<p>Horizontal width class of the glyphs.</p>
<p>See https://docs.microsoft.com/en-us/typography/opentype/spec/os2#uswidthclass.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ULTRA_CONDENSED</code></td>
            <td><code>1</code></td>
            <td><p>50% of normal width</p>
</td>
        </tr><tr>
            <td><code>EXTRA_CONDENSED</code></td>
            <td><code>2</code></td>
            <td><p>62.5% of normal width</p>
</td>
        </tr><tr>
            <td><code>CONDENSED</code></td>
            <td><code>3</code></td>
            <td><p>75% of normal width</p>
</td>
        </tr><tr>
            <td><code>SEMI_CONDENSED</code></td>
            <td><code>4</code></td>
            <td><p>87.5% of normal width</p>
</td>
        </tr><tr>
            <td><code>NORMAL</code></td>
            <td><code>5</code></td>
            <td><p>Normal width</p>
</td>
        </tr><tr>
            <td><code>SEMI_EXPANDED</code></td>
            <td><code>6</code></td>
            <td><p>112.5% of normal width</p>
</td>
        </tr><tr>
            <td><code>EXPANDED</code></td>
            <td><code>7</code></td>
            <td><p>125% of normal width</p>
</td>
        </tr><tr>
            <td><code>EXTRA_EXPANDED</code></td>
            <td><code>8</code></td>
            <td><p>150% of normal width</p>
</td>
        </tr><tr>
            <td><code>ULTRA_EXPANDED</code></td>
            <td><code>9</code></td>
            <td><p>200% of normal width</p>
</td>
        </tr></table>

### GenericFontFamily {#GenericFontFamily}
Type: <code>uint32</code>

*Defined in [fuchsia.fonts/styles.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/styles.fidl#82)*

<p>Generic groups of font families that can serve as fallbacks for a specific family.</p>
<p>Every font family belongs to some <em>generic</em> font family (see examples below).</p>
<p>If an exact requested family is unavailable but a fallback group is specified in the request,
the provider may return some other family that belongs to the fallback group. For example, if
the client requests the &quot;Arial&quot; family with a <code>SANS_SERIF</code> fallback, and &quot;Arial&quot; is unavailable,
the provider may return another available sans serif family, such as &quot;Roboto Regular&quot;, instead.</p>
<p>See also:
https://www.w3.org/TR/css-fonts-4/#generic-font-families</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SERIF</code></td>
            <td><code>1</code></td>
            <td><p>Glyphs have little &quot;serifs&quot;, hooks, or notches at the ends of most strokes.
Examples: Georgia, Noto Serif, Times New Roman.</p>
</td>
        </tr><tr>
            <td><code>SANS_SERIF</code></td>
            <td><code>2</code></td>
            <td><p>Glyphs that have no serifs at the ends of most strokes.
Examples: Arial, Noto Sans, Roboto, Tahoma.</p>
</td>
        </tr><tr>
            <td><code>MONOSPACE</code></td>
            <td><code>3</code></td>
            <td><p>Fixed-width fonts.
Examples: Consolas, Courier New, Inconsolata.</p>
</td>
        </tr><tr>
            <td><code>CURSIVE</code></td>
            <td><code>4</code></td>
            <td><p>Handwritten or cursive fonts.
Examples: Brush Script, Comic Sans, Lucida Calligraphy.</p>
</td>
        </tr><tr>
            <td><code>FANTASY</code></td>
            <td><code>5</code></td>
            <td><p>Decorative fonts.
Examples: Impact, Papyrus.</p>
</td>
        </tr><tr>
            <td><code>SYSTEM_UI</code></td>
            <td><code>6</code></td>
            <td><p>The default user interface font on the target platform.
This is included for completeness with the CSS specification; font manifests should not
declare that a font belongs to the <code>SYSTEM_UI</code> generic family, but instead should declare a
more specific option (e.g. <code>SERIF</code> for Roboto).</p>
<p>Not commonly used.</p>
</td>
        </tr><tr>
            <td><code>EMOJI</code></td>
            <td><code>7</code></td>
            <td><p>Fonts that are used specifically for rendering emoji code points.
Examples: Noto Color Emoji.</p>
</td>
        </tr><tr>
            <td><code>MATH</code></td>
            <td><code>8</code></td>
            <td><p>Fonts that are used primarily for rendering mathematical expressions.</p>
<p>Not commonly used.</p>
</td>
        </tr><tr>
            <td><code>FANGSONG</code></td>
            <td><code>9</code></td>
            <td><p>A group of Chinese fonts between serif and cursive, often used for official Chinese
Government documents.</p>
<p>Not commonly used.</p>
</td>
        </tr></table>



## **TABLES**

### FontSetUpdatedEvent {#FontSetUpdatedEvent}


*Defined in [fuchsia.fonts/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/events.fidl#23)*

<p>An event indicating that the set of fonts available in the <code>Provider</code> has changed. This is most
frequently caused by an ephemeral font being downloaded and cached. Clients should consider
re-requesting fonts and re-rendering any displayed text.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    </table>

### TypefaceRequest {#TypefaceRequest}


*Defined in [fuchsia.fonts/provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/provider.fidl#68)*

<p>Parameters for requesting a typeface.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>query</code></td>
            <td>
                <code><a class='link' href='#TypefaceQuery'>TypefaceQuery</a></code>
            </td>
            <td><p>Parameters for looking up a typeface.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>flags</code></td>
            <td>
                <code><a class='link' href='#TypefaceRequestFlags'>TypefaceRequestFlags</a></code>
            </td>
            <td><p>Flags for how to process the request, such as which kinds of substitutions are permitted.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>cache_miss_policy</code></td>
            <td>
                <code><a class='link' href='#CacheMissPolicy'>CacheMissPolicy</a></code>
            </td>
            <td><p>Setting for what to do if the requested typeface exists but is not cached, and therefore
cannot be served immediately.</p>
<p>If this field is empty, the default policy is
<a class='link' href='#CacheMissPolicy.BLOCK_UNTIL_DOWNLOADED'>CacheMissPolicy.BLOCK_UNTIL_DOWNLOADED</a>.</p>
<p>If the client needs an immediate response, it can choose one of the non-blocking policies.
In this case, clients can also register to be notified when new fonts have been added to the
cache by calling <a class='link' href='#Provider.RegisterFontSetEventListener'>Provider.RegisterFontSetEventListener</a>.</p>
</td>
        </tr></table>

### TypefaceQuery {#TypefaceQuery}


*Defined in [fuchsia.fonts/provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/provider.fidl#88)*

<p>Parameters for looking up a typeface.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>family</code></td>
            <td>
                <code><a class='link' href='#FamilyName'>FamilyName</a></code>
            </td>
            <td><p>Desired font family name, e.g. &quot;Roboto&quot;. Font family search is case-insensitive.</p>
<p>Note: In cases where the specified family doesn't exist, or the specified family doesn't
have a glyph for the requested <code>code_point</code>, a face from another family may be returned.
This behavior can be disabled using <code>TypefaceRequestFlags.EXACT_FAMILY</code>.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>style</code></td>
            <td>
                <code><a class='link' href='#Style2'>Style2</a></code>
            </td>
            <td><p>Style properties of the desired typeface.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>languages</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.intl/'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/#LocaleId'>LocaleId</a>&gt;[8]</code>
            </td>
            <td><p>Language tags in order of preference. This allows disambiguating code points that map
to different glyphs in different languages (e.g. CJK code points).</p>
<p>See <code>fuchsia.intl.LocaleId</code>.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>code_points</code></td>
            <td>
                <code>vector&lt;uint32&gt;[128]</code>
            </td>
            <td><p>Optional code points for which glyphs must be present in the returned face.</p>
<p>Callers that specify this field are expected to extract the character set from the result
and cache it in order to avoid calling the API more than necessary.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>fallback_family</code></td>
            <td>
                <code><a class='link' href='#GenericFontFamily'>GenericFontFamily</a></code>
            </td>
            <td><p>A generic font family to fall back to if an exact match is unavailable or does not contain
the requested code point.</p>
<p>Every font family belongs to a generic family (configured in the font manifest). If a
particular font family doesn't contain a requested code point, the provider can search for
the code point in other font families <em>in the same generic family</em> as a fallback.</p>
<p>Specifying <code>fallback_family</code> in a query allows the client to override the generic family
that would be used as a fallback.</p>
</td>
        </tr></table>

### TypefaceResponse {#TypefaceResponse}


*Defined in [fuchsia.fonts/provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/provider.fidl#127)*

<p>Response to a TypefaceRequest. Contains the digital font file and metadata corresponding to a
returned typeface. Clients are expected to cache the results if they plan to reuse them.</p>
<p>If a matching typeface cannot be found, the table will be empty.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td><p>A memory buffer containing the bytes of a digital font file.
It is the client's responsibility to identify the type of file and to parse it (usually by
delegating to FreeType or a similar library).</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>buffer_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Identifier for the buffer. Responses with the same <code>buffer_id</code> are guaranteed to contain the
same data in the buffer. Clients may use this value to detect if they already have the font
cached in parsed form.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>font_index</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Index of the returned typeface within <code>buffer</code>. Used for digital font formats that may
contain more than one typeface per file, e.g. TTC (TrueType Collection).</p>
</td>
        </tr></table>

### FontFamilyInfo {#FontFamilyInfo}


*Defined in [fuchsia.fonts/provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/provider.fidl#146)*

<p>Information about a font family that can be requested using <code>Provider.GetFontFamilyInfo()</code>.</p>
<p>If a matching font family is not found, the table will be empty.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code><a class='link' href='#FamilyName'>FamilyName</a></code>
            </td>
            <td><p>Canonical font family name. Note that this may be different from the value passed to
<code>GetFontFamilyInfo()</code> due to the resolution of font aliases, and/or differences in
whitespace and capitalization.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>styles</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Style2'>Style2</a>&gt;[300]</code>
            </td>
            <td><p>Unordered list of all available styles in the family.</p>
</td>
        </tr></table>

### Style2 {#Style2}


*Defined in [fuchsia.fonts/styles.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/styles.fidl#56)*

<p>Style properties that can be used when requesting or describing a type face.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>slant</code></td>
            <td>
                <code><a class='link' href='#Slant'>Slant</a></code>
            </td>
            <td><p>See <code>Slant</code>.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>weight</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>Weight or thickness of the glyphs. Allowed values are integers in the range [1, 1000], but
most real-world font families only support some integer multiples of 100:
{100, 200, ..., 900}. Normal text (<code>WEIGHT_NORMAL</code>) is 400; <code>WEIGHT_BOLD</code> is 700.</p>
<p>See:
https://developer.mozilla.org/en-US/docs/Web/CSS/font-weight#Common_weight_name_mapping
https://docs.microsoft.com/en-us/typography/opentype/spec/os2#usweightclass</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>width</code></td>
            <td>
                <code><a class='link' href='#Width'>Width</a></code>
            </td>
            <td><p>See <code>Width</code>.</p>
</td>
        </tr></table>







## **BITS**

### TypefaceRequestFlags {#TypefaceRequestFlags}
Type: <code>uint32</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>EXACT_FAMILY</td>
            <td>1</td>
            <td><p>Disables font family fallback. The service won't try to search the fallback font set if the
requested font family doesn't exist or if it doesn't contain the requested code point.</p>
</td>
        </tr><tr>
            <td>EXACT_STYLE</td>
            <td>2</td>
            <td><p>Disables approximate style matching. The service will only return a face that matches the
requested style exactly. For example, there will be no substitutions of &quot;medium&quot; for a
requested &quot;semi-bold&quot; weight, or &quot;oblique&quot; for a requested &quot;italic&quot; slant.</p>
</td>
        </tr></table>



## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/font_provider.fidl#26">REQUEST_FLAG_NO_FALLBACK</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Deprecated. See <code>FaceRequestFlags</code>.
Disables font fallback. The service won't try to search fallback font set if
there is no requested font family or if it doesn't contain requested
character.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/font_provider.fidl#31">REQUEST_FLAG_EXACT_MATCH</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Deprecated. See <code>FaceRequestFlags</code>.
Disables approximate style matching. The service will only return font that
matches the requested style exactly.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/provider.fidl#11">MAX_FAMILY_NAME_LENGTH</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum length of a font family name.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/provider.fidl#14">MAX_FACE_QUERY_CODE_POINTS</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum number of code points allowed in a typeface query.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/provider.fidl#17">MAX_FACE_QUERY_LANGUAGES</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum number of preferred languages allowed in a typeface query.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/provider.fidl#20">MAX_FAMILY_STYLES</a></td>
            <td>
                    <code>300</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum number of styles that will be returned for a font family.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/styles.fidl#10">WEIGHT_THIN</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/styles.fidl#11">WEIGHT_EXTRA_LIGHT</a></td>
            <td>
                    <code>200</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/styles.fidl#12">WEIGHT_LIGHT</a></td>
            <td>
                    <code>300</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/styles.fidl#13">WEIGHT_NORMAL</a></td>
            <td>
                    <code>400</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/styles.fidl#14">WEIGHT_MEDIUM</a></td>
            <td>
                    <code>500</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/styles.fidl#15">WEIGHT_SEMI_BOLD</a></td>
            <td>
                    <code>600</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/styles.fidl#16">WEIGHT_BOLD</a></td>
            <td>
                    <code>700</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/styles.fidl#17">WEIGHT_EXTRA_BOLD</a></td>
            <td>
                    <code>800</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/styles.fidl#18">WEIGHT_BLACK</a></td>
            <td>
                    <code>900</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    
</table>



## **TYPE ALIASES**

<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/styles.fidl#7">Weight</a></td>
            <td>
                <code>uint16</code></td>
            <td></td>
        </tr></table>

