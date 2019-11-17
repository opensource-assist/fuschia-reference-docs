[TOC]

# fuchsia.netemul.environment


## **PROTOCOLS**

## ManagedEnvironment {#ManagedEnvironment}
*Defined in [fuchsia.netemul.environment/environment.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/environment.fidl#72)*

<p>Managed environment is made available on netemul runners.
Typically this interface will be used by the root runner
to setup the testing environment.</p>

### GetLauncher {#GetLauncher}

<p>Gets the managed launcher for the environment.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>launcher</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.sys/'>fuchsia.sys</a>/<a class='link' href='../fuchsia.sys/#Launcher'>Launcher</a>&gt;</code>
            </td>
        </tr></table>



### CreateChildEnvironment {#CreateChildEnvironment}

<p>Creates a nested managed environment.</p>

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



### ConnectToService {#ConnectToService}

<p>Connects to a service named <code>name</code> provided by this environment.</p>

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



### AddDevice {#AddDevice}

<p>Exposes new virtual device <code>device</code> for all components within this environment</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device</code></td>
            <td>
                <code><a class='link' href='#VirtualDevice'>VirtualDevice</a></code>
            </td>
        </tr></table>



### RemoveDevice {#RemoveDevice}

<p>Removes virtual device mounted at <code>path</code> (relative to /vdev)</p>

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

### LaunchService {#LaunchService}
*Defined in [fuchsia.netemul.environment/environment.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/environment.fidl#11)*



<p>A single service to be launched in managed environment.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>Service name.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>url</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>Service launch url (fuchsia component url).</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>arguments</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
            <td><p>Service launch arguments</p>
</td>
            <td>No default</td>
        </tr>
</table>

### VirtualDevice {#VirtualDevice}
*Defined in [fuchsia.netemul.environment/environment.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/environment.fidl#22)*



<p>A single virtual device to make available for child processes.
Virtual devices are mounted on /vdev.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>path</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>Relative path to /vdev.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>device</code></td>
            <td>
                <code><a class='link' href='../fuchsia.netemul.network/'>fuchsia.netemul.network</a>/<a class='link' href='../fuchsia.netemul.network/#DeviceProxy'>DeviceProxy</a></code>
            </td>
            <td><p>Virtual device server.</p>
</td>
            <td>No default</td>
        </tr>
</table>





## **TABLES**

### LoggerOptions {#LoggerOptions}


*Defined in [fuchsia.netemul.environment/environment.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/environment.fidl#30)*

<p>Logger specific options for a created environment</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>enabled</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Enable printing logs.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>klogs_enabled</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Enable kernel logs (no effect if <code>enabled</code> is false).</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>filter_options</code></td>
            <td>
                <code><a class='link' href='../fuchsia.logger/'>fuchsia.logger</a>/<a class='link' href='../fuchsia.logger/#LogFilterOptions'>LogFilterOptions</a></code>
            </td>
            <td><p>LogFilter Options straight from fuchsia.logger.LogFilter.
The LogFilterOptions will be passed directly to the <code>Listen</code>
function of the fuchsia.logger.Log service without any
modification. If none provided, assume null. See <code>Listen</code> of
fuchsia.logger.Log for more information.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>syslog_output</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Use the parent environment's syslog for output, only enriching
tags with environment names. If false or not provided,
environment logs are printed to stdout.</p>
</td>
        </tr></table>

### EnvironmentOptions {#EnvironmentOptions}


*Defined in [fuchsia.netemul.environment/environment.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/network/testing/netemul/lib/fidl/environment.fidl#48)*

<p>Options used to create environment.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>Environment name, for debugging purposes.
If none provided, a random name will be generated.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>services</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#LaunchService'>LaunchService</a>&gt;</code>
            </td>
            <td><p>Services to register on environment.
If none provided, no additional services will be registered.
However, a ManagedEnvironment may still register some default
services.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>devices</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#VirtualDevice'>VirtualDevice</a>&gt;</code>
            </td>
            <td><p>Devices to make available.
If none provided, no devices will be made available.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>inherit_parent_launch_services</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Whether to inherit service launch options from parent environment.
If none provided, assume false.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>logger_options</code></td>
            <td>
                <code><a class='link' href='#LoggerOptions'>LoggerOptions</a></code>
            </td>
            <td><p>Logger Options.
If none provided, log printing is disabled by default.</p>
</td>
        </tr></table>









