[TOC]

# fidl.test.unionmigration




## **STRUCTS**

### BasicXUnionStruct {#BasicXUnionStruct}
*Defined in [fidl.test.unionmigration/union_migration.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/union_migration.test.fidl#18)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>val</code></td>
            <td>
                <code><a class='link' href='#BasicXUnion'>BasicXUnion</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### BasicUnionStruct {#BasicUnionStruct}
*Defined in [fidl.test.unionmigration/union_migration.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/union_migration.test.fidl#22)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>val</code></td>
            <td>
                <code><a class='link' href='#BasicUnion'>BasicUnion</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SingleVariantUnionStruct {#SingleVariantUnionStruct}
*Defined in [fidl.test.unionmigration/union_migration.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/union_migration.test.fidl#30)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>u</code></td>
            <td>
                <code><a class='link' href='#SingleVariantUnion'>SingleVariantUnion</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SingleVariantUnionStructWithHeader {#SingleVariantUnionStructWithHeader}
*Defined in [fidl.test.unionmigration/union_migration.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/union_migration.test.fidl#34)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>header</code></td>
            <td>
                <code>uint8[16]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>body</code></td>
            <td>
                <code><a class='link' href='#SingleVariantUnionStruct'>SingleVariantUnionStruct</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>







## **UNIONS**

### BasicUnion {#BasicUnion}
*Defined in [fidl.test.unionmigration/union_migration.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/union_migration.test.fidl#14)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>i32</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### SingleVariantUnion {#SingleVariantUnion}
*Defined in [fidl.test.unionmigration/union_migration.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/union_migration.test.fidl#26)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr></table>



## **XUNIONS**

### BasicXUnion {#BasicXUnion}
*Defined in [fidl.test.unionmigration/union_migration.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/union_migration.test.fidl#10)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>i32</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>





