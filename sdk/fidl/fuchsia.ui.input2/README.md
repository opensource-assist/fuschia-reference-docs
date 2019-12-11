[TOC]

# fuchsia.ui.input2


## **PROTOCOLS**

## Keyboard {#Keyboard}
*Defined in [fuchsia.ui.input2/keyboard.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input2/keyboard.fidl#12)*

<p>Components may request this service from their namespace to
be notified of physical key events.</p>

### SetListener {#SetListener}

<p>Set key event listener for the specified View.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_ref</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/#ViewRef'>ViewRef</a></code>
            </td>
        </tr><tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='#KeyListener'>KeyListener</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## KeyListener {#KeyListener}
*Defined in [fuchsia.ui.input2/keyboard.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input2/keyboard.fidl#23)*

<p>Client should implement this protocol to get notified of key events.
Returning HANDLED will stop event propagation to other clients.
This notification is triggered on the following conditions:</p>
<ol>
<li>Component is focused (ViewRef is on FocusChain)</li>
<li>Parent Views get the event first, child views last</li>
<li>Client returning HANDLED stops the propagation to subsequent clients</li>
</ol>

### OnKeyEvent {#OnKeyEvent}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>event</code></td>
            <td>
                <code><a class='link' href='#KeyEvent'>KeyEvent</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>

## KeyboardLayoutState {#KeyboardLayoutState}
*Defined in [fuchsia.ui.input2/layout.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input2/layout.fidl#13)*

<p>Input method editors should implement this protocol to populate
<code>KeyEvent.symbol</code> field based on current key layout.</p>

### Watch {#Watch}

<p>Get current key layout. Returns immediately on first call;
subsequent calls return when the value changes.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>layout</code></td>
            <td>
                <code><a class='link' href='#KeyboardLayout'>KeyboardLayout</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### PhysicalKeyMapEntry {#PhysicalKeyMapEntry}
*Defined in [fuchsia.ui.input2/layout.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input2/layout.fidl#42)*



<p>A mapping of a physical key to a key.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>physical_key</code></td>
            <td>
                <code><a class='link' href='#PhysicalKey'>PhysicalKey</a></code>
            </td>
            <td><p>Physical key that's being mapped.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>key</code></td>
            <td>
                <code><a class='link' href='#Key'>Key</a></code>
            </td>
            <td><p>A key to which the physical key is mapped to.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### SemanticKeyMapEntry {#SemanticKeyMapEntry}
*Defined in [fuchsia.ui.input2/layout.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input2/layout.fidl#97)*



<p>A mapping of a key to the semantic meaning.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code><a class='link' href='#Key'>Key</a></code>
            </td>
            <td><p>Key that's being mapped.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>semantic_key</code></td>
            <td>
                <code><a class='link' href='#SemanticKey'>SemanticKey</a></code>
            </td>
            <td><p>Semantic key corresponding to the key.</p>
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### KeyEventPhase {#KeyEventPhase}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.input2/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input2/events.fidl#8)*

<p>Phase of the keyboard key input.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>PRESSED</code></td>
            <td><code>0</code></td>
            <td><p>Key is pressed down.</p>
</td>
        </tr><tr>
            <td><code>RELEASED</code></td>
            <td><code>1</code></td>
            <td><p>Key is released.</p>
</td>
        </tr></table>

### Status {#Status}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.input2/keyboard.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input2/keyboard.fidl#28)*

<p>Return type for clients key events listener.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>HANDLED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>NOT_HANDLED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### Key {#Key}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.input2/keys.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input2/keys.fidl#18)*

<p>A Fuchsia key represents a control that can be pressed or released
such as a button on a keyboard.</p>
<p>Where applicable, the definition of each key is derived from one of the
following sources albeit with a Fuchsia-specific numeric value:</p>
<ul>
<li>USB HID usage codes for usage page 0x0007 (Keyboard/Keypad)</li>
<li>USB HID usage codes for usage page 0x000c (Consumer)</li>
<li>Common but non-standard keys (vendor defined)</li>
</ul>
<p>The example key mappings included in this documentation assume a
US English keyboard layout. Actual behavior varies by layout.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>A</code></td>
            <td><code>1</code></td>
            <td><p>Keyboard a and A
Corresponds to USB HID page 0x0007 usage 0x0004</p>
</td>
        </tr><tr>
            <td><code>B</code></td>
            <td><code>2</code></td>
            <td><p>Keyboard b and B
Corresponds to USB HID page 0x0007 usage 0x0005</p>
</td>
        </tr><tr>
            <td><code>C</code></td>
            <td><code>3</code></td>
            <td><p>Keyboard c and C
Corresponds to USB HID page 0x0007 usage 0x0006</p>
</td>
        </tr><tr>
            <td><code>D</code></td>
            <td><code>4</code></td>
            <td><p>Keyboard d and D
Corresponds to USB HID page 0x0007 usage 0x0007</p>
</td>
        </tr><tr>
            <td><code>E</code></td>
            <td><code>5</code></td>
            <td><p>Keyboard e and E
Corresponds to USB HID page 0x0007 usage 0x0008</p>
</td>
        </tr><tr>
            <td><code>F</code></td>
            <td><code>6</code></td>
            <td><p>Keyboard f and F
Corresponds to USB HID page 0x0007 usage 0x0009</p>
</td>
        </tr><tr>
            <td><code>G</code></td>
            <td><code>7</code></td>
            <td><p>Keyboard g and G
Corresponds to USB HID page 0x0007 usage 0x000a</p>
</td>
        </tr><tr>
            <td><code>H</code></td>
            <td><code>8</code></td>
            <td><p>Keyboard h and H
Corresponds to USB HID page 0x0007 usage 0x000b</p>
</td>
        </tr><tr>
            <td><code>I</code></td>
            <td><code>9</code></td>
            <td><p>Keyboard i and I
Corresponds to USB HID page 0x0007 usage 0x000c</p>
</td>
        </tr><tr>
            <td><code>J</code></td>
            <td><code>10</code></td>
            <td><p>Keyboard j and J
Corresponds to USB HID page 0x0007 usage 0x000d</p>
</td>
        </tr><tr>
            <td><code>K</code></td>
            <td><code>11</code></td>
            <td><p>Keyboard k and K
Corresponds to USB HID page 0x0007 usage 0x000e</p>
</td>
        </tr><tr>
            <td><code>L</code></td>
            <td><code>12</code></td>
            <td><p>Keyboard l and L
Corresponds to USB HID page 0x0007 usage 0x000f</p>
</td>
        </tr><tr>
            <td><code>M</code></td>
            <td><code>13</code></td>
            <td><p>Keyboard m and M
Corresponds to USB HID page 0x0007 usage 0x0010</p>
</td>
        </tr><tr>
            <td><code>N</code></td>
            <td><code>14</code></td>
            <td><p>Keyboard n and N
Corresponds to USB HID page 0x0007 usage 0x0011</p>
</td>
        </tr><tr>
            <td><code>O</code></td>
            <td><code>15</code></td>
            <td><p>Keyboard o and O
Corresponds to USB HID page 0x0007 usage 0x0012</p>
</td>
        </tr><tr>
            <td><code>P</code></td>
            <td><code>16</code></td>
            <td><p>Keyboard p and P
Corresponds to USB HID page 0x0007 usage 0x0013</p>
</td>
        </tr><tr>
            <td><code>Q</code></td>
            <td><code>17</code></td>
            <td><p>Keyboard q and Q
Corresponds to USB HID page 0x0007 usage 0x0014</p>
</td>
        </tr><tr>
            <td><code>R</code></td>
            <td><code>18</code></td>
            <td><p>Keyboard r and R
Corresponds to USB HID page 0x0007 usage 0x0015</p>
</td>
        </tr><tr>
            <td><code>S</code></td>
            <td><code>19</code></td>
            <td><p>Keyboard s and S
Corresponds to USB HID page 0x0007 usage 0x0016</p>
</td>
        </tr><tr>
            <td><code>T</code></td>
            <td><code>20</code></td>
            <td><p>Keyboard t and T
Corresponds to USB HID page 0x0007 usage 0x0017</p>
</td>
        </tr><tr>
            <td><code>U</code></td>
            <td><code>21</code></td>
            <td><p>Keyboard u and U
Corresponds to USB HID page 0x0007 usage 0x0018</p>
</td>
        </tr><tr>
            <td><code>V</code></td>
            <td><code>22</code></td>
            <td><p>Keyboard v and V
Corresponds to USB HID page 0x0007 usage 0x0019</p>
</td>
        </tr><tr>
            <td><code>W</code></td>
            <td><code>23</code></td>
            <td><p>Keyboard w and W
Corresponds to USB HID page 0x0007 usage 0x001a</p>
</td>
        </tr><tr>
            <td><code>X</code></td>
            <td><code>24</code></td>
            <td><p>Keyboard x and X
Corresponds to USB HID page 0x0007 usage 0x001b</p>
</td>
        </tr><tr>
            <td><code>Y</code></td>
            <td><code>25</code></td>
            <td><p>Keyboard y and Y
Corresponds to USB HID page 0x0007 usage 0x001c</p>
</td>
        </tr><tr>
            <td><code>Z</code></td>
            <td><code>26</code></td>
            <td><p>Keyboard z and Z
Corresponds to USB HID page 0x0007 usage 0x001d</p>
</td>
        </tr><tr>
            <td><code>KEY_1</code></td>
            <td><code>27</code></td>
            <td><p>Keyboard 1 and !
Corresponds to USB HID page 0x0007 usage 0x001e</p>
</td>
        </tr><tr>
            <td><code>KEY_2</code></td>
            <td><code>28</code></td>
            <td><p>Keyboard 2 and @
Corresponds to USB HID page 0x0007 usage 0x001f</p>
</td>
        </tr><tr>
            <td><code>KEY_3</code></td>
            <td><code>29</code></td>
            <td><p>Keyboard 3 and #
Corresponds to USB HID page 0x0007 usage 0x0020</p>
</td>
        </tr><tr>
            <td><code>KEY_4</code></td>
            <td><code>30</code></td>
            <td><p>Keyboard 4 and $
Corresponds to USB HID page 0x0007 usage 0x0021</p>
</td>
        </tr><tr>
            <td><code>KEY_5</code></td>
            <td><code>31</code></td>
            <td><p>Keyboard 5 and %
Corresponds to USB HID page 0x0007 usage 0x0022</p>
</td>
        </tr><tr>
            <td><code>KEY_6</code></td>
            <td><code>32</code></td>
            <td><p>Keyboard 6 and ^
Corresponds to USB HID page 0x0007 usage 0x0023</p>
</td>
        </tr><tr>
            <td><code>KEY_7</code></td>
            <td><code>33</code></td>
            <td><p>Keyboard 7 and &amp;
Corresponds to USB HID page 0x0007 usage 0x0024</p>
</td>
        </tr><tr>
            <td><code>KEY_8</code></td>
            <td><code>34</code></td>
            <td><p>Keyboard 8 and *
Corresponds to USB HID page 0x0007 usage 0x0025</p>
</td>
        </tr><tr>
            <td><code>KEY_9</code></td>
            <td><code>35</code></td>
            <td><p>Keyboard 9 and (
Corresponds to USB HID page 0x0007 usage 0x0026</p>
</td>
        </tr><tr>
            <td><code>KEY_0</code></td>
            <td><code>36</code></td>
            <td><p>Keyboard 0 and )
Corresponds to USB HID page 0x0007 usage 0x0027</p>
</td>
        </tr><tr>
            <td><code>ENTER</code></td>
            <td><code>37</code></td>
            <td><p>Keyboard Enter (Return)
Corresponds to USB HID page 0x0007 usage 0x0028</p>
</td>
        </tr><tr>
            <td><code>ESCAPE</code></td>
            <td><code>38</code></td>
            <td><p>Keyboard Escape
Corresponds to USB HID page 0x0007 usage 0x0029</p>
</td>
        </tr><tr>
            <td><code>BACKSPACE</code></td>
            <td><code>39</code></td>
            <td><p>Keyboard Backspace (Backward Delete)
Corresponds to USB HID page 0x0007 usage 0x002a</p>
</td>
        </tr><tr>
            <td><code>TAB</code></td>
            <td><code>40</code></td>
            <td><p>Keyboard Tab
Corresponds to USB HID page 0x0007 usage 0x002b</p>
</td>
        </tr><tr>
            <td><code>SPACE</code></td>
            <td><code>41</code></td>
            <td><p>Keyboard Spacebar
Corresponds to USB HID page 0x0007 usage 0x002c</p>
</td>
        </tr><tr>
            <td><code>MINUS</code></td>
            <td><code>42</code></td>
            <td><p>Keyboard - and (underscore)
Corresponds to USB HID page 0x0007 usage 0x002d</p>
</td>
        </tr><tr>
            <td><code>EQUALS</code></td>
            <td><code>43</code></td>
            <td><p>Keyboard = and +
Corresponds to USB HID page 0x0007 usage 0x002e</p>
</td>
        </tr><tr>
            <td><code>LEFT_BRACE</code></td>
            <td><code>44</code></td>
            <td><p>Keyboard [ and {
Corresponds to USB HID page 0x0007 usage 0x002f</p>
</td>
        </tr><tr>
            <td><code>RIGHT_BRACE</code></td>
            <td><code>45</code></td>
            <td><p>Keyboard ] and }
Corresponds to USB HID page 0x0007 usage 0x0030</p>
</td>
        </tr><tr>
            <td><code>BACKSLASH</code></td>
            <td><code>46</code></td>
            <td><p>Keyboard \ and |
Corresponds to USB HID page 0x0007 usage 0x0031</p>
</td>
        </tr><tr>
            <td><code>NON_US_HASH</code></td>
            <td><code>47</code></td>
            <td><p>Keyboard Non-US # and ~
Corresponds to USB HID page 0x0007 usage 0x0032</p>
</td>
        </tr><tr>
            <td><code>SEMICOLON</code></td>
            <td><code>48</code></td>
            <td><p>Keyboard ; and :
Corresponds to USB HID page 0x0007 usage 0x0033</p>
</td>
        </tr><tr>
            <td><code>APOSTROPHE</code></td>
            <td><code>49</code></td>
            <td><p>Keyboard ' and &quot;
Corresponds to USB HID page 0x0007 usage 0x0034</p>
</td>
        </tr><tr>
            <td><code>GRAVE_ACCENT</code></td>
            <td><code>50</code></td>
            <td><p>Keyboard Grave Accent and Tilde
Corresponds to USB HID page 0x0007 usage 0x0035</p>
</td>
        </tr><tr>
            <td><code>COMMA</code></td>
            <td><code>51</code></td>
            <td><p>Keyboard , and &lt;
Corresponds to USB HID page 0x0007 usage 0x0036</p>
</td>
        </tr><tr>
            <td><code>DOT</code></td>
            <td><code>52</code></td>
            <td><p>Keyboard . and &gt;
Corresponds to USB HID page 0x0007 usage 0x0037</p>
</td>
        </tr><tr>
            <td><code>SLASH</code></td>
            <td><code>53</code></td>
            <td><p>Keyboard / and ?
Corresponds to USB HID page 0x0007 usage 0x0038</p>
</td>
        </tr><tr>
            <td><code>CAPS_LOCK</code></td>
            <td><code>54</code></td>
            <td><p>Keyboard Caps Lock
Corresponds to USB HID page 0x0007 usage 0x0039</p>
</td>
        </tr><tr>
            <td><code>F1</code></td>
            <td><code>55</code></td>
            <td><p>Keyboard F1
Corresponds to USB HID page 0x0007 usage 0x003a</p>
</td>
        </tr><tr>
            <td><code>F2</code></td>
            <td><code>56</code></td>
            <td><p>Keyboard F2
Corresponds to USB HID page 0x0007 usage 0x003b</p>
</td>
        </tr><tr>
            <td><code>F3</code></td>
            <td><code>57</code></td>
            <td><p>Keyboard F3
Corresponds to USB HID page 0x0007 usage 0x003c</p>
</td>
        </tr><tr>
            <td><code>F4</code></td>
            <td><code>58</code></td>
            <td><p>Keyboard F4
Corresponds to USB HID page 0x0007 usage 0x003d</p>
</td>
        </tr><tr>
            <td><code>F5</code></td>
            <td><code>59</code></td>
            <td><p>Keyboard F5
Corresponds to USB HID page 0x0007 usage 0x003e</p>
</td>
        </tr><tr>
            <td><code>F6</code></td>
            <td><code>60</code></td>
            <td><p>Keyboard F6
Corresponds to USB HID page 0x0007 usage 0x003f</p>
</td>
        </tr><tr>
            <td><code>F7</code></td>
            <td><code>61</code></td>
            <td><p>Keyboard F7
Corresponds to USB HID page 0x0007 usage 0x0040</p>
</td>
        </tr><tr>
            <td><code>F8</code></td>
            <td><code>62</code></td>
            <td><p>Keyboard F8
Corresponds to USB HID page 0x0007 usage 0x0041</p>
</td>
        </tr><tr>
            <td><code>F9</code></td>
            <td><code>63</code></td>
            <td><p>Keyboard F9
Corresponds to USB HID page 0x0007 usage 0x0042</p>
</td>
        </tr><tr>
            <td><code>F10</code></td>
            <td><code>64</code></td>
            <td><p>Keyboard F10
Corresponds to USB HID page 0x0007 usage 0x0043</p>
</td>
        </tr><tr>
            <td><code>F11</code></td>
            <td><code>65</code></td>
            <td><p>Keyboard F11
Corresponds to USB HID page 0x0007 usage 0x0044</p>
</td>
        </tr><tr>
            <td><code>F12</code></td>
            <td><code>66</code></td>
            <td><p>Keyboard F12
Corresponds to USB HID page 0x0007 usage 0x0045</p>
</td>
        </tr><tr>
            <td><code>PRINT_SCREEN</code></td>
            <td><code>67</code></td>
            <td><p>Keyboard Print Screen
Corresponds to USB HID page 0x0007 usage 0x0046</p>
</td>
        </tr><tr>
            <td><code>SCROLL_LOCK</code></td>
            <td><code>68</code></td>
            <td><p>Keyboard Scroll Lock
Corresponds to USB HID page 0x0007 usage 0x0047</p>
</td>
        </tr><tr>
            <td><code>PAUSE</code></td>
            <td><code>69</code></td>
            <td><p>Keyboard Pause
Corresponds to USB HID page 0x0007 usage 0x0048</p>
</td>
        </tr><tr>
            <td><code>INSERT</code></td>
            <td><code>70</code></td>
            <td><p>Keyboard Insert
Corresponds to USB HID page 0x0007 usage 0x0049</p>
</td>
        </tr><tr>
            <td><code>HOME</code></td>
            <td><code>71</code></td>
            <td><p>Keyboard Home
Corresponds to USB HID page 0x0007 usage 0x004a</p>
</td>
        </tr><tr>
            <td><code>PAGE_UP</code></td>
            <td><code>72</code></td>
            <td><p>Keyboard Page Up
Corresponds to USB HID page 0x0007 usage 0x004b</p>
</td>
        </tr><tr>
            <td><code>DELETE</code></td>
            <td><code>73</code></td>
            <td><p>Keyboard Forward Delete
Corresponds to USB HID page 0x0007 usage 0x004c</p>
</td>
        </tr><tr>
            <td><code>END</code></td>
            <td><code>74</code></td>
            <td><p>Keyboard End
Corresponds to USB HID page 0x0007 usage 0x004d</p>
</td>
        </tr><tr>
            <td><code>PAGE_DOWN</code></td>
            <td><code>75</code></td>
            <td><p>Keyboard Page Down
Corresponds to USB HID page 0x0007 usage 0x004e</p>
</td>
        </tr><tr>
            <td><code>RIGHT</code></td>
            <td><code>76</code></td>
            <td><p>Keyboard Right Arrow
Corresponds to USB HID page 0x0007 usage 0x004f</p>
</td>
        </tr><tr>
            <td><code>LEFT</code></td>
            <td><code>77</code></td>
            <td><p>Keyboard Left Arrow
Corresponds to USB HID page 0x0007 usage 0x0050</p>
</td>
        </tr><tr>
            <td><code>DOWN</code></td>
            <td><code>78</code></td>
            <td><p>Keyboard Down Arrow
Corresponds to USB HID page 0x0007 usage 0x0051</p>
</td>
        </tr><tr>
            <td><code>UP</code></td>
            <td><code>79</code></td>
            <td><p>Keyboard Up Arrow
Corresponds to USB HID page 0x0007 usage 0x0052</p>
</td>
        </tr><tr>
            <td><code>NON_US_BACKSLASH</code></td>
            <td><code>80</code></td>
            <td><p>Keyboard Non-US \ and |
Corresponds to USB HID page 0x0007 usage 0x0064</p>
</td>
        </tr><tr>
            <td><code>LEFT_CTRL</code></td>
            <td><code>81</code></td>
            <td><p>Keyboard Left Control
Corresponds to USB HID page 0x0007 usage 0x00e0</p>
</td>
        </tr><tr>
            <td><code>LEFT_SHIFT</code></td>
            <td><code>82</code></td>
            <td><p>Keyboard Left Shift
Corresponds to USB HID page 0x0007 usage 0x00e1</p>
</td>
        </tr><tr>
            <td><code>LEFT_ALT</code></td>
            <td><code>83</code></td>
            <td><p>Keyboard Left Alt
Corresponds to USB HID page 0x0007 usage 0x00e2</p>
</td>
        </tr><tr>
            <td><code>LEFT_META</code></td>
            <td><code>84</code></td>
            <td><p>Keyboard Left GUI (Meta, Windows)
Corresponds to USB HID page 0x0007 usage 0x00e3</p>
</td>
        </tr><tr>
            <td><code>RIGHT_CTRL</code></td>
            <td><code>85</code></td>
            <td><p>Keyboard Right Control
Corresponds to USB HID page 0x0007 usage 0x00e4</p>
</td>
        </tr><tr>
            <td><code>RIGHT_SHIFT</code></td>
            <td><code>86</code></td>
            <td><p>Keyboard Right Shift
Corresponds to USB HID page 0x0007 usage 0x00e5</p>
</td>
        </tr><tr>
            <td><code>RIGHT_ALT</code></td>
            <td><code>87</code></td>
            <td><p>Keyboard Right Alt
Corresponds to USB HID page 0x0007 usage 0x00e6</p>
</td>
        </tr><tr>
            <td><code>RIGHT_META</code></td>
            <td><code>88</code></td>
            <td><p>Keyboard Right GUI (Meta, Windows)
Corresponds to USB HID page 0x0007 usage 0x00e7</p>
</td>
        </tr><tr>
            <td><code>MENU</code></td>
            <td><code>89</code></td>
            <td><p>Keyboard Menu
Corresponds to USB HID page 0x0007 usage 0x0076</p>
</td>
        </tr><tr>
            <td><code>NUM_LOCK</code></td>
            <td><code>512</code></td>
            <td><p>Keypad Num Lock and Clear
Corresponds to USB HID page 0x0007 usage 0x0053</p>
</td>
        </tr><tr>
            <td><code>KEYPAD_SLASH</code></td>
            <td><code>513</code></td>
            <td><p>Keypad /
Corresponds to USB HID page 0x0007 usage 0x0054</p>
</td>
        </tr><tr>
            <td><code>KEYPAD_ASTERISK</code></td>
            <td><code>514</code></td>
            <td><p>Keypad *
Corresponds to USB HID page 0x0007 usage 0x0055</p>
</td>
        </tr><tr>
            <td><code>KEYPAD_MINUS</code></td>
            <td><code>515</code></td>
            <td><p>Keypad -
Corresponds to USB HID page 0x0007 usage 0x0056</p>
</td>
        </tr><tr>
            <td><code>KEYPAD_PLUS</code></td>
            <td><code>516</code></td>
            <td><p>Keypad +
Corresponds to USB HID page 0x0007 usage 0x0057</p>
</td>
        </tr><tr>
            <td><code>KEYPAD_ENTER</code></td>
            <td><code>517</code></td>
            <td><p>Keypad ENTER
Corresponds to USB HID page 0x0007 usage 0x0058</p>
</td>
        </tr><tr>
            <td><code>KEYPAD_1</code></td>
            <td><code>518</code></td>
            <td><p>Keypad 1 and End
Corresponds to USB HID page 0x0007 usage 0x0059</p>
</td>
        </tr><tr>
            <td><code>KEYPAD_2</code></td>
            <td><code>519</code></td>
            <td><p>Keypad 2 and Down Arrow
Corresponds to USB HID page 0x0007 usage 0x005a</p>
</td>
        </tr><tr>
            <td><code>KEYPAD_3</code></td>
            <td><code>520</code></td>
            <td><p>Keypad 3 and Page Down
Corresponds to USB HID page 0x0007 usage 0x005b</p>
</td>
        </tr><tr>
            <td><code>KEYPAD_4</code></td>
            <td><code>521</code></td>
            <td><p>Keypad 4 and Left Arrow
Corresponds to USB HID page 0x0007 usage 0x005c</p>
</td>
        </tr><tr>
            <td><code>KEYPAD_5</code></td>
            <td><code>522</code></td>
            <td><p>Keypad 5
Corresponds to USB HID page 0x0007 usage 0x005d</p>
</td>
        </tr><tr>
            <td><code>KEYPAD_6</code></td>
            <td><code>523</code></td>
            <td><p>Keypad 6 and Right Arrow
Corresponds to USB HID page 0x0007 usage 0x005e</p>
</td>
        </tr><tr>
            <td><code>KEYPAD_7</code></td>
            <td><code>524</code></td>
            <td><p>Keypad 7 and Home
Corresponds to USB HID page 0x0007 usage 0x005f</p>
</td>
        </tr><tr>
            <td><code>KEYPAD_8</code></td>
            <td><code>525</code></td>
            <td><p>Keypad 8 and Up Arrow
Corresponds to USB HID page 0x0007 usage 0x0060</p>
</td>
        </tr><tr>
            <td><code>KEYPAD_9</code></td>
            <td><code>526</code></td>
            <td><p>Keypad 9 and Page Up
Corresponds to USB HID page 0x0007 usage 0x0061</p>
</td>
        </tr><tr>
            <td><code>KEYPAD_0</code></td>
            <td><code>527</code></td>
            <td><p>Keypad 0 and Insert
Corresponds to USB HID page 0x0007 usage 0x0062</p>
</td>
        </tr><tr>
            <td><code>KEYPAD_DOT</code></td>
            <td><code>528</code></td>
            <td><p>Keypad . and Delete
Corresponds to USB HID page 0x0007 usage 0x0063</p>
</td>
        </tr><tr>
            <td><code>KEYPAD_EQUALS</code></td>
            <td><code>529</code></td>
            <td></td>
        </tr><tr>
            <td><code>MEDIA_MUTE</code></td>
            <td><code>768</code></td>
            <td></td>
        </tr><tr>
            <td><code>MEDIA_VOLUME_INCREMENT</code></td>
            <td><code>769</code></td>
            <td></td>
        </tr><tr>
            <td><code>MEDIA_VOLUME_DECREMENT</code></td>
            <td><code>770</code></td>
            <td></td>
        </tr></table>

### SemanticKeyAction {#SemanticKeyAction}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.input2/semantic_keys.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input2/semantic_keys.fidl#11)*

<p>Semantic Key represents the meaning of a non-symbolic key on a keyboard.</p>
<p>Definition of each key is derived from W3C named values of a key attribute:
https://www.w3.org/TR/uievents-key/#named-key-attribute-values</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ALT</code></td>
            <td><code>1</code></td>
            <td><p>The Alt (Alternative) key.
This key enables the alternate modifier function for interpreting
concurrent or subsequent keyboard input.
This key value is also used for the Apple Option key.</p>
</td>
        </tr><tr>
            <td><code>ALT_GRAPH</code></td>
            <td><code>2</code></td>
            <td><p>The Alternate Graphics (AltGr or AltGraph) key.
This key is used enable the ISO Level 3 shift modifier (the standard
Shift key is the level 2 modifier). See [ISO9995-1].</p>
</td>
        </tr><tr>
            <td><code>CAPS_LOCK</code></td>
            <td><code>3</code></td>
            <td><p>The Caps Lock (Capital) key.
Toggle capital character lock function for interpreting subsequent
keyboard input event.</p>
</td>
        </tr><tr>
            <td><code>CONTROL</code></td>
            <td><code>4</code></td>
            <td><p>The Control or Ctrl key, to enable control modifier function for
interpreting concurrent or subsequent keyboard input.</p>
</td>
        </tr><tr>
            <td><code>META</code></td>
            <td><code>5</code></td>
            <td><p>The Meta key, to enable meta modifier function for interpreting
concurrent or subsequent keyboard input.
This key value is used for the Windows Logo key and the Apple Command
or ⌘ key.</p>
</td>
        </tr><tr>
            <td><code>NUM_LOCK</code></td>
            <td><code>6</code></td>
            <td><p>The NumLock or Number Lock key, to toggle numpad mode function for
interpreting subsequent keyboard input.</p>
</td>
        </tr><tr>
            <td><code>SCROLL_LOCK</code></td>
            <td><code>7</code></td>
            <td><p>&quot;ScrollLock&quot; The Scroll Lock key, to toggle between scrolling and cursor
movement modes.</p>
</td>
        </tr><tr>
            <td><code>SHIFT</code></td>
            <td><code>8</code></td>
            <td><p>The Shift key, to enable shift modifier function for interpreting
concurrent or subsequent keyboard input.</p>
</td>
        </tr><tr>
            <td><code>ARROW_DOWN</code></td>
            <td><code>33</code></td>
            <td><p>The down arrow key, to navigate or traverse downward.</p>
</td>
        </tr><tr>
            <td><code>ARROW_LEFT</code></td>
            <td><code>34</code></td>
            <td><p>The left arrow key, to navigate or traverse leftward.</p>
</td>
        </tr><tr>
            <td><code>ARROW_RIGHT</code></td>
            <td><code>35</code></td>
            <td><p>The right arrow key, to navigate or traverse rightward.</p>
</td>
        </tr><tr>
            <td><code>ARROW_UP</code></td>
            <td><code>36</code></td>
            <td><p>The up arrow key, to navigate or traverse upward.</p>
</td>
        </tr><tr>
            <td><code>END</code></td>
            <td><code>37</code></td>
            <td><p>The End key, used with keyboard entry to go to the end of content.</p>
</td>
        </tr><tr>
            <td><code>HOME</code></td>
            <td><code>38</code></td>
            <td><p>The Home key, used with keyboard entry, to go to start of content.
For the mobile phone Home key (which goes to the phone’s main screen),
use &quot;GO_HOME&quot;.</p>
</td>
        </tr><tr>
            <td><code>PAGE_DOWN</code></td>
            <td><code>39</code></td>
            <td></td>
        </tr><tr>
            <td><code>PAGE_UP</code></td>
            <td><code>40</code></td>
            <td></td>
        </tr><tr>
            <td><code>ENTER</code></td>
            <td><code>49</code></td>
            <td><p>The Enter or ↵ key, to activate current selection or accept current input.
This key value is also used for the Return (Macintosh numpad) key.</p>
</td>
        </tr><tr>
            <td><code>TAB</code></td>
            <td><code>50</code></td>
            <td><p>The Horizontal Tabulation Tab key.</p>
</td>
        </tr><tr>
            <td><code>BACKSPACE</code></td>
            <td><code>65</code></td>
            <td><p>The Backspace key. This key value is also used for the key labeled Delete
on MacOS keyboards.</p>
</td>
        </tr><tr>
            <td><code>DELETE</code></td>
            <td><code>66</code></td>
            <td><p>The Delete (Del) Key.
This key value is also used for the key labeled Delete on MacOS keyboards
when modified by the Fn key.</p>
</td>
        </tr><tr>
            <td><code>INSERT</code></td>
            <td><code>67</code></td>
            <td><p>The Insert (Ins) key, to toggle between text modes for insertion or
overtyping.</p>
</td>
        </tr><tr>
            <td><code>F1</code></td>
            <td><code>97</code></td>
            <td></td>
        </tr><tr>
            <td><code>F2</code></td>
            <td><code>98</code></td>
            <td></td>
        </tr><tr>
            <td><code>F3</code></td>
            <td><code>99</code></td>
            <td></td>
        </tr><tr>
            <td><code>F4</code></td>
            <td><code>100</code></td>
            <td></td>
        </tr><tr>
            <td><code>F5</code></td>
            <td><code>101</code></td>
            <td></td>
        </tr><tr>
            <td><code>F6</code></td>
            <td><code>102</code></td>
            <td></td>
        </tr><tr>
            <td><code>F7</code></td>
            <td><code>103</code></td>
            <td></td>
        </tr><tr>
            <td><code>F8</code></td>
            <td><code>104</code></td>
            <td></td>
        </tr><tr>
            <td><code>F9</code></td>
            <td><code>105</code></td>
            <td></td>
        </tr><tr>
            <td><code>F10</code></td>
            <td><code>106</code></td>
            <td></td>
        </tr><tr>
            <td><code>F11</code></td>
            <td><code>107</code></td>
            <td></td>
        </tr><tr>
            <td><code>F12</code></td>
            <td><code>108</code></td>
            <td></td>
        </tr><tr>
            <td><code>CONTEXT_MENU</code></td>
            <td><code>129</code></td>
            <td><p>Show the application’s context menu.
This key is commonly found between the right Meta key and the right
Control key.</p>
</td>
        </tr><tr>
            <td><code>ESCAPE</code></td>
            <td><code>130</code></td>
            <td><p>The Esc key. This key was originally used to initiate an escape sequence,
but is now more generally used to exit or &quot;escape&quot; the current context,
such as closing a dialog or exiting full screen mode.</p>
</td>
        </tr><tr>
            <td><code>GO_BACK</code></td>
            <td><code>177</code></td>
            <td><p>The Back key.</p>
</td>
        </tr><tr>
            <td><code>GO_HOME</code></td>
            <td><code>178</code></td>
            <td><p>The Home key, which goes to the phone’s main screen.</p>
</td>
        </tr></table>



## **TABLES**

### KeyEvent {#KeyEvent}


*Defined in [fuchsia.ui.input2/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input2/events.fidl#44)*

<p>Keyboard event is generated to reflect key input.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>key</code></td>
            <td>
                <code><a class='link' href='#Key'>Key</a></code>
            </td>
            <td><p>The key that was pressed or released, taking the keyboard layout into account.</p>
<p>Use this value for the following purposes:</p>
<ul>
<li>interpreting keyboard shortcuts such as CTRL+C</li>
</ul>
<p>The input system derives this value from <code>physical_key</code> by consulting the
physical key map of the <code>KeyboardLayout</code> that was active for the keyboard when
when the key was pressed.  Note that the same value will be reported when
the key is released even if the keyboard layout changes in the interim between press
and release.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>phase</code></td>
            <td>
                <code><a class='link' href='#KeyEventPhase'>KeyEventPhase</a></code>
            </td>
            <td><p>Phase of input.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>modifiers</code></td>
            <td>
                <code><a class='link' href='#Modifiers'>Modifiers</a></code>
            </td>
            <td><p>Modifier keys being held.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>semantic_key</code></td>
            <td>
                <code><a class='link' href='#SemanticKey'>SemanticKey</a></code>
            </td>
            <td><p>The semantic meaning of the key that was pressed or released, taking the keyboard
layout and modifiers into account.</p>
<p>Use this value for the following purposes:</p>
<ul>
<li>typing text when implementing an input method editor (IME) or when IME services
are not available (this won’t work for languages that require composition)</li>
</ul>
<p>The input system derives this value from the combination of <code>physical_key</code> and
<code>modifiers</code> by consulting the key symbol map of <code>KeyboardLayout</code> that was active
for the keyboard when the key was pressed. Note that the same value will be reported
when the key is released even if the keyboard layout or modifiers change in the
interim between press and release.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>physical_key</code></td>
            <td>
                <code><a class='link' href='#PhysicalKey'>PhysicalKey</a></code>
            </td>
            <td><p>Identifies the physical key, ignoring modifiers and layout.</p>
<p>Use this value for the following purposes:</p>
<ul>
<li>applying keyboard layout translations</li>
<li>synthesizing input events into virtual machines, since VMs will do own layout mapping</li>
</ul>
<p>The input system derives this value from the data reported by the keyboard itself
without taking into account the keyboard’s current <code>KeyboardLayout</code> or modifiers.</p>
</td>
        </tr></table>

### KeyboardLayout {#KeyboardLayout}


*Defined in [fuchsia.ui.input2/layout.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input2/layout.fidl#28)*

<p>Collection of key maps.</p>
<p>A physical key is first converted to key using <code>key_map</code>.
The key is then used to populate <code>symbol</code> using <code>symbol_map</code>.
Maps in <code>KeySymbolMap</code> should be searched for the key mapping in the order
they are included.
First key mapping found in an applicable map should be used.
Only maps with matching modifiers should be used.
See <code>KeySymbolMap</code> for modifiers matching criteria and examples.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>key_map</code></td>
            <td>
                <code><a class='link' href='#PhysicalKeyMap'>PhysicalKeyMap</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>semantic_key_map</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#SemanticKeyMap'>SemanticKeyMap</a>&gt;[64]</code>
            </td>
            <td></td>
        </tr></table>

### PhysicalKeyMap {#PhysicalKeyMap}


*Defined in [fuchsia.ui.input2/layout.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input2/layout.fidl#36)*

<p>Key map describes a conversion of a physical key to a key.
Physical keys not included here are translated directly into keys.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>entries</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#PhysicalKeyMapEntry'>PhysicalKeyMapEntry</a>&gt;[1024]</code>
            </td>
            <td><p>Collection of keys that should be explicitly mapped.</p>
</td>
        </tr></table>

### SemanticKeyMap {#SemanticKeyMap}


*Defined in [fuchsia.ui.input2/layout.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input2/layout.fidl#79)*

<p>Key map describes a conversion of a key to symbol representation.</p>
<p>The map should be validated using key event modifier states.
Map is applied if every modifier in the 'modifiers' list is active,
and all other active modifiers are members of the 'optional_modifiers' list.
If a modifier is enabled and not listed in neither <code>modifiers</code> nor
<code>optional_modifiers</code>, the map should be ignored.</p>
<p>Example:
Keyboard has NumLock and CapsLock enabled, and user presses Shift + Key.A</p>
<p>Map1:
modifiers: &quot;CapsLock&quot;
optional_modifiers: &quot;NumLock&quot;
Map2:
modifiers: &quot;Shift&quot;,
optional_modifiers: &quot;NumLock&quot;, &quot;CapsLock&quot;, &quot;ScrollLock&quot;
Map3:
modifiers: None
optional_modifiers: &quot;Shift&quot;, &quot;CapsLock&quot;</p>
<p>Map1 should be ignored, since &quot;Shift&quot; is pressed but is not included in
<code>modifiers</code> or <code>optional_modifiers</code>.</p>
<p>Map2 should be searched, since required &quot;Shift&quot; is enabled, and all other
enabled modifiers are included in <code>optional_modifiers</code>.</p>
<p>Map3 should be ignored, since &quot;NumLock&quot; is enabled but not included in
<code>modifiers</code> or <code>optional_modifiers</code>.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>modifiers</code></td>
            <td>
                <code><a class='link' href='#Modifiers'>Modifiers</a></code>
            </td>
            <td><p>Combination of modifiers required for this map to be applied.
E.g. if CAPS_LOCK bit is set for this map, the map will be
applied if the Caps Lock state is ON.
Otherwise this map will be ignored if Caps Lock is off.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>optional_modifiers</code></td>
            <td>
                <code><a class='link' href='#Modifiers'>Modifiers</a></code>
            </td>
            <td><p>Combination of modifiers that may be enabled for this map to be applied.
E.g. if CAPS_LOCK bit is set for this map, the map will be
applied if Caps Lock state is ON.
Also it may be applied if Caps Lock is off.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>entries</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#SemanticKeyMapEntry'>SemanticKeyMapEntry</a>&gt;[1024]</code>
            </td>
            <td><p>Collection of key to semantic meaning mappings.</p>
</td>
        </tr></table>





## **XUNIONS**

### SemanticKey {#SemanticKey}
*Defined in [fuchsia.ui.input2/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input2/events.fidl#29)*

<p>Semantic for a physical key typed by the user.
For letter or symbolic keys, is a string representation of the key typed.
For non-symbolic keys, is a SemanticKeyAction value corresponding to the key pressed.</p>
<p>Examples:
Key.A:
&quot;a&quot; or &quot;A&quot; in US key layout, depending on CapsLock and Shift
Key.SPACE:
&quot; &quot;
Key.TAB:
SemanticKeyAction.TAB
Key.GRAVE_ACCENT:
&quot;`&quot; or &quot;]&quot; or &quot;&lt;&quot;, depending on key layout</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>symbol</code></td>
            <td>
                <code>string[16]</code>
            </td>
            <td><p>For symbolic keys: string representing character typed.</p>
</td>
        </tr><tr>
            <td><code>action</code></td>
            <td>
                <code><a class='link' href='#SemanticKeyAction'>SemanticKeyAction</a></code>
            </td>
            <td><p>For non-symbolic keys: meaning of the key pressed.</p>
</td>
        </tr></table>



## **BITS**

### Modifiers {#Modifiers}
Type: <code>uint32</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>SHIFT</td>
            <td>1</td>
            <td><p>Applies when either the <code>LEFT_SHIFT</code> or <code>RIGHT_SHIFT</code> modifier is pressed.</p>
</td>
        </tr><tr>
            <td>LEFT_SHIFT</td>
            <td>2</td>
            <td><p>Applies when the <code>LEFT_SHIFT</code> modifier is pressed.</p>
</td>
        </tr><tr>
            <td>RIGHT_SHIFT</td>
            <td>4</td>
            <td><p>Applies when the <code>RIGHT_SHIFT</code> modifier is pressed.</p>
</td>
        </tr><tr>
            <td>CONTROL</td>
            <td>8</td>
            <td><p>Applies when either the <code>LEFT_CONTROL</code> or <code>RIGHT_CONTROL</code> modifier is pressed.</p>
</td>
        </tr><tr>
            <td>LEFT_CONTROL</td>
            <td>16</td>
            <td><p>Applies when the <code>LEFT_CONTROL</code> modifier is pressed.</p>
</td>
        </tr><tr>
            <td>RIGHT_CONTROL</td>
            <td>32</td>
            <td><p>Applies when the <code>RIGHT_CONTROL</code> modifier is pressed.</p>
</td>
        </tr><tr>
            <td>ALT</td>
            <td>64</td>
            <td><p>Applies when either the <code>LEFT_ALT</code> or <code>RIGHT_ALT</code> modifier is pressed.</p>
</td>
        </tr><tr>
            <td>LEFT_ALT</td>
            <td>128</td>
            <td><p>Applies when the <code>LEFT_ALT</code> modifier is pressed.</p>
</td>
        </tr><tr>
            <td>RIGHT_ALT</td>
            <td>256</td>
            <td><p>Applies when the <code>RIGHT_ALT</code> modifier is pressed.</p>
</td>
        </tr><tr>
            <td>META</td>
            <td>512</td>
            <td><p>Applies when either the <code>LEFT_META</code> or <code>RIGHT_META</code> modifier is pressed.</p>
</td>
        </tr><tr>
            <td>LEFT_META</td>
            <td>1024</td>
            <td><p>Applies when the <code>LEFT_META</code> modifier is pressed.</p>
</td>
        </tr><tr>
            <td>RIGHT_META</td>
            <td>2048</td>
            <td><p>Applies when the <code>RIGHT_META</code> modifier is pressed.</p>
</td>
        </tr><tr>
            <td>CAPS_LOCK</td>
            <td>4096</td>
            <td><p>Applies when the <code>CAPS_LOCK</code> modifier is locked.</p>
</td>
        </tr><tr>
            <td>NUM_LOCK</td>
            <td>8192</td>
            <td><p>Applies when the <code>NUM_LOCK</code> modifier is locked.</p>
</td>
        </tr><tr>
            <td>SCROLL_LOCK</td>
            <td>16384</td>
            <td><p>Applies when the <code>SCROLL_LOCK</code> modifier is locked.</p>
</td>
        </tr></table>



## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="MAX_ENTRIES_PER_MAP">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input2/layout.fidl#7">MAX_ENTRIES_PER_MAP</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr id="MAX_MAPS_PER_LAYOUT">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input2/layout.fidl#8">MAX_MAPS_PER_LAYOUT</a></td>
            <td>
                    <code>64</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    
</table>



## **TYPE ALIASES**

<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr id="PhysicalKey">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input2/events.fidl#41">PhysicalKey</a></td>
            <td>
                <code>fuchsia.ui.input2/Key</code></td>
            <td><p>Direct key mapping from hardware code (USB HID).</p>
<p>Example:
Key.Q for USB HID page 0x0007 usage 0x0014</p>
</td>
        </tr></table>

