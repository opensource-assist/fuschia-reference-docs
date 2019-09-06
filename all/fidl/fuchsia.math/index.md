Project: /_project.yaml
Book: /_book.yaml

# fuchsia.math




## **STRUCTS**

### Point {:#Point}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#12)*



 An integer position in a 2D cartesian space.

 This type does not specify units. Protocols that use this type should
 specify the characteristics of the vector space, including orientation and
 units.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The number of units along the x-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The number of units along the y-axis.
</td>
            <td>No default</td>
        </tr>
</table>

### PointF {:#PointF}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#25)*



 A floating point position in a 2D cartesian space.

 This type does not specify units. Protocols that use this type should
 specify the characteristics of the vector space, including orientation and
 units.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The number of units along the x-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The number of units along the y-axis.
</td>
            <td>No default</td>
        </tr>
</table>

### Point3F {:#Point3F}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#38)*



 A floating point position in a 3D cartesian space.

 This type does not specify units. Protocols that use this type should
 specify the characteristics of the vector space, including orientation and
 units.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The number of units along the x-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The number of units along the y-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>z</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The number of units along the z-axis.
</td>
            <td>No default</td>
        </tr>
</table>

### Size {:#Size}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#58)*



 The integer dimensions of a rectangular region in a 2D cartesian space.

 This type does not specify units. Protocols that use this type should
 specify the characteristics of the vector space, including orientation and
 units.

 This type allows for negative dimensions, to which protocols can give
 semantics. Protocols that use this type should specify whether negative
 dimensions are meaningful, and, if they are meaningful, what they mean.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>width</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The distance along the x-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The distance along the y-axis.
</td>
            <td>No default</td>
        </tr>
</table>

### SizeF {:#SizeF}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#76)*



 The floating point dimensions of a rectangular region in a 2D cartesian
 space.

 This type does not specify units. Protocols that use this type should
 specify the characteristics of the vector space, including orientation and
 units.

 This type allows for negative dimensions, to which protocols can give
 semantics. Protocols that use this type should specify whether negative
 dimensions are meaningful, and, if they are meaningful, what they mean.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>width</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The distance along the x-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The distance along the y-axis.
</td>
            <td>No default</td>
        </tr>
</table>

### Rect {:#Rect}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#90)*



 An integral, rectangular, axis-aligned region in a 2D cartesian
 space.

 This type does not specify units. Protocols that use this type should
 specify the characteristics of the vector space, including orientation and
 units.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The location of the origin of the rectangle in the x-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The location of the origin of the rectangle in the y-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>width</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The distance along the x-axis.

 If `width` is positive, the region includes x values starting at `x` and
 increasing along the x-axis. If `width` is negative, the region includes
 x values starting at `x` and decreasing along the x-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The distance along the y-axis.

 If `height` is positive, the region includes y values starting at `y`
 and increasing along the y-axis. If `height` is negative, the region
 includes y values starting at `y` and decreasing along the y-axis.
</td>
            <td>No default</td>
        </tr>
</table>

### RectF {:#RectF}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#118)*



 A floating point, rectangular, axis-aligned region in a 2D cartesian
 space.

 This type does not specify units. Protocols that use this type should
 specify the characteristics of the vector space, including orientation and
 units.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The location of the origin of the rectangle in the x-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The location of the origin of the rectangle in the y-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>width</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The distance along the x-axis.

 If `width` is positive, the region includes x values starting at `x` and
 increasing along the x-axis. If `width` is negative, the region includes
 x values starting at `x` and decreasing along the x-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The distance along the y-axis.

 If `height` is positive, the region includes y values starting at `y`
 and increasing along the y-axis. If `height` is negative, the region
 includes y values starting at `y` and decreasing along the y-axis.
</td>
            <td>No default</td>
        </tr>
</table>

### RRectF {:#RRectF}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#152)*



 A floating point rounded rectangle with the custom radii for all four
 corners.

 A region in a 2D cartesian space consisting of linear, axis-aligned sides
 with corners rounded into a quarter ellipse.

 If the quarter ellipses in two corners would overlap, their radii are
 clamped such that the ellipses meet with an axis-aligned tangent.

 This type does not specify units. Protocols that use this type should
 specify the characteristics of the vector space, including orientation and
 units.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The location of the origin of the region in the x-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The location of the origin of the region in the y-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>width</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The distance along the x-axis.

 If `width` is positive, the region includes x values starting at `x` and
 increasing along the x-axis. If `width` is negative, the region includes
 x values starting at `x` and decreasing along the x-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The distance along the y-axis.

 If `height` is positive, the region includes y values starting at `y`
 and increasing along the y-axis. If `height` is negative, the region
 includes y values starting at `y` and decreasing along the y-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>top_left_radius_x</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The radius of the quarter ellipse in the top-left corner along the
 x-axis.

 Must not be negative.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>top_left_radius_y</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The radius of the quarter ellipse in the top-left corner along the
 y-axis.

 Must not be negative.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>top_right_radius_x</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The radius of the quarter ellipse in the top-right corner along the
 x-axis.

 Must not be negative.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>top_right_radius_y</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The radius of the quarter ellipse in the top-right corner along the
 y-axis.

 Must not be negative.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>bottom_left_radius_x</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The radius of the quarter ellipse in the bottom-left corner along the
 x-axis.

 Must not be negative.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>bottom_left_radius_y</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The radius of the quarter ellipse in the bottom-left corner along the
 y-axis.

 Must not be negative.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>bottom_right_radius_x</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The radius of the quarter ellipse in the bottom-right corner along the
 x-axis.

 Must not be negative.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>bottom_right_radius_y</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The radius of the quarter ellipse in the bottom-right corner along the
 y-axis.

 Must not be negative.
</td>
            <td>No default</td>
        </tr>
</table>

### Transform {:#Transform}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#228)*



 A projective transformation of a 3D cartesian space.

 A transform consists of a 4x4 matrix that operates in homogeneous
 coordinates. For example, a point located at (x, y, z) in the cartesian
 space is transformed by `M` to a point located at (x'/w', y'/w', z'/w'),
 where `(x', y', z', w') = M (x, y, z, 1)`.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>matrix</code></td>
            <td>
                <code>float32[16]</code>
            </td>
            <td> The entries in the transformation matrix in row major order.

 Specifically, if the matrix is as follows:

 ```
 a b c d
 e f g h
 i j k l
 m n o p
 ```

 then the entries in this array are
 `(a, b, c, d, e, f, g, h, i, j, k, l, m, n, o, p)`.
</td>
            <td>No default</td>
        </tr>
</table>

### Inset {:#Inset}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#250)*



 An integer offset to apply to each edge of a rectangle.

 This type does not specify units. Protocols that use this type should
 specify the characteristics of the vector space, including orientation and
 units.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>top</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The amount to move the top edge of the rectangle towards the center of
 the rectangle.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>right</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The amount to move the right edge of the rectangle towards the center of
 the rectangle.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>bottom</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The amount to move the bottom edge of the rectangle towards the center
 of the rectangle.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>left</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The amount to move the left edge of the rectangle towards the center of
 the rectangle.
</td>
            <td>No default</td>
        </tr>
</table>

### InsetF {:#InsetF}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#273)*



 A floating point offset to apply to each edge of a rectangle.

 This type does not specify units. Protocols that use this type should
 specify the characteristics of the vector space, including orientation and
 units.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>top</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The amount to move the top edge of the rectangle towards the center of
 the rectangle.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>right</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The amount to move the right edge of the rectangle towards the center of
 the rectangle.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>bottom</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The amount to move the bottom edge of the rectangle towards the center
 of the rectangle.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>left</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The amount to move the left edge of the rectangle towards the center of
 the rectangle.
</td>
            <td>No default</td>
        </tr>
</table>

### Point {:#Point}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#12)*



 An integer position in a 2D cartesian space.

 This type does not specify units. Protocols that use this type should
 specify the characteristics of the vector space, including orientation and
 units.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The number of units along the x-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The number of units along the y-axis.
</td>
            <td>No default</td>
        </tr>
</table>

### PointF {:#PointF}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#25)*



 A floating point position in a 2D cartesian space.

 This type does not specify units. Protocols that use this type should
 specify the characteristics of the vector space, including orientation and
 units.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The number of units along the x-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The number of units along the y-axis.
</td>
            <td>No default</td>
        </tr>
</table>

### Point3F {:#Point3F}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#38)*



 A floating point position in a 3D cartesian space.

 This type does not specify units. Protocols that use this type should
 specify the characteristics of the vector space, including orientation and
 units.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The number of units along the x-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The number of units along the y-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>z</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The number of units along the z-axis.
</td>
            <td>No default</td>
        </tr>
</table>

### Size {:#Size}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#58)*



 The integer dimensions of a rectangular region in a 2D cartesian space.

 This type does not specify units. Protocols that use this type should
 specify the characteristics of the vector space, including orientation and
 units.

 This type allows for negative dimensions, to which protocols can give
 semantics. Protocols that use this type should specify whether negative
 dimensions are meaningful, and, if they are meaningful, what they mean.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>width</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The distance along the x-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The distance along the y-axis.
</td>
            <td>No default</td>
        </tr>
</table>

### SizeF {:#SizeF}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#76)*



 The floating point dimensions of a rectangular region in a 2D cartesian
 space.

 This type does not specify units. Protocols that use this type should
 specify the characteristics of the vector space, including orientation and
 units.

 This type allows for negative dimensions, to which protocols can give
 semantics. Protocols that use this type should specify whether negative
 dimensions are meaningful, and, if they are meaningful, what they mean.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>width</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The distance along the x-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The distance along the y-axis.
</td>
            <td>No default</td>
        </tr>
</table>

### Rect {:#Rect}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#90)*



 An integral, rectangular, axis-aligned region in a 2D cartesian
 space.

 This type does not specify units. Protocols that use this type should
 specify the characteristics of the vector space, including orientation and
 units.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The location of the origin of the rectangle in the x-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The location of the origin of the rectangle in the y-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>width</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The distance along the x-axis.

 If `width` is positive, the region includes x values starting at `x` and
 increasing along the x-axis. If `width` is negative, the region includes
 x values starting at `x` and decreasing along the x-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The distance along the y-axis.

 If `height` is positive, the region includes y values starting at `y`
 and increasing along the y-axis. If `height` is negative, the region
 includes y values starting at `y` and decreasing along the y-axis.
</td>
            <td>No default</td>
        </tr>
</table>

### RectF {:#RectF}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#118)*



 A floating point, rectangular, axis-aligned region in a 2D cartesian
 space.

 This type does not specify units. Protocols that use this type should
 specify the characteristics of the vector space, including orientation and
 units.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The location of the origin of the rectangle in the x-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The location of the origin of the rectangle in the y-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>width</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The distance along the x-axis.

 If `width` is positive, the region includes x values starting at `x` and
 increasing along the x-axis. If `width` is negative, the region includes
 x values starting at `x` and decreasing along the x-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The distance along the y-axis.

 If `height` is positive, the region includes y values starting at `y`
 and increasing along the y-axis. If `height` is negative, the region
 includes y values starting at `y` and decreasing along the y-axis.
</td>
            <td>No default</td>
        </tr>
</table>

### RRectF {:#RRectF}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#152)*



 A floating point rounded rectangle with the custom radii for all four
 corners.

 A region in a 2D cartesian space consisting of linear, axis-aligned sides
 with corners rounded into a quarter ellipse.

 If the quarter ellipses in two corners would overlap, their radii are
 clamped such that the ellipses meet with an axis-aligned tangent.

 This type does not specify units. Protocols that use this type should
 specify the characteristics of the vector space, including orientation and
 units.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The location of the origin of the region in the x-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The location of the origin of the region in the y-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>width</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The distance along the x-axis.

 If `width` is positive, the region includes x values starting at `x` and
 increasing along the x-axis. If `width` is negative, the region includes
 x values starting at `x` and decreasing along the x-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The distance along the y-axis.

 If `height` is positive, the region includes y values starting at `y`
 and increasing along the y-axis. If `height` is negative, the region
 includes y values starting at `y` and decreasing along the y-axis.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>top_left_radius_x</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The radius of the quarter ellipse in the top-left corner along the
 x-axis.

 Must not be negative.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>top_left_radius_y</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The radius of the quarter ellipse in the top-left corner along the
 y-axis.

 Must not be negative.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>top_right_radius_x</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The radius of the quarter ellipse in the top-right corner along the
 x-axis.

 Must not be negative.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>top_right_radius_y</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The radius of the quarter ellipse in the top-right corner along the
 y-axis.

 Must not be negative.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>bottom_left_radius_x</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The radius of the quarter ellipse in the bottom-left corner along the
 x-axis.

 Must not be negative.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>bottom_left_radius_y</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The radius of the quarter ellipse in the bottom-left corner along the
 y-axis.

 Must not be negative.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>bottom_right_radius_x</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The radius of the quarter ellipse in the bottom-right corner along the
 x-axis.

 Must not be negative.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>bottom_right_radius_y</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The radius of the quarter ellipse in the bottom-right corner along the
 y-axis.

 Must not be negative.
</td>
            <td>No default</td>
        </tr>
</table>

### Transform {:#Transform}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#228)*



 A projective transformation of a 3D cartesian space.

 A transform consists of a 4x4 matrix that operates in homogeneous
 coordinates. For example, a point located at (x, y, z) in the cartesian
 space is transformed by `M` to a point located at (x'/w', y'/w', z'/w'),
 where `(x', y', z', w') = M (x, y, z, 1)`.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>matrix</code></td>
            <td>
                <code>float32[16]</code>
            </td>
            <td> The entries in the transformation matrix in row major order.

 Specifically, if the matrix is as follows:

 ```
 a b c d
 e f g h
 i j k l
 m n o p
 ```

 then the entries in this array are
 `(a, b, c, d, e, f, g, h, i, j, k, l, m, n, o, p)`.
</td>
            <td>No default</td>
        </tr>
</table>

### Inset {:#Inset}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#250)*



 An integer offset to apply to each edge of a rectangle.

 This type does not specify units. Protocols that use this type should
 specify the characteristics of the vector space, including orientation and
 units.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>top</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The amount to move the top edge of the rectangle towards the center of
 the rectangle.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>right</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The amount to move the right edge of the rectangle towards the center of
 the rectangle.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>bottom</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The amount to move the bottom edge of the rectangle towards the center
 of the rectangle.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>left</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The amount to move the left edge of the rectangle towards the center of
 the rectangle.
</td>
            <td>No default</td>
        </tr>
</table>

### InsetF {:#InsetF}
*Defined in [fuchsia.math/math.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.math/math.fidl#273)*



 A floating point offset to apply to each edge of a rectangle.

 This type does not specify units. Protocols that use this type should
 specify the characteristics of the vector space, including orientation and
 units.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>top</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The amount to move the top edge of the rectangle towards the center of
 the rectangle.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>right</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The amount to move the right edge of the rectangle towards the center of
 the rectangle.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>bottom</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The amount to move the bottom edge of the rectangle towards the center
 of the rectangle.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>left</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The amount to move the left edge of the rectangle towards the center of
 the rectangle.
</td>
            <td>No default</td>
        </tr>
</table>













