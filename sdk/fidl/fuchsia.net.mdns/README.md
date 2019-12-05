[TOC]

# fuchsia.net.mdns


## **PROTOCOLS**

## Resolver {#Resolver}
*Defined in [fuchsia.net.mdns/mdns.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.mdns/mdns.fidl#43)*

<p>Discoverable protocol for resolving host names to IP addresses.</p>

### ResolveHostName {#ResolveHostName}

<p>Gets the addresses for the specified host. <code>timeout</code> specifies how long
the service should wait before giving up when waiting for a response to
a resolution query. In typical use, a timeout of two or three seconds
is recommended.</p>
<p>A successful resolution may return one or both addresses. An
unsuccessful resolution is indicated when both addresses are null.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>host</code></td>
            <td>
                <code>string[255]</code>
            </td>
        </tr><tr>
            <td><code>timeout</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>v4_address</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Ipv4Address'>Ipv4Address</a>?</code>
            </td>
        </tr><tr>
            <td><code>v6_address</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Ipv6Address'>Ipv6Address</a>?</code>
            </td>
        </tr></table>

## Subscriber {#Subscriber}
*Defined in [fuchsia.net.mdns/mdns.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.mdns/mdns.fidl#58)*

<p>Discoverable protocol for finding service instances.</p>

### SubscribeToService {#SubscribeToService}

<p>Subscribes to a service. The subscription lasts until <code>subscriber</code> is
unbound.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service</code></td>
            <td>
                <code>string[22]</code>
            </td>
        </tr><tr>
            <td><code>subscriber</code></td>
            <td>
                <code><a class='link' href='#ServiceSubscriber'>ServiceSubscriber</a></code>
            </td>
        </tr></table>



## Publisher {#Publisher}
*Defined in [fuchsia.net.mdns/mdns.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.mdns/mdns.fidl#66)*

<p>Discoverable protocol for publishing service instances.</p>

### PublishServiceInstance {#PublishServiceInstance}

<p>Publishes a service instance. <code>publication_responder</code> is consulted via its
<code>OnPublication</code> method for initial announcements and to answer queries.
The service is published until the <code>publication_responder</code> channel closes. In
addition to announcements and queries for the service type, all queries
for subtypes are answered subject to filtering through the responder.
<code>perform_probe</code> indicates whether a probe for a conflicting instance
should be performed before publishing the instance. This value should
be <code>true</code> unless the instance name is known to be unique.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service</code></td>
            <td>
                <code>string[22]</code>
            </td>
        </tr><tr>
            <td><code>instance</code></td>
            <td>
                <code>string[63]</code>
            </td>
        </tr><tr>
            <td><code>perform_probe</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>publication_responder</code></td>
            <td>
                <code><a class='link' href='#PublicationResponder'>PublicationResponder</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Publisher_PublishServiceInstance_Result'>Publisher_PublishServiceInstance_Result</a></code>
            </td>
        </tr></table>

## ServiceSubscriber {#ServiceSubscriber}
*Defined in [fuchsia.net.mdns/mdns.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.mdns/mdns.fidl#102)*

<p>Client-implemented interface for subscribers. Method replies are used to
throttle traffic. The service won't necessarily wait for a reply before
calling another method.</p>

### OnInstanceDiscovered {#OnInstanceDiscovered}

<p>Notifies the subscriber that a service instance has been discovered.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>instance</code></td>
            <td>
                <code><a class='link' href='#ServiceInstance'>ServiceInstance</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### OnInstanceChanged {#OnInstanceChanged}

<p>Notifies the subscriber that addresses or text for a known service
instance have changed.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>instance</code></td>
            <td>
                <code><a class='link' href='#ServiceInstance'>ServiceInstance</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### OnInstanceLost {#OnInstanceLost}

<p>Notifies the subscriber that a known service instance has been lost.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service</code></td>
            <td>
                <code>string[22]</code>
            </td>
        </tr><tr>
            <td><code>instance</code></td>
            <td>
                <code>string[63]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## PublicationResponder {#PublicationResponder}
*Defined in [fuchsia.net.mdns/mdns.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.mdns/mdns.fidl#139)*

<p>Client-supplied publication responder interface.</p>

### OnPublication {#OnPublication}

<p>Provides instance information for initial announcements and query
responses relating to the service instance specified in
<code>Publisher.PublishServiceInstance</code>. <code>query</code> indicates whether data is
requested for an initial announcement (false) or in response to a query
(true). If the publication relates to a subtype of the service,
<code>subtype</code> contains the subtype, otherwise it is null. If <code>publication</code>
is null, no announcement or response is transmitted. Strings in <code>text</code>
are transmitted in the TXT record.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>query</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>subtype</code></td>
            <td>
                <code>string[63]?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>publication</code></td>
            <td>
                <code><a class='link' href='#Publication'>Publication</a>?</code>
            </td>
        </tr></table>

### SetSubtypes {#SetSubtypes}

<p>Sets the subtypes for the service instance. The specified subtypes will
be announced subject to filtering through the responder. The initial
subtype collection is empty.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>subtypes</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr></table>

### Reannounce {#Reannounce}

<p>Initiates reannouncement of the service instance due to a change in the
instance's port number or text strings. All announcements are filtered
through <code>OnPublication</code>, which replies with the new port and text
values.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## **STRUCTS**

### Publisher_PublishServiceInstance_Response {#Publisher_PublishServiceInstance_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### ServiceInstance {#ServiceInstance}
*Defined in [fuchsia.net.mdns/mdns.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.mdns/mdns.fidl#115)*



<p>Describes a service instance.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>service</code></td>
            <td>
                <code>string[22]</code>
            </td>
            <td><p>The name of the service.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>instance</code></td>
            <td>
                <code>string[63]</code>
            </td>
            <td><p>The name of the service instance.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>endpoints</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Endpoint'>Endpoint</a>&gt;[2]</code>
            </td>
            <td><p>Endpoints for the service. If two endpoints are supplied, one will be a
V4 and the other will be a V6.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>text</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td><p>Text strings describing the instance.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>srv_priority</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>The priority of the SRV resource record for this publication. See
<a href="https://tools.ietf.org/html/rfc6763">RFC6763</a> for details.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>srv_weight</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>The weight of the SRV resource record for this publication. See
<a href="https://tools.ietf.org/html/rfc6763">RFC6763</a> for details.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### Publication {#Publication}
*Defined in [fuchsia.net.mdns/mdns.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.mdns/mdns.fidl#168)*



<p>Describes an initial instance announcement or query response. In typical
use, the default SRV priority, SRV weight and TTL values should be used. TTL
values are rounded down to the nearest second. TTL values less than one
second are not permitted and will result in the <code>PublicationResponder</code>
channel being closed.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>port</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>The port at which the service instance is addressable.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>text</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td><p>Text strings describing the instance.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>srv_priority</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>The priority of the SRV resource record for this publication. See
<a href="https://tools.ietf.org/html/rfc6763">RFC6763</a> for details.</p>
</td>
            <td><a class='link' href='#DEFAULT_SRV_PRIORITY'>DEFAULT_SRV_PRIORITY</a></td>
        </tr><tr>
            <td><code>srv_weight</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>The weight of the SRV resource record for this publication. See
<a href="https://tools.ietf.org/html/rfc6763">RFC6763</a> for details.</p>
</td>
            <td><a class='link' href='#DEFAULT_SRV_WEIGHT'>DEFAULT_SRV_WEIGHT</a></td>
        </tr><tr>
            <td><code>ptr_ttl</code></td>
            <td>
                <code>int64</code>
            </td>
            <td><p>Time-to-live for PTR resource records.</p>
</td>
            <td><a class='link' href='#DEFAULT_PTR_TTL'>DEFAULT_PTR_TTL</a></td>
        </tr><tr>
            <td><code>srv_ttl</code></td>
            <td>
                <code>int64</code>
            </td>
            <td><p>Time-to-live for SRV resource records.</p>
</td>
            <td><a class='link' href='#DEFAULT_SRV_TTL'>DEFAULT_SRV_TTL</a></td>
        </tr><tr>
            <td><code>txt_ttl</code></td>
            <td>
                <code>int64</code>
            </td>
            <td><p>Time-to-live for TXT resource records.</p>
</td>
            <td><a class='link' href='#DEFAULT_TXT_TTL'>DEFAULT_TXT_TTL</a></td>
        </tr>
</table>



## **ENUMS**

### Error {#Error}
Type: <code>int32</code>

*Defined in [fuchsia.net.mdns/mdns.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.mdns/mdns.fidl#82)*

<p>Error values for instance publishing.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INVALID_SERVICE_NAME</code></td>
            <td><code>1</code></td>
            <td><p>The specified service name is invalid.</p>
</td>
        </tr><tr>
            <td><code>INVALID_INSTANCE_NAME</code></td>
            <td><code>2</code></td>
            <td><p>The specified instance name is invalid.</p>
</td>
        </tr><tr>
            <td><code>ALREADY_PUBLISHED_LOCALLY</code></td>
            <td><code>3</code></td>
            <td><p>The specified service instance is already being published by this
mDNS implementation.</p>
</td>
        </tr><tr>
            <td><code>ALREADY_PUBLISHED_ON_SUBNET</code></td>
            <td><code>4</code></td>
            <td><p>The specified service instance is already being published by another
host on the subnet. This result occurs when an initial probe discovers
a conflicting instance.</p>
</td>
        </tr></table>





## **UNIONS**

### Publisher_PublishServiceInstance_Result {#Publisher_PublishServiceInstance_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Publisher_PublishServiceInstance_Response'>Publisher_PublishServiceInstance_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.mdns/mdns.fidl#193">DEFAULT_SRV_PRIORITY</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.mdns/mdns.fidl#194">DEFAULT_SRV_WEIGHT</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.mdns/mdns.fidl#195">DEFAULT_PTR_TTL</a></td>
            <td>
                    <code>4500000000000</code>
                </td>
                <td><code>int64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.mdns/mdns.fidl#196">DEFAULT_SRV_TTL</a></td>
            <td>
                    <code>120000000000</code>
                </td>
                <td><code>int64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.mdns/mdns.fidl#197">DEFAULT_TXT_TTL</a></td>
            <td>
                    <code>4500000000000</code>
                </td>
                <td><code>int64</code></td>
            <td></td>
        </tr>
    
</table>



## **TYPE ALIASES**

<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.mdns/mdns.fidl#16">host_name</a></td>
            <td>
                <code>string</code></td>
            <td></td>
        </tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.mdns/mdns.fidl#24">service_name</a></td>
            <td>
                <code>string</code></td>
            <td></td>
        </tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.mdns/mdns.fidl#29">instance_name</a></td>
            <td>
                <code>string</code></td>
            <td></td>
        </tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.mdns/mdns.fidl#34">subtype_name</a></td>
            <td>
                <code>string</code></td>
            <td></td>
        </tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.mdns/mdns.fidl#39">txt_string</a></td>
            <td>
                <code>string</code></td>
            <td></td>
        </tr></table>

