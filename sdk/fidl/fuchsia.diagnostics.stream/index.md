Project: /_project.yaml
Book: /_book.yaml

# fuchsia.diagnostics.stream


## **PROTOCOLS**

## Source {:#Source}
*Defined in [fuchsia.diagnostics.stream/source.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics.stream/source.fidl#29)*

 A component with records for the Diagnostics system to retrieve.

 To record diagnostics, a component allocates a VMO and begins writing records into the buffer,
 incrementing a header value after each write to inform readers how much of the buffer has been
 filled.

 If any retrievers are connected, the `Source` sends them `OnBufferInit` events for each
 diagnostic buffer created.

 When the buffer fills, the `Source` sends `OnBufferDone` to the retrievers, and will wait for
 all notified retrievers to reply with `RetireBuffer` when they have finished reading from the
 buffer.

 When all readers of the buffer have finished, the `Source` may recycle the buffer by zeroing it
 and sending `OnBufferInit` again to connected retrievers.

 Once a `Source` has sent `OnBufferDone` to a retriever, it is up to the `Source` to handle new
 records that are generated while the retriever drains the buffer. Double buffering is
 recommended to prevent excessive blocking, but this protocol does not mandate a specific
 approach to handling records generated while buffers are full.

### OnBufferInit {:#OnBufferInit}

 Notifies the connected retriever of a new stream buffer. Should be emitted as soon as each
 buffer is (re)initialized.

 `latest` should be read-only.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>latest</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr></table>

### OnBufferDone {:#OnBufferDone}

 Asks the connected retriever to finish working with `buffer`, usually because the `Source`
 does not intend to write further records.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### RetireBuffer {:#RetireBuffer}

 Notifies the `Source` that the retriever is done reading from the buffer. If the `Source`
 wishes it should zero the buffer's contents and recycle it for future records. Buffers must
 be re-sent via `OnBufferInit` after they're zeroed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### RegisterInterest {:#RegisterInterest}

 Notifies the component of interest in a subset of diagnostic records.

 Before the component receives this request it should filter according to a default interest
 specifier.

 After receiving this message components begin writing records according to the new
 specifier. `Source` components must be prepared to handle multiple client connections,
 and may filter records according to the union of all interest specifiers. Clients may
 receive records outside the scope of their interest.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>desired</code></td>
            <td>
                <code><a class='link' href='#Interest'>Interest</a></code>
            </td>
        </tr></table>







## **ENUMS**

### Severity {:#Severity}
Type: <code>uint32</code>

*Defined in [fuchsia.diagnostics.stream/source.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics.stream/source.fidl#67)*

 The severity of a given record.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>FATAL</code></td>
            <td><code>5</code></td>
            <td> Components should only record fatal records prior to terminating operation. Fatal
 records are informative only, and front-end libraries which trigger an exit in response
 to them should clearly document this behavior to their users.
</td>
        </tr><tr>
            <td><code>ERROR</code></td>
            <td><code>4</code></td>
            <td> Components should include error records as well as more severe records.
</td>
        </tr><tr>
            <td><code>WARN</code></td>
            <td><code>3</code></td>
            <td> Components should include warning records as well as more severe records.
</td>
        </tr><tr>
            <td><code>INFO</code></td>
            <td><code>2</code></td>
            <td> Components should include informative records as well as more severe records. (default)
</td>
        </tr><tr>
            <td><code>DEBUG</code></td>
            <td><code>1</code></td>
            <td> Components should include developer-facing debug records as well as more severe records.
</td>
        </tr><tr>
            <td><code>ANY</code></td>
            <td><code>0</code></td>
            <td> Components should include all records.
</td>
        </tr></table>



## **TABLES**

### Interest {:#Interest}


*Defined in [fuchsia.diagnostics.stream/source.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics.stream/source.fidl#61)*

 The system's current interest in records.

 Without having received an interest specifier or receiving one with empty fields, components
 should assume a default interest specifier, as documented for each field in this table.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>min_severity</code></td>
            <td>
                <code><a class='link' href='#Severity'>Severity</a></code>
            </td>
            <td> Minimum desired severity. The default is `INFO`.
</td>
        </tr></table>









