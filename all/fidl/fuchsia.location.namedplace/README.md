[TOC]

# fuchsia.location.namedplace

<p>Protocols and types related to named places. Named places include cities,
countries, regions, etc. This specifically excludes protocols and types
related to latitude and longitude.</p>

## **PROTOCOLS**

## RegulatoryRegionConfigurator {#RegulatoryRegionConfigurator}
*Defined in [fuchsia.location.namedplace/namedplace.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.location/namedplace.fidl#20)*

<p>The RegulatoryRegionConfigurator protocol provides mechanisms to
inform Location Services of the inputs that should be used to
determine the regulatory region whose rules should govern the
operation of radios on the system.</p>

### SetRegion {#SetRegion}

<p>Sets the region.</p>
<p>Clients should take care that their calls to this API arrive in a
well-defined order. For example, when using Zircon channels as the
underlying transport, the code below may not behave as intended.</p>
<pre><code>// DANGER: The service may receive &quot;BB&quot; before &quot;AA&quot;.
service1 = Open(RegulatoryRegionConfigurator);
service1.SetRegion(&quot;AA&quot;);
service1.Close();
service2 = Open(RegulatoryRegionConfigurator);
service2.SetRegion(&quot;BB&quot;);
service2.Close();
</code></pre>
<p>A client can avoid this problem by holding a single channel open to
the service, for the lifetime of the client.</p>
<pre><code>// We use a single channel to ensure that calls arrive in a
// well-defined order.
service = Open(RegulatoryRegionConfigurator);
service1.SetRegion(&quot;AA&quot;);
service2.SetRegion(&quot;BB&quot;);
</code></pre>
<ul>
<li>request <code>region</code> the current regulatory region.</li>
</ul>

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
*Defined in [fuchsia.location.namedplace/namedplace.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.location/namedplace.fidl#56)*

<p>The RegulatoryRegionWatcher protocol provides the mechanism for
radio subsystems to learn the currently applicable regulatory
region, and to be notified when that value changes.</p>

### GetUpdate {#GetUpdate}

<p>Returns the new RegionCode, when it changes.</p>
<p>Notes:</p>
<ul>
<li>The first call returns immediately, if the region is already known.</li>
<li>The client is <em>not</em> guaranteed to observe the effects of every call
to <code>SetRegion()</code>.</li>
<li>The client can, however, achieve <em>eventual</em> consistency by always
issuing a new request when a request completes.</li>
<li>Clients should <em>not</em> issue concurrent requests to this method.
<ul>
<li>At present, concurrent requests
<ul>
<li>May yield the same value, or different values.</li>
<li>May complete out-of-order.</li>
</ul>
</li>
<li>In the future, concurrent requests will cause the channel to be
closed with <code>ZX_ERR_BAD_STATE</code>.</li>
</ul>
</li>
</ul>
<ul>
<li>response <code>new_region</code> the current regulatory region.</li>
</ul>

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















