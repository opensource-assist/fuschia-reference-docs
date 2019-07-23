Project: /_project.yaml
Book: /_book.yaml

# fuchsia.fonts.experimental


## **PROTOCOLS**

## Provider {:#Provider}
*Defined in [fuchsia.fonts.experimental/provider.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts.experimental/provider.test.fidl#23)*

 Experimental additions to `Provider`.

### GetTypefaceById {:#GetTypefaceById}

 Get an exact font by asset ID. This would typically be called
 after `ListTypefaces`, e.g. as part of a font selection interface.
 As with `fuchsia.fonts.GetTypeface`, it is the caller's responsibility
 to properly parse the file.

 Possible errors:
 `NOT_FOUND` if no asset with the requested `id` exists.
 `INTERNAL` if the requested `id` exists, but the asset failed to load.

 Eventually this should probably be folded into `GetTypeface`.

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
                <code><a class='link' href='../fuchsia.fonts.experimental/index.html#Provider_GetTypefaceById_Result'>Provider_GetTypefaceById_Result</a></code>
            </td>
        </tr></table>

### ListTypefaces {:#ListTypefaces}

 Creates a `ListTypefacesIterator` instance that will return a paginated
 list of fonts matching `request`.

 Possible errors:
 `INTERNAL` if something bad happens.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts.experimental/index.html#ListTypefacesRequest'>ListTypefacesRequest</a></code>
            </td>
        </tr><tr>
            <td><code>iterator</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.fonts.experimental/index.html#ListTypefacesIterator'>ListTypefacesIterator</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts.experimental/index.html#Provider_ListTypefaces_Result'>Provider_ListTypefaces_Result</a></code>
            </td>
        </tr></table>

### GetTypefacesByFamily {:#GetTypefacesByFamily}

 Returns a `TypefaceInfo` for each font in the requested `family`. The
 results' `family` fields will hold the canonical family name, even if
 this method is called with an alias.

 This method should be called only if the caller knows `family` exists.
 Requesting a family that does not exist results in an error. To search
 for fonts by family name (or alias), use `ListTypefaces` instead.

 Possible errors:
 `NOT_FOUND` if no family name or alias matches the requested `family`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>family</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts/index.html'>fuchsia.fonts</a>/<a class='link' href='../fuchsia.fonts/index.html#FamilyName'>FamilyName</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts.experimental/index.html#Provider_GetTypefacesByFamily_Result'>Provider_GetTypefacesByFamily_Result</a></code>
            </td>
        </tr></table>

## ListTypefacesIterator {:#ListTypefacesIterator}
*Defined in [fuchsia.fonts.experimental/provider.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts.experimental/provider.test.fidl#56)*


### GetNext {:#GetNext}

 Returns the next chunk of `TypefaceInfo` for all typefaces that match
 the bound `ListTypefacesRequest`. If `response.results` is empty, no
 results remain.

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
                <code><a class='link' href='../fuchsia.fonts.experimental/index.html#TypefaceInfoResponse'>TypefaceInfoResponse</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Provider_GetTypefaceById_Response {:#Provider_GetTypefaceById_Response}
*Defined in [fuchsia.fonts.experimental/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#2)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts/index.html'>fuchsia.fonts</a>/<a class='link' href='../fuchsia.fonts/index.html#TypefaceResponse'>TypefaceResponse</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Provider_ListTypefaces_Response {:#Provider_ListTypefaces_Response}
*Defined in [fuchsia.fonts.experimental/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#9)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Provider_GetTypefacesByFamily_Response {:#Provider_GetTypefacesByFamily_Response}
*Defined in [fuchsia.fonts.experimental/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#16)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts.experimental/index.html#TypefaceInfoResponse'>TypefaceInfoResponse</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### Error {:#Error}
Type: <code>uint32</code>

*Defined in [fuchsia.fonts.experimental/provider.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts.experimental/provider.test.fidl#16)*



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

### ListTypefacesRequest {:#ListTypefacesRequest}


*Defined in [fuchsia.fonts.experimental/provider.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts.experimental/provider.test.fidl#65)*

 Query parameters for `ListTypefaces`. Results must match all included
 fields. All fields are optional; omitted fields will match any font.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>flags</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts.experimental/index.html#ListTypefacesFlags'>ListTypefacesFlags</a></code>
            </td>
            <td> Optional flags to modify matching behavior. Ignored if no other fields
 are set.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>family</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts/index.html'>fuchsia.fonts</a>/<a class='link' href='../fuchsia.fonts/index.html#FamilyName'>FamilyName</a></code>
            </td>
            <td> The name or alias of a font family. By default, families whose name
 exactly matches`family`. For substring matching, set the request's
 `MATCH_FAMILY_NAME_SUBSTRING` flag.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>styles</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.fonts/index.html'>fuchsia.fonts</a>/<a class='link' href='../fuchsia.fonts/index.html#Style2'>Style2</a>&gt;[300]</code>
            </td>
            <td> Styles to match. Note that combining styles will change results.
 For example, `[{slant: UPRIGHT}, {weight: WEIGHT_BOLD}]` matches fonts
 that are upright *or* bold but `[{slant: UPRIGHT, weight: WEIGHT_BOLD}]`
 only matches fonts that are both upright *and* bold.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>languages</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.intl/index.html'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/index.html#LocaleId'>LocaleId</a>&gt;[8]</code>
            </td>
            <td> Languages that results must support.
 Each result must support all requested languages.
</td>
        </tr><tr>
            <td>5</td>
            <td><code>code_points</code></td>
            <td>
                <code>vector&lt;uint32&gt;</code>
            </td>
            <td> Code points that results must include.
 Each result must include all requested code points.
</td>
        </tr><tr>
            <td>6</td>
            <td><code>generic_families</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.fonts/index.html'>fuchsia.fonts</a>/<a class='link' href='../fuchsia.fonts/index.html#GenericFontFamily'>GenericFontFamily</a>&gt;</code>
            </td>
            <td> Generic font families to match. Results will include fonts belonging to
 any requested generic family. Note that a font can only belong to one
 generic family, so there is no way to request a font belonging to
 all requested generic families.
</td>
        </tr></table>

### TypefaceInfoResponse {:#TypefaceInfoResponse}


*Defined in [fuchsia.fonts.experimental/provider.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts.experimental/provider.test.fidl#105)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>results</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.fonts.experimental/index.html#TypefaceInfo'>TypefaceInfo</a>&gt;[16]</code>
            </td>
            <td></td>
        </tr></table>

### TypefaceInfo {:#TypefaceInfo}


*Defined in [fuchsia.fonts.experimental/provider.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts.experimental/provider.test.fidl#111)*

 Collection of typeface metadata that should be sufficient for clients to
 perform some kind of selection (likely via human) and request an exact font.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>asset_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Identifier for the font asset. This ID is valid for the lifetime of the
 font service. May be used in conjunction with `font_index` to directly
 request this font.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>font_index</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Index of the font within its parent asset. May be used in conjunction
 with `asset_id` to directly request this font.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>family</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts/index.html'>fuchsia.fonts</a>/<a class='link' href='../fuchsia.fonts/index.html#FamilyName'>FamilyName</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>style</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts/index.html'>fuchsia.fonts</a>/<a class='link' href='../fuchsia.fonts/index.html#Style2'>Style2</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>languages</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.intl/index.html'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/index.html#LocaleId'>LocaleId</a>&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td>6</td>
            <td><code>generic_family</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts/index.html'>fuchsia.fonts</a>/<a class='link' href='../fuchsia.fonts/index.html#GenericFontFamily'>GenericFontFamily</a></code>
            </td>
            <td></td>
        </tr></table>



## **UNIONS**

### Provider_GetTypefaceById_Result {:#Provider_GetTypefaceById_Result}
*Defined in [fuchsia.fonts.experimental/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#5)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts.experimental/index.html#Provider_GetTypefaceById_Response'>Provider_GetTypefaceById_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts.experimental/index.html#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Provider_ListTypefaces_Result {:#Provider_ListTypefaces_Result}
*Defined in [fuchsia.fonts.experimental/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#12)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts.experimental/index.html#Provider_ListTypefaces_Response'>Provider_ListTypefaces_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts.experimental/index.html#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Provider_GetTypefacesByFamily_Result {:#Provider_GetTypefacesByFamily_Result}
*Defined in [fuchsia.fonts.experimental/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#19)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts.experimental/index.html#Provider_GetTypefacesByFamily_Response'>Provider_GetTypefacesByFamily_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts.experimental/index.html#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>





## **BITS**
### ListTypefacesFlags {:#ListTypefacesFlags}
Type: <code>uint32</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>MATCH_FAMILY_NAME_SUBSTRING</td>
            <td>1</td>
            <td> Match families whose name or alias exactly contains the requested
 `FamilyName`. If not set, match families whose name or alias exactly
 matches `FamilyName`.

 Note: Matching will always ignore case.
</td>
        </tr></table>



## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.fonts.experimental/provider.test.fidl#14">MAX_TYPEFACE_RESULTS</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    
</table>

