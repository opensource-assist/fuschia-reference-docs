Project: /_project.yaml
Book: /_book.yaml

# test.fidlcat.sys


## **PROTOCOLS**

## ComponentController {:#ComponentController}
*Defined in [test.fidlcat.sys/sys.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/sys.test.fidl#55)*


### Kill {:#Kill}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Detach {:#Detach}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### OnTerminated {:#OnTerminated}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>return_code</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>termination_reason</code></td>
            <td>
                <code><a class='link' href='#TerminationReason'>TerminationReason</a></code>
            </td>
        </tr></table>

### OnDirectoryReady {:#OnDirectoryReady}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## EnvironmentController {:#EnvironmentController}
*Defined in [test.fidlcat.sys/sys.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/sys.test.fidl#94)*


### Kill {:#Kill}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### Detach {:#Detach}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### OnCreated {:#OnCreated}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## Environment {:#Environment}
*Defined in [test.fidlcat.sys/sys.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/sys.test.fidl#137)*


### CreateNestedEnvironment {:#CreateNestedEnvironment}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>environment</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Environment'>Environment</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>controller</code></td>
            <td>
                <code>request&lt;<a class='link' href='#EnvironmentController'>EnvironmentController</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>label</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>additional_services</code></td>
            <td>
                <code><a class='link' href='#ServiceList'>ServiceList</a>?</code>
            </td>
        </tr><tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#EnvironmentOptions'>EnvironmentOptions</a></code>
            </td>
        </tr></table>



### GetLauncher {:#GetLauncher}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>launcher</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Launcher'>Launcher</a>&gt;</code>
            </td>
        </tr></table>



### GetServices {:#GetServices}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>services</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ServiceProvider'>ServiceProvider</a>&gt;</code>
            </td>
        </tr></table>



### GetDirectory {:#GetDirectory}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>directory_request</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



## JobProvider {:#JobProvider}
*Defined in [test.fidlcat.sys/sys.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/sys.test.fidl#198)*


### GetJob {:#GetJob}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>job</code></td>
            <td>
                <code>handle&lt;job&gt;</code>
            </td>
        </tr></table>

## Launcher {:#Launcher}
*Defined in [test.fidlcat.sys/sys.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/sys.test.fidl#274)*


### CreateComponent {:#CreateComponent}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>launch_info</code></td>
            <td>
                <code><a class='link' href='#LaunchInfo'>LaunchInfo</a></code>
            </td>
        </tr><tr>
            <td><code>controller</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ComponentController'>ComponentController</a>&gt;?</code>
            </td>
        </tr></table>



## Loader {:#Loader}
*Defined in [test.fidlcat.sys/sys.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/sys.test.fidl#291)*


### LoadUrl {:#LoadUrl}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>url</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>package</code></td>
            <td>
                <code><a class='link' href='#Package'>Package</a>?</code>
            </td>
        </tr></table>

## Runner {:#Runner}
*Defined in [test.fidlcat.sys/sys.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/sys.test.fidl#352)*


### StartComponent {:#StartComponent}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>package</code></td>
            <td>
                <code><a class='link' href='#Package'>Package</a></code>
            </td>
        </tr><tr>
            <td><code>startup_info</code></td>
            <td>
                <code><a class='link' href='#StartupInfo'>StartupInfo</a></code>
            </td>
        </tr><tr>
            <td><code>controller</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ComponentController'>ComponentController</a>&gt;?</code>
            </td>
        </tr></table>



## ServiceProvider {:#ServiceProvider}
*Defined in [test.fidlcat.sys/sys.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/sys.test.fidl#375)*


### ConnectToService {:#ConnectToService}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>channel</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>





## **STRUCTS**

### Buffer {:#Buffer}
*Defined in [test.fidlcat.sys/sys.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/sys.test.fidl#17)*



 A Buffer for data whose size is not necessarily a multiple of the page
 size.

 VMO objects have a physical size that is always a multiple of the page
 size. As such, VMO alone cannot serve as a buffer for arbitrarly sized
 data. `fuchsia.mem.Buffer` is a standard struct that aggregate the VMO
 and its size.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
            <td> The vmo.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The size of the data in the vmo in bytes. This size must be smaller
 than the physical size of the vmo.
</td>
            <td>No default</td>
        </tr>
</table>

### EnvironmentOptions {:#EnvironmentOptions}
*Defined in [test.fidlcat.sys/sys.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/sys.test.fidl#115)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>inherit_parent_services</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>allow_parent_runners</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>kill_on_oom</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>delete_storage_on_death</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FlatNamespace {:#FlatNamespace}
*Defined in [test.fidlcat.sys/sys.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/sys.test.fidl#184)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>paths</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>directories</code></td>
            <td>
                <code>vector&lt;channel&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FileDescriptor {:#FileDescriptor}
*Defined in [test.fidlcat.sys/sys.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/sys.test.fidl#205)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>type0</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>type1</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>type2</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>handle0</code></td>
            <td>
                <code>handle&lt;handle&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>handle1</code></td>
            <td>
                <code>handle&lt;handle&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>handle2</code></td>
            <td>
                <code>handle&lt;handle&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### LaunchInfo {:#LaunchInfo}
*Defined in [test.fidlcat.sys/sys.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/sys.test.fidl#219)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>url</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>arguments</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>out</code></td>
            <td>
                <code><a class='link' href='#FileDescriptor'>FileDescriptor</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#FileDescriptor'>FileDescriptor</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>directory_request</code></td>
            <td>
                <code>handle&lt;channel&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>flat_namespace</code></td>
            <td>
                <code><a class='link' href='#FlatNamespace'>FlatNamespace</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>additional_services</code></td>
            <td>
                <code><a class='link' href='#ServiceList'>ServiceList</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ServiceList {:#ServiceList}
*Defined in [test.fidlcat.sys/sys.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/sys.test.fidl#257)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>names</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>provider</code></td>
            <td>
                <code><a class='link' href='#ServiceProvider'>ServiceProvider</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>host_directory</code></td>
            <td>
                <code>handle&lt;channel&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StartupInfo {:#StartupInfo}
*Defined in [test.fidlcat.sys/sys.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/sys.test.fidl#300)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>launch_info</code></td>
            <td>
                <code><a class='link' href='#LaunchInfo'>LaunchInfo</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>flat_namespace</code></td>
            <td>
                <code><a class='link' href='#FlatNamespace'>FlatNamespace</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>program_metadata</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ProgramMetadata'>ProgramMetadata</a>&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ProgramMetadata {:#ProgramMetadata}
*Defined in [test.fidlcat.sys/sys.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/sys.test.fidl#316)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Package {:#Package}
*Defined in [test.fidlcat.sys/sys.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/sys.test.fidl#330)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='#Buffer'>Buffer</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>directory</code></td>
            <td>
                <code>handle&lt;channel&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>resolved_url</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### TerminationReason {:#TerminationReason}
Type: <code>uint32</code>

*Defined in [test.fidlcat.sys/sys.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/sys.test.fidl#26)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>EXITED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>URL_INVALID</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>PACKAGE_NOT_FOUND</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>INTERNAL_ERROR</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>PROCESS_CREATION_ERROR</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>RUNNER_FAILED</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>RUNNER_TERMINATED</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNSUPPORTED</code></td>
            <td><code>8</code></td>
            <td></td>
        </tr></table>











## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/sys.test.fidl#113">kLabelMaxLength</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    
</table>

