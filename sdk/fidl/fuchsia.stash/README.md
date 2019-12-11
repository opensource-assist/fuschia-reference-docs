[TOC]

# fuchsia.stash


## **PROTOCOLS**

## ListIterator {#ListIterator}
*Defined in [fuchsia.stash/stash.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.stash/stash.fidl#55)*

<p>The iterator returned when a series of keys are being listed. Returns an
empty vector when there are no more remaining ListItems.</p>

### GetNext {#GetNext}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>keys</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ListItem'>ListItem</a>&gt;</code>
            </td>
        </tr></table>

## GetIterator {#GetIterator}
*Defined in [fuchsia.stash/stash.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.stash/stash.fidl#61)*

<p>The iterator returned when a series of keys are being read. Returns an
empty vector when there are no more remaining KeyValues.</p>

### GetNext {#GetNext}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>kvs</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#KeyValue'>KeyValue</a>&gt;</code>
            </td>
        </tr></table>

## StoreAccessor {#StoreAccessor}
*Defined in [fuchsia.stash/stash.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.stash/stash.fidl#66)*

<p>The interface returned when a new accessor is created.</p>

### GetValue {#GetValue}

<p>Gets a single value from the store.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>string[256]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>val</code></td>
            <td>
                <code><a class='link' href='#Value'>Value</a>?</code>
            </td>
        </tr></table>

### SetValue {#SetValue}

<p>Sets a single value in the store. Overwrites existing values. Commit()
must be called for this change to take effect.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>string[256]</code>
            </td>
        </tr><tr>
            <td><code>val</code></td>
            <td>
                <code><a class='link' href='#Value'>Value</a></code>
            </td>
        </tr></table>



### DeleteValue {#DeleteValue}

<p>Deletes a single value in the store. Does nothing if the value doesn't
exist. Commit() must be called for this change to take effect.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>string[256]</code>
            </td>
        </tr></table>



### ListPrefix {#ListPrefix}

<p>Lists all keys under a given prefix.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>prefix</code></td>
            <td>
                <code>string[256]</code>
            </td>
        </tr><tr>
            <td><code>it</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ListIterator'>ListIterator</a>&gt;</code>
            </td>
        </tr></table>



### GetPrefix {#GetPrefix}

<p>Reads the values of all keys under a given prefix.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>prefix</code></td>
            <td>
                <code>string[256]</code>
            </td>
        </tr><tr>
            <td><code>it</code></td>
            <td>
                <code>request&lt;<a class='link' href='#GetIterator'>GetIterator</a>&gt;</code>
            </td>
        </tr></table>



### DeletePrefix {#DeletePrefix}

<p>Deletes the all keys under a given prefix.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>prefix</code></td>
            <td>
                <code>string[256]</code>
            </td>
        </tr></table>



### Commit {#Commit}

<p>Atomically causes all of the state modifications that happened in this
accessor to take place.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Flush {#Flush}

<p>Atomically causes all of the state modifications that happened
in this accessor to take place, returning only when those
modifications were written to disk.
This operation is equivalent to Commit.
Returns a FlushError if this operations could not be committed.</p>

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
                <code><a class='link' href='#StoreAccessor_Flush_Result'>StoreAccessor_Flush_Result</a></code>
            </td>
        </tr></table>

## Store {#Store}
*Defined in [fuchsia.stash/stash.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.stash/stash.fidl#101)*

<p>Interface used to interact with a given client's key/value store</p>

### Identify {#Identify}

<p>Identify should be called at the beginning of a connection to identify
which client service's store is to be accessed. In the future this will
be deprecated in favor of component monikers, and each client will only
be able to access its own store.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string[256]</code>
            </td>
        </tr></table>



### CreateAccessor {#CreateAccessor}

<p>Creates a accessor for interacting with the store. The resulting
interface can be used to inspect and modify the state of the store.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>read_only</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>accessor_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#StoreAccessor'>StoreAccessor</a>&gt;</code>
            </td>
        </tr></table>



## SecureStore {#SecureStore}
*Defined in [fuchsia.stash/stash.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.stash/stash.fidl#116)*

<p>Interface used to interact with a given client's key/value store. The bytes
type is disabled in this store.</p>

### Identify {#Identify}

<p>Identify should be called at the beginning of a connection to identify
which client service's store is to be accessed. In the future this will
be deprecated in favor of component monikers, and each client will only
be able to access its own store.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string[256]</code>
            </td>
        </tr></table>



### CreateAccessor {#CreateAccessor}

<p>Creates a accessor for interacting with the store. The resulting
interface can be used to inspect and modify the state of the store.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>read_only</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>accessor_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#StoreAccessor'>StoreAccessor</a>&gt;</code>
            </td>
        </tr></table>





## **STRUCTS**

### StoreAccessor_Flush_Response {#StoreAccessor_Flush_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### ListItem {#ListItem}
*Defined in [fuchsia.stash/stash.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.stash/stash.fidl#22)*



<p>ListItem is returned when a series of keys are being listed.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code>string[256]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#ValueType'>ValueType</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### KeyValue {#KeyValue}
*Defined in [fuchsia.stash/stash.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.stash/stash.fidl#29)*



<p>KeyValue is used when a series of keys are being read, or the default state
for the store is being set.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code>string[256]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>val</code></td>
            <td>
                <code><a class='link' href='#Value'>Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### ValueType {#ValueType}
Type: <code>uint8</code>

*Defined in [fuchsia.stash/stash.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.stash/stash.fidl#13)*

<p>ValueType encodes a type for a field in the store</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INT_VAL</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>FLOAT_VAL</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>BOOL_VAL</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>STRING_VAL</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>BYTES_VAL</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr></table>

### FlushError {#FlushError}
Type: <code>uint32</code>

*Defined in [fuchsia.stash/stash.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.stash/stash.fidl#45)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>READ_ONLY</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>COMMIT_FAILED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>





## **UNIONS**

### StoreAccessor_Flush_Result {#StoreAccessor_Flush_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#StoreAccessor_Flush_Response'>StoreAccessor_Flush_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#FlushError'>FlushError</a></code>
            </td>
            <td></td>
        </tr></table>

### Value {#Value}
*Defined in [fuchsia.stash/stash.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.stash/stash.fidl#35)*

<p>Value holds a value for a given key.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>intval</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>floatval</code></td>
            <td>
                <code>float64</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>boolval</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>stringval</code></td>
            <td>
                <code>string[12000]</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>bytesval</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="MAX_STRING_SIZE">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.stash/stash.fidl#9">MAX_STRING_SIZE</a></td>
            <td>
                    <code>12000</code>
                </td>
                <td><code>uint64</code></td>
            <td><p>Strings over 12 kb will be tossed. This number is chosen arbitrarily, if you
think it should be higher just ask.</p>
</td>
        </tr>
    <tr id="MAX_KEY_SIZE">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.stash/stash.fidl#10">MAX_KEY_SIZE</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    
</table>



