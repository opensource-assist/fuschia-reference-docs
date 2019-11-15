[TOC]

# fuchsia.inspect


## **PROTOCOLS**

## TreeNameIterator {#TreeNameIterator}
*Defined in [fuchsia.inspect/tree.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-inspect/tree.fidl#39)*

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
*Defined in [fuchsia.inspect/tree.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-inspect/tree.fidl#49)*

<p>The Tree protocol represents a hierarchy of Inspect VMOs.</p>

### GetContent {#GetContent}

<p>Get the content for the Inspect VMO backing this tree.</p>

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

### ListChildrenNames {#ListChildrenNames}

<p>Iterate over the names of Trees that are children of this Tree.</p>

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







## **ENUMS**

### TreeState {#TreeState}
Type: <code>uint32</code>

*Defined in [fuchsia.inspect/tree.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-inspect/tree.fidl#27)*

<p>The state of the buffer returned in a TreeContent.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>IN_USE</code></td>
            <td><code>1</code></td>
            <td><p>The VMO backing the buffer is still in use. Clients must interpret
the whole buffer accoring to the Inspect format reading algorithm.</p>
</td>
        </tr><tr>
            <td><code>COMPLETE</code></td>
            <td><code>2</code></td>
            <td><p>The VMO backing the buffer is complete, and will not be modified further.
Clients may read the buffer without performing the whole
consistency algorithm, but they should still be wary of the input.</p>
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
        </tr><tr>
            <td>2</td>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#TreeState'>TreeState</a></code>
            </td>
            <td><p>Describes the current state of the buffer, which informs the
reader how to interpet it (see below).</p>
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

