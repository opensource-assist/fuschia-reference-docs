[TOC]

# fuchsia.math




## **STRUCTS**

### Point {#Point}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#12)*



<p>An integer position in a 2D cartesian space.</p>
<p>This type does not specify units. Protocols that use this type should
specify the characteristics of the vector space, including orientation and
units.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code>int32</code>
            </td>
            <td><p>The number of units along the x-axis.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>int32</code>
            </td>
            <td><p>The number of units along the y-axis.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### PointF {#PointF}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#25)*



<p>A floating point position in a 2D cartesian space.</p>
<p>This type does not specify units. Protocols that use this type should
specify the characteristics of the vector space, including orientation and
units.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The number of units along the x-axis.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The number of units along the y-axis.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### Point3F {#Point3F}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#38)*



<p>A floating point position in a 3D cartesian space.</p>
<p>This type does not specify units. Protocols that use this type should
specify the characteristics of the vector space, including orientation and
units.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The number of units along the x-axis.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The number of units along the y-axis.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>z</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The number of units along the z-axis.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### Size {#Size}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#58)*



<p>The integer dimensions of a rectangular region in a 2D cartesian space.</p>
<p>This type does not specify units. Protocols that use this type should
specify the characteristics of the vector space, including orientation and
units.</p>
<p>This type allows for negative dimensions, to which protocols can give
semantics. Protocols that use this type should specify whether negative
dimensions are meaningful, and, if they are meaningful, what they mean.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>width</code></td>
            <td>
                <code>int32</code>
            </td>
            <td><p>The distance along the x-axis.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code>int32</code>
            </td>
            <td><p>The distance along the y-axis.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### SizeF {#SizeF}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#76)*



<p>The floating point dimensions of a rectangular region in a 2D cartesian
space.</p>
<p>This type does not specify units. Protocols that use this type should
specify the characteristics of the vector space, including orientation and
units.</p>
<p>This type allows for negative dimensions, to which protocols can give
semantics. Protocols that use this type should specify whether negative
dimensions are meaningful, and, if they are meaningful, what they mean.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>width</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The distance along the x-axis.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The distance along the y-axis.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### Rect {#Rect}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#90)*



<p>An integral, rectangular, axis-aligned region in a 2D cartesian
space.</p>
<p>This type does not specify units. Protocols that use this type should
specify the characteristics of the vector space, including orientation and
units.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code>int32</code>
            </td>
            <td><p>The location of the origin of the rectangle in the x-axis.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>int32</code>
            </td>
            <td><p>The location of the origin of the rectangle in the y-axis.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>width</code></td>
            <td>
                <code>int32</code>
            </td>
            <td><p>The distance along the x-axis.</p>
<p>If <code>width</code> is positive, the region includes x values starting at <code>x</code> and
increasing along the x-axis. If <code>width</code> is negative, the region includes
x values starting at <code>x</code> and decreasing along the x-axis.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code>int32</code>
            </td>
            <td><p>The distance along the y-axis.</p>
<p>If <code>height</code> is positive, the region includes y values starting at <code>y</code>
and increasing along the y-axis. If <code>height</code> is negative, the region
includes y values starting at <code>y</code> and decreasing along the y-axis.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### RectF {#RectF}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#118)*



<p>A floating point, rectangular, axis-aligned region in a 2D cartesian
space.</p>
<p>This type does not specify units. Protocols that use this type should
specify the characteristics of the vector space, including orientation and
units.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The location of the origin of the rectangle in the x-axis.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The location of the origin of the rectangle in the y-axis.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>width</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The distance along the x-axis.</p>
<p>If <code>width</code> is positive, the region includes x values starting at <code>x</code> and
increasing along the x-axis. If <code>width</code> is negative, the region includes
x values starting at <code>x</code> and decreasing along the x-axis.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The distance along the y-axis.</p>
<p>If <code>height</code> is positive, the region includes y values starting at <code>y</code>
and increasing along the y-axis. If <code>height</code> is negative, the region
includes y values starting at <code>y</code> and decreasing along the y-axis.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### RRectF {#RRectF}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#152)*



<p>A floating point rounded rectangle with the custom radii for all four
corners.</p>
<p>A region in a 2D cartesian space consisting of linear, axis-aligned sides
with corners rounded into a quarter ellipse.</p>
<p>If the quarter ellipses in two corners would overlap, their radii are
clamped such that the ellipses meet with an axis-aligned tangent.</p>
<p>This type does not specify units. Protocols that use this type should
specify the characteristics of the vector space, including orientation and
units.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The location of the origin of the region in the x-axis.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The location of the origin of the region in the y-axis.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>width</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The distance along the x-axis.</p>
<p>If <code>width</code> is positive, the region includes x values starting at <code>x</code> and
increasing along the x-axis. If <code>width</code> is negative, the region includes
x values starting at <code>x</code> and decreasing along the x-axis.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The distance along the y-axis.</p>
<p>If <code>height</code> is positive, the region includes y values starting at <code>y</code>
and increasing along the y-axis. If <code>height</code> is negative, the region
includes y values starting at <code>y</code> and decreasing along the y-axis.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>top_left_radius_x</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The radius of the quarter ellipse in the top-left corner along the
x-axis.</p>
<p>Must not be negative.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>top_left_radius_y</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The radius of the quarter ellipse in the top-left corner along the
y-axis.</p>
<p>Must not be negative.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>top_right_radius_x</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The radius of the quarter ellipse in the top-right corner along the
x-axis.</p>
<p>Must not be negative.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>top_right_radius_y</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The radius of the quarter ellipse in the top-right corner along the
y-axis.</p>
<p>Must not be negative.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>bottom_left_radius_x</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The radius of the quarter ellipse in the bottom-left corner along the
x-axis.</p>
<p>Must not be negative.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>bottom_left_radius_y</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The radius of the quarter ellipse in the bottom-left corner along the
y-axis.</p>
<p>Must not be negative.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>bottom_right_radius_x</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The radius of the quarter ellipse in the bottom-right corner along the
x-axis.</p>
<p>Must not be negative.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>bottom_right_radius_y</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The radius of the quarter ellipse in the bottom-right corner along the
y-axis.</p>
<p>Must not be negative.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### Transform {#Transform}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#228)*



<p>A projective transformation of a 3D cartesian space.</p>
<p>A transform consists of a 4x4 matrix that operates in homogeneous
coordinates. For example, a point located at (x, y, z) in the cartesian
space is transformed by <code>M</code> to a point located at (x'/w', y'/w', z'/w'),
where <code>(x', y', z', w') = M (x, y, z, 1)</code>.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>matrix</code></td>
            <td>
                <code>float32[16]</code>
            </td>
            <td><p>The entries in the transformation matrix in row major order.</p>
<p>Specifically, if the matrix is as follows:</p>
<pre><code>a b c d
e f g h
i j k l
m n o p
</code></pre>
<p>then the entries in this array are
<code>(a, b, c, d, e, f, g, h, i, j, k, l, m, n, o, p)</code>.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### Inset {#Inset}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#250)*



<p>An integer offset to apply to each edge of a rectangle.</p>
<p>This type does not specify units. Protocols that use this type should
specify the characteristics of the vector space, including orientation and
units.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>top</code></td>
            <td>
                <code>int32</code>
            </td>
            <td><p>The amount to move the top edge of the rectangle towards the center of
the rectangle.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>right</code></td>
            <td>
                <code>int32</code>
            </td>
            <td><p>The amount to move the right edge of the rectangle towards the center of
the rectangle.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>bottom</code></td>
            <td>
                <code>int32</code>
            </td>
            <td><p>The amount to move the bottom edge of the rectangle towards the center
of the rectangle.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>left</code></td>
            <td>
                <code>int32</code>
            </td>
            <td><p>The amount to move the left edge of the rectangle towards the center of
the rectangle.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### InsetF {#InsetF}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#273)*



<p>A floating point offset to apply to each edge of a rectangle.</p>
<p>This type does not specify units. Protocols that use this type should
specify the characteristics of the vector space, including orientation and
units.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>top</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The amount to move the top edge of the rectangle towards the center of
the rectangle.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>right</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The amount to move the right edge of the rectangle towards the center of
the rectangle.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>bottom</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The amount to move the bottom edge of the rectangle towards the center
of the rectangle.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>left</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The amount to move the left edge of the rectangle towards the center of
the rectangle.</p>
</td>
            <td>No default</td>
        </tr>
</table>













