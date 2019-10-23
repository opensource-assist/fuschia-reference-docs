[TOC]

# fuchsia.debugdata


## **PROTOCOLS**

## DebugData {#DebugData}
*Defined in [fuchsia.debugdata/debugdata.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-debugdata/debugdata.fidl#12)*

 DebugData defines the interface for instrumentation configuration and data publishing.

### Publish {#Publish}

 The program runtime sends a string naming a `data_sink` and transfers the sole handle to
 a VMO containing the `data` it wants published there.  The `data_sink` string identifies
 a type of data, and the VMO's object name can specifically identify the data set in this
 VMO.  The client must transfer the only handle to the VMO (which prevents the VMO being
 resized without the receiver's knowledge), but it might still have the VMO mapped in and
 continue to write data to it.  Code instrumentation runtimes use this to deliver large
 binary trace results.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data_sink</code></td>
            <td>
                <code>string[1024]</code>
            </td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr></table>



### LoadConfig {#LoadConfig}

 The program runtime names a `config_name` referring to a debug configuration of some kind
 and gets back a VMO to read configuration data from.  The sanitizer runtimes use this to
 allow large options text to be stored in a file rather than passed directly in environment
 strings.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config_name</code></td>
            <td>
                <code>string[1024]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code>handle&lt;vmo&gt;?</code>
            </td>
        </tr></table>















## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-debugdata/debugdata.fidl#8">MAX_NAME</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint64</code></td>
            <td> The maximum length, in bytes, of data sink or configuration name.
</td>
        </tr>
    
</table>

