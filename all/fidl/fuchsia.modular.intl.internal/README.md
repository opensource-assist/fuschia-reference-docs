[TOC]

# fuchsia.modular.intl.internal




## **STRUCTS**

### HourCycle {#HourCycle}
*Defined in [fuchsia.modular.intl.internal/internal.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/modular/bin/basemgr/intl_property_provider_impl/internal.fidl#12)*



<p>Stores the optional hour cycle setting.  An enum can not be optional so we
wrap it here.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>setting</code></td>
            <td>
                <code><a class='link' href='../fuchsia.setui/'>fuchsia.setui</a>/<a class='link' href='../fuchsia.setui/#HourCycle'>HourCycle</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### RawProfileData {#RawProfileData}
*Defined in [fuchsia.modular.intl.internal/internal.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/modular/bin/basemgr/intl_property_provider_impl/internal.fidl#19)*



<p>Raw inputs for producing a <code>fuchsia.intl.Profile</code>. This is only used internally in
<code>IntlPropertyProviderImpl</code>, for keeping track of incoming settings before assembling a
<code>fuchsia.intl.Profile</code>.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>language_tags</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.intl/'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/#LocaleId'>LocaleId</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>time_zone_ids</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.intl/'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/#TimeZoneId'>TimeZoneId</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>calendar_ids</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.intl/'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/#CalendarId'>CalendarId</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>temperature_unit</code></td>
            <td>
                <code><a class='link' href='../fuchsia.intl/'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/#TemperatureUnit'>TemperatureUnit</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>hour_cycle</code></td>
            <td>
                <code><a class='link' href='#HourCycle'>HourCycle</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>













