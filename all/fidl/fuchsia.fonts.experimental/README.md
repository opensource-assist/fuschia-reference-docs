[TOC]

# fuchsia.fonts.experimental


## **PROTOCOLS**

## Provider {#Provider}
*Defined in [fuchsia.fonts.experimental/provider.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts.experimental/provider.test.fidl#24)*

<p>Experimental additions to <code>Provider</code>.</p>

### GetTypefaceById {#GetTypefaceById}

<p>Get an exact font by asset ID. This would typically be called
after <code>ListTypefaces</code>, e.g. as part of a font selection interface.
As with <code>fuchsia.fonts.GetTypeface</code>, it is the caller's responsibility
to properly parse the file.</p>
<p>Possible errors:
<code>NOT_FOUND</code> if no asset with the requested <code>id</code> exists.
<code>INTERNAL</code> if the requested <code>id</code> exists, but the asset failed to load.</p>
<p>Eventually this should probably be folded into <code>GetTypeface</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Provider_GetTypefaceById_Result'>Provider_GetTypefaceById_Result</a></code>
            </td>
        </tr></table>

### ListTypefaces {#ListTypefaces}

<p>Creates a <code>ListTypefacesIterator</code> instance that will return a paginated
list of fonts matching <code>request</code>.</p>
<p>Possible errors:
<code>INTERNAL</code> if something bad happens.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code><a class='link' href='#ListTypefacesRequest'>ListTypefacesRequest</a></code>
            </td>
        </tr><tr>
            <td><code>iterator</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ListTypefacesIterator'>ListTypefacesIterator</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Provider_ListTypefaces_Result'>Provider_ListTypefaces_Result</a></code>
            </td>
        </tr></table>

### GetTypefacesByFamily {#GetTypefacesByFamily}

<p>Returns a <code>TypefaceInfo</code> for each font in the requested <code>family</code>. The
results' <code>family</code> fields will hold the canonical family name, even if
this method is called with an alias.</p>
<p>This method should be called only if the caller knows <code>family</code> exists.
Requesting a family that does not exist results in an error. To search
for fonts by family name (or alias), use <code>ListTypefaces</code> instead.</p>
<p>Possible errors:
<code>NOT_FOUND</code> if no family name or alias matches the requested <code>family</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>family</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts/'>fuchsia.fonts</a>/<a class='link' href='../fuchsia.fonts/#FamilyName'>FamilyName</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Provider_GetTypefacesByFamily_Result'>Provider_GetTypefacesByFamily_Result</a></code>
            </td>
        </tr></table>

## ListTypefacesIterator {#ListTypefacesIterator}
*Defined in [fuchsia.fonts.experimental/provider.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts.experimental/provider.test.fidl#57)*


### GetNext {#GetNext}

<p>Returns the next chunk of <code>TypefaceInfo</code> for all typefaces that match
the bound <code>ListTypefacesRequest</code>. If <code>response.results</code> is empty, no
results remain.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#TypefaceInfoResponse'>TypefaceInfoResponse</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Provider_GetTypefaceById_Response {#Provider_GetTypefaceById_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts/'>fuchsia.fonts</a>/<a class='link' href='../fuchsia.fonts/#TypefaceResponse'>TypefaceResponse</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Provider_ListTypefaces_Response {#Provider_ListTypefaces_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Provider_GetTypefacesByFamily_Response {#Provider_GetTypefacesByFamily_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#TypefaceInfoResponse'>TypefaceInfoResponse</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SlantRange {#SlantRange}
*Defined in [fuchsia.fonts.experimental/provider.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts.experimental/provider.test.fidl#109)*



<p>Represents a range of acceptable <code>Slant</code>s. Both bounds are inclusive.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>lower</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts/'>fuchsia.fonts</a>/<a class='link' href='../fuchsia.fonts/#Slant'>Slant</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>upper</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts/'>fuchsia.fonts</a>/<a class='link' href='../fuchsia.fonts/#Slant'>Slant</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### WeightRange {#WeightRange}
*Defined in [fuchsia.fonts.experimental/provider.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts.experimental/provider.test.fidl#115)*



<p>Represents a range of acceptable <code>Weight</code>s. Both bounds are inclusive.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>lower</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>upper</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### WidthRange {#WidthRange}
*Defined in [fuchsia.fonts.experimental/provider.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts.experimental/provider.test.fidl#121)*



<p>Represents a range of acceptable <code>Width</code>s. Both bounds are inclusive.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>lower</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts/'>fuchsia.fonts</a>/<a class='link' href='../fuchsia.fonts/#Width'>Width</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>upper</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts/'>fuchsia.fonts</a>/<a class='link' href='../fuchsia.fonts/#Width'>Width</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### Error {#Error}
Type: <code>uint32</code>

*Defined in [fuchsia.fonts.experimental/provider.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts.experimental/provider.test.fidl#17)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NOT_FOUND</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>INTERNAL</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### ListTypefacesRequest {#ListTypefacesRequest}


*Defined in [fuchsia.fonts.experimental/provider.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts.experimental/provider.test.fidl#66)*

<p>Query parameters for <code>ListTypefaces</code>. Results must match all included
fields. All fields are optional; omitted fields will match any font.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>flags</code></td>
            <td>
                <code><a class='link' href='#ListTypefacesFlags'>ListTypefacesFlags</a></code>
            </td>
            <td><p>Optional flags to modify matching behavior. Ignored if no other fields
are set.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>family</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts/'>fuchsia.fonts</a>/<a class='link' href='../fuchsia.fonts/#FamilyName'>FamilyName</a></code>
            </td>
            <td><p>The name or alias of a font family. By default, families whose name
exactly matches<code>family</code>. For substring matching, set the request's
<code>MATCH_FAMILY_NAME_SUBSTRING</code> flag.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>slant</code></td>
            <td>
                <code><a class='link' href='#SlantRange'>SlantRange</a></code>
            </td>
            <td><p>Results must have a slant within this inclusive range.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>weight</code></td>
            <td>
                <code><a class='link' href='#WeightRange'>WeightRange</a></code>
            </td>
            <td><p>Results must have a weight within this inclusive range.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>width</code></td>
            <td>
                <code><a class='link' href='#WidthRange'>WidthRange</a></code>
            </td>
            <td><p>Results must have a width within this inclusive range.</p>
</td>
        </tr><tr>
            <td>6</td>
            <td><code>languages</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.intl/'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/#LocaleId'>LocaleId</a>&gt;[8]</code>
            </td>
            <td><p>Languages that results must support.
Each result must support all requested languages.</p>
</td>
        </tr><tr>
            <td>7</td>
            <td><code>code_points</code></td>
            <td>
                <code>vector&lt;uint32&gt;</code>
            </td>
            <td><p>Code points that results must include.
Each result must include all requested code points.</p>
</td>
        </tr><tr>
            <td>8</td>
            <td><code>generic_family</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts/'>fuchsia.fonts</a>/<a class='link' href='../fuchsia.fonts/#GenericFontFamily'>GenericFontFamily</a></code>
            </td>
            <td><p>Generic font family which results must belong to. If a font's generic
family is not set, it will only be matched if this field is also not
set. However, omitting this field will still cause it to match any font.</p>
</td>
        </tr></table>

### TypefaceInfoResponse {#TypefaceInfoResponse}


*Defined in [fuchsia.fonts.experimental/provider.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts.experimental/provider.test.fidl#126)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>results</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#TypefaceInfo'>TypefaceInfo</a>&gt;[16]</code>
            </td>
            <td></td>
        </tr></table>

### TypefaceInfo {#TypefaceInfo}


*Defined in [fuchsia.fonts.experimental/provider.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts.experimental/provider.test.fidl#132)*

<p>Collection of typeface metadata that should be sufficient for clients to
perform some kind of selection (likely via human) and request an exact font.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>asset_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Identifier for the font asset. This ID is valid for the lifetime of the
font service. May be used in conjunction with <code>font_index</code> to directly
request this font.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>font_index</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Index of the font within its parent asset. May be used in conjunction
with <code>asset_id</code> to directly request this font.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>family</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts/'>fuchsia.fonts</a>/<a class='link' href='../fuchsia.fonts/#FamilyName'>FamilyName</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>style</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts/'>fuchsia.fonts</a>/<a class='link' href='../fuchsia.fonts/#Style2'>Style2</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>languages</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.intl/'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/#LocaleId'>LocaleId</a>&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td>6</td>
            <td><code>generic_family</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts/'>fuchsia.fonts</a>/<a class='link' href='../fuchsia.fonts/#GenericFontFamily'>GenericFontFamily</a></code>
            </td>
            <td></td>
        </tr></table>



## **UNIONS**

### Provider_GetTypefaceById_Result {#Provider_GetTypefaceById_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Provider_GetTypefaceById_Response'>Provider_GetTypefaceById_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Provider_ListTypefaces_Result {#Provider_ListTypefaces_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Provider_ListTypefaces_Response'>Provider_ListTypefaces_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Provider_GetTypefacesByFamily_Result {#Provider_GetTypefacesByFamily_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Provider_GetTypefacesByFamily_Response'>Provider_GetTypefacesByFamily_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>





## **BITS**

### ListTypefacesFlags {#ListTypefacesFlags}
Type: <code>uint32</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>MATCH_FAMILY_NAME_SUBSTRING</td>
            <td>1</td>
            <td><p>Match families whose name or alias exactly contains the requested
<code>FamilyName</code>. If not set, match families whose name or alias exactly
matches <code>FamilyName</code>.</p>
<p>Note: Matching will always ignore case.</p>
</td>
        </tr></table>



## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts.experimental/provider.test.fidl#15">MAX_TYPEFACE_RESULTS</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum number of font families that can be returned in a
<code>TypefaceInfoResponse</code>.</p>
</td>
        </tr>
    
</table>

