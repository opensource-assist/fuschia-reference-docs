Project: /_project.yaml
Book: /_book.yaml

# fuchsia.hwinfo


## **PROTOCOLS**

## Device {:#Device}
*Defined in [fuchsia.hwinfo/hwinfo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.hwinfo/hwinfo.fidl#34)*

 Device provides an interface to retrieve device-specific properties.

### GetInfo {:#GetInfo}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#DeviceInfo'>DeviceInfo</a></code>
            </td>
        </tr></table>

## Product {:#Product}
*Defined in [fuchsia.hwinfo/hwinfo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.hwinfo/hwinfo.fidl#40)*

 Product provides an interface to retrieve product-specific properties.

### GetInfo {:#GetInfo}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#ProductInfo'>ProductInfo</a></code>
            </td>
        </tr></table>

## Board {:#Board}
*Defined in [fuchsia.hwinfo/hwinfo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.hwinfo/hwinfo.fidl#46)*

 Board provides an interface to retrieve hardware-specific information.

### GetInfo {:#GetInfo}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#BoardInfo'>BoardInfo</a></code>
            </td>
        </tr></table>







## **TABLES**

### DeviceInfo {:#DeviceInfo}


*Defined in [fuchsia.hwinfo/hwinfo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.hwinfo/hwinfo.fidl#9)*

 Collection of properties that is unique per device.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>serial_number</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr></table>

### ProductInfo {:#ProductInfo}


*Defined in [fuchsia.hwinfo/hwinfo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.hwinfo/hwinfo.fidl#15)*

 Collection of properties that is shared with other devices within the same
 product line.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>sku</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>language</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>regulatory_domain</code></td>
            <td>
                <code><a class='link' href='../fuchsia.intl/index.html'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/index.html#RegulatoryDomain'>RegulatoryDomain</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>locale_list</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.intl/index.html'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/index.html#LocaleId'>LocaleId</a>&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td>6</td>
            <td><code>model</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td>7</td>
            <td><code>manufacturer</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr></table>

### BoardInfo {:#BoardInfo}


*Defined in [fuchsia.hwinfo/hwinfo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.hwinfo/hwinfo.fidl#27)*

 Collection of properties that are common among a set of devices based on
 hardware type


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>revision</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr></table>









