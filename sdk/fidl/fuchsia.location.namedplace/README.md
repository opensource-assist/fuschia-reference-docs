[TOC]

# fuchsia.location.namedplace

 Protocols and types related to named places. Named places include cities,
 countries, regions, etc. This specifically excludes protocols and types
 related to latitude and longitude.

## **PROTOCOLS**

## RegulatoryRegionConfigurator {#RegulatoryRegionConfigurator}
*Defined in [fuchsia.location.namedplace/namedplace.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.location/namedplace.fidl#20)*

 The RegulatoryRegionConfigurator protocol provides mechanisms to
 inform Location Services of the inputs that should be used to
 determine the regulatory region whose rules should govern the
 operation of radios on the system.

### SetRegion {#SetRegion}

 Sets the region.
 + request `region` the current regulatory region.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>region</code></td>
            <td>
                <code>string[2]</code>
            </td>
        </tr></table>

















