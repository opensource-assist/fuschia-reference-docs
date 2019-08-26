Project: /_project.yaml
Book: /_book.yaml

# fuchsia.modular.intl.internal




## **STRUCTS**

### RawProfileData {:#RawProfileData}
*Defined in [fuchsia.modular.intl.internal/internal.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/modular/bin/basemgr/intl_property_provider_impl/internal.fidl#12)*



 Raw inputs for producing a `fuchsia.intl.Profile`. This is only used internally in
 `IntlPropertyProviderImpl`, for keeping track of incoming settings before assembling a
 `fuchsia.intl.Profile`.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>language_tags</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.intl/index.html'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/index.html#LocaleId'>LocaleId</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>time_zone_ids</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.intl/index.html'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/index.html#TimeZoneId'>TimeZoneId</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>calendar_ids</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.intl/index.html'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/index.html#CalendarId'>CalendarId</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>temperature_unit</code></td>
            <td>
                <code><a class='link' href='../fuchsia.intl/index.html'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/index.html#TemperatureUnit'>TemperatureUnit</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>













