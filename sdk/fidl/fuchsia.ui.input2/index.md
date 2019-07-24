Project: /_project.yaml
Book: /_book.yaml

# fuchsia.ui.input2


## **PROTOCOLS**

## Keyboard {:#Keyboard}
*Defined in [fuchsia.ui.input2/keyboard.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input2/keyboard.fidl#12)*

 Components may request this service from their namespace to
 be notified of physical key events.

### SetListener {:#SetListener}

 Set key event listener for the specified View.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_ref</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#ViewRef'>ViewRef</a></code>
            </td>
        </tr><tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='#KeyListener'>KeyListener</a></code>
            </td>
        </tr></table>



## KeyListener {:#KeyListener}
*Defined in [fuchsia.ui.input2/keyboard.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input2/keyboard.fidl#23)*

 Client should implement this protocol to get notified of key events.
 Returning HANDLED will stop event propagation to other clients.
 This notification is triggered on the following conditions:
 1. Component is focused (ViewRef is on FocusChain)
 2. Parent Views get the event first, child views last
 3. Client returning HANDLED stops the propagation to subsequent clients

### OnKeyEvent {:#OnKeyEvent}


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





## **ENUMS**

### KeyEventPhase {:#KeyEventPhase}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.input2/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input2/events.fidl#8)*

 Phase of the keyboard key input.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>PRESSED</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>RELEASED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### Status {:#Status}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.input2/keyboard.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input2/keyboard.fidl#28)*

 Return type for clients key events listener.


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

### Key {:#Key}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.input2/keys.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input2/keys.fidl#18)*

 A Fuchsia key represents a control that can be pressed or released
 such as a button on a keyboard.

 Where applicable, the definition of each key is derived from one of the
 following sources albeit with a Fuchsia-specific numeric value:
 - USB HID usage codes for usage page 0x0007 (Keyboard/Keypad)
 - USB HID usage codes for usage page 0x000c (Consumer)
 - Common but non-standard keys (vendor defined)

 The example key mappings included in this documentation assume a
 US English keyboard layout. Actual behavior varies by layout.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>A</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>B</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>C</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>D</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>E</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>F</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>G</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr><tr>
            <td><code>H</code></td>
            <td><code>8</code></td>
            <td></td>
        </tr><tr>
            <td><code>I</code></td>
            <td><code>9</code></td>
            <td></td>
        </tr><tr>
            <td><code>J</code></td>
            <td><code>10</code></td>
            <td></td>
        </tr><tr>
            <td><code>K</code></td>
            <td><code>11</code></td>
            <td></td>
        </tr><tr>
            <td><code>L</code></td>
            <td><code>12</code></td>
            <td></td>
        </tr><tr>
            <td><code>M</code></td>
            <td><code>13</code></td>
            <td></td>
        </tr><tr>
            <td><code>N</code></td>
            <td><code>14</code></td>
            <td></td>
        </tr><tr>
            <td><code>O</code></td>
            <td><code>15</code></td>
            <td></td>
        </tr><tr>
            <td><code>P</code></td>
            <td><code>16</code></td>
            <td></td>
        </tr><tr>
            <td><code>Q</code></td>
            <td><code>17</code></td>
            <td></td>
        </tr><tr>
            <td><code>R</code></td>
            <td><code>18</code></td>
            <td></td>
        </tr><tr>
            <td><code>S</code></td>
            <td><code>19</code></td>
            <td></td>
        </tr><tr>
            <td><code>T</code></td>
            <td><code>20</code></td>
            <td></td>
        </tr><tr>
            <td><code>U</code></td>
            <td><code>21</code></td>
            <td></td>
        </tr><tr>
            <td><code>V</code></td>
            <td><code>22</code></td>
            <td></td>
        </tr><tr>
            <td><code>W</code></td>
            <td><code>23</code></td>
            <td></td>
        </tr><tr>
            <td><code>X</code></td>
            <td><code>24</code></td>
            <td></td>
        </tr><tr>
            <td><code>Y</code></td>
            <td><code>25</code></td>
            <td></td>
        </tr><tr>
            <td><code>Z</code></td>
            <td><code>26</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEY_1</code></td>
            <td><code>27</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEY_2</code></td>
            <td><code>28</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEY_3</code></td>
            <td><code>29</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEY_4</code></td>
            <td><code>30</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEY_5</code></td>
            <td><code>31</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEY_6</code></td>
            <td><code>32</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEY_7</code></td>
            <td><code>33</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEY_8</code></td>
            <td><code>34</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEY_9</code></td>
            <td><code>35</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEY_0</code></td>
            <td><code>36</code></td>
            <td></td>
        </tr><tr>
            <td><code>ENTER</code></td>
            <td><code>37</code></td>
            <td></td>
        </tr><tr>
            <td><code>ESCAPE</code></td>
            <td><code>38</code></td>
            <td></td>
        </tr><tr>
            <td><code>BACKSPACE</code></td>
            <td><code>39</code></td>
            <td></td>
        </tr><tr>
            <td><code>TAB</code></td>
            <td><code>40</code></td>
            <td></td>
        </tr><tr>
            <td><code>SPACE</code></td>
            <td><code>41</code></td>
            <td></td>
        </tr><tr>
            <td><code>MINUS</code></td>
            <td><code>42</code></td>
            <td></td>
        </tr><tr>
            <td><code>EQUALS</code></td>
            <td><code>43</code></td>
            <td></td>
        </tr><tr>
            <td><code>LEFT_BRACE</code></td>
            <td><code>44</code></td>
            <td></td>
        </tr><tr>
            <td><code>RIGHT_BRACE</code></td>
            <td><code>45</code></td>
            <td></td>
        </tr><tr>
            <td><code>BACKSLASH</code></td>
            <td><code>46</code></td>
            <td></td>
        </tr><tr>
            <td><code>NON_US_HASH</code></td>
            <td><code>47</code></td>
            <td></td>
        </tr><tr>
            <td><code>SEMICOLON</code></td>
            <td><code>48</code></td>
            <td></td>
        </tr><tr>
            <td><code>APOSTROPHE</code></td>
            <td><code>49</code></td>
            <td></td>
        </tr><tr>
            <td><code>GRAVE_ACCENT</code></td>
            <td><code>50</code></td>
            <td></td>
        </tr><tr>
            <td><code>COMMA</code></td>
            <td><code>51</code></td>
            <td></td>
        </tr><tr>
            <td><code>DOT</code></td>
            <td><code>52</code></td>
            <td></td>
        </tr><tr>
            <td><code>SLASH</code></td>
            <td><code>53</code></td>
            <td></td>
        </tr><tr>
            <td><code>CAPS_LOCK</code></td>
            <td><code>54</code></td>
            <td></td>
        </tr><tr>
            <td><code>F1</code></td>
            <td><code>55</code></td>
            <td></td>
        </tr><tr>
            <td><code>F2</code></td>
            <td><code>56</code></td>
            <td></td>
        </tr><tr>
            <td><code>F3</code></td>
            <td><code>57</code></td>
            <td></td>
        </tr><tr>
            <td><code>F4</code></td>
            <td><code>58</code></td>
            <td></td>
        </tr><tr>
            <td><code>F5</code></td>
            <td><code>59</code></td>
            <td></td>
        </tr><tr>
            <td><code>F6</code></td>
            <td><code>60</code></td>
            <td></td>
        </tr><tr>
            <td><code>F7</code></td>
            <td><code>61</code></td>
            <td></td>
        </tr><tr>
            <td><code>F8</code></td>
            <td><code>62</code></td>
            <td></td>
        </tr><tr>
            <td><code>F9</code></td>
            <td><code>63</code></td>
            <td></td>
        </tr><tr>
            <td><code>F10</code></td>
            <td><code>64</code></td>
            <td></td>
        </tr><tr>
            <td><code>F11</code></td>
            <td><code>65</code></td>
            <td></td>
        </tr><tr>
            <td><code>F12</code></td>
            <td><code>66</code></td>
            <td></td>
        </tr><tr>
            <td><code>PRINT_SCREEN</code></td>
            <td><code>67</code></td>
            <td></td>
        </tr><tr>
            <td><code>SCROLL_LOCK</code></td>
            <td><code>68</code></td>
            <td></td>
        </tr><tr>
            <td><code>PAUSE</code></td>
            <td><code>69</code></td>
            <td></td>
        </tr><tr>
            <td><code>INSERT</code></td>
            <td><code>70</code></td>
            <td></td>
        </tr><tr>
            <td><code>HOME</code></td>
            <td><code>71</code></td>
            <td></td>
        </tr><tr>
            <td><code>PAGE_UP</code></td>
            <td><code>72</code></td>
            <td></td>
        </tr><tr>
            <td><code>DELETE</code></td>
            <td><code>73</code></td>
            <td></td>
        </tr><tr>
            <td><code>END</code></td>
            <td><code>74</code></td>
            <td></td>
        </tr><tr>
            <td><code>PAGE_DOWN</code></td>
            <td><code>75</code></td>
            <td></td>
        </tr><tr>
            <td><code>RIGHT</code></td>
            <td><code>76</code></td>
            <td></td>
        </tr><tr>
            <td><code>LEFT</code></td>
            <td><code>77</code></td>
            <td></td>
        </tr><tr>
            <td><code>DOWN</code></td>
            <td><code>78</code></td>
            <td></td>
        </tr><tr>
            <td><code>UP</code></td>
            <td><code>79</code></td>
            <td></td>
        </tr><tr>
            <td><code>NON_US_BACKSLASH</code></td>
            <td><code>80</code></td>
            <td></td>
        </tr><tr>
            <td><code>LEFT_CTRL</code></td>
            <td><code>81</code></td>
            <td></td>
        </tr><tr>
            <td><code>LEFT_SHIFT</code></td>
            <td><code>82</code></td>
            <td></td>
        </tr><tr>
            <td><code>LEFT_ALT</code></td>
            <td><code>83</code></td>
            <td></td>
        </tr><tr>
            <td><code>LEFT_META</code></td>
            <td><code>84</code></td>
            <td></td>
        </tr><tr>
            <td><code>RIGHT_CTRL</code></td>
            <td><code>85</code></td>
            <td></td>
        </tr><tr>
            <td><code>RIGHT_SHIFT</code></td>
            <td><code>86</code></td>
            <td></td>
        </tr><tr>
            <td><code>RIGHT_ALT</code></td>
            <td><code>87</code></td>
            <td></td>
        </tr><tr>
            <td><code>RIGHT_META</code></td>
            <td><code>88</code></td>
            <td></td>
        </tr><tr>
            <td><code>NUM_LOCK</code></td>
            <td><code>512</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEYPAD_SLASH</code></td>
            <td><code>513</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEYPAD_ASTERISK</code></td>
            <td><code>514</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEYPAD_MINUS</code></td>
            <td><code>515</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEYPAD_PLUS</code></td>
            <td><code>516</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEYPAD_ENTER</code></td>
            <td><code>517</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEYPAD_1</code></td>
            <td><code>518</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEYPAD_2</code></td>
            <td><code>519</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEYPAD_3</code></td>
            <td><code>520</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEYPAD_4</code></td>
            <td><code>521</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEYPAD_5</code></td>
            <td><code>522</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEYPAD_6</code></td>
            <td><code>523</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEYPAD_7</code></td>
            <td><code>524</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEYPAD_8</code></td>
            <td><code>525</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEYPAD_9</code></td>
            <td><code>526</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEYPAD_0</code></td>
            <td><code>527</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEYPAD_DOT</code></td>
            <td><code>528</code></td>
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



## **TABLES**

### KeyEvent {:#KeyEvent}


*Defined in [fuchsia.ui.input2/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input2/events.fidl#17)*

 Keyboard event is generated to reflect key input.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>key</code></td>
            <td>
                <code><a class='link' href='#Key'>Key</a></code>
            </td>
            <td> Physical key being pressed.

 Keyboard layout is applied (QWERTY/AZERTY/Dvorak/etc).
</td>
        </tr><tr>
            <td>2</td>
            <td><code>phase</code></td>
            <td>
                <code><a class='link' href='#KeyEventPhase'>KeyEventPhase</a></code>
            </td>
            <td> Phase of input.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>modifiers</code></td>
            <td>
                <code><a class='link' href='#Modifiers'>Modifiers</a></code>
            </td>
            <td> Modifier keys being held.
</td>
        </tr></table>







## **BITS**
### Modifiers {:#Modifiers}
Type: <code>uint32</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>SHIFT</td>
            <td>1</td>
            <td> Applies when either the LEFT_SHIFT or RIGHT_SHIFT modifier is pressed.
</td>
        </tr><tr>
            <td>LEFT_SHIFT</td>
            <td>2</td>
            <td> Applies when the LEFT_SHIFT modifier is pressed.
</td>
        </tr><tr>
            <td>RIGHT_SHIFT</td>
            <td>4</td>
            <td> Applies when the RIGHT_SHIFT modifier is pressed.
</td>
        </tr><tr>
            <td>CONTROL</td>
            <td>8</td>
            <td> Applies when either the LEFT_CONTROL or RIGHT_CONTROL modifier is pressed.
</td>
        </tr><tr>
            <td>LEFT_CONTROL</td>
            <td>16</td>
            <td> Applies when the LEFT_CONTROL modifier is pressed.
</td>
        </tr><tr>
            <td>RIGHT_CONTROL</td>
            <td>32</td>
            <td> Applies when the RIGHT_CONTROL modifier is pressed.
</td>
        </tr><tr>
            <td>ALT</td>
            <td>64</td>
            <td> Applies when either the LEFT_ALT or RIGHT_ALT modifier is pressed.
</td>
        </tr><tr>
            <td>LEFT_ALT</td>
            <td>128</td>
            <td> Applies when the LEFT_ALT modifier is pressed.
</td>
        </tr><tr>
            <td>RIGHT_ALT</td>
            <td>256</td>
            <td> Applies when the RIGHT_ALT modifier is pressed.
</td>
        </tr><tr>
            <td>META</td>
            <td>512</td>
            <td> Applies when either the LEFT_META or RIGHT_META modifier is pressed.
</td>
        </tr><tr>
            <td>LEFT_META</td>
            <td>1024</td>
            <td> Applies when the LEFT_META modifier is pressed.
</td>
        </tr><tr>
            <td>RIGHT_META</td>
            <td>2048</td>
            <td> Applies when the RIGHT_META modifier is pressed.
</td>
        </tr><tr>
            <td>CAPS_LOCK</td>
            <td>4096</td>
            <td> Applies when the CAPS_LOCK modifier is locked.
</td>
        </tr><tr>
            <td>NUM_LOCK</td>
            <td>8192</td>
            <td> Applies when the NUM_LOCK modifier is locked.
</td>
        </tr><tr>
            <td>SCROLL_LOCK</td>
            <td>16384</td>
            <td> Applies when the SCROLL_LOCK modifier is locked.
</td>
        </tr></table>



