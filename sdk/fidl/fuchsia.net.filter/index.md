Project: /_project.yaml
Book: /_book.yaml

# fuchsia.net.filter


## **PROTOCOLS**

## Filter {:#Filter}
*Defined in [fuchsia.net.filter/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.filter/commands.fidl#15)*


### Enable {:#Enable}

 Enable enables the filter if true is passed.
 It disables the filter if false is passed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>enabled</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>

### IsEnabled {:#IsEnabled}

 IsEnabled returns true if the filter is enabled.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>enabled</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

### GetRules {:#GetRules}

 GetRules gets the current rules. They do not include NAT or RDR rules.
 (use GetNATRules or GetRDRRules instead).

 GetRules also returns a generation number associated with the current
 rules.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rules</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Rule'>Rule</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>generation</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>

### UpdateRules {:#UpdateRules}

 UpdateRules updates the current rules. It does not update NAT or RDR rules
 (use UpdateNATRules or UpdateRDRRules instead).

 UpdateRules takes a generation number that is previously returned from
 GetRules. To successfully update the current rules, the generation number
 passed to UpdateRules needs to be up-to-date.

 If somebody else has updated the rules since the previous GetRules, the
 generation number won't match and err_generation_mismatch will be returned.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rules</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Rule'>Rule</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>generation</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>

### GetNATRules {:#GetNATRules}

 GetNATRules gets the current NAT rules.

 It also returns a generation number that can be passed to UpdateNATRules.


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rules</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#NAT'>NAT</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>generation</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>

### UpdateNATRules {:#UpdateNATRules}

 UpdateNATRules updates the current NAT rules.

 It takes a generation number that is returned from GetNATRules. To
 successfully update the current rules, the generation number passed to
 UpdateNATRules needs to be up-to-date.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rules</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#NAT'>NAT</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>generation</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>

### GetRDRRules {:#GetRDRRules}

 GetRDRRules gets the current RDR rules.

 It also returns a generation number that can be passed to UpdateRDRRules.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rules</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#RDR'>RDR</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>generation</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>

### UpdateRDRRules {:#UpdateRDRRules}

 UpdateRDRRules updates the previous RDR rules with new rules.

 It takes a generation number that is returned from GetRDRRules. To
 successfully update the current rules, the generation number passed to
 UpdateRDRRules needs to be up-to-date.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rules</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#RDR'>RDR</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>generation</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Rule {:#Rule}
*Defined in [fuchsia.net.filter/ruleset.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.filter/ruleset.fidl#31)*



 Rule describes the conditions and the action of a rule.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>action</code></td>
            <td>
                <code><a class='link' href='#Action'>Action</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>direction</code></td>
            <td>
                <code><a class='link' href='#Direction'>Direction</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>quick</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, no more rules will be tested.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>proto</code></td>
            <td>
                <code><a class='link' href='#SocketProtocol'>SocketProtocol</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>src_subnet</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/index.html'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/index.html#Subnet'>Subnet</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>src_subnet_invert_match</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, matches any address that is NOT contained in the subnet.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>src_port</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>dst_subnet</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/index.html'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/index.html#Subnet'>Subnet</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>dst_subnet_invert_match</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, matches any address that is NOT contained in the subnet.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>dst_port</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nic</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>log</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>keepState</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### NAT {:#NAT}
*Defined in [fuchsia.net.filter/ruleset.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.filter/ruleset.fidl#52)*



 NAT is a special rule for Network Address Translation, which rewrites
 the address of an outgoing packet.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>proto</code></td>
            <td>
                <code><a class='link' href='#SocketProtocol'>SocketProtocol</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>src_subnet</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/index.html'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/index.html#Subnet'>Subnet</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>new_src_addr</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/index.html'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/index.html#IpAddress'>IpAddress</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nic</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### RDR {:#RDR}
*Defined in [fuchsia.net.filter/ruleset.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.filter/ruleset.fidl#61)*



 RDR is a special rule for Redirector, which forwards an incoming packet
 to a machine inside the firewall.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>proto</code></td>
            <td>
                <code><a class='link' href='#SocketProtocol'>SocketProtocol</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>dst_addr</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/index.html'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/index.html#IpAddress'>IpAddress</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>dst_port</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>new_dst_addr</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/index.html'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/index.html#IpAddress'>IpAddress</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>new_dst_port</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nic</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### Status {:#Status}
Type: <code>uint32</code>

*Defined in [fuchsia.net.filter/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.filter/commands.fidl#7)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ok</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>err_internal</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>err_generation_mismatch</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>err_bad_rule</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### Direction {:#Direction}
Type: <code>uint32</code>

*Defined in [fuchsia.net.filter/ruleset.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.filter/ruleset.fidl#10)*

 Direction is which way (Incoming or Outgoing) a packet is moving in the stack.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>incoming</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>outgoing</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### Action {:#Action}
Type: <code>uint32</code>

*Defined in [fuchsia.net.filter/ruleset.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.filter/ruleset.fidl#15)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>pass</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>drop</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>drop_reset</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### SocketProtocol {:#SocketProtocol}
Type: <code>uint32</code>

*Defined in [fuchsia.net.filter/ruleset.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.filter/ruleset.fidl#21)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ip</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>icmp</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>tcp</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>udp</code></td>
            <td><code>17</code></td>
            <td></td>
        </tr><tr>
            <td><code>ipv6</code></td>
            <td><code>41</code></td>
            <td></td>
        </tr><tr>
            <td><code>icmpv6</code></td>
            <td><code>58</code></td>
            <td></td>
        </tr></table>











