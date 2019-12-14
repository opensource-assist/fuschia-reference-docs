[TOC]

# fuchsia.net.filter


## **PROTOCOLS**

## Filter {#Filter}
*Defined in [fuchsia.net.filter/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.filter/commands.fidl#19)*


### Enable {#Enable}

<p>Enable enables the filter if true is passed.
It disables the filter if false is passed.</p>

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

### IsEnabled {#IsEnabled}

<p>IsEnabled returns true if the filter is enabled.</p>

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

### GetRules {#GetRules}

<p>GetRules gets the current rules. They do not include NAT or RDR rules.
(use GetNatRules or GetRdrRules instead).</p>
<p>GetRules also returns a generation number associated with the current
rules.</p>

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
                <code>vector&lt;<a class='link' href='#Rule'>Rule</a>&gt;[128]</code>
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

### UpdateRules {#UpdateRules}

<p>UpdateRules updates the current rules. It does not update NAT or RDR rules
(use UpdateNatRules or UpdateRdrRules instead).</p>
<p>UpdateRules takes a generation number that is previously returned from
GetRules. To successfully update the current rules, the generation number
passed to UpdateRules needs to be up-to-date.</p>
<p>If somebody else has updated the rules since the previous GetRules, the
generation number won't match and err_generation_mismatch will be returned.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rules</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Rule'>Rule</a>&gt;[128]</code>
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

### GetNatRules {#GetNatRules}

<p>GetNatRules gets the current NAT rules.</p>
<p>It also returns a generation number that can be passed to UpdateNatRules.</p>

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
                <code>vector&lt;<a class='link' href='#Nat'>Nat</a>&gt;[128]</code>
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

### UpdateNatRules {#UpdateNatRules}

<p>UpdateNatRules updates the current NAT rules.</p>
<p>It takes a generation number that is returned from GetNatRules. To
successfully update the current rules, the generation number passed to
UpdateNatRules needs to be up-to-date.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rules</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Nat'>Nat</a>&gt;[128]</code>
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

### GetRdrRules {#GetRdrRules}

<p>GetRdrRules gets the current RDR rules.</p>
<p>It also returns a generation number that can be passed to UpdateRdrRules.</p>

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
                <code>vector&lt;<a class='link' href='#Rdr'>Rdr</a>&gt;[128]</code>
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

### UpdateRdrRules {#UpdateRdrRules}

<p>UpdateRdrRules updates the previous RDR rules with new rules.</p>
<p>It takes a generation number that is returned from GetRdrRules. To
successfully update the current rules, the generation number passed to
UpdateRdrRules needs to be up-to-date.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rules</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Rdr'>Rdr</a>&gt;[128]</code>
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

### PortRange {#PortRange}
*Defined in [fuchsia.net.filter/ruleset.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.filter/ruleset.fidl#30)*



<p>PortRange specifies an inclusive range of port numbers.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>start</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>end</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Rule {#Rule}
*Defined in [fuchsia.net.filter/ruleset.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.filter/ruleset.fidl#36)*



<p>Rule describes the conditions and the action of a rule.</p>


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
            <td><p>If true, no more rules will be tested.</p>
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
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Subnet'>Subnet</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>src_subnet_invert_match</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>If true, matches any address that is NOT contained in the subnet.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>src_port_range</code></td>
            <td>
                <code><a class='link' href='#PortRange'>PortRange</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>dst_subnet</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Subnet'>Subnet</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>dst_subnet_invert_match</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>If true, matches any address that is NOT contained in the subnet.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>dst_port_range</code></td>
            <td>
                <code><a class='link' href='#PortRange'>PortRange</a></code>
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
            <td><code>keep_state</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Nat {#Nat}
*Defined in [fuchsia.net.filter/ruleset.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.filter/ruleset.fidl#57)*



<p>NAT is a special rule for Network Address Translation, which rewrites
the address of an outgoing packet.</p>


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
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Subnet'>Subnet</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>new_src_addr</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#IpAddress'>IpAddress</a></code>
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

### Rdr {#Rdr}
*Defined in [fuchsia.net.filter/ruleset.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.filter/ruleset.fidl#66)*



<p>RDR is a special rule for Redirector, which forwards an incoming packet
to a machine inside the firewall.</p>


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
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#IpAddress'>IpAddress</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>dst_port_range</code></td>
            <td>
                <code><a class='link' href='#PortRange'>PortRange</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>new_dst_addr</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#IpAddress'>IpAddress</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>new_dst_port_range</code></td>
            <td>
                <code><a class='link' href='#PortRange'>PortRange</a></code>
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

### Status {#Status}
Type: <code>uint32</code>

*Defined in [fuchsia.net.filter/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.filter/commands.fidl#8)*

<p>Status codes for commands.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OK</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERR_INTERNAL</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERR_GENERATION_MISMATCH</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERR_BAD_RULE</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### Direction {#Direction}
Type: <code>uint32</code>

*Defined in [fuchsia.net.filter/ruleset.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.filter/ruleset.fidl#10)*

<p>Direction is which way (Incoming or Outgoing) a packet is moving in the stack.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INCOMING</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>OUTGOING</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### Action {#Action}
Type: <code>uint32</code>

*Defined in [fuchsia.net.filter/ruleset.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.filter/ruleset.fidl#15)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>PASS</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>DROP</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>DROP_RESET</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### SocketProtocol {#SocketProtocol}
Type: <code>uint32</code>

*Defined in [fuchsia.net.filter/ruleset.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.filter/ruleset.fidl#21)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ANY</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>ICMP</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>TCP</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>UDP</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>ICMPV6</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr></table>











## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="MAX_RULES">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.filter/commands.fidl#16">MAX_RULES</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum number of rules.</p>
</td>
        </tr>
    
</table>



