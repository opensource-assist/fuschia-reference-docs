Project: /_project.yaml
Book: /_book.yaml

# fuchsia.intl


## **PROTOCOLS**

## PropertyProvider {:#PropertyProvider}
*Defined in [fuchsia.intl/property_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.intl/property_provider.fidl#16)*

 Provides internationalization properties.

 Components that need to change their behavior in response to the user's internationalization
 profile may request an instance of this service from their namespace, if available. A component
 may choose to pass along the service that it received from its parent to its own children, or to
 override it and apply additional customizations.

 See also `fuchsia.ui.views.View`.

### GetProfile {:#GetProfile}

 Gets the user's internationalization profile.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>profile</code></td>
            <td>
                <code><a class='link' href='#Profile'>Profile</a></code>
            </td>
        </tr></table>

### OnChange {:#OnChange}

 Indicates that the properties may have changed and the client should query them again.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## **STRUCTS**

### LocaleId {:#LocaleId}
*Defined in [fuchsia.intl/intl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.intl/intl.fidl#18)*



 Typed identifier for a single Locale, which is a set of internationalization-related properties.

 Most APIs that consume locales will probably want to accept a vector of locales to account for
 priority.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Unicode BCP-47 Locale Identifier
 (http://www.unicode.org/reports/tr35/#BCP_47_Conformance).

 Must be canonicalized and well-formed. This field should not be populated from arbitrary
 user- or third-party input, but instead generated programmatically.

 Includes language, region, script, and variant, plus Unicode extensions (under the "u"
 singleton). Other extensions are allowed but ignored.

 Examples:
   "en-US"
     American English
   "fr-u-hc-h12"
     French, with 12-hour clock
   "ar-EG-u-fw-mon-nu-latn"
     Egyptian Arabic with "Latin" numerals and first day of week on Monday
</td>
            <td>No default</td>
        </tr>
</table>

### CalendarId {:#CalendarId}
*Defined in [fuchsia.intl/intl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.intl/intl.fidl#39)*



 Typed identifier for a single calendar system. Currently consists only of a calendar ID.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Unicode BCP-47 Locale Identifier with an undefined language tag and a single extension
 specifying the calendar ID (from
 https://unicode.org/repos/cldr/trunk/common/bcp47/calendar.xml).

 Examples:
   "und-u-ca-gregory"
   "und-u-ca-islamic"
</td>
            <td>No default</td>
        </tr>
</table>

### TimeZoneId {:#TimeZoneId}
*Defined in [fuchsia.intl/intl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.intl/intl.fidl#51)*



 Typed identifier for a time zone.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Time zone ID from tzdata, e.g. "America/New_York". See https://www.iana.org/time-zones.
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### TemperatureUnit {:#TemperatureUnit}
Type: <code>uint32</code>

*Defined in [fuchsia.intl/intl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.intl/intl.fidl#57)*

 Selection of temperature unit.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>CELSIUS</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>FAHRENHEIT</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### RegulatoryDomain {:#RegulatoryDomain}


*Defined in [fuchsia.intl/intl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.intl/intl.fidl#8)*

 Typed identifier for a regulatory domain as specified in the IEEE 802.11 standard.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>country_code</code></td>
            <td>
                <code>string</code>
            </td>
            <td> ISO 3166-1 alpha-2, a two-letter code representing a domain of operation.
 (https://www.iso.org/publication/PUB500001.html)
</td>
        </tr></table>

### Profile {:#Profile}


*Defined in [fuchsia.intl/intl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.intl/intl.fidl#69)*

 A collection of ranked internationalization properties.

 There is no implied origin for this information; it might come from a user account, device
 settings, a synthesis of user settings and app-specific overrides, or anywhere else.

 Language-independent properties that are supported by Unicode BCP-47 Locale IDs (e.g.
 first-day-of-week, time zone) are denormalized into the locale IDs in `locales`.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>locales</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#LocaleId'>LocaleId</a>&gt;</code>
            </td>
            <td> Ranked list of locales (in descending order).
</td>
        </tr><tr>
            <td>2</td>
            <td><code>calendars</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#CalendarId'>CalendarId</a>&gt;</code>
            </td>
            <td> Ranked list of calendars (in descending order). The first entry is the primary calendar, and
 will be equal to the calendar indicated in `locales`.
 The list is intended for use by applications that can display multiple calendar systems.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>time_zones</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#TimeZoneId'>TimeZoneId</a>&gt;</code>
            </td>
            <td> Ranked list of time zones (in descending order). The first entry is the primary time zone,
 which should be used by default for formatting dates and times; it will be equal to the
 calendar indicated in `locales`.
 The list is intended for use by applications that can display multiple time zones, e.g.
 a world clock.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>temperature_unit</code></td>
            <td>
                <code><a class='link' href='#TemperatureUnit'>TemperatureUnit</a></code>
            </td>
            <td> Selected temperature unit.
</td>
        </tr></table>









