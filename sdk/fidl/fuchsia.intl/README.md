[TOC]

# fuchsia.intl


## **PROTOCOLS**

## PropertyProvider {#PropertyProvider}
*Defined in [fuchsia.intl/property_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.intl/property_provider.fidl#16)*

<p>Provides internationalization properties.</p>
<p>Components that need to change their behavior in response to the user's internationalization
profile may request an instance of this service from their namespace, if available. A component
may choose to pass along the service that it received from its parent to its own children, or to
override it and apply additional customizations.</p>
<p>See also <code>fuchsia.ui.views.View</code>.</p>

### GetProfile {#GetProfile}

<p>Gets the user's internationalization profile.</p>

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

### OnChange {#OnChange}

<p>Indicates that the properties may have changed and the client should query them again.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## **STRUCTS**

### LocaleId {#LocaleId}
*Defined in [fuchsia.intl/intl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.intl/intl.fidl#18)*



<p>Typed identifier for a single Locale, which is a set of internationalization-related properties.</p>
<p>Most APIs that consume locales will probably want to accept a vector of locales to account for
priority.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>Unicode BCP-47 Locale Identifier
(http://www.unicode.org/reports/tr35/#BCP_47_Conformance).</p>
<p>Must be canonicalized and well-formed. This field should not be populated from arbitrary
user- or third-party input, but instead generated programmatically.</p>
<p>Includes language, region, script, and variant, plus Unicode extensions (under the &quot;u&quot;
singleton). Other extensions are allowed but ignored.</p>
<p>Examples:
&quot;en-US&quot;
American English
&quot;fr-u-hc-h12&quot;
French, with 12-hour clock
&quot;ar-EG-u-fw-mon-nu-latn&quot;
Egyptian Arabic with &quot;Latin&quot; numerals and first day of week on Monday</p>
</td>
            <td>No default</td>
        </tr>
</table>

### CalendarId {#CalendarId}
*Defined in [fuchsia.intl/intl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.intl/intl.fidl#39)*



<p>Typed identifier for a single calendar system. Currently consists only of a calendar ID.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>Unicode BCP-47 Locale Identifier with an undefined language tag and a single extension
specifying the calendar ID (from
https://unicode.org/repos/cldr/trunk/common/bcp47/calendar.xml).</p>
<p>Examples:
&quot;und-u-ca-gregory&quot;
&quot;und-u-ca-islamic&quot;</p>
</td>
            <td>No default</td>
        </tr>
</table>

### TimeZoneId {#TimeZoneId}
*Defined in [fuchsia.intl/intl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.intl/intl.fidl#54)*



<p>Typed identifier for a time zone.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>Time zone ID from tzdata, e.g. &quot;America/New_York&quot;. See https://www.iana.org/time-zones.</p>
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### TemperatureUnit {#TemperatureUnit}
Type: <code>uint32</code>

*Defined in [fuchsia.intl/intl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.intl/intl.fidl#60)*

<p>Selection of <a href="https://en.wikipedia.org/wiki/Degree_(temperature)">temperature units</a>.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>CELSIUS</code></td>
            <td><code>0</code></td>
            <td><p>The temperature should be formatted to show temperature in degrees Celsius.</p>
</td>
        </tr><tr>
            <td><code>FAHRENHEIT</code></td>
            <td><code>1</code></td>
            <td><p>The temperature should be formatted to show temperature in degrees Fahrenheit.</p>
</td>
        </tr></table>



## **TABLES**

### RegulatoryDomain {#RegulatoryDomain}


*Defined in [fuchsia.intl/intl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.intl/intl.fidl#8)*

<p>Typed identifier for a regulatory domain as specified in the IEEE 802.11 standard.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>country_code</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>ISO 3166-1 alpha-2, a two-letter code representing a domain of operation.
(https://www.iso.org/publication/PUB500001.html)</p>
</td>
        </tr></table>

### Profile {#Profile}


*Defined in [fuchsia.intl/intl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.intl/intl.fidl#74)*

<p>A collection of ranked internationalization properties.</p>
<p>There is no implied origin for this information; it might come from a user account, device
settings, a synthesis of user settings and app-specific overrides, or anywhere else.</p>
<p>Language-independent properties that are supported by Unicode BCP-47 Locale IDs (e.g.
first-day-of-week, time zone) are denormalized into the locale IDs in <code>locales</code>.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>locales</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#LocaleId'>LocaleId</a>&gt;</code>
            </td>
            <td><p>Ranked list of locales (in descending order of preference).  The vector will always
contain at least one element.  For example, locales = [ LocaleId(&quot;en-US&quot;) ] is valid, but
locales = [], or locales = <unset> is not.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>calendars</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#CalendarId'>CalendarId</a>&gt;</code>
            </td>
            <td><p>Ranked list of calendars (in descending order of preference).
The first entry is the primary calendar, and will be equal to the calendar indicated
in <code>locales</code>.
The vector will always contain at least one element.
The list allows multiple ranked preferences, and is intended for use
by applications that can display multiple calendar systems.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>time_zones</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#TimeZoneId'>TimeZoneId</a>&gt;</code>
            </td>
            <td><p>Ranked list of time zones (in descending order). The first entry is the primary time zone,
which should be used by default for formatting dates and times; it will be equal to the
calendar indicated in <code>locales</code>.
The list is intended for use by applications that can display multiple time zones, e.g.
a world clock.
The vector will always contain at least one element.
On Fuchsia, the default time zone is always <code>DEFAULT_TIME_ZONE_ID</code> when
no more specific time zones have been defined or selected.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>temperature_unit</code></td>
            <td>
                <code><a class='link' href='#TemperatureUnit'>TemperatureUnit</a></code>
            </td>
            <td><p>Selected temperature unit. The unit is always reported: if there is no
setting in the current environment, the default value of CELSIUS is
used.</p>
</td>
        </tr></table>









## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="DEFAULT_TIME_ZONE_ID">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.intl/intl.fidl#51">DEFAULT_TIME_ZONE_ID</a></td>
            <td><code>UTC</code></td>
                    <td><code>String</code></td>
            <td><p>This is the time zone reported when no time zones have been set.</p>
</td>
        </tr>
    
</table>



