Project: /_project.yaml
Book: /_book.yaml

# fidl.examples.bindingstest


## **PROTOCOLS**

## TestServer {:#TestServer}
*Defined in [fidl.examples.bindingstest/bindings_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/fidl_bindings_test/fidl/bindings_test.test.fidl#38)*


### OneWayNoArgs {:#OneWayNoArgs}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### ReceivedOneWayNoArgs {:#ReceivedOneWayNoArgs}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>received</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

### OneWayStringArg {:#OneWayStringArg}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### ReceivedOneWayString {:#ReceivedOneWayString}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

### OneWayThreeArgs {:#OneWayThreeArgs}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>x</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>z</code></td>
            <td>
                <code><a class='link' href='#NoHandleStruct'>NoHandleStruct</a></code>
            </td>
        </tr></table>



### ReceivedOneWayThreeArgs {:#ReceivedOneWayThreeArgs}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>x</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>z</code></td>
            <td>
                <code><a class='link' href='#NoHandleStruct'>NoHandleStruct</a></code>
            </td>
        </tr></table>

### OneWayExampleTable {:#OneWayExampleTable}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#ExampleTable'>ExampleTable</a></code>
            </td>
        </tr></table>



### ReceivedOneWayExampleTable {:#ReceivedOneWayExampleTable}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>received</code></td>
            <td>
                <code><a class='link' href='#ExampleTable'>ExampleTable</a></code>
            </td>
        </tr></table>

### TwoWayNoArgs {:#TwoWayNoArgs}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### TwoWayStringArg {:#TwoWayStringArg}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

### TwoWayThreeArgs {:#TwoWayThreeArgs}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>x</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>z</code></td>
            <td>
                <code><a class='link' href='#NoHandleStruct'>NoHandleStruct</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>x</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>z</code></td>
            <td>
                <code><a class='link' href='#NoHandleStruct'>NoHandleStruct</a></code>
            </td>
        </tr></table>

### OneWayExampleXunion {:#OneWayExampleXunion}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#ExampleXunion'>ExampleXunion</a></code>
            </td>
        </tr></table>



### ReceivedOneWayExampleXunion {:#ReceivedOneWayExampleXunion}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>received</code></td>
            <td>
                <code><a class='link' href='#ExampleXunion'>ExampleXunion</a></code>
            </td>
        </tr></table>

### OneWayExampleBits {:#OneWayExampleBits}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#ExampleBits'>ExampleBits</a></code>
            </td>
        </tr></table>



### ReceivedOneWayExampleBits {:#ReceivedOneWayExampleBits}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>received</code></td>
            <td>
                <code><a class='link' href='#ExampleBits'>ExampleBits</a></code>
            </td>
        </tr></table>

### SendEmptyEvent {:#SendEmptyEvent}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### EmptyEvent {:#EmptyEvent}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### SendStringEvent {:#SendStringEvent}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### StringEvent {:#StringEvent}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

### SendThreeArgEvent {:#SendThreeArgEvent}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>x</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>z</code></td>
            <td>
                <code><a class='link' href='#NoHandleStruct'>NoHandleStruct</a></code>
            </td>
        </tr></table>



### ThreeArgEvent {:#ThreeArgEvent}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>x</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>z</code></td>
            <td>
                <code><a class='link' href='#NoHandleStruct'>NoHandleStruct</a></code>
            </td>
        </tr></table>

### SendMultipleEvents {:#SendMultipleEvents}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>count</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>intervalSeconds</code></td>
            <td>
                <code>float64</code>
            </td>
        </tr></table>



### MultipleEvent {:#MultipleEvent}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>index</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### ReplySlowly {:#ReplySlowly}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>delaySeconds</code></td>
            <td>
                <code>float64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

### ReplyWithErrorZero {:#ReplyWithErrorZero}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>with_error</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#TestServer_ReplyWithErrorZero_Result'>TestServer_ReplyWithErrorZero_Result</a></code>
            </td>
        </tr></table>

### ReplyWithErrorOne {:#ReplyWithErrorOne}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>with_error</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>value</code></td>
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
                <code><a class='link' href='#TestServer_ReplyWithErrorOne_Result'>TestServer_ReplyWithErrorOne_Result</a></code>
            </td>
        </tr></table>

### ReplyWithErrorMore {:#ReplyWithErrorMore}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>with_error</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>other_value</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#TestServer_ReplyWithErrorMore_Result'>TestServer_ReplyWithErrorMore_Result</a></code>
            </td>
        </tr></table>

### ReplyWithErrorEnumZero {:#ReplyWithErrorEnumZero}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>with_error</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#TestServer_ReplyWithErrorEnumZero_Result'>TestServer_ReplyWithErrorEnumZero_Result</a></code>
            </td>
        </tr></table>

### ReplyWithErrorEnumOne {:#ReplyWithErrorEnumOne}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>with_error</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>value</code></td>
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
                <code><a class='link' href='#TestServer_ReplyWithErrorEnumOne_Result'>TestServer_ReplyWithErrorEnumOne_Result</a></code>
            </td>
        </tr></table>

### ReplyWithErrorEnumMore {:#ReplyWithErrorEnumMore}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>with_error</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>other_value</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#TestServer_ReplyWithErrorEnumMore_Result'>TestServer_ReplyWithErrorEnumMore_Result</a></code>
            </td>
        </tr></table>

### CloseConnection {:#CloseConnection}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>delaySeconds</code></td>
            <td>
                <code>float64</code>
            </td>
        </tr></table>



### NeverEvent {:#NeverEvent}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## SimpleServer {:#SimpleServer}
*Defined in [fidl.examples.bindingstest/bindings_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/fidl_bindings_test/fidl/bindings_test.test.fidl#118)*


### Ping {:#Ping}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## **STRUCTS**

### TestServer_ReplyWithErrorZero_Response {:#TestServer_ReplyWithErrorZero_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### TestServer_ReplyWithErrorOne_Response {:#TestServer_ReplyWithErrorOne_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TestServer_ReplyWithErrorMore_Response {:#TestServer_ReplyWithErrorMore_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>other_value</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TestServer_ReplyWithErrorEnumZero_Response {:#TestServer_ReplyWithErrorEnumZero_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### TestServer_ReplyWithErrorEnumOne_Response {:#TestServer_ReplyWithErrorEnumOne_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TestServer_ReplyWithErrorEnumMore_Response {:#TestServer_ReplyWithErrorEnumMore_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>other_value</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### NoHandleStruct {:#NoHandleStruct}
*Defined in [fidl.examples.bindingstest/bindings_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/fidl_bindings_test/fidl/bindings_test.test.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>foo</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bar</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>baz</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ExampleStruct {:#ExampleStruct}
*Defined in [fidl.examples.bindingstest/bindings_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/fidl_bindings_test/fidl/bindings_test.test.fidl#13)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>foo</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bar</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>baz</code></td>
            <td>
                <code>vector&lt;uint8&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### HandleStruct {:#HandleStruct}
*Defined in [fidl.examples.bindingstest/bindings_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/fidl_bindings_test/fidl/bindings_test.test.fidl#100)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>foo</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bar</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>baz</code></td>
            <td>
                <code>handle&lt;handle&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### EmptyStruct {:#EmptyStruct}
*Defined in [fidl.examples.bindingstest/conformance.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/fidl_bindings_test/fidl/conformance.test.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### TestEmptyStructSandwich {:#TestEmptyStructSandwich}
*Defined in [fidl.examples.bindingstest/conformance.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/fidl_bindings_test/fidl/conformance.test.fidl#10)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>before</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>es</code></td>
            <td>
                <code><a class='link' href='#EmptyStruct'>EmptyStruct</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>after</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TestSimpleTable {:#TestSimpleTable}
*Defined in [fidl.examples.bindingstest/conformance.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/fidl_bindings_test/fidl/conformance.test.fidl#24)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>table</code></td>
            <td>
                <code><a class='link' href='#SimpleTable'>SimpleTable</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TestTableWithStringAndVector {:#TestTableWithStringAndVector}
*Defined in [fidl.examples.bindingstest/conformance.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/fidl_bindings_test/fidl/conformance.test.fidl#34)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>table</code></td>
            <td>
                <code><a class='link' href='#TableWithStringAndVector'>TableWithStringAndVector</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Int64Struct {:#Int64Struct}
*Defined in [fidl.examples.bindingstest/conformance.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/fidl_bindings_test/fidl/conformance.test.fidl#46)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TestInlineXUnionInStruct {:#TestInlineXUnionInStruct}
*Defined in [fidl.examples.bindingstest/conformance.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/fidl_bindings_test/fidl/conformance.test.fidl#56)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>before</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>xu</code></td>
            <td>
                <code><a class='link' href='#SampleXUnion'>SampleXUnion</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>after</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TestOptionalXUnionInStruct {:#TestOptionalXUnionInStruct}
*Defined in [fidl.examples.bindingstest/conformance.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/fidl_bindings_test/fidl/conformance.test.fidl#62)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>before</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>xu</code></td>
            <td>
                <code><a class='link' href='#SampleXUnion'>SampleXUnion</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>after</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TestXUnionInTable {:#TestXUnionInTable}
*Defined in [fidl.examples.bindingstest/conformance.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/fidl_bindings_test/fidl/conformance.test.fidl#74)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#XUnionInTable'>XUnionInTable</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TestString3 {:#TestString3}
*Defined in [fidl.examples.bindingstest/conformance.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/fidl_bindings_test/fidl/conformance.test.fidl#78)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>a</code></td>
            <td>
                <code>[2]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>b</code></td>
            <td>
                <code>[2]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TestStringWithBound {:#TestStringWithBound}
*Defined in [fidl.examples.bindingstest/conformance.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/fidl_bindings_test/fidl/conformance.test.fidl#83)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>a</code></td>
            <td>
                <code>string[8]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### EnumOne {:#EnumOne}
Type: <code>uint32</code>

*Defined in [fidl.examples.bindingstest/bindings_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/fidl_bindings_test/fidl/bindings_test.test.fidl#88)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ONE</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>TWO</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>THREE</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### EnumTwo {:#EnumTwo}
Type: <code>uint32</code>

*Defined in [fidl.examples.bindingstest/bindings_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/fidl_bindings_test/fidl/bindings_test.test.fidl#94)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ONE</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>TWO</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>THREE</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### ExampleTable {:#ExampleTable}


*Defined in [fidl.examples.bindingstest/bindings_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/fidl_bindings_test/fidl/bindings_test.test.fidl#19)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>foo</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>bar</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>baz</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
        </tr></table>

### SimpleTable {:#SimpleTable}


*Defined in [fidl.examples.bindingstest/conformance.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/fidl_bindings_test/fidl/conformance.test.fidl#16)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>x</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code></code></td>
            <td>
                <code></code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code></code></td>
            <td>
                <code></code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code></code></td>
            <td>
                <code></code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>y</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
        </tr></table>

### TableWithStringAndVector {:#TableWithStringAndVector}


*Defined in [fidl.examples.bindingstest/conformance.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/fidl_bindings_test/fidl/conformance.test.fidl#28)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>foo</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>bar</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>baz</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
        </tr></table>

### XUnionInTable {:#XUnionInTable}


*Defined in [fidl.examples.bindingstest/conformance.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/fidl_bindings_test/fidl/conformance.test.fidl#68)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>before</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>xu</code></td>
            <td>
                <code><a class='link' href='#SampleXUnion'>SampleXUnion</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>after</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr></table>



## **UNIONS**

### TestServer_ReplyWithErrorZero_Result {:#TestServer_ReplyWithErrorZero_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#TestServer_ReplyWithErrorZero_Response'>TestServer_ReplyWithErrorZero_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr></table>

### TestServer_ReplyWithErrorOne_Result {:#TestServer_ReplyWithErrorOne_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#TestServer_ReplyWithErrorOne_Response'>TestServer_ReplyWithErrorOne_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr></table>

### TestServer_ReplyWithErrorMore_Result {:#TestServer_ReplyWithErrorMore_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#TestServer_ReplyWithErrorMore_Response'>TestServer_ReplyWithErrorMore_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr></table>

### TestServer_ReplyWithErrorEnumZero_Result {:#TestServer_ReplyWithErrorEnumZero_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#TestServer_ReplyWithErrorEnumZero_Response'>TestServer_ReplyWithErrorEnumZero_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#EnumOne'>EnumOne</a></code>
            </td>
            <td></td>
        </tr></table>

### TestServer_ReplyWithErrorEnumOne_Result {:#TestServer_ReplyWithErrorEnumOne_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#TestServer_ReplyWithErrorEnumOne_Response'>TestServer_ReplyWithErrorEnumOne_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#EnumOne'>EnumOne</a></code>
            </td>
            <td></td>
        </tr></table>

### TestServer_ReplyWithErrorEnumMore_Result {:#TestServer_ReplyWithErrorEnumMore_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#TestServer_ReplyWithErrorEnumMore_Response'>TestServer_ReplyWithErrorEnumMore_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#EnumOne'>EnumOne</a></code>
            </td>
            <td></td>
        </tr></table>

### UnionOne {:#UnionOne}
*Defined in [fidl.examples.bindingstest/bindings_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/fidl_bindings_test/fidl/bindings_test.test.fidl#106)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>foo</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>bar</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>baz</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr></table>

### UnionTwo {:#UnionTwo}
*Defined in [fidl.examples.bindingstest/bindings_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/fidl_bindings_test/fidl/bindings_test.test.fidl#112)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>foo</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>bar</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>baz</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr></table>

### SimpleUnion {:#SimpleUnion}
*Defined in [fidl.examples.bindingstest/conformance.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/fidl_bindings_test/fidl/conformance.test.fidl#38)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>i32</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>i64</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>s</code></td>
            <td>
                <code><a class='link' href='#Int64Struct'>Int64Struct</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>os</code></td>
            <td>
                <code><a class='link' href='#Int64Struct'>Int64Struct</a>?</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>str</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr></table>



## **XUNIONS**

### ExampleXunion {:#ExampleXunion}
*Defined in [fidl.examples.bindingstest/bindings_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/fidl_bindings_test/fidl/bindings_test.test.fidl#25)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>foo</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>bar</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>baz</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
        </tr></table>

### SampleXUnion {:#SampleXUnion}
*Defined in [fidl.examples.bindingstest/conformance.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/fidl_bindings_test/fidl/conformance.test.fidl#50)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>u</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>su</code></td>
            <td>
                <code><a class='link' href='#SimpleUnion'>SimpleUnion</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>st</code></td>
            <td>
                <code><a class='link' href='#SimpleTable'>SimpleTable</a></code>
            </td>
            <td></td>
        </tr></table>



## **BITS**
### ExampleBits {:#ExampleBits}
Type: <code>uint32</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>MEMBER_A</td>
            <td>2</td>
            <td></td>
        </tr><tr>
            <td>MEMBER_B</td>
            <td>4</td>
            <td></td>
        </tr><tr>
            <td>MEMBER_C</td>
            <td>8</td>
            <td></td>
        </tr></table>



