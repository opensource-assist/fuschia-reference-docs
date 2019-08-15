Project: /_project.yaml
Book: /_book.yaml

# fuchsia.ui.text


## **PROTOCOLS**

## TextField {:#TextField}
*Defined in [fuchsia.ui.text/text_field.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.text/text_field.fidl#77)*

 Represents a text field or other kind of editing interface that wants to receive text input
 from the operating system. This interface is also what is passed to a keyboard to allow it
 to read state and make changes to text fields.

 All editing methods must happen within an edit transaction. The edits aren't
 applied until CommitEdit is called. **This isn't a lock!** The TextField
 can still apply edits on its side, which would increase the current revision
 number. When CommitEdit is called, the edits are only run if the revision
 number passed to BeginEdit is still valid. TextField implementations can
 assume that there will only be one client at a time; they don't need to
 keep track of a separate transaction list for each client.

### OnUpdate {:#OnUpdate}

 Any time the revision number increments, this event fires, with the latest version of
 the state. It also fires when a new client connects to the service, so it can get an
 initial state without waiting for an edit.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#TextFieldState'>TextFieldState</a></code>
            </td>
        </tr></table>

### PositionOffset {:#PositionOffset}

 Returns a new position that is `offset` unicode code points away from `old_position`

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>old_position</code></td>
            <td>
                <code><a class='link' href='#Position'>Position</a></code>
            </td>
        </tr><tr>
            <td><code>offset</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>revision</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>new_position</code></td>
            <td>
                <code><a class='link' href='#Position'>Position</a></code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
        </tr></table>

### Distance {:#Distance}

 Returns number of unicode code points between two positions. If the position range.start is after
 range.end, then the range is considered `inverted` and distance will be negative.
 For all positions A and B, PositionOffset(A, Distance(A, B)) == B

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>range</code></td>
            <td>
                <code><a class='link' href='#Range'>Range</a></code>
            </td>
        </tr><tr>
            <td><code>revision</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>distance</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
        </tr></table>

### Contents {:#Contents}

 Returns string of unicode code points between two positions

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>range</code></td>
            <td>
                <code><a class='link' href='#Range'>Range</a></code>
            </td>
        </tr><tr>
            <td><code>revision</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>contents</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>start</code></td>
            <td>
                <code><a class='link' href='#Position'>Position</a></code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
        </tr></table>

### BeginEdit {:#BeginEdit}

 Starts a transaction. If it's called a second time with no CommitEdit()
 call, the changes from the first uncommitted transaction are discarded as
 though AbortEdit() was called.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>revision</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### CommitEdit {:#CommitEdit}

 If the transaction's revision number (from BeginEdit) is still current,
 runs all edit commands queued in this transaction. If not, returns
 `BAD_REVISION`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
        </tr></table>

### AbortEdit {:#AbortEdit}

 Discards the current transaction.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Replace {:#Replace}

 Replaces text in the range with new_text. It's the client's
 responsibility to make sure new_text isn't too long for a FIDL message;
 if it is, the client should break up the string into separate replace
 calls.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>range</code></td>
            <td>
                <code><a class='link' href='#Range'>Range</a></code>
            </td>
        </tr><tr>
            <td><code>new_text</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### SetSelection {:#SetSelection}

 Sets the selection range.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>selection</code></td>
            <td>
                <code><a class='link' href='#Selection'>Selection</a></code>
            </td>
        </tr></table>



### SetComposition {:#SetComposition}

 Sets the composition range and the composition highlight range. For more info,
 see TextState's comments.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>composition_range</code></td>
            <td>
                <code><a class='link' href='#Range'>Range</a></code>
            </td>
        </tr><tr>
            <td><code>highlight_range</code></td>
            <td>
                <code><a class='link' href='#Range'>Range</a>?</code>
            </td>
        </tr></table>



### ClearComposition {:#ClearComposition}

 Clears both the composition range, and the composition highlight range.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SetDeadKeyHighlight {:#SetDeadKeyHighlight}

 Sets the dead key highlight range. For more info, see TextState's comments.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>range</code></td>
            <td>
                <code><a class='link' href='#Range'>Range</a></code>
            </td>
        </tr></table>



### ClearDeadKeyHighlight {:#ClearDeadKeyHighlight}

 Clears the dead key highlight range.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## TextInputContext {:#TextInputContext}
*Defined in [fuchsia.ui.text/text_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.text/text_manager.fidl#14)*

 A service provided to keyboard apps that allows them to access a TextField
 interface for the currently focused text field. Requests to this TextField
 interface are proxied through the TextManager to batch edits together,
 and to ensure requests aren't sent to unfocused TextFields.

### HideKeyboard {:#HideKeyboard}

 Tells anyone listening to ImeVisibilityService (usually a shell) to hide
 the onscreen keyboard.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### OnFocus {:#OnFocus}

 This event fires any time a new text field is focused. It also is sent to
 newly connected keyboards when they connect, if there is a focused text
 field. If focus is lost, the TextField handle will be closed.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>text_field</code></td>
            <td>
                <code><a class='link' href='#TextField'>TextField</a></code>
            </td>
        </tr></table>

### OnInputEvent {:#OnInputEvent}

 This event fires any time a physical keyboard event is sent to the
 TextManager. The keyboard may translate it into an edit on the focused
 text field if it so desires. It's expected that this interface will change
 as the routing for keyboard events and keymaps evolves.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>event</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.input/index.html'>fuchsia.ui.input</a>/<a class='link' href='../fuchsia.ui.input/index.html#InputEvent'>InputEvent</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Position {:#Position}
*Defined in [fuchsia.ui.text/primitives.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.text/primitives.fidl#18)*



 Indicates a character position in a text field, either between two grapheme clusters
 or at the very edge of the document.

 Any valid Position is a place a typing caret could appear, and vice-versa.
 Instead of using absolute character indexes, each Position has a
 TextField-assigned ID; it's the TextField's responsibility to keep a mapping
 of position IDs to its internal representation of position.

 When the TextField's revision number increments, all existing Positions
 become invalid. TextField should take care never reuse position IDs, even across
 revisions.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Selection {:#Selection}
*Defined in [fuchsia.ui.text/primitives.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.text/primitives.fidl#31)*



 A selection is the current range of the text that is selected by the user,
 or the current position of the blinking input caret.

 A zero-length selection is a caret. Affinity only has an effect on carets.

 Even in mixed RTL and LTR text situations, a selection is still just the
 string-wise slice between `focus` and `anchor` — graphical representations
 of selections flip directions when crossing the RTL/LTR boundary, but no
 special code is needed to handle crossing the boundary in the model.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>range</code></td>
            <td>
                <code><a class='link' href='#Range'>Range</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>anchor</code></td>
            <td>
                <code><a class='link' href='#SelectionAnchor'>SelectionAnchor</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>affinity</code></td>
            <td>
                <code><a class='link' href='#Affinity'>Affinity</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Range {:#Range}
*Defined in [fuchsia.ui.text/primitives.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.text/primitives.fidl#50)*



 A range is the grapheme clusters between `start` and `end`. When sending
 ranges to clients, TextField must ensure `start` is always upstream of
 `end`. However, when receiving ranges from clients, it should accept
 `start` and `end` in any order.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>start</code></td>
            <td>
                <code><a class='link' href='#Position'>Position</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>end</code></td>
            <td>
                <code><a class='link' href='#Position'>Position</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### SelectionAnchor {:#SelectionAnchor}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.text/primitives.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.text/primitives.fidl#41)*

 Selection anchor states which edge of the selection is the anchor, and which
 is the focus. While holding down shift and using the arrow keys, or while
 dragging across some text to select it, the anchor is the edge that stays in
 place, and the focus is the edge that moves around.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ANCHORED_AT_START</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>ANCHORED_AT_END</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### Affinity {:#Affinity}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.text/primitives.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.text/primitives.fidl#61)*

 Whether a Position is visually upstream or downstream when ambiguous.

 For example, when a position exists at a soft line break, a single offset has
 two visual positions, UPSTREAM (at the end of the first line) and DOWNSTREAM
 (at the start of the second line). A text affinity disambiguates between those
 cases. (Something similar happens with between runs of bidirectional text.)


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UPSTREAM</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>DOWNSTREAM</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### Error {:#Error}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.text/text_field.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.text/text_field.fidl#44)*

 Indicates errors that can occur with various TextField methods. Until FIDL supports
 result return types, if Error has any value except OK, the client must ignore
 all other return data from that method.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OK</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>BAD_REVISION</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVALID_EDIT</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>BAD_REQUEST</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNKNOWABLE</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### TextFieldState {:#TextFieldState}


*Defined in [fuchsia.ui.text/text_field.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.text/text_field.fidl#10)*

 Lists the Positions for selection and other related ranges, at a particular
 revision number. Any time the revision number is incremented, all these Positions
 become invalid, and a new TextFieldState is sent through OnUpdate.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>document</code></td>
            <td>
                <code><a class='link' href='#Range'>Range</a></code>
            </td>
            <td> (required) The start and end of the entire text field.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>selection</code></td>
            <td>
                <code><a class='link' href='#Selection'>Selection</a></code>
            </td>
            <td> (required) The currently selected range of text.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>composition</code></td>
            <td>
                <code><a class='link' href='#Range'>Range</a></code>
            </td>
            <td> The range that indicates the text that is being composed, or currently
 receiving suggestions from the keyboard. It should be displayed in some
 distinct way, such as underlined.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>composition_highlight</code></td>
            <td>
                <code><a class='link' href='#Range'>Range</a></code>
            </td>
            <td> Some keyboards, notably Japanese, give the user buttons to highlight just a
 subset of the composition string for suggestions. It must be equal to or a subset
 of the composition range. If the composition range changes, the TextField may
 discard this and require the keyboard to create a new one.
</td>
        </tr><tr>
            <td>5</td>
            <td><code>dead_key_highlight</code></td>
            <td>
                <code><a class='link' href='#Range'>Range</a></code>
            </td>
            <td> A dead key is a key combination you press before another key to add diacritical
 marks, accents, or other changes to the second key. After the first key, a
 highlighted character indicates that the next character will be different. This
 range is that highlighted character. If the selection moves away from this
 highlight range, or if the contents of the highlight range change, the TextField
 may discard this and require the keyboard to create a new one.
</td>
        </tr><tr>
            <td>6</td>
            <td><code>revision</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> (required) This number is increased any time content in the text field is changed,
 if the selection is changed, or if anything else about the state is changed.
</td>
        </tr></table>









