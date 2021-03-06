[TOC]

# fuchsia.net.dhcp


## **PROTOCOLS**

## Client {#Client}
*Defined in [fuchsia.net.dhcp/client.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.dhcp/client.fidl#10)*

<p>Client provides control operations on a DHCP client.</p>

### Start {#Start}

<p>Start runs the DHCP client represented by this protocol.</p>
<h1>Errors</h1>
<p>In the case that the interface this client represents no longer exists,
the server end of this protocol's channel will be closed.</p>
<p>Start returns no other errors currently, but callers should check the error
value in case new errors are returned in the future.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Client_Start_Result'>Client_Start_Result</a></code>
            </td>
        </tr></table>

### Stop {#Stop}

<p>Stops the DHCP client (if it is running).</p>
<h1>Errors</h1>
<p>In the case that the interface this client represents no longer exists,
the server end of this protocol's channel will be closed.</p>
<p>Stop returns no other errors currently, but callers should check the error
value in case new errors are returned in the future.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Client_Stop_Result'>Client_Stop_Result</a></code>
            </td>
        </tr></table>

## Server {#Server}
*Defined in [fuchsia.net.dhcp/server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.dhcp/server.fidl#85)*

<p>Provides methods for DHCP Server configuration.</p>

### GetOption {#GetOption}

<p>Returns the requested Option if it is supported.</p>
<ul>
<li>request <code>code</code> the code of an Option whose value has been requested.</li>
</ul>
<ul>
<li>response <code>value</code> the value of the requested Option.</li>
</ul>
<ul>
<li>error a zx.status indicating why the value could not be retrieved.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>code</code></td>
            <td>
                <code><a class='link' href='#OptionCode'>OptionCode</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Server_GetOption_Result'>Server_GetOption_Result</a></code>
            </td>
        </tr></table>

### GetParameter {#GetParameter}

<p>Returns the requested Parameter if it is supported.</p>
<ul>
<li>request <code>name</code> the name of a Parameter whose value has been requested.</li>
</ul>
<ul>
<li>response <code>value</code> the value of the requested Parameter.</li>
</ul>
<ul>
<li>error a zx.status indicating why the value could not be retrieved.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code><a class='link' href='#ParameterName'>ParameterName</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Server_GetParameter_Result'>Server_GetParameter_Result</a></code>
            </td>
        </tr></table>

### SetOption {#SetOption}

<p>Sets the Option to the argument. Each SetOption call is treated as its own atomic
transaction. On success, a SetOption will take effect immediately.</p>
<ul>
<li>request <code>value</code> an Option whose value will be set to the value of this argument.</li>
</ul>
<ul>
<li>error a zx.status indicating the cause of failure.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#Option'>Option</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Server_SetOption_Result'>Server_SetOption_Result</a></code>
            </td>
        </tr></table>

### SetParameter {#SetParameter}

<p>Sets the Parameter to the argument. Each SetParameter call is treated as its own atomic
transaction. On success, a SetParameter will take effect immediately.</p>
<ul>
<li>request <code>value</code> a Parameter whose value will be set to the value of this argument.</li>
</ul>
<ul>
<li>error a zx.status indicating the cause of failure.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#Parameter'>Parameter</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Server_SetParameter_Result'>Server_SetParameter_Result</a></code>
            </td>
        </tr></table>

### ListOptions {#ListOptions}

<p>Lists all DHCP options for which the Server has a value. Any option which does
not have a value will be omitted from the returned list. ListOptions provides administrators
a means to print a server's configuration as opposed to querying the value of a single
Option.</p>
<ul>
<li>response <code>options</code> a vector containing all of the options for which the Server has a
value. Bounded to 256 as options are identified by a 1 octet code and 256 is the maximum
number of such codes.</li>
</ul>
<ul>
<li>error a zx.status indicating the cause of failure.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Server_ListOptions_Result'>Server_ListOptions_Result</a></code>
            </td>
        </tr></table>

### ListParameters {#ListParameters}

<p>Lists all DHCP server parameters. ListParameters provides administrators a means to print a
server's configuration as opposed to querying the value of a single Parameter.</p>
<ul>
<li>response <code>parameter</code> a vector containing the values of all of the Server's parameters.
Bounded to 256 to provide a generous upper limit on the number of server parameters while
being of the same size as ListOptions.</li>
</ul>
<ul>
<li>error a zx.status indicating the cause of failure.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Server_ListParameters_Result'>Server_ListParameters_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Client_Start_Response {#Client_Start_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Client_Stop_Response {#Client_Stop_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Server_GetOption_Response {#Server_GetOption_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#Option'>Option</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Server_GetParameter_Response {#Server_GetParameter_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#Parameter'>Parameter</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Server_SetOption_Response {#Server_SetOption_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Server_SetParameter_Response {#Server_SetParameter_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Server_ListOptions_Response {#Server_ListOptions_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>options</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Option'>Option</a>&gt;[256]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Server_ListParameters_Response {#Server_ListParameters_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>parameters</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Parameter'>Parameter</a>&gt;[256]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### OptionOverloadValue {#OptionOverloadValue}
Type: <code>uint8</code>

*Defined in [fuchsia.net.dhcp/options.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.dhcp/options.fidl#27)*

<p>A indication of which DHCP message field should be used to store additional options.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>FILE</code></td>
            <td><code>1</code></td>
            <td><p>The file DHCP field.</p>
</td>
        </tr><tr>
            <td><code>SNAME</code></td>
            <td><code>2</code></td>
            <td><p>The sname DHCP field.</p>
</td>
        </tr><tr>
            <td><code>BOTH</code></td>
            <td><code>3</code></td>
            <td><p>Both file and sname DHCP fields.</p>
</td>
        </tr></table>

### MessageType {#MessageType}
Type: <code>uint8</code>

*Defined in [fuchsia.net.dhcp/options.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.dhcp/options.fidl#52)*

<p>The type of DHCP message. The DHCP protocol requires that all messages identify
their type by including the MessageType option. These values are specified
in https://tools.ietf.org/html/rfc2132#section-9.6.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DHCPDISCOVER</code></td>
            <td><code>1</code></td>
            <td><p>A DHCP Discover message.</p>
</td>
        </tr><tr>
            <td><code>DHCPOFFER</code></td>
            <td><code>2</code></td>
            <td><p>A DHCP Offer message.</p>
</td>
        </tr><tr>
            <td><code>DHCPREQUEST</code></td>
            <td><code>3</code></td>
            <td><p>A DHCP Request message.</p>
</td>
        </tr><tr>
            <td><code>DHCPDECLINE</code></td>
            <td><code>4</code></td>
            <td><p>A DHCP Decline message.</p>
</td>
        </tr><tr>
            <td><code>DHCPACK</code></td>
            <td><code>5</code></td>
            <td><p>A DHCP Ack message.</p>
</td>
        </tr><tr>
            <td><code>DHCPNAK</code></td>
            <td><code>6</code></td>
            <td><p>A DHCP Nak message;</p>
</td>
        </tr><tr>
            <td><code>DHCPRELEASE</code></td>
            <td><code>7</code></td>
            <td><p>A DHCP Release message;</p>
</td>
        </tr><tr>
            <td><code>DHCPINFORM</code></td>
            <td><code>8</code></td>
            <td><p>A DHCP Inform message.</p>
</td>
        </tr></table>

### OptionCode {#OptionCode}
Type: <code>uint32</code>

*Defined in [fuchsia.net.dhcp/options.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.dhcp/options.fidl#334)*

<p>The code of a DHCP option to be retrieved by Server.GetOption(). The code
values are from https://tools.ietf.org/html/rfc2132 and the enum variants
have been listed in the order they are presented in the RFC.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SUBNET_MASK</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>TIME_OFFSET</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>ROUTER</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>TIME_SERVER</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>NAME_SERVER</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>DOMAIN_NAME_SERVER</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>LOG_SERVER</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr><tr>
            <td><code>COOKIE_SERVER</code></td>
            <td><code>8</code></td>
            <td></td>
        </tr><tr>
            <td><code>LPR_SERVER</code></td>
            <td><code>9</code></td>
            <td></td>
        </tr><tr>
            <td><code>IMPRESS_SERVER</code></td>
            <td><code>10</code></td>
            <td></td>
        </tr><tr>
            <td><code>RESOURCE_LOCATION_SERVER</code></td>
            <td><code>11</code></td>
            <td></td>
        </tr><tr>
            <td><code>HOST_NAME</code></td>
            <td><code>12</code></td>
            <td></td>
        </tr><tr>
            <td><code>BOOT_FILE_SIZE</code></td>
            <td><code>13</code></td>
            <td></td>
        </tr><tr>
            <td><code>MERIT_DUMP_FILE</code></td>
            <td><code>14</code></td>
            <td></td>
        </tr><tr>
            <td><code>DOMAIN_NAME</code></td>
            <td><code>15</code></td>
            <td></td>
        </tr><tr>
            <td><code>SWAP_SERVER</code></td>
            <td><code>16</code></td>
            <td></td>
        </tr><tr>
            <td><code>ROOT_PATH</code></td>
            <td><code>17</code></td>
            <td></td>
        </tr><tr>
            <td><code>EXTENSIONS_PATH</code></td>
            <td><code>18</code></td>
            <td></td>
        </tr><tr>
            <td><code>IP_FORWARDING</code></td>
            <td><code>19</code></td>
            <td></td>
        </tr><tr>
            <td><code>NON_LOCAL_SOURCE_ROUTING</code></td>
            <td><code>20</code></td>
            <td></td>
        </tr><tr>
            <td><code>POLICY_FILTER</code></td>
            <td><code>21</code></td>
            <td></td>
        </tr><tr>
            <td><code>MAX_DATAGRAM_REASSEMBLY_SIZE</code></td>
            <td><code>22</code></td>
            <td></td>
        </tr><tr>
            <td><code>DEFAULT_IP_TTL</code></td>
            <td><code>23</code></td>
            <td></td>
        </tr><tr>
            <td><code>PATH_MTU_AGING_TIMEOUT</code></td>
            <td><code>24</code></td>
            <td></td>
        </tr><tr>
            <td><code>PATH_MTU_PLATEAU_TABLE</code></td>
            <td><code>25</code></td>
            <td></td>
        </tr><tr>
            <td><code>INTERFACE_MTU</code></td>
            <td><code>26</code></td>
            <td></td>
        </tr><tr>
            <td><code>ALL_SUBNETS_LOCAL</code></td>
            <td><code>27</code></td>
            <td></td>
        </tr><tr>
            <td><code>BROADCAST_ADDRESS</code></td>
            <td><code>28</code></td>
            <td></td>
        </tr><tr>
            <td><code>PERFORM_MASK_DISCOVERY</code></td>
            <td><code>29</code></td>
            <td></td>
        </tr><tr>
            <td><code>MASK_SUPPLIER</code></td>
            <td><code>30</code></td>
            <td></td>
        </tr><tr>
            <td><code>PERFORM_ROUTER_DISCOVERY</code></td>
            <td><code>31</code></td>
            <td></td>
        </tr><tr>
            <td><code>ROUTER_SOLICITATION_ADDRESS</code></td>
            <td><code>32</code></td>
            <td></td>
        </tr><tr>
            <td><code>STATIC_ROUTE</code></td>
            <td><code>33</code></td>
            <td></td>
        </tr><tr>
            <td><code>TRAILER_ENCAPSULATION</code></td>
            <td><code>34</code></td>
            <td></td>
        </tr><tr>
            <td><code>ARP_CACHE_TIMEOUT</code></td>
            <td><code>35</code></td>
            <td></td>
        </tr><tr>
            <td><code>ETHERNET_ENCAPSULATION</code></td>
            <td><code>36</code></td>
            <td></td>
        </tr><tr>
            <td><code>TCP_DEFAULT_TTL</code></td>
            <td><code>37</code></td>
            <td></td>
        </tr><tr>
            <td><code>TCP_KEEPALIVE_INTERVAL</code></td>
            <td><code>38</code></td>
            <td></td>
        </tr><tr>
            <td><code>TCP_KEEPALIVE_GARBAGE</code></td>
            <td><code>39</code></td>
            <td></td>
        </tr><tr>
            <td><code>NETWORK_INFORMATION_SERVICE_DOMAIN</code></td>
            <td><code>40</code></td>
            <td></td>
        </tr><tr>
            <td><code>NETWORK_INFORMATION_SERVERS</code></td>
            <td><code>41</code></td>
            <td></td>
        </tr><tr>
            <td><code>NETWORK_TIME_PROTOCOL_SERVERS</code></td>
            <td><code>42</code></td>
            <td></td>
        </tr><tr>
            <td><code>VENDOR_SPECIFIC_INFORMATION</code></td>
            <td><code>43</code></td>
            <td></td>
        </tr><tr>
            <td><code>NETBIOS_OVER_TCPIP_NAME_SERVER</code></td>
            <td><code>44</code></td>
            <td></td>
        </tr><tr>
            <td><code>NETBIOS_OVER_TCPIP_DATAGRAM_DISTRIBUTION_SERVER</code></td>
            <td><code>45</code></td>
            <td></td>
        </tr><tr>
            <td><code>NETBIOS_OVER_TCPIP_NODE_TYPE</code></td>
            <td><code>46</code></td>
            <td></td>
        </tr><tr>
            <td><code>NETBIOS_OVER_TCPIP_SCOPE</code></td>
            <td><code>47</code></td>
            <td></td>
        </tr><tr>
            <td><code>X_WINDOW_SYSTEM_FONT_SERVER</code></td>
            <td><code>48</code></td>
            <td></td>
        </tr><tr>
            <td><code>X_WINDOW_SYSTEM_DISPLAY_MANAGER</code></td>
            <td><code>49</code></td>
            <td></td>
        </tr><tr>
            <td><code>NETWORK_INFORMATION_SERVICE_PLUS_DOMAIN</code></td>
            <td><code>64</code></td>
            <td></td>
        </tr><tr>
            <td><code>NETWORK_INFORMATION_SERVICE_PLUS_SERVERS</code></td>
            <td><code>65</code></td>
            <td></td>
        </tr><tr>
            <td><code>MOBILE_IP_HOME_AGENT</code></td>
            <td><code>68</code></td>
            <td></td>
        </tr><tr>
            <td><code>SMTP_SERVER</code></td>
            <td><code>69</code></td>
            <td></td>
        </tr><tr>
            <td><code>POP3_SERVER</code></td>
            <td><code>70</code></td>
            <td></td>
        </tr><tr>
            <td><code>NNTP_SERVER</code></td>
            <td><code>71</code></td>
            <td></td>
        </tr><tr>
            <td><code>DEFAULT_WWW_SERVER</code></td>
            <td><code>72</code></td>
            <td></td>
        </tr><tr>
            <td><code>DEFAULT_FINGER_SERVER</code></td>
            <td><code>73</code></td>
            <td></td>
        </tr><tr>
            <td><code>DEFAULT_IRC_SERVER</code></td>
            <td><code>74</code></td>
            <td></td>
        </tr><tr>
            <td><code>STREETTALK_SERVER</code></td>
            <td><code>75</code></td>
            <td></td>
        </tr><tr>
            <td><code>STREETTALK_DIRECTORY_ASSISTANCE_SERVER</code></td>
            <td><code>76</code></td>
            <td></td>
        </tr><tr>
            <td><code>OPTION_OVERLOAD</code></td>
            <td><code>52</code></td>
            <td></td>
        </tr><tr>
            <td><code>TFTP_SERVER_NAME</code></td>
            <td><code>66</code></td>
            <td></td>
        </tr><tr>
            <td><code>BOOTFILE_NAME</code></td>
            <td><code>67</code></td>
            <td></td>
        </tr><tr>
            <td><code>MAX_DHCP_MESSAGE_SIZE</code></td>
            <td><code>57</code></td>
            <td></td>
        </tr><tr>
            <td><code>RENEWAL_TIME_VALUE</code></td>
            <td><code>58</code></td>
            <td></td>
        </tr><tr>
            <td><code>REBINDING_TIME_VALUE</code></td>
            <td><code>59</code></td>
            <td></td>
        </tr></table>

### ParameterName {#ParameterName}
Type: <code>uint32</code>

*Defined in [fuchsia.net.dhcp/server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.dhcp/server.fidl#74)*

<p>The name of the Parameter to be retrieved by Server.GetParameter().</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>IP_ADDRS</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>ADDRESS_POOL</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>LEASE_LENGTH</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>PERMITTED_MACS</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>STATICALLY_ASSIGNED_ADDRS</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>ARP_PROBE</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### AddressPool {#AddressPool}


*Defined in [fuchsia.net.dhcp/server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.dhcp/server.fidl#10)*

<p>The pool of addresses managed by a DHCP server and from which leases are supplied.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>network_id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Ipv4Address'>Ipv4Address</a></code>
            </td>
            <td><p>The network ID of the address pool's subnet.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>broadcast</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Ipv4Address'>Ipv4Address</a></code>
            </td>
            <td><p>The broadcast address of the address pool's subnet.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>mask</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Ipv4Address'>Ipv4Address</a></code>
            </td>
            <td><p>The subnet mask of the address pool's network.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>pool_range_start</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Ipv4Address'>Ipv4Address</a></code>
            </td>
            <td><p>The starting address, inclusive, of the range of addresses which the DHCP server
will lease to clients. This address must be in the subnet defined by the network_id
and mask members of the AddressPool.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>pool_range_stop</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Ipv4Address'>Ipv4Address</a></code>
            </td>
            <td><p>The ending address, inclusive, of the range of addresses which the server will
to clients. This address must be in the subnet defined by the network_id and mask
members of the AddressPool.</p>
</td>
        </tr></table>

### LeaseLength {#LeaseLength}


*Defined in [fuchsia.net.dhcp/server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.dhcp/server.fidl#28)*

<p>The duration of leases offered by the server.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>default</code></td>
            <td>
                <code><a class='link' href='#Duration'>Duration</a></code>
            </td>
            <td><p>The default lease length to be issued to clients. This field must have a value.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>max</code></td>
            <td>
                <code><a class='link' href='#Duration'>Duration</a></code>
            </td>
            <td><p>The maximum lease length value which the server will issue to clients who
have requested a specific lease length. If omitted, the max lease length is
equivalent to the default lease length.</p>
</td>
        </tr></table>

### StaticAssignment {#StaticAssignment}


*Defined in [fuchsia.net.dhcp/server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.dhcp/server.fidl#38)*

<p>A static IP address assignment for a host or device on the network managed by Server.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>host</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#MacAddress'>MacAddress</a></code>
            </td>
            <td><p>The MAC address of the host or device which will have the static IP address assignment.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>assigned_addr</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Ipv4Address'>Ipv4Address</a></code>
            </td>
            <td><p>The IP address which the host or device will always be assigned by dhcpd.</p>
</td>
        </tr></table>



## **UNIONS**

### Client_Start_Result {#Client_Start_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Client_Start_Response'>Client_Start_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### Client_Stop_Result {#Client_Stop_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Client_Stop_Response'>Client_Stop_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### Server_GetOption_Result {#Server_GetOption_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Server_GetOption_Response'>Server_GetOption_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### Server_GetParameter_Result {#Server_GetParameter_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Server_GetParameter_Response'>Server_GetParameter_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### Server_SetOption_Result {#Server_SetOption_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Server_SetOption_Response'>Server_SetOption_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### Server_SetParameter_Result {#Server_SetParameter_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Server_SetParameter_Response'>Server_SetParameter_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### Server_ListOptions_Result {#Server_ListOptions_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Server_ListOptions_Response'>Server_ListOptions_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### Server_ListParameters_Result {#Server_ListParameters_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Server_ListParameters_Response'>Server_ListParameters_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>



## **XUNIONS**

### Option {#Option}
*Defined in [fuchsia.net.dhcp/options.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.dhcp/options.fidl#87)*

<p>A generic representation of client configuration parameters and DHCP settings. Options are the
mechanism by which the DHCP protocol communicates configuration parameters from a repository on
a DHCP server to DHCP clients, or by which DHCP clients and servers communicate data relevant to
a DHCP transaction.
All DHCP option values must have a length which can fit within a single byte, i.e. less than 256.
Options for which there is no reasonable administrator-configurable value have been omitted
from this xunion. The omitted options are:</p>
<ul>
<li>Pad - never has a value</li>
<li>End - never has a value</li>
<li>RequestedIpAddress - value always selected by the DHCP client.</li>
<li>DhcpMessageType - value always determined by state of transaction between DHCP client and server.</li>
<li>ServerIdentifier - value always determined by address to which the server is bound.</li>
<li>ParameterRequestList - value always selected by the DHCP client.</li>
<li>Message - value determined in response to runtime error.</li>
<li>VendorClassIdentifer - value always selected by the DHCP client.</li>
<li>ClientIdentifier - value always selected by the DHCP client.</li>
</ul>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>subnet_mask</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Ipv4Address'>Ipv4Address</a></code>
            </td>
            <td><p>A 32-bit IPv4 subnet mask.</p>
</td>
        </tr><tr>
            <td><code>time_offset</code></td>
            <td>
                <code>int32</code>
            </td>
            <td><p>The client's offset from UTC in seconds. A positive offset is east of the zero meridian, and
a negative offset is west of the zero meridian.</p>
</td>
        </tr><tr>
            <td><code>router</code></td>
            <td>
                <code><a class='link' href='#Addresses'>Addresses</a></code>
            </td>
            <td><p>A list of the routers in a client's subnet, listed in order of preference.</p>
</td>
        </tr><tr>
            <td><code>time_server</code></td>
            <td>
                <code><a class='link' href='#Addresses'>Addresses</a></code>
            </td>
            <td><p>A list of time servers available to the client, in order of preference.</p>
</td>
        </tr><tr>
            <td><code>name_server</code></td>
            <td>
                <code><a class='link' href='#Addresses'>Addresses</a></code>
            </td>
            <td><p>A list of IEN 116 Name servers available to the client, in order of preference.</p>
</td>
        </tr><tr>
            <td><code>domain_name_server</code></td>
            <td>
                <code><a class='link' href='#Addresses'>Addresses</a></code>
            </td>
            <td><p>A list of Domain Name System servers available to the client, in order of preference;</p>
</td>
        </tr><tr>
            <td><code>log_server</code></td>
            <td>
                <code><a class='link' href='#Addresses'>Addresses</a></code>
            </td>
            <td><p>A list of MIT-LCS UDP Log servers available to the client, in order of preference.</p>
</td>
        </tr><tr>
            <td><code>cookie_server</code></td>
            <td>
                <code><a class='link' href='#Addresses'>Addresses</a></code>
            </td>
            <td><p>A list of RFC 865 Cookie servers available to the client, in order of preference.</p>
</td>
        </tr><tr>
            <td><code>lpr_server</code></td>
            <td>
                <code><a class='link' href='#Addresses'>Addresses</a></code>
            </td>
            <td><p>A list of RFC 1179 Line Printer servers available to the client, in order of preference.</p>
</td>
        </tr><tr>
            <td><code>impress_server</code></td>
            <td>
                <code><a class='link' href='#Addresses'>Addresses</a></code>
            </td>
            <td><p>A list of Imagen Impress servers available to the client, in order of preference.</p>
</td>
        </tr><tr>
            <td><code>resource_location_server</code></td>
            <td>
                <code><a class='link' href='#Addresses'>Addresses</a></code>
            </td>
            <td><p>A list of RFC 887 Resource Location servers available to the client, in order of preference.</p>
</td>
        </tr><tr>
            <td><code>host_name</code></td>
            <td>
                <code><a class='link' href='#AsciiString'>AsciiString</a></code>
            </td>
            <td><p>The host name of the client, which may or may not be qualified with the local domain name.</p>
</td>
        </tr><tr>
            <td><code>boot_file_size</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>The size of the client's default boot image in 512-octet blocks.</p>
</td>
        </tr><tr>
            <td><code>merit_dump_file</code></td>
            <td>
                <code><a class='link' href='#AsciiString'>AsciiString</a></code>
            </td>
            <td><p>The path name to the client's core dump in the event the client crashes.</p>
</td>
        </tr><tr>
            <td><code>domain_name</code></td>
            <td>
                <code><a class='link' href='#AsciiString'>AsciiString</a></code>
            </td>
            <td><p>The client's domain name for use in resolving hostnames in the DNS.</p>
</td>
        </tr><tr>
            <td><code>swap_server</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Ipv4Address'>Ipv4Address</a></code>
            </td>
            <td><p>The address of the client's swap server.</p>
</td>
        </tr><tr>
            <td><code>root_path</code></td>
            <td>
                <code><a class='link' href='#AsciiString'>AsciiString</a></code>
            </td>
            <td><p>The path name to the client's root disk.</p>
</td>
        </tr><tr>
            <td><code>extensions_path</code></td>
            <td>
                <code><a class='link' href='#AsciiString'>AsciiString</a></code>
            </td>
            <td><p>The path name to a TFTP-retrievable file. This file contains data which can be interpreted
as the BOOTP vendor-extension field. Unlike the BOOTP vendor-extension field, this file has
an unconstrained length and any references to Tag 18 are ignored.</p>
</td>
        </tr><tr>
            <td><code>ip_forwarding</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>A flag which will enabled IP layer packet forwarding when true.</p>
</td>
        </tr><tr>
            <td><code>non_local_source_routing</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>A flag which will enable forwarding of IP packets with non-local source routes.</p>
</td>
        </tr><tr>
            <td><code>policy_filter</code></td>
            <td>
                <code><a class='link' href='#Addresses'>Addresses</a></code>
            </td>
            <td><p>Policy filters for non-local source routing.
A list of IP Address and Subnet Mask pairs. If an incoming source-routed packet has a
next-hop that does not match one of these pairs, then the packet will be dropped.</p>
</td>
        </tr><tr>
            <td><code>max_datagram_reassembly_size</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>The maximum sized datagram that the client should be able to reassemble, in octets. The
minimum legal value is 576.</p>
</td>
        </tr><tr>
            <td><code>default_ip_ttl</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td><p>The default time-to-live to use on outgoing IP datagrams. The value must be between 1 and
255.</p>
</td>
        </tr><tr>
            <td><code>path_mtu_aging_timeout</code></td>
            <td>
                <code><a class='link' href='#Duration'>Duration</a></code>
            </td>
            <td><p>The timeout to be used when aging Path MTU values by the mechanism in RFC 1191.</p>
</td>
        </tr><tr>
            <td><code>path_mtu_plateau_table</code></td>
            <td>
                <code>vector&lt;uint16&gt;[127]</code>
            </td>
            <td><p>Table of MTU sizes for Path MTU Discovery.
A list of MTU sizes, ordered from smallest to largest. The smallest value cannot be smaller
than 68.</p>
</td>
        </tr><tr>
            <td><code>interface_mtu</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>The MTU for the client's interface. Minimum value of 68.</p>
</td>
        </tr><tr>
            <td><code>all_subnets_local</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>A flag indicating if all subents of the IP network to which the client is connected have the
same MTU.</p>
</td>
        </tr><tr>
            <td><code>broadcast_address</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Ipv4Address'>Ipv4Address</a></code>
            </td>
            <td><p>The broadcast address of the client's subnet. Legal values are defined in RFC 1122.</p>
</td>
        </tr><tr>
            <td><code>perform_mask_discovery</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>A flag indicating whether the client should perform subnet mask discovery via ICMP.</p>
</td>
        </tr><tr>
            <td><code>mask_supplier</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>A flag indicating whether the client should respond to subnet mask discovery requests via
ICMP.</p>
</td>
        </tr><tr>
            <td><code>perform_router_discovery</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>A flag indicating whether the client should solicit routers using Router Discovery as
defined in RFC 1256.</p>
</td>
        </tr><tr>
            <td><code>router_solicitation_address</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Ipv4Address'>Ipv4Address</a></code>
            </td>
            <td><p>The address to which the client should transmit Router Solicitation requests.</p>
</td>
        </tr><tr>
            <td><code>static_route</code></td>
            <td>
                <code><a class='link' href='#Addresses'>Addresses</a></code>
            </td>
            <td><p>Static Routes which the host should put in its routing cache.
A list of Destination address/Next-hop address pairs defining static routes for the client's
routing table. The routes should be listed in descending order of priority. It is illegal
to use 0.0.0.0 as the destination in a static route.</p>
</td>
        </tr><tr>
            <td><code>trailer_encapsulation</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>A flag specifying whether the client negotiate the use of trailers when using ARP, per RFC
893.</p>
</td>
        </tr><tr>
            <td><code>arp_cache_timeout</code></td>
            <td>
                <code><a class='link' href='#Duration'>Duration</a></code>
            </td>
            <td><p>The timeout for ARP cache entries.</p>
</td>
        </tr><tr>
            <td><code>ethernet_encapsulation</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>A flag specifying that the client should use Ethernet v2 encapsulation when false, and IEEE
802.3 encapsulation when true.</p>
</td>
        </tr><tr>
            <td><code>tcp_default_ttl</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td><p>The default time-to-live that the client should use for outgoing TCP segments. The minimum
value is 1.</p>
</td>
        </tr><tr>
            <td><code>tcp_keepalive_interval</code></td>
            <td>
                <code><a class='link' href='#Duration'>Duration</a></code>
            </td>
            <td><p>The interval the client should wait before sending a TCP keepalive message. A
value of 0 indicates that the client should not send keepalive messages unless specifically
requested by an application.</p>
</td>
        </tr><tr>
            <td><code>tcp_keepalive_garbage</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>A flag specifying whether the client should send TCP keepalive messages with an octet of
garbage for compatibility with older implementations.</p>
</td>
        </tr><tr>
            <td><code>network_information_service_domain</code></td>
            <td>
                <code><a class='link' href='#AsciiString'>AsciiString</a></code>
            </td>
            <td><p>The name of the client's Network Information Service domain.</p>
</td>
        </tr><tr>
            <td><code>network_information_servers</code></td>
            <td>
                <code><a class='link' href='#Addresses'>Addresses</a></code>
            </td>
            <td><p>A list of Network Information Service server addresses available to the client, listed in
order of preference.</p>
</td>
        </tr><tr>
            <td><code>network_time_protocol_servers</code></td>
            <td>
                <code><a class='link' href='#Addresses'>Addresses</a></code>
            </td>
            <td><p>A list of Network Time Protocol (NTP) server addresses available to the client, listed in
order of preference.</p>
</td>
        </tr><tr>
            <td><code>vendor_specific_information</code></td>
            <td>
                <code>vector&lt;uint8&gt;[255]</code>
            </td>
            <td><p>An opaque object of octets for exchanging vendor-specific information.</p>
</td>
        </tr><tr>
            <td><code>netbios_over_tcpip_name_server</code></td>
            <td>
                <code><a class='link' href='#Addresses'>Addresses</a></code>
            </td>
            <td><p>A list of NetBIOS name server addresses available to the client, listed in order of
preference.</p>
</td>
        </tr><tr>
            <td><code>netbios_over_tcpip_datagram_distribution_server</code></td>
            <td>
                <code><a class='link' href='#Addresses'>Addresses</a></code>
            </td>
            <td><p>A list of NetBIOS datagram distribution servers available to the client, listed in order of
preference.</p>
</td>
        </tr><tr>
            <td><code>netbios_over_tcpip_node_type</code></td>
            <td>
                <code><a class='link' href='#NodeTypes'>NodeTypes</a></code>
            </td>
            <td><p>The NetBIOS node type which should be used by the client.</p>
</td>
        </tr><tr>
            <td><code>netbios_over_tcpip_scope</code></td>
            <td>
                <code><a class='link' href='#AsciiString'>AsciiString</a></code>
            </td>
            <td><p>The NetBIOS over TCP/IP scope parameter, as defined in RFC 1001, for the client.</p>
</td>
        </tr><tr>
            <td><code>x_window_system_font_server</code></td>
            <td>
                <code><a class='link' href='#Addresses'>Addresses</a></code>
            </td>
            <td><p>A list of X Window System Font server addresses available to the client, listed in order of
preference.</p>
</td>
        </tr><tr>
            <td><code>x_window_system_display_manager</code></td>
            <td>
                <code><a class='link' href='#Addresses'>Addresses</a></code>
            </td>
            <td><p>A list of X Window System Display Manager system addresses available to the client, listed
in order of preference.</p>
</td>
        </tr><tr>
            <td><code>network_information_service_plus_domain</code></td>
            <td>
                <code><a class='link' href='#AsciiString'>AsciiString</a></code>
            </td>
            <td><p>The name of the client's Network Information System+ domain.</p>
</td>
        </tr><tr>
            <td><code>network_information_service_plus_servers</code></td>
            <td>
                <code><a class='link' href='#Addresses'>Addresses</a></code>
            </td>
            <td><p>A list of Network Information System+ server addresses available to the client, listed in
order of preference.</p>
</td>
        </tr><tr>
            <td><code>mobile_ip_home_agent</code></td>
            <td>
                <code><a class='link' href='#Addresses'>Addresses</a></code>
            </td>
            <td><p>A list of mobile IP home agent addresses available to the client, listed in order of
preference.</p>
</td>
        </tr><tr>
            <td><code>smtp_server</code></td>
            <td>
                <code><a class='link' href='#Addresses'>Addresses</a></code>
            </td>
            <td><p>A list of Simple Mail Transport Protocol (SMTP) server address available to the client,
listed in order of preference.</p>
</td>
        </tr><tr>
            <td><code>pop3_server</code></td>
            <td>
                <code><a class='link' href='#Addresses'>Addresses</a></code>
            </td>
            <td><p>A list of Post Office Protocol (POP3) server addresses available to the client, listed in
order of preference.</p>
</td>
        </tr><tr>
            <td><code>nntp_server</code></td>
            <td>
                <code><a class='link' href='#Addresses'>Addresses</a></code>
            </td>
            <td><p>A list Network News Transport Protocol (NNTP) server addresses available to the client,
listed in order of preference.</p>
</td>
        </tr><tr>
            <td><code>default_www_server</code></td>
            <td>
                <code><a class='link' href='#Addresses'>Addresses</a></code>
            </td>
            <td><p>A list of default World Wide Web (WWW) server addresses available to the client, listed in
order of preference.</p>
</td>
        </tr><tr>
            <td><code>default_finger_server</code></td>
            <td>
                <code><a class='link' href='#Addresses'>Addresses</a></code>
            </td>
            <td><p>A list of default Finger server addresses available to the client, listed in order of
preference.</p>
</td>
        </tr><tr>
            <td><code>default_irc_server</code></td>
            <td>
                <code><a class='link' href='#Addresses'>Addresses</a></code>
            </td>
            <td><p>A list of Internet Relay Chat server addresses available to the client, listed in order of
preference.</p>
</td>
        </tr><tr>
            <td><code>streettalk_server</code></td>
            <td>
                <code><a class='link' href='#Addresses'>Addresses</a></code>
            </td>
            <td><p>A list of StreetTalk server addresses available to the client, listed in order of
preference.</p>
</td>
        </tr><tr>
            <td><code>streettalk_directory_assistance_server</code></td>
            <td>
                <code><a class='link' href='#Addresses'>Addresses</a></code>
            </td>
            <td><p>A list of StreetTalk Directory Assistance server addresses available to the client, listed
in order of preference.</p>
</td>
        </tr><tr>
            <td><code>option_overload</code></td>
            <td>
                <code><a class='link' href='#OptionOverloadValue'>OptionOverloadValue</a></code>
            </td>
            <td><p>An option specifying whether the <code>sname</code>, <code>file</code>, or both fields have been overloaded to
carry DHCP options. If this option is present, the client interprets the additional fields
after it concludes interpreting standard option fields.</p>
</td>
        </tr><tr>
            <td><code>tftp_server_name</code></td>
            <td>
                <code><a class='link' href='#AsciiString'>AsciiString</a></code>
            </td>
            <td><p>The TFTP server name available to the client. This option should be used when the <code>sname</code>
field has been overloaded to carry options.</p>
</td>
        </tr><tr>
            <td><code>bootfile_name</code></td>
            <td>
                <code><a class='link' href='#AsciiString'>AsciiString</a></code>
            </td>
            <td><p>The bootfile name for the client. This option should be used when the <code>file</code> field has been
overloaded to carry options.</p>
</td>
        </tr><tr>
            <td><code>max_dhcp_message_size</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>The maximum length in octets of a DHCP message that the participant is willing to accept.
The minimum value is 576.</p>
</td>
        </tr><tr>
            <td><code>renewal_time_value</code></td>
            <td>
                <code><a class='link' href='#Duration'>Duration</a></code>
            </td>
            <td><p>The time interval after address assignment at which the client will transition
to the Renewing state.</p>
</td>
        </tr><tr>
            <td><code>rebinding_time_value</code></td>
            <td>
                <code><a class='link' href='#Duration'>Duration</a></code>
            </td>
            <td><p>The time interval after address assignment at which the client will transition
to the Rebinding state.</p>
</td>
        </tr></table>

### Parameter {#Parameter}
*Defined in [fuchsia.net.dhcp/server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.dhcp/server.fidl#46)*

<p>The configurable server parameters.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>ip_addrs</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Ipv4Address'>Ipv4Address</a>&gt;[256]</code>
            </td>
            <td><p>The IP addresses to which the server is bound. The vector bound has been
arbitrarily selected as a generous upper limit.</p>
</td>
        </tr><tr>
            <td><code>address_pool</code></td>
            <td>
                <code><a class='link' href='#AddressPool'>AddressPool</a></code>
            </td>
            <td><p>The server's pool of managed addresses. Changing the address pool will not cancel existing
leases because the DHCP protocol does not provide a mechanism for doing so. Administrators
should take care when changing the address pool for a server with active leases.</p>
</td>
        </tr><tr>
            <td><code>lease</code></td>
            <td>
                <code><a class='link' href='#LeaseLength'>LeaseLength</a></code>
            </td>
            <td><p>The duration of leases issued by dhcpd.</p>
</td>
        </tr><tr>
            <td><code>permitted_macs</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#MacAddress'>MacAddress</a>&gt;[256]</code>
            </td>
            <td><p>The client MAC addresses which the server will issue leases to. By default,
the server will not have a permitted MAC list, in which case it will attempt to
issue a lease to every client which requests one. If permitted_macs has a non-zero length
then the server will only respond to lease requests from clients with a MAC in the list. The
vector bound has been arbitrarily selected as a generous upper limit.</p>
</td>
        </tr><tr>
            <td><code>statically_assigned_addrs</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#StaticAssignment'>StaticAssignment</a>&gt;[256]</code>
            </td>
            <td><p>Addresses statically assigned to specific hosts or devices. Typically, a network
administrator will statically assign addresses to always-on network
devices which should always have the same IP address, such as network printers. The vector
bound has been arbitrarily selected as a generous upper limit.</p>
</td>
        </tr><tr>
            <td><code>arp_probe</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Enables server behavior where the server ARPs an IP address prior to issuing
it in a lease. If the server receives a response, the server will mark the
address as in-use and try again with a different address.</p>
</td>
        </tr></table>



## **BITS**

### NodeTypes {#NodeTypes}
Type: <code>uint8</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>B_NODE</td>
            <td>1</td>
            <td><p>A B node type.</p>
</td>
        </tr><tr>
            <td>P_NODE</td>
            <td>2</td>
            <td><p>A P node type.</p>
</td>
        </tr><tr>
            <td>M_NODE</td>
            <td>4</td>
            <td><p>A M node type.</p>
</td>
        </tr><tr>
            <td>H_NODE</td>
            <td>8</td>
            <td><p>A H node type.</p>
</td>
        </tr></table>





## **TYPE ALIASES**

<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr id="Duration">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.dhcp/options.fidl#11">Duration</a></td>
            <td>
                <code>uint32</code></td>
            <td><p>A DHCP duration value, in seconds. As specified in
https://tools.ietf.org/html/rfc2131#section-3.3, DHCP duration values are
relative times.</p>
</td>
        </tr><tr id="Addresses">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.dhcp/options.fidl#16">Addresses</a></td>
            <td>
                <code>vector</code></td>
            <td><p>A list of IP addresses. The vector bounds of this list are MAX_OPTION_LEN /
len(Ipv4Address), where MAX_OPTION_LEN is the maximum byte length of a value
for a DHCP option as defined in https://tools.ietf.org/html/rfc2132#section-2:
&quot;All other options are variable-length with a length octet following the tag octet.&quot;</p>
</td>
        </tr><tr id="AsciiString">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.dhcp/options.fidl#24">AsciiString</a></td>
            <td>
                <code>string</code></td>
            <td><p>An ASCII string with a length limit of 255. All DHCP Option values must have
a length that can fit in an octet, cf. &quot;All other options are variable-length with a length octet following the tag octet.&quot;
from https://tools.ietf.org/html/rfc2132#section-2. Similarly all DHCP Option
string values must be limited to the ASCII character set. Should non-ASCII
characters be sent in a <code>AsciiString</code> to Server, Server will close the channel to
the client.</p>
</td>
        </tr></table>

