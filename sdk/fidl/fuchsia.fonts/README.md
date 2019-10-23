[TOC]

# fuchsia.fonts


## **PROTOCOLS**

## FontSetEventListener {#FontSetEventListener}
*Defined in [fuchsia.fonts/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/events.fidl#10)*

 Protocol for listening to possible events that may occur in the `Provider`'s set of fonts.

 Register a listener using <a class='link' href='#Provider.RegisterFontSetEventListener'>Provider.RegisterFontSetEventListener</a>.

### OnFontSetUpdated {#OnFontSetUpdated}

 The set of fonts available in the `Provider` has changed. See
 <a class='link' href='#FontSetUpdatedEvent'>FontSetUpdatedEvent</a>.

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

 Provider of digital font files and metadata.

 TODO(I18N-12): Remove deprecated methods and move to provider.fidl.

### GetFont {#GetFont}

 Deprecated. See `GetTypeface`.

 Returns font that matches specified `request`.

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

 Deprecated. See `GetFontFamilyInfo`.

 Returns information for the specified font family or null if there is
 no family with the specified name. This function respects family name
 aliases and ignores case, so request for "robotoSLAB" will return
 FamilyInfo for "Roboto Slab".

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

 Returns a typeface that matches the specified `request`, or an empty table if no matching
 face is found. (The latter is more likely to happen if `TypefaceRequestFlags.EXACT_FAMILY`
 is used to disable fallbacks.)

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

 Returns information for the specified font family, or an empty table if there is no family
 with the specified name.

 This function respects family name aliases and ignores case. For example, "RobotoSlab" is an
 alias for the canonical name "Roboto Slab". A request for "robotoSLAB" would return the
 `FontFamilyInfo` for "Roboto Slab" due to the case-insensitivity and alias resolution.

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

 Register a listener to be notified when the set of available fonts or mappings has changed.
 A client can register as many listeners as it wishes.

 To unregister, close the channel.

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



 Deprecated. See `FaceRequest`.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>family</code></td>
            <td>
                <code>string[128]?</code>
            </td>
            <td> Desired font family name, e.g. "Roboto". Font family search is
 case-insensitive. In case when there is no specified family or the
 specified family doesn't have glyph for the requested `character` then
 a font from another family may be returned. This behavior can be disabled
 using `REQUEST_FLAG_NO_FALLBACK`.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>weight</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> For example, 400 is normal, 700 is bold.
</td>
            <td>400</td>
        </tr><tr>
            <td><code>width</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Numeric values matching OS/2 & Windows Metrics usWidthClass table.
 https://www.microsoft.com/typography/otspec/os2.htm
 For example, 5 is normal.
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
            <td> BCP47 language tags in order of preference. See
 https://tools.ietf.org/html/bcp47 .
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>character</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Codepoint for the character that must be present in the returned font or 0.
 Caller that specify this field are expected to extract character set from
 the result and cache it in order to avoid calling the API more than
 necessary.
</td>
            <td>0</td>
        </tr><tr>
            <td><code>fallback_group</code></td>
            <td>
                <code><a class='link' href='#FallbackGroup'>FallbackGroup</a></code>
            </td>
            <td> Fallback group preference. Caller can leave this field set to NONE. In
 that case the font provider will use fallback group of the specified font
 family.
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
            <td> Buffer identifier for the buffer. Responses with the same buffer_id are
 guaranteed to contain the same data in the buffer. Clients may use this
 value to detect if they already have the font cached in parsed form.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>font_index</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Font index within `buffer`. Used for font formats that may contain more
 than one font per file, e.g. TTC (TrueType Collection).
</td>
            <td>No default</td>
        </tr>
</table>

### Style {#Style}
*Defined in [fuchsia.fonts/font_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/font_provider.fidl#85)*



 Deprecated.
 See `Style2`.


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



 Deprecated. See `FontFamilyInfo`.

 Information about font family that can be requested using GetFamilyInfo().


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td> Canonical font family name. Note that this may be different from the
 value passed to GetFamilyInfo() because GetFamilyInfo() also resolves
 font aliases and ignores case. For example GetFamilyInfo("robotoslab")
 will FamilyInfo.name = "Robot Slab".
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>styles</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Style'>Style</a>&gt;[300]</code>
            </td>
            <td> Unordered list of all available styles in the family.
</td>
            <td>No default</td>
        </tr>
</table>

### FamilyName {#FamilyName}
*Defined in [fuchsia.fonts/provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/provider.fidl#22)*



 The name of a family of fonts.

 Examples: "Roboto", "Noto Serif".


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td> The characters that make up the name.
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### FallbackGroup {#FallbackGroup}
Type: <code>uint32</code>

*Defined in [fuchsia.fonts/font_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/font_provider.fidl#13)*

 Deprecated. See `GenericFontFamily`.


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

### Slant {#Slant}
Type: <code>uint32</code>

*Defined in [fuchsia.fonts/styles.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/styles.fidl#21)*

 The type of slant of a type face.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UPRIGHT</code></td>
            <td><code>1</code></td>
            <td> The default; upright glyphs.
</td>
        </tr><tr>
            <td><code>ITALIC</code></td>
            <td><code>2</code></td>
            <td> Specially designed, slanted and slightly calligraphic glyphs.
</td>
        </tr><tr>
            <td><code>OBLIQUE</code></td>
            <td><code>3</code></td>
            <td> Skewed glyphs. Oblique usually means an geometric transformation of the upright variant,
 rather than a custom-designed variant.
</td>
        </tr></table>

### Width {#Width}
Type: <code>uint32</code>

*Defined in [fuchsia.fonts/styles.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/styles.fidl#34)*

 Horizontal width class of the glyphs.

 See https://docs.microsoft.com/en-us/typography/opentype/spec/os2#uswidthclass.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ULTRA_CONDENSED</code></td>
            <td><code>1</code></td>
            <td> 50% of normal width
</td>
        </tr><tr>
            <td><code>EXTRA_CONDENSED</code></td>
            <td><code>2</code></td>
            <td> 62.5% of normal width
</td>
        </tr><tr>
            <td><code>CONDENSED</code></td>
            <td><code>3</code></td>
            <td> 75% of normal width
</td>
        </tr><tr>
            <td><code>SEMI_CONDENSED</code></td>
            <td><code>4</code></td>
            <td> 87.5% of normal width
</td>
        </tr><tr>
            <td><code>NORMAL</code></td>
            <td><code>5</code></td>
            <td> Normal width
</td>
        </tr><tr>
            <td><code>SEMI_EXPANDED</code></td>
            <td><code>6</code></td>
            <td> 112.5% of normal width
</td>
        </tr><tr>
            <td><code>EXPANDED</code></td>
            <td><code>7</code></td>
            <td> 125% of normal width
</td>
        </tr><tr>
            <td><code>EXTRA_EXPANDED</code></td>
            <td><code>8</code></td>
            <td> 150% of normal width
</td>
        </tr><tr>
            <td><code>ULTRA_EXPANDED</code></td>
            <td><code>9</code></td>
            <td> 200% of normal width
</td>
        </tr></table>

### GenericFontFamily {#GenericFontFamily}
Type: <code>uint32</code>

*Defined in [fuchsia.fonts/styles.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/styles.fidl#82)*

 Generic groups of font families that can serve as fallbacks for a specific family.

 Every font family belongs to some _generic_ font family (see examples below).

 If an exact requested family is unavailable but a fallback group is specified in the request,
 the provider may return some other family that belongs to the fallback group. For example, if
 the client requests the "Arial" family with a `SANS_SERIF` fallback, and "Arial" is unavailable,
 the provider may return another available sans serif family, such as "Roboto Regular", instead.

 See also:
 https://www.w3.org/TR/css-fonts-4/#generic-font-families


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SERIF</code></td>
            <td><code>1</code></td>
            <td> Glyphs have little "serifs", hooks, or notches at the ends of most strokes.
 Examples: Georgia, Noto Serif, Times New Roman.
</td>
        </tr><tr>
            <td><code>SANS_SERIF</code></td>
            <td><code>2</code></td>
            <td> Glyphs that have no serifs at the ends of most strokes.
 Examples: Arial, Noto Sans, Roboto, Tahoma.
</td>
        </tr><tr>
            <td><code>MONOSPACE</code></td>
            <td><code>3</code></td>
            <td> Fixed-width fonts.
 Examples: Consolas, Courier New, Inconsolata.
</td>
        </tr><tr>
            <td><code>CURSIVE</code></td>
            <td><code>4</code></td>
            <td> Handwritten or cursive fonts.
 Examples: Brush Script, Comic Sans, Lucida Calligraphy.
</td>
        </tr><tr>
            <td><code>FANTASY</code></td>
            <td><code>5</code></td>
            <td> Decorative fonts.
 Examples: Impact, Papyrus.
</td>
        </tr><tr>
            <td><code>SYSTEM_UI</code></td>
            <td><code>6</code></td>
            <td> The default user interface font on the target platform.
 This is included for completeness with the CSS specification; font manifests should not
 declare that a font belongs to the `SYSTEM_UI` generic family, but instead should declare a
 more specific option (e.g. `SERIF` for Roboto).

 Not commonly used.
</td>
        </tr><tr>
            <td><code>EMOJI</code></td>
            <td><code>7</code></td>
            <td> Fonts that are used specifically for rendering emoji code points.
 Examples: Noto Color Emoji.
</td>
        </tr><tr>
            <td><code>MATH</code></td>
            <td><code>8</code></td>
            <td> Fonts that are used primarily for rendering mathematical expressions.

 Not commonly used.
</td>
        </tr><tr>
            <td><code>FANGSONG</code></td>
            <td><code>9</code></td>
            <td> A group of Chinese fonts between serif and cursive, often used for official Chinese
 Government documents.

 Not commonly used.
</td>
        </tr></table>



## **TABLES**

### FontSetUpdatedEvent {#FontSetUpdatedEvent}


*Defined in [fuchsia.fonts/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/events.fidl#23)*

 An event indicating that the set of fonts available in the `Provider` has changed. This is most
 frequently caused by an ephemeral font being downloaded and cached. Clients should consider
 re-requesting fonts and re-rendering any displayed text.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    </table>

### TypefaceRequest {#TypefaceRequest}


*Defined in [fuchsia.fonts/provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/provider.fidl#40)*

 Parameters for requesting a typeface.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>query</code></td>
            <td>
                <code><a class='link' href='#TypefaceQuery'>TypefaceQuery</a></code>
            </td>
            <td> Parameters for looking up a typeface.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>flags</code></td>
            <td>
                <code><a class='link' href='#TypefaceRequestFlags'>TypefaceRequestFlags</a></code>
            </td>
            <td> Flags for how to process the request, such as which kinds of substitutions are permitted.
</td>
        </tr></table>

### TypefaceQuery {#TypefaceQuery}


*Defined in [fuchsia.fonts/provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/provider.fidl#48)*

 Parameters for looking up a typeface.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>family</code></td>
            <td>
                <code><a class='link' href='#FamilyName'>FamilyName</a></code>
            </td>
            <td> Desired font family name, e.g. "Roboto". Font family search is case-insensitive.

 Note: In cases where the specified family doesn't exist, or the specified family doesn't
 have a glyph for the requested `code_point`, a face from another family may be returned.
 This behavior can be disabled using `TypefaceRequestFlags.EXACT_FAMILY`.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>style</code></td>
            <td>
                <code><a class='link' href='#Style2'>Style2</a></code>
            </td>
            <td> Style properties of the desired typeface.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>languages</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.intl/'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/#LocaleId'>LocaleId</a>&gt;[8]</code>
            </td>
            <td> Language tags in order of preference. This allows disambiguating code points that map
 to different glyphs in different languages (e.g. CJK code points).

 See `fuchsia.intl.LocaleId`.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>code_points</code></td>
            <td>
                <code>vector&lt;uint32&gt;</code>
            </td>
            <td> Optional code points for which glyphs must be present in the returned face.

 Callers that specify this field are expected to extract the character set from the result
 and cache it in order to avoid calling the API more than necessary.
</td>
        </tr><tr>
            <td>5</td>
            <td><code>fallback_family</code></td>
            <td>
                <code><a class='link' href='#GenericFontFamily'>GenericFontFamily</a></code>
            </td>
            <td> A generic font family to fall back to if an exact match is unavailable or does not contain
 the requested code point.

 Every font family belongs to a generic family (configured in the font manifest). If a
 particular font family doesn't contain a requested code point, the provider can search for
 the code point in other font families _in the same generic family_ as a fallback.

 Specifying `fallback_family` in a query allows the client to override the generic family
 that would be used as a fallback.
</td>
        </tr></table>

### TypefaceResponse {#TypefaceResponse}


*Defined in [fuchsia.fonts/provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/provider.fidl#87)*

 Response to a TypefaceRequest. Contains the digital font file and metadata corresponding to a
 returned typeface. Clients are expected to cache the results if they plan to reuse them.

 If a matching typeface cannot be found, the table will be empty.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td> A memory buffer containing the bytes of a digital font file.
 It is the client's responsibility to identify the type of file and to parse it (usually by
 delegating to FreeType or a similar library).
</td>
        </tr><tr>
            <td>2</td>
            <td><code>buffer_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Identifier for the buffer. Responses with the same `buffer_id` are guaranteed to contain the
 same data in the buffer. Clients may use this value to detect if they already have the font
 cached in parsed form.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>font_index</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Index of the returned typeface within `buffer`. Used for digital font formats that may
 contain more than one typeface per file, e.g. TTC (TrueType Collection).
</td>
        </tr></table>

### FontFamilyInfo {#FontFamilyInfo}


*Defined in [fuchsia.fonts/provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/provider.fidl#106)*

 Information about a font family that can be requested using `Provider.GetFontFamilyInfo()`.

 If a matching font family is not found, the table will be empty.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code><a class='link' href='#FamilyName'>FamilyName</a></code>
            </td>
            <td> Canonical font family name. Note that this may be different from the value passed to
 `GetFontFamilyInfo()` due to the resolution of font aliases, and/or differences in
 whitespace and capitalization.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>styles</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Style2'>Style2</a>&gt;[300]</code>
            </td>
            <td> Unordered list of all available styles in the family.
</td>
        </tr></table>

### Style2 {#Style2}


*Defined in [fuchsia.fonts/styles.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/styles.fidl#56)*

 Style properties that can be used when requesting or describing a type face.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>slant</code></td>
            <td>
                <code><a class='link' href='#Slant'>Slant</a></code>
            </td>
            <td> See `Slant`.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>weight</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td> Weight or thickness of the glyphs. Allowed values are integers in the range [1, 1000], but
 most real-world font families only support some integer multiples of 100:
 {100, 200, ..., 900}. Normal text (`WEIGHT_NORMAL`) is 400; `WEIGHT_BOLD` is 700.

 See:
 https://developer.mozilla.org/en-US/docs/Web/CSS/font-weight#Common_weight_name_mapping
 https://docs.microsoft.com/en-us/typography/opentype/spec/os2#usweightclass
</td>
        </tr><tr>
            <td>3</td>
            <td><code>width</code></td>
            <td>
                <code><a class='link' href='#Width'>Width</a></code>
            </td>
            <td> See `Width`.
</td>
        </tr></table>







## **BITS**

### TypefaceRequestFlags {#TypefaceRequestFlags}
Type: <code>uint32</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>EXACT_FAMILY</td>
            <td>1</td>
            <td> Disables font family fallback. The service won't try to search the fallback font set if the
 requested font family doesn't exist or if it doesn't contain the requested code point.
</td>
        </tr><tr>
            <td>EXACT_STYLE</td>
            <td>2</td>
            <td> Disables approximate style matching. The service will only return a face that matches the
 requested style exactly. For example, there will be no substitutions of "medium" for a
 requested "semi-bold" weight, or "oblique" for a requested "italic" slant.
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
            <td> Deprecated. See `FaceRequestFlags`.
 Disables font fallback. The service won't try to search fallback font set if
 there is no requested font family or if it doesn't contain requested
 character.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/font_provider.fidl#31">REQUEST_FLAG_EXACT_MATCH</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td> Deprecated. See `FaceRequestFlags`.
 Disables approximate style matching. The service will only return font that
 matches the requested style exactly.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/provider.fidl#11">MAX_FAMILY_NAME_LENGTH</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
            <td> The maximum length of a font family name.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/provider.fidl#14">MAX_FACE_QUERY_LANGUAGES</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint32</code></td>
            <td> The maximum number of preferred languages allowed in a typeface query.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts/provider.fidl#17">MAX_FAMILY_STYLES</a></td>
            <td>
                    <code>300</code>
                </td>
                <td><code>uint32</code></td>
            <td> The maximum number of styles that will be returned for a font family.
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

