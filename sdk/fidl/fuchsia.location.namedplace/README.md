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



## RegulatoryRegionWatcher {#RegulatoryRegionWatcher}
*Defined in [fuchsia.location.namedplace/namedplace.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.location/namedplace.fidl#30)*

 The RegulatoryRegionWatcher protocol provides the mechanism for
 radio subsystems to learn the currently applicable regulatory
 region, and to be notified when that value changes.

### GetUpdate {#GetUpdate}

 Returns the new RegionCode, when it changes.

 Notes:
 * The first call returns immediately, if the region is already known.
 * The client is _not_ guaranteed to observe the effects of every call
   to `SetRegion()`.
 * The client can, however, achieve _eventual_ consistency by always
   issuing a new request when a request completes.
 * Clients should _not_ issue concurrent requests to this method.
   * At present, concurrent requests
     * May yield the same value, or different values.
     * May complete out-of-order.
   * In the future, concurrent requests will cause the channel to be
     closed with `ZX_ERR_BAD_STATE`.

 - response `new_region` the current regulatory region.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>new_region</code></td>
            <td>
                <code>string[2]</code>
            </td>
        </tr></table>















