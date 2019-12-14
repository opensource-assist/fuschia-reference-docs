[TOC]

# fidl.examples.test


## **PROTOCOLS**

## Drawing {#Drawing}
*Defined in [fidl.examples.test/test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/test.test.fidl#39)*


### Draw {#Draw}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>p</code></td>
            <td>
                <code><a class='link' href='#Point'>Point</a></code>
            </td>
        </tr><tr>
            <td><code>d</code></td>
            <td>
                <code><a class='link' href='#Direction'>Direction</a></code>
            </td>
        </tr></table>



### DrawLots {#DrawLots}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ps</code></td>
            <td>
                <code><a class='link' href='#Points'>Points</a></code>
            </td>
        </tr></table>



### DrawSucceeded {#DrawSucceeded}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>draws</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



## **STRUCTS**

### Point {#Point}
*Defined in [fidl.examples.test/test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/test.test.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ArraysOfPoints {#ArraysOfPoints}
*Defined in [fidl.examples.test/test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/test.test.fidl#19)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>p</code></td>
            <td>
                <code>[4]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>more_points</code></td>
            <td>
                <code><a class='link' href='#ArraysOfPoints'>ArraysOfPoints</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### VectorOfPoints {#VectorOfPoints}
*Defined in [fidl.examples.test/test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/test.test.fidl#24)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>p</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Point'>Point</a>&gt;[4]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### VectorOfDirections {#VectorOfDirections}
*Defined in [fidl.examples.test/test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/test.test.fidl#28)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>d</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Direction'>Direction</a>&gt;[4]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### Direction {#Direction}
Type: <code>uint32</code>

*Defined in [fidl.examples.test/test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/test.test.fidl#12)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>Up</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>Down</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>Left</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>Right</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>





## **UNIONS**

### Points {#Points}
*Defined in [fidl.examples.test/test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/test.test.fidl#32)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>one_point</code></td>
            <td>
                <code><a class='link' href='#Point'>Point</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>many_points</code></td>
            <td>
                <code><a class='link' href='#ArraysOfPoints'>ArraysOfPoints</a></code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="NumberOfDirections">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/test.test.fidl#37">NumberOfDirections</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    
</table>



