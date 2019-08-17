Project: /_project.yaml
Book: /_book.yaml

# fuchsia.term


## **PROTOCOLS**

## Pty {:#Pty}
*Defined in [fuchsia.term/term.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/app/term/term.fidl#12)*

 Defines a protocol to read and write to a Pty terminal.

### OnClose {:#OnClose}

 Event stream when command is closed.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### OnRead {:#OnRead}

 Event stream when data is available.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[900]</code>
            </td>
        </tr></table>

### Write {:#Write}

 Writes data.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[900]</code>
            </td>
        </tr></table>



### SetWindowSize {:#SetWindowSize}

 Sets the window size.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>columns</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>rows</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



## Term {:#Term}
*Defined in [fuchsia.term/term.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/app/term/term.fidl#28)*

 Defines a protocol to create Pty terminal.

### CreatePty {:#CreatePty}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>commandArgs</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr><tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Pty'>Pty</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>















## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/topaz/app/term/term.fidl#9">MAX_BUF</a></td>
            <td>
                    <code>900</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    
</table>

