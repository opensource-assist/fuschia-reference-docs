[TOC]

# fuchsia.ui.focus


## **PROTOCOLS**

## FocusChainListener {#FocusChainListener}
*Defined in [fuchsia.ui.focus/focus_chain.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.focus/focus_chain.fidl#30)*

<p>A FocusChainListener receives an updated FocusChain when focus changes.</p>

### OnFocusChange {#OnFocusChange}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>focus_chain</code></td>
            <td>
                <code><a class='link' href='#FocusChain'>FocusChain</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## FocusChainListenerRegistry {#FocusChainListenerRegistry}
*Defined in [fuchsia.ui.focus/focus_chain.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.focus/focus_chain.fidl#36)*

<p>A FocusChainListenerRegistry allows listening to FocusChain updates.</p>

### Register {#Register}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='#FocusChainListener'>FocusChainListener</a></code>
            </td>
        </tr></table>









## **TABLES**

### FocusChain {#FocusChain}


*Defined in [fuchsia.ui.focus/focus_chain.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.focus/focus_chain.fidl#25)*

<p>A FocusChain tracks the status of the View hierarchy as View focus changes.</p>
<p>Description. The <code>focus_chain</code> is a vector of ViewRefs in order of
dominance in the View hierarchy; each pair of elements represents a
parent-child relationship.  The root View is always present and occupies
slot 0.  The newly-focused View receives a fuchsia.ui.input.FocusEvent and
occupies the final slot in the vector.  If a View gets destroyed, a
FocusChain holder that listens will receive a <code>ZX_EVENTPAIR_PEER_CLOSED</code>
signal on the corresponding ViewRef.</p>
<p>Invalidation. A FocusChain is invalid if one if its ViewRefs is invalid. If
no View is destroyed, Scenic can still cause invalidation by raising a
<code>ZX_USER_SIGNAL_0</code> on the root ViewRef.</p>
<p>Reception. Only certain components may receive a FocusChain, as it
captures global information about the scene graph.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>focus_chain</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.ui.views/'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/#ViewRef'>ViewRef</a>&gt;</code>
            </td>
            <td></td>
        </tr></table>











