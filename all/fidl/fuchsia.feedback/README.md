[TOC]

# fuchsia.feedback


## **PROTOCOLS**

## CrashReporter {#CrashReporter}
*Defined in [fuchsia.feedback/crash_reporter.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.feedback/crash_reporter.fidl#12)*

<p>Provides the ability to file crash reports.</p>

### File {#File}

<p>Files a crash <code>report</code>.</p>
<p>This could mean generating a crash report in a local crash report database or uploading the
crash report to a remote crash server depending on the FIDL server's configuration.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>report</code></td>
            <td>
                <code><a class='link' href='#CrashReport'>CrashReport</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#CrashReporter_File_Result'>CrashReporter_File_Result</a></code>
            </td>
        </tr></table>

## DataProvider {#DataProvider}
*Defined in [fuchsia.feedback/data_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.feedback/data_provider.fidl#13)*

<p>Provides data useful to attach in feedback reports (crash or user feedback).</p>

### GetData {#GetData}

<p>Returns all the feedback data except the screenshot, which is provided
separately.</p>

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
                <code><a class='link' href='#DataProvider_GetData_Result'>DataProvider_GetData_Result</a></code>
            </td>
        </tr></table>

### GetScreenshot {#GetScreenshot}

<p>Returns an image of the current view encoded in the provided <code>encoding</code>.</p>
<p><code>screenshot</code> may be null if the encoding is not supported, the device
does not have a display, or there is not enough memory to allocate the
screenshot image.</p>
<p>The screenshot is provided separately from the rest of the data as
callers might want to block on it before changing the view.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>encoding</code></td>
            <td>
                <code><a class='link' href='#ImageEncoding'>ImageEncoding</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>screenshot</code></td>
            <td>
                <code><a class='link' href='#Screenshot'>Screenshot</a>?</code>
            </td>
        </tr></table>



## **STRUCTS**

### Annotation {#Annotation}
*Defined in [fuchsia.feedback/annotation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.feedback/annotation.fidl#9)*



<p>An annotation and its plain ASCII string key.
Annotations are short strings, e.g., the board name or the build version.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Attachment {#Attachment}
*Defined in [fuchsia.feedback/attachment.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.feedback/attachment.fidl#11)*



<p>An attachment and its plain ASCII string key.
Attachments are larger objects, e.g., log files. They may be binary or text data.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### CrashReporter_File_Response {#CrashReporter_File_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### DataProvider_GetData_Response {#DataProvider_GetData_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='#Data'>Data</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Screenshot {#Screenshot}
*Defined in [fuchsia.feedback/data_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.feedback/data_provider.fidl#57)*



<p>An encoded image of the screen.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>image</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>dimensions_in_px</code></td>
            <td>
                <code><a class='link' href='../fuchsia.math/'>fuchsia.math</a>/<a class='link' href='../fuchsia.math/#Size'>Size</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### ImageEncoding {#ImageEncoding}
Type: <code>uint32</code>

*Defined in [fuchsia.feedback/data_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.feedback/data_provider.fidl#52)*

<p>The encoding used for the image.</p>
<p>Today, only PNG is supported, but in the future the screenshot could be
returned in other encodings if need arises.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>PNG</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### CrashReport {#CrashReport}


*Defined in [fuchsia.feedback/crash_reporter.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.feedback/crash_reporter.fidl#21)*

<p>Represents a crash report.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>program_name</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>The name of the program that crashed, e.g., the process or component's name.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>specific_report</code></td>
            <td>
                <code><a class='link' href='#SpecificCrashReport'>SpecificCrashReport</a></code>
            </td>
            <td><p>The specific report that depends on the type of crashes.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>annotations</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Annotation'>Annotation</a>&gt;[32]</code>
            </td>
            <td><p>A vector of key-value string pairs representing arbitrary data that should be attached to a
crash report. Keys should be unique.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>attachments</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Attachment'>Attachment</a>&gt;[16]</code>
            </td>
            <td><p>A vector of key-value string-to-VMO pairs representing arbitrary data that should be
attached to a crash report. Keys should be unique.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>event_id</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td><p>A text ID that the crash server can use to group multiple crash reports related to the
same event.</p>
<p>Unlike the crash signature, crash reports sharing the same ID correspond to different
crashes, but can be considered as belonging to the same event, e.g., a crash in a low-level
server causing a crash in a high-level UI widget.</p>
</td>
        </tr></table>

### GenericCrashReport {#GenericCrashReport}


*Defined in [fuchsia.feedback/crash_reporter.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.feedback/crash_reporter.fidl#61)*

<p>Represents a generic crash report.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>crash_signature</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td><p>A text signature that the crash server can use to track the same crash over time, e.g.,
&quot;kernel-panic&quot; or &quot;oom&quot;.</p>
<p>Unlike the event ID, crash reports sharing the same signature correspond to the same crash,
but happening over multiple events, e.g., a null pointer exception in a server whenever
asked the same request.</p>
</td>
        </tr></table>

### NativeCrashReport {#NativeCrashReport}


*Defined in [fuchsia.feedback/crash_reporter.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.feedback/crash_reporter.fidl#72)*

<p>Represents a crash report for a native exception out of which the client has built a minidump.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>minidump</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td><p>The core dump in the Minidump format.</p>
</td>
        </tr></table>

### RuntimeCrashReport {#RuntimeCrashReport}


*Defined in [fuchsia.feedback/crash_reporter.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.feedback/crash_reporter.fidl#78)*

<p>Represents a crash report for a runtime exception, applicable to most languages.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>exception_type</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td><p>The exception type, e.g., &quot;FileSystemException&quot;.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>exception_message</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>The exception message, e.g., &quot;cannot open file&quot;.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>exception_stack_trace</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td><p>The text representation of the exception stack trace.</p>
</td>
        </tr></table>

### Data {#Data}


*Defined in [fuchsia.feedback/data_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.feedback/data_provider.fidl#34)*

<p>Data to attach to feedback reports.</p>
<p>Clients typically upload the data straight to servers without expecting some
particular fields. So the data comes in the form of arbitrary key-value pairs
that clients can directly forward to the servers.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>annotations</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Annotation'>Annotation</a>&gt;[32]</code>
            </td>
            <td><p>A vector of key-value string pairs. Keys are guaranteed to be unique.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>attachments</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Attachment'>Attachment</a>&gt;[16]</code>
            </td>
            <td><p>A vector of key-value string-to-VMO pairs. Keys are guaranteed to be unique.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>attachment_bundle</code></td>
            <td>
                <code><a class='link' href='#Attachment'>Attachment</a></code>
            </td>
            <td><p>A bundle of Attachments objects stored as an Attachment itself, e.g., it
could be a ZIP archive bundling a vector of Attachment objects.</p>
</td>
        </tr></table>



## **UNIONS**

### CrashReporter_File_Result {#CrashReporter_File_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#CrashReporter_File_Response'>CrashReporter_File_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### DataProvider_GetData_Result {#DataProvider_GetData_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#DataProvider_GetData_Response'>DataProvider_GetData_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>



## **XUNIONS**

### SpecificCrashReport {#SpecificCrashReport}
*Defined in [fuchsia.feedback/crash_reporter.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.feedback/crash_reporter.fidl#49)*

<p>Represents a specific crash report.</p>
<p>Add a new member when the server needs to special case how it handles certain annotations and
attachments for a given type of crashes, e.g., a <code>RuntimeCrashReport</code> for Javascript.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>generic</code></td>
            <td>
                <code><a class='link' href='#GenericCrashReport'>GenericCrashReport</a></code>
            </td>
            <td><p>Intended for arbitrary crashes, e.g., OOM, out-of-disk.</p>
</td>
        </tr><tr>
            <td><code>native</code></td>
            <td>
                <code><a class='link' href='#NativeCrashReport'>NativeCrashReport</a></code>
            </td>
            <td><p>Intended for a native exception.</p>
</td>
        </tr><tr>
            <td><code>dart</code></td>
            <td>
                <code><a class='link' href='#RuntimeCrashReport'>RuntimeCrashReport</a></code>
            </td>
            <td><p>Intended for a Dart exception.</p>
</td>
        </tr></table>





