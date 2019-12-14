[TOC]

# fuchsia.sys.index


## **PROTOCOLS**

## ComponentIndex {#ComponentIndex}
*Defined in [fuchsia.sys.index/index.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/component_index/fidl/index.fidl#14)*

<p>ComponentIndex provides search and indexing interfaces for components.</p>

### FuzzySearch {#FuzzySearch}

<p>Returns a list of fuchsia-pkg URL components that matches the input
string based on fuzzy matching.</p>
<p>The input string must be a single alphanumeric word with optional ‘_’
and ‘-’ characters -- the allowed character set of a component name.
Additionally, the forward slash ‘/’ is allowed, to match URI path
segments. Period '.' is also allowed, to match file extensions.</p>
<p>There is no support for globbing.</p>
<p>Returns an empty list if there are no matches, or if needle is empty.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>needle</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#ComponentIndex_FuzzySearch_Result'>ComponentIndex_FuzzySearch_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### ComponentIndex_FuzzySearch_Response {#ComponentIndex_FuzzySearch_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>uris</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### FuzzySearchError {#FuzzySearchError}
Type: <code>uint32</code>

*Defined in [fuchsia.sys.index/index.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/component_index/fidl/index.fidl#8)*

<p>Errors that the FuzzySearch interface presents.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>MALFORMED_INPUT</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>





## **UNIONS**

### ComponentIndex_FuzzySearch_Result {#ComponentIndex_FuzzySearch_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#ComponentIndex_FuzzySearch_Response'>ComponentIndex_FuzzySearch_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#FuzzySearchError'>FuzzySearchError</a></code>
            </td>
            <td></td>
        </tr></table>









