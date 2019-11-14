[TOC]

# fuchsia.pkg.rewrite


## **PROTOCOLS**

## Engine {#Engine}
*Defined in [fuchsia.pkg.rewrite/rewrite.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg.rewrite/rewrite.fidl#95)*

<p>Manages fuchsia-pkg:// rewrite rules.</p>
<p>When a package resolver is asked to resolve a fuchsia-pkg URL, it must first
iterate through its sequence of rewrite rules (given by <a class='link' href='#List'>List</a>). The
rewrite engine will rewrite the given URL with the first rule that:</p>
<ul>
<li>matches the given URL</li>
<li>produces a valid URL when applied to the given URL
If no rules match, the URL is resolved as-is.</li>
</ul>
<p>This interface is intended to be implemented by package resolver components,
and used by repository administration tools.</p>

### StartEditTransaction {#StartEditTransaction}

<p>Begins a rule edit transaction.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>transaction</code></td>
            <td>
                <code>request&lt;<a class='link' href='#EditTransaction'>EditTransaction</a>&gt;</code>
            </td>
        </tr></table>



### List {#List}

<p>Return an iterator over all rewrite rules.</p>
<ul>
<li>request <code>iterator</code> is a request for an iterator.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>iterator</code></td>
            <td>
                <code>request&lt;<a class='link' href='#RuleIterator'>RuleIterator</a>&gt;</code>
            </td>
        </tr></table>



### ListStatic {#ListStatic}

<p>Return an iterator over all static (immutable) rewrite rules. These
rules are handled as lower priority than dynamic rules and cannot be
modified (although they can be overridden) by <a class='link' href='#EditTransaction'>EditTransaction</a>s.</p>
<ul>
<li>request <code>iterator</code> is a request for an iterator.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>iterator</code></td>
            <td>
                <code>request&lt;<a class='link' href='#RuleIterator'>RuleIterator</a>&gt;</code>
            </td>
        </tr></table>



### TestApply {#TestApply}

<p>Rewrite the given <code>url</code> with the current rewrite rule set, returning the
<code>rewritten</code> url.  If no rules match or a rule matches but performs an
identity transformation, this API returns <code>url</code> unchanged.</p>
<p>This API is intended only for reflecting on rule side effects. Using
this API to pre-apply the rules, then passing the result to
<a class='link' href='../fuchsia.pkg/'>fuchsia.pkg</a>/<a class='link' href='../fuchsia.pkg/#PackageResolver.Resolve'>PackageResolver.Resolve</a> would apply the rules twice.</p>
<ul>
<li>request <code>url</code> the url to rewrite.</li>
</ul>
<ul>
<li>response <code>rewritten</code> the rewritten url.</li>
</ul>
<ul>
<li>error <code>ZX_ERR_INVALID_ARGS</code> If <code>url</code> is not a valid <code>fuchsia-pkg://</code>
URL. See <a class='link' href='#fuchsia-pkg URL'>fuchsia-pkg URL</a>.</li>
</ul>
<p><a class='link' href='#fuchsia-pkg URL'>fuchsia-pkg URL</a>:
https://fuchsia.googlesource.com/fuchsia/+/master/docs/the-book/package_url.md</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>url</code></td>
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
                <code><a class='link' href='#Engine_TestApply_Result'>Engine_TestApply_Result</a></code>
            </td>
        </tr></table>

## EditTransaction {#EditTransaction}
*Defined in [fuchsia.pkg.rewrite/rewrite.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg.rewrite/rewrite.fidl#129)*


### ListDynamic {#ListDynamic}

<p>Return an iterator over all dynamic (editable) rewrite rules. The
iterator will reflect any changes made to the rewrite rules so far in
this transaction.</p>
<ul>
<li>request <code>iterator</code> is a request for an iterator.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>iterator</code></td>
            <td>
                <code>request&lt;<a class='link' href='#RuleIterator'>RuleIterator</a>&gt;</code>
            </td>
        </tr></table>



### ResetAll {#ResetAll}

<p>Removes all dynamically configured rewrite rules, leaving only any
statically configured rules.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Add {#Add}

<p>Add a rewrite rule with highest priority. If <code>rule</code> already exists, this
API will prioritize it over other rules.</p>
<ul>
<li>request <code>rule</code> the rewrite rule to persist.</li>
</ul>
<ul>
<li>status <code>ZX_OK</code> if the rule was staged to be added.</li>
<li>status <code>ZX_ERR_INVALID_ARGS</code> If <code>url</code> is not a valid <code>fuchsia-pkg://</code>
URL. See <a class='link' href='#fuchsia-pkg URL'>fuchsia-pkg URL</a>.</li>
</ul>
<p><a class='link' href='#fuchsia-pkg URL'>fuchsia-pkg URL</a>:
https://fuchsia.googlesource.com/fuchsia/+/master/docs/the-book/package_url.md</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rule</code></td>
            <td>
                <code><a class='link' href='#Rule'>Rule</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### Commit {#Commit}

<p>Commit this transaction, or detect another transaction that committed
before this one.</p>
<ul>
<li>status <code>ZX_OK</code> the staged edits were successfully committed.</li>
<li>status <code>ZX_ERR_UNAVAILABLE</code> another transaction committed before this one.</li>
<li>status <code>ZX_ERR_ACCESS_DENIED</code> editing dynamic rewrite rules is permanently disabled.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

## RuleIterator {#RuleIterator}
*Defined in [fuchsia.pkg.rewrite/rewrite.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg.rewrite/rewrite.fidl#164)*

<p>The iterator over all the rewrite rules defined in a <a class='link' href='#Engine'>Engine</a>.</p>

### Next {#Next}

<p>Advance the iterator and return the next batch of rules.</p>
<ul>
<li>response <code>rules</code> a vector of <a class='link' href='#Rule'>Rule</a> rules. Will return an empty
vector when there are no more rules.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rules</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Rule'>Rule</a>&gt;</code>
            </td>
        </tr></table>



## **STRUCTS**

### Engine_TestApply_Response {#Engine_TestApply_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>rewritten</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### LiteralRule {#LiteralRule}
*Defined in [fuchsia.pkg.rewrite/rewrite.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg.rewrite/rewrite.fidl#45)*



<p>A literal match and replacement rule.</p>
<h1>Examples</h1>
<p>Replaces example.com with test.example.com for all packages</p>
<pre><code>{
    host_match: &quot;example.com&quot;
    host_replacement: &quot;test.example.com&quot;
    path_prefix_match: &quot;/&quot;
    path_prefix_replacement: &quot;/&quot;
}
</code></pre>
<p>Replaces example.com with test.example.com for
fuchsia-pkg://example.com/rolldice. A package called &quot;rolldice&quot; in another
repo would not be rewritten.</p>
<pre><code>{
    host_match: &quot;example.com&quot;
    host_replacement: &quot;test.example.com&quot;
    path_prefix_match: &quot;/rolldice&quot;
    path_prefix_replacement: &quot;/rolldice&quot;
}
</code></pre>
<p>Redirects all packages under &quot;fuchsia-pkg://example.com/examples/&quot; to
&quot;fuchsia-pkg://example.com/examples/beta/&quot;.</p>
<pre><code>{
    host_match: &quot;example.com&quot;
    host_replacement: &quot;example.com&quot;
    path_prefix_match: &quot;/examples/&quot;
    path_prefix_replacement: &quot;/examples/beta/&quot;
}
</code></pre>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>host_match</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The exact hostname to match.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>host_replacement</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The new hostname to replace the matched <code>host_match</code> with.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>path_prefix_match</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The absolute path to a package or directory to match against.</p>
<p>If <code>path_prefix_match</code> ends with '/', it will match any packages or
subdirectories below the matched path.
If <code>path_prefix_match</code> does not end with '/', it will be interpreted as
as an exact match.</p>
<h1>Examples</h1>
<p>&quot;/example&quot; only matches a package called &quot;example&quot; at the root of the
repo. &quot;/parent/examples&quot; and &quot;/examples&quot; would not match.</p>
<p>&quot;/example/&quot; would match any package under the &quot;example&quot; path at the root
of the repo.  For example, &quot;/example/&quot;, &quot;/example/package&quot; would both
match.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>path_prefix_replacement</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The absolute path to a single package or a directory to replace the
matched <code>path_prefix_match</code> with.</p>
<p><code>path_prefix_match</code> and <code>path_prefix_replacement</code> must both match
directories or both match exact packages. Mixing the two forms is not
allowed.</p>
</td>
            <td>No default</td>
        </tr>
</table>







## **UNIONS**

### Engine_TestApply_Result {#Engine_TestApply_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Engine_TestApply_Response'>Engine_TestApply_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>



## **XUNIONS**

### Rule {#Rule}
*Defined in [fuchsia.pkg.rewrite/rewrite.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg.rewrite/rewrite.fidl#79)*

<p>A rewrite rule, represented as an xunion for future compatibility.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>literal</code></td>
            <td>
                <code><a class='link' href='#LiteralRule'>LiteralRule</a></code>
            </td>
            <td></td>
        </tr></table>





