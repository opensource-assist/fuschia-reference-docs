[TOC]

# fuchsia.hwinfo


## **PROTOCOLS**

## Device {#Device}
*Defined in [fuchsia.hwinfo/hwinfo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.hwinfo/hwinfo.fidl#34)*

<p>Device provides an interface to retrieve device-specific properties.</p>

### GetInfo {#GetInfo}


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

## Product {#Product}
*Defined in [fuchsia.hwinfo/hwinfo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.hwinfo/hwinfo.fidl#40)*

<p>Product provides an interface to retrieve product-specific properties.</p>

### GetInfo {#GetInfo}


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

## Board {#Board}
*Defined in [fuchsia.hwinfo/hwinfo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.hwinfo/hwinfo.fidl#46)*

<p>Board provides an interface to retrieve hardware-specific information.</p>

### GetInfo {#GetInfo}


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

### DeviceInfo {#DeviceInfo}


*Defined in [fuchsia.hwinfo/hwinfo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.hwinfo/hwinfo.fidl#9)*

<p>Collection of properties that is unique per device.</p>


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

### ProductInfo {#ProductInfo}


*Defined in [fuchsia.hwinfo/hwinfo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.hwinfo/hwinfo.fidl#15)*

<p>Collection of properties that is shared with other devices within the same
product line.</p>


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
                <code><a class='link' href='../fuchsia.intl/'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/#RegulatoryDomain'>RegulatoryDomain</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>locale_list</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.intl/'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/#LocaleId'>LocaleId</a>&gt;</code>
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

### BoardInfo {#BoardInfo}


*Defined in [fuchsia.hwinfo/hwinfo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.hwinfo/hwinfo.fidl#27)*

<p>Collection of properties that are common among a set of devices based on
hardware type</p>


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











