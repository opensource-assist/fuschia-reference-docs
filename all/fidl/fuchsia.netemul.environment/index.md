Project: /_project.yaml
Book: /_book.yaml

# fuchsia.netemul.environment


## **PROTOCOLS**

## ManagedEnvironment {:#ManagedEnvironment}
*Defined in [fuchsia.netemul.environment/environment.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/environment.fidl#72)*

 Managed environment is made available on netemul runners.
 Typically this interface will be used by the root runner
 to setup the testing environment.

### GetLauncher {:#GetLauncher}

 Gets the managed launcher for the environment.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>launcher</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.sys/index.html'>fuchsia.sys</a>/<a class='link' href='../fuchsia.sys/index.html#Launcher'>Launcher</a>&gt;</code>
            </td>
        </tr></table>



### CreateChildEnvironment {:#CreateChildEnvironment}

 Creates a nested managed environment.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>child_env</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ManagedEnvironment'>ManagedEnvironment</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#EnvironmentOptions'>EnvironmentOptions</a></code>
            </td>
        </tr></table>



### ConnectToService {:#ConnectToService}

 Connects to a service named `name` provided by this environment.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>req</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



### AddDevice {:#AddDevice}

 Exposes new virtual device `device` for all components within this environment

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device</code></td>
            <td>
                <code><a class='link' href='#VirtualDevice'>VirtualDevice</a></code>
            </td>
        </tr></table>



### RemoveDevice {:#RemoveDevice}

 Removes virtual device mounted at `path` (relative to /vdev)

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>path</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>





## **STRUCTS**

### LaunchService {:#LaunchService}
*Defined in [fuchsia.netemul.environment/environment.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/environment.fidl#11)*



 A single service to be launched in managed environment.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Service name.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>url</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Service launch url (fuchsia component url).
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>arguments</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
            <td> Service launch arguments
</td>
            <td>No default</td>
        </tr>
</table>

### VirtualDevice {:#VirtualDevice}
*Defined in [fuchsia.netemul.environment/environment.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/environment.fidl#22)*



 A single virtual device to make available for child processes.
 Virtual devices are mounted on /vdev.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>path</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Relative path to /vdev.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>device</code></td>
            <td>
                <code><a class='link' href='../fuchsia.netemul.network/index.html'>fuchsia.netemul.network</a>/<a class='link' href='../fuchsia.netemul.network/index.html#DeviceProxy'>DeviceProxy</a></code>
            </td>
            <td> Virtual device server.
</td>
            <td>No default</td>
        </tr>
</table>





## **TABLES**

### LoggerOptions {:#LoggerOptions}


*Defined in [fuchsia.netemul.environment/environment.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/environment.fidl#30)*

 Logger specific options for a created environment


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>enabled</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Enable printing logs.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>klogs_enabled</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Enable kernel logs (no effect if `enabled` is false).
</td>
        </tr><tr>
            <td>3</td>
            <td><code>filter_options</code></td>
            <td>
                <code><a class='link' href='../fuchsia.logger/index.html'>fuchsia.logger</a>/<a class='link' href='../fuchsia.logger/index.html#LogFilterOptions'>LogFilterOptions</a></code>
            </td>
            <td> LogFilter Options straight from fuchsia.logger.LogFilter.
 The LogFilterOptions will be passed directly to the `Listen`
 function of the fuchsia.logger.Log service without any
 modification. If none provided, assume null. See `Listen` of
 fuchsia.logger.Log for more information.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>syslog_output</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Use the parent environment's syslog for output, only enriching
 tags with environment names. If false or not provided,
 environment logs are printed to stdout.
</td>
        </tr></table>

### EnvironmentOptions {:#EnvironmentOptions}


*Defined in [fuchsia.netemul.environment/environment.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/environment.fidl#48)*

 Options used to create environment.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Environment name, for debugging purposes.
 If none provided, a random name will be generated.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>services</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#LaunchService'>LaunchService</a>&gt;</code>
            </td>
            <td> Services to register on environment.
 If none provided, no additional services will be registered.
 However, a ManagedEnvironment may still register some default
 services.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>devices</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#VirtualDevice'>VirtualDevice</a>&gt;</code>
            </td>
            <td> Devices to make available.
 If none provided, no devices will be made available.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>inherit_parent_launch_services</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Whether to inherit service launch options from parent environment.
 If none provided, assume false.
</td>
        </tr><tr>
            <td>5</td>
            <td><code>logger_options</code></td>
            <td>
                <code><a class='link' href='#LoggerOptions'>LoggerOptions</a></code>
            </td>
            <td> Logger Options.
 If none provided, log printing is disabled by default.
</td>
        </tr></table>









