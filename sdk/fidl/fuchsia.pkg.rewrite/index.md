Project: /_project.yaml
Book: /_book.yaml

# fuchsia.pkg.rewrite


## **PROTOCOLS**

## Engine {:#Engine}
*Defined in [fuchsia.pkg.rewrite/rewrite.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg.rewrite/rewrite.fidl#95)*

 Manages fuchsia-pkg:// rewrite rules.

 When a package resolver is asked to resolve a fuchsia-pkg URL, it must first
 iterate through its sequence of rewrite rules (given by <a class='link' href='#List'>List</a>). The
 rewrite engine will rewrite the given URL with the first rule that:
 * matches the given URL
 * produces a valid URL when applied to the given URL
 If no rules match, the URL is resolved as-is.

 This interface is intended to be implemented by package resolver components,
 and used by repository administration tools.

### StartEditTransaction {:#StartEditTransaction}

 Begins a rule edit transaction.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>transaction</code></td>
            <td>
                <code>request&lt;<a class='link' href='#EditTransaction'>EditTransaction</a>&gt;</code>
            </td>
        </tr></table>



### List {:#List}

 Return an iterator over all rewrite rules.

 + request `iterator` is a request for an iterator.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>iterator</code></td>
            <td>
                <code>request&lt;<a class='link' href='#RuleIterator'>RuleIterator</a>&gt;</code>
            </td>
        </tr></table>



### ListStatic {:#ListStatic}

 Return an iterator over all static (immutable) rewrite rules. These
 rules are handled as lower priority than dynamic rules and cannot be
 modified (although they can be overridden) by <a class='link' href='#EditTransaction'>EditTransaction</a>s.

 + request `iterator` is a request for an iterator.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>iterator</code></td>
            <td>
                <code>request&lt;<a class='link' href='#RuleIterator'>RuleIterator</a>&gt;</code>
            </td>
        </tr></table>



### TestApply {:#TestApply}

 Rewrite the given `url` with the current rewrite rule set, returning the
 `rewritten` url.  If no rules match or a rule matches but performs an
 identity transformation, this API returns `url` unchanged.

 This API is intended only for reflecting on rule side effects. Using
 this API to pre-apply the rules, then passing the result to
 <a class='link' href='../fuchsia.pkg/index.html'>fuchsia.pkg</a>/<a class='link' href='../fuchsia.pkg/index.html#PackageResolver.Resolve'>PackageResolver.Resolve</a> would apply the rules twice.

 + request `url` the url to rewrite.
 - response `rewritten` the rewritten url.
 * error `ZX_ERR_INVALID_ARGS` If `url` is not a valid `fuchsia-pkg://`
    URL. See <a class='link' href='#fuchsia-pkg URL'>fuchsia-pkg URL</a>.

 <a class='link' href='#fuchsia-pkg URL'>fuchsia-pkg URL</a>:
    https://fuchsia.googlesource.com/fuchsia/+/master/docs/the-book/package_url.md

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

## EditTransaction {:#EditTransaction}
*Defined in [fuchsia.pkg.rewrite/rewrite.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg.rewrite/rewrite.fidl#129)*


### ListDynamic {:#ListDynamic}

 Return an iterator over all dynamic (editable) rewrite rules. The
 iterator will reflect any changes made to the rewrite rules so far in
 this transaction.

 + request `iterator` is a request for an iterator.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>iterator</code></td>
            <td>
                <code>request&lt;<a class='link' href='#RuleIterator'>RuleIterator</a>&gt;</code>
            </td>
        </tr></table>



### ResetAll {:#ResetAll}

 Removes all dynamically configured rewrite rules, leaving only any
 statically configured rules.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Add {:#Add}

 Add a rewrite rule with highest priority. If `rule` already exists, this
 API will prioritize it over other rules.

 + request `rule` the rewrite rule to persist.

 * status `ZX_OK` if the rule was staged to be added.
 * status `ZX_ERR_INVALID_ARGS` If `url` is not a valid `fuchsia-pkg://`
    URL. See <a class='link' href='#fuchsia-pkg URL'>fuchsia-pkg URL</a>.

 <a class='link' href='#fuchsia-pkg URL'>fuchsia-pkg URL</a>:
    https://fuchsia.googlesource.com/fuchsia/+/master/docs/the-book/package_url.md

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

### Commit {:#Commit}

 Commit this transaction, or detect another transaction that committed
 before this one.

 * status `ZX_OK` the staged edits were successfully committed.
 * status `ZX_ERR_UNAVAILABLE` another transaction committed before this one.

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

## RuleIterator {:#RuleIterator}
*Defined in [fuchsia.pkg.rewrite/rewrite.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg.rewrite/rewrite.fidl#164)*

 The iterator over all the rewrite rules defined in a <a class='link' href='#Engine'>Engine</a>.

### Next {:#Next}

 Advance the iterator and return the next batch of rules.

 - response `rules` a vector of <a class='link' href='#Rule'>Rule</a> rules. Will return an empty
    vector when there are no more rules.

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

### Engine_TestApply_Response {:#Engine_TestApply_Response}
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

### LiteralRule {:#LiteralRule}
*Defined in [fuchsia.pkg.rewrite/rewrite.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg.rewrite/rewrite.fidl#45)*



 A literal match and replacement rule.

 # Examples

 Replaces example.com with test.example.com for all packages
 ```
 {
     host_match: "example.com"
     host_replacement: "test.example.com"
     path_prefix_match: "/"
     path_prefix_replacement: "/"
 }
 ```

 Replaces example.com with test.example.com for
 fuchsia-pkg://example.com/rolldice. A package called "rolldice" in another
 repo would not be rewritten.
 ```
 {
     host_match: "example.com"
     host_replacement: "test.example.com"
     path_prefix_match: "/rolldice"
     path_prefix_replacement: "/rolldice"
 }
 ```

 Redirects all packages under "fuchsia-pkg://example.com/examples/" to
 "fuchsia-pkg://example.com/examples/beta/".
 ```
 {
     host_match: "example.com"
     host_replacement: "example.com"
     path_prefix_match: "/examples/"
     path_prefix_replacement: "/examples/beta/"
 }
 ```


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>host_match</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The exact hostname to match.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>host_replacement</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The new hostname to replace the matched `host_match` with.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>path_prefix_match</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The absolute path to a package or directory to match against.

 If `path_prefix_match` ends with '/', it will match any packages or
 subdirectories below the matched path.
 If `path_prefix_match` does not end with '/', it will be interpreted as
 as an exact match.

 # Examples

 "/example" only matches a package called "example" at the root of the
 repo. "/parent/examples" and "/examples" would not match.

 "/example/" would match any package under the "example" path at the root
 of the repo.  For example, "/example/", "/example/package" would both
 match.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>path_prefix_replacement</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The absolute path to a single package or a directory to replace the
 matched `path_prefix_match` with.

 `path_prefix_match` and `path_prefix_replacement` must both match
 directories or both match exact packages. Mixing the two forms is not
 allowed.
</td>
            <td>No default</td>
        </tr>
</table>







## **UNIONS**

### Engine_TestApply_Result {:#Engine_TestApply_Result}
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

### Rule {:#Rule}
*Defined in [fuchsia.pkg.rewrite/rewrite.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.pkg.rewrite/rewrite.fidl#79)*

 A rewrite rule, represented as an xunion for future compatibility.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>literal</code></td>
            <td>
                <code><a class='link' href='#LiteralRule'>LiteralRule</a></code>
            </td>
            <td></td>
        </tr></table>





