[TOC]

# fuchsia.inspect


## **PROTOCOLS**

## TreeNameIterator {#TreeNameIterator}
*Defined in [fuchsia.inspect/tree.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-inspect/tree.fidl#23)*

<p>Iterator protocol for listing the names of children of a particular Tree.</p>

### GetNext {#GetNext}

<p>Get the next batch of names.</p>
<p>Returns an empty vector and closes the channel when no more names are present.
Implementors may eagerly close the channel after sending the last batch.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>vector&lt;string&gt;[64]</code>
            </td>
        </tr></table>

## Tree {#Tree}
*Defined in [fuchsia.inspect/tree.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-inspect/tree.fidl#43)*

<p>The Tree protocol represents a hierarchy of Inspect VMOs.</p>
<p>Link values stored in an Inspect file contain references to new
named files that contain a continuation of the data for the overall
hierarchy. Protocol Tree allows clients to request these named files so
long as the hosting component is still alive.</p>
<p>Connecting to a particular tree keeps the content for that Tree resident
in memory. Clients are recommended to traverse the trees in depth-first
order to reduce memory usage. Serving components are free to deny
connections to avoid unbounded memory usage.</p>

### GetContent {#GetContent}

<p>Get the content for the Inspect VMO backing this tree.</p>
<p>So long as the Tree connection is still maintained, the contents
of the tree are guaranteed to still be live. Once the connection is
lost, the serving component is free to clear the contents of returned
shared buffers.</p>
<p>Serving components may return different buffers to GetContent
requests for the same Tree.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>content</code></td>
            <td>
                <code><a class='link' href='#TreeContent'>TreeContent</a></code>
            </td>
        </tr></table>

### ListChildNames {#ListChildNames}

<p>Iterate over the names of Trees that are children of this Tree.</p>
<p>The underlying list of children may change in between calls to
ListChildNames and OpenChild.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>tree_iterator</code></td>
            <td>
                <code>request&lt;<a class='link' href='#TreeNameIterator'>TreeNameIterator</a>&gt;</code>
            </td>
        </tr></table>



### OpenChild {#OpenChild}

<p>Open a child Tree by name.</p>
<p>If the child cannot be opened, the given request is closed.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>child_name</code></td>
            <td>
                <code>string[2040]</code>
            </td>
        </tr><tr>
            <td><code>tree</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Tree'>Tree</a>&gt;</code>
            </td>
        </tr></table>









## **TABLES**

### TreeContent {#TreeContent}


*Defined in [fuchsia.inspect/tree.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-inspect/tree.fidl#17)*

<p>The content of a specific Inspect Tree.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td><p>Buffer containing the bytes of a tree in Inspect format.</p>
</td>
        </tr></table>









## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-inspect/tree.fidl#9">MAX_TREE_NAME_LENGTH</a></td>
            <td>
                    <code>2040</code>
                </td>
                <td><code>uint64</code></td>
            <td><p>Maximum length of an Inspect Tree, specified by the format.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-inspect/tree.fidl#12">MAX_TREE_NAME_LIST_SIZE</a></td>
            <td>
                    <code>64</code>
                </td>
                <td><code>uint64</code></td>
            <td><p>Maximum number of children returned by a single read of the tree name iterator.</p>
</td>
        </tr>
    
</table>

