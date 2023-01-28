# POSIX Time Zone Specifications
The POSIX time zone format is the traditionally used format for AIX systems, The advantage of POSIX is that you can easily and explicitly specify the time zone and daylight saving time (DST) details manually, however you wish.And whenever a nation's government decides to change its DST rules, the POSIX format is simpler because we can simply change the variable definition.

SuperY WiFI Clock can accept time zone specifications that are written according to the POSIX standard's rules. POSIX time zone specifications are inadequate to deal with the complexity of real-world time zone history, but there are sometimes reasons to use them.

A POSIX time zone specification has the form

```STD offset [ DST [ dstoffset ] [ , rule ] ]```

(For readability, we show spaces between the fields, but spaces should not be used in practice.) The fields are:

- STD is the zone abbreviation to be used for standard time(It's just a name)
- offset is the zone's standard-time offset from UTC.
- DST is the zone abbreviation to be used for daylight-savings time(It's just a name). If this field and the following ones are omitted, the zone uses a fixed UTC offset with no daylight-savings rule.
- dstoffset is the daylight-savings offset from UTC. This field is typically omitted, since it defaults to one hour less than the standard-time offset, which is usually the right thing.
- rule defines the rule for when daylight savings is in effect, as described below.

The daylight-savings transition rule has the format

```
dstdate [ / dsttime ] , stddate [ / stdtime ]
```

(As before, spaces should not be included in practice.) The dstdate and dsttime fields define when daylight-savings time starts, while stddate and stdtime define when standard time starts. (In some cases, notably in zones south of the equator, the former might be later in the year than the latter.) The date fields have one of these formats:

### n(SuperY WiFi Clock not support this)

A plain integer denotes a day of the year, counting from zero to 364, or to 365 in leap years.

### Jn(SuperY WiFi Clock not support this)

In this form, n counts from 1 to 365, and February 29 is not counted even if it is present. (Thus, a transition occurring on February 29 could not be specified this way. However, days after February have the same numbers whether it's a leap year or not, so that this form is usually more useful than the plain-integer form for transitions on fixed dates.)

### Mm.n.d

This form specifies a transition that always happens during the same month and on the same day of the week. m identifies the month, from 1 to 12. n specifies the n'th occurrence of the weekday identified by d. n is a number between 1 and 4, or 5 meaning the last occurrence of that weekday in the month (which could be the fourth or the fifth). d is a number between 0 and 6, with 0 indicating Sunday. For example, M3.2.0 means “the second Sunday in March”.

The time fields in a transition rule have the same format as the offset fields described previously, except that they cannot contain signs. They define the current local time at which the change to the other time occurs. If omitted, they default to 02:00.

The default posixrules is to use the rule M3.2.0,M11.1.0, which corresponds to USA practice as of 2020 (that is, spring forward on the second Sunday of March, fall back on the first Sunday of November, both transitions occurring at 2AM prevailing time).

## Example

```
CST6CDT5,M3.2.0/2:00,M11.1.0/2:00
```

This would effect a change to daylight saving time at 2:00 AM on the second Sunday in March and change back at 2:00 AM on the first Sunday in November. The breakdown of the string is:

- CST is the abbreviation name used when DST is off
- 6 hours is the time difference from UTC , means UTC -6:00
- CDT is the abbreviation name used when DST is on
- 5 means UTC-5:00 when DST is on
- ,M3 is the third month
- .2 is the second occurrence of the day in the month
- .0 is Sunday
- /2:00 is the time
- ,M11 is the eleventh month
- .1 is the first occurrence of the day in the month
- .0 is Sunday
- /2:00 is the time


It can be abbreviated as CST6CDT , The default posixrules is to use the rule M3.2.0/2:00,M11.1.0/2:00 and dstoffset is one hour ahead of STD.

and some common posix string:



or I also write a simple page to generate posix string at http://www.topyuan.top/posix

you can study global timezone rules at:

https://en.wikipedia.org/wiki/List_of_tz_database_time_zones

If you have any questions about posix time zone or find bugs on SuperY WiFi Clock , please contact me admin@topyuan.top
