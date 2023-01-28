# POSIX Time Zone Specifications
The POSIX time zone format is the traditionally used format for AIX systems, The advantage of POSIX is that you can easily and explicitly specify the time zone and daylight saving time (DST) details manually, however you wish.And whenever a nation's government decides to change its DST rules, the POSIX format is simpler because we can simply change the variable definition.

SuperY WiFI Clock can accept time zone specifications that are written according to the POSIX standard's rules. POSIX time zone specifications are inadequate to deal with the complexity of real-world time zone history, but there are sometimes reasons to use them.

A POSIX time zone specification has the form

```STD offset [ DST [ dstoffset ] [ , rule ] ]```

(For readability, we show spaces between the fields, but spaces should not be used in practice.) The fields are:

- STD is the zone abbreviation to be used for standard time(It's just a name), and if <name> means name can use + or -, for example you can write <+3> as STD name
- offset is the zone's standard-time offset from UTC.
- DST is the zone abbreviation to be used for daylight-savings time(It's just a name), and if <name> means name can use + or -, for example you can write <+3> as DST name. If this field and the following ones are omitted, the zone uses a fixed UTC offset with no daylight-savings rule.
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

|Region|Posix String|
:-|-:
|Africa/Casablanca|WET0WEST,M3.5.0,M10.5.0/3|
|Africa/Ceuta|CET-1CEST,M3.5.0,M10.5.0/3|
|Africa/El_Aaiun|WET0WEST,M3.5.0,M10.5.0/3|
|Africa/Windhoek|WAT-1WAST,M9.1.0,M4.1.0|
|America/Adak|HST10HDT,M3.2.0,M11.1.0|
|America/Anchorage|AKST9AKDT,M3.2.0,M11.1.0|
|America/Asuncion|<-04>4<-03>,M10.1.0/0,M3.4.0/0|
|America/Bahia_Banderas|CST6CDT,M4.1.0,M10.5.0|
|America/Boise|MST7MDT,M3.2.0,M11.1.0|
|America/Cambridge_Bay|MST7MDT,M3.2.0,M11.1.0|
|America/Campo_Grande|<-04>4<-03>,M10.3.0/0,M2.3.0/0|
|America/Chicago|CST6CDT,M3.2.0,M11.1.0|
|America/Chihuahua|MST7MDT,M4.1.0,M10.5.0|
|America/Cuiaba|<-04>4<-03>,M10.3.0/0,M2.3.0/0|
|America/Dawson|PST8PDT,M3.2.0,M11.1.0|
|America/Denver|MST7MDT,M3.2.0,M11.1.0|
|America/Detroit|EST5EDT,M3.2.0,M11.1.0|
|America/Edmonton|MST7MDT,M3.2.0,M11.1.0|
|America/Glace_Bay|AST4ADT,M3.2.0,M11.1.0|
|America/Goose_Bay|AST4ADT,M3.2.0,M11.1.0|
|America/Halifax|AST4ADT,M3.2.0,M11.1.0|
|America/Havana|CST5CDT,M3.2.0/0,M11.1.0/1|
|America/Indiana/Indianapolis|EST5EDT,M3.2.0,M11.1.0|
|America/Indiana/Knox|CST6CDT,M3.2.0,M11.1.0|
|America/Indiana/Marengo|EST5EDT,M3.2.0,M11.1.0|
|America/Indiana/Petersburg|EST5EDT,M3.2.0,M11.1.0|
|America/Indiana/Tell_City|CST6CDT,M3.2.0,M11.1.0|
|America/Indiana/Vevay|EST5EDT,M3.2.0,M11.1.0|
|America/Indiana/Vincennes|EST5EDT,M3.2.0,M11.1.0|
|America/Indiana/Winamac|EST5EDT,M3.2.0,M11.1.0|
|America/Inuvik|MST7MDT,M3.2.0,M11.1.0|
|America/Iqaluit|EST5EDT,M3.2.0,M11.1.0|
|America/Juneau|AKST9AKDT,M3.2.0,M11.1.0|
|America/Kentucky/Louisville|EST5EDT,M3.2.0,M11.1.0|
|America/Kentucky/Monticello|EST5EDT,M3.2.0,M11.1.0|
|America/Los_Angeles|PST8PDT,M3.2.0,M11.1.0|
|America/Matamoros|CST6CDT,M3.2.0,M11.1.0|
|America/Mazatlan|MST7MDT,M4.1.0,M10.5.0|
|America/Menominee|CST6CDT,M3.2.0,M11.1.0|
|America/Merida|CST6CDT,M4.1.0,M10.5.0|
|America/Metlakatla|AKST9AKDT,M3.2.0,M11.1.0|
|America/Mexico_City|CST6CDT,M4.1.0,M10.5.0|
|America/Miquelon|<-03>3<-02>,M3.2.0,M11.1.0|
|America/Moncton|AST4ADT,M3.2.0,M11.1.0|
|America/Monterrey|CST6CDT,M4.1.0,M10.5.0|
|America/Nassau|EST5EDT,M3.2.0,M11.1.0|
|America/New_York|EST5EDT,M3.2.0,M11.1.0|
|America/Nipigon|EST5EDT,M3.2.0,M11.1.0|
|America/Nome|AKST9AKDT,M3.2.0,M11.1.0|
|America/North_Dakota/Beulah|CST6CDT,M3.2.0,M11.1.0|
|America/North_Dakota/Center|CST6CDT,M3.2.0,M11.1.0|
|America/North_Dakota/New_Salem|CST6CDT,M3.2.0,M11.1.0|
|America/Ojinaga|MST7MDT,M3.2.0,M11.1.0|
|America/Pangnirtung|EST5EDT,M3.2.0,M11.1.0|
|America/Port-au-Prince|EST5EDT,M3.2.0,M11.1.0|
|America/Rainy_River|CST6CDT,M3.2.0,M11.1.0|
|America/Rankin_Inlet|CST6CDT,M3.2.0,M11.1.0|
|America/Resolute|CST6CDT,M3.2.0,M11.1.0|
|America/Sao_Paulo|<-03>3<-02>,M10.3.0/0,M2.3.0/0|
|America/Scoresbysund|<-01>1<+00>,M3.5.0/0,M10.5.0/1|
|America/Sitka|AKST9AKDT,M3.2.0,M11.1.0|
|America/St_Johns|NST3:30NDT,M3.2.0,M11.1.0|
|America/Thule|AST4ADT,M3.2.0,M11.1.0|
|America/Thunder_Bay|EST5EDT,M3.2.0,M11.1.0|
|America/Tijuana|PST8PDT,M3.2.0,M11.1.0|
|America/Toronto|EST5EDT,M3.2.0,M11.1.0|
|America/Vancouver|PST8PDT,M3.2.0,M11.1.0|
|America/Whitehorse|PST8PDT,M3.2.0,M11.1.0|
|America/Winnipeg|CST6CDT,M3.2.0,M11.1.0|
|America/Yakutat|AKST9AKDT,M3.2.0,M11.1.0|
|America/Yellowknife|MST7MDT,M3.2.0,M11.1.0|
|Antarctica/McMurdo|NZST-12NZDT,M9.5.0,M4.1.0/3|
|Antarctica/Troll|<+00>0<+02>-2,M3.5.0/1,M10.5.0/3|
|Arctic/Longyearbyen|CET-1CEST,M3.5.0,M10.5.0/3|
|Asia/Amman|EET-2EEST,M3.5.4/24,M10.5.5/1|
|Asia/Beirut|EET-2EEST,M3.5.0/0,M10.5.0/0|
|Asia/Damascus|EET-2EEST,M3.5.5/0,M10.5.5/0|
|Asia/Gaza|EET-2EEST,M3.5.6/1,M10.5.6/1|
|Asia/Hebron|EET-2EEST,M3.5.6/1,M10.5.6/1|
|Asia/Nicosia|EET-2EEST,M3.5.0/3,M10.5.0/4|
|Atlantic/Azores|<-01>1<+00>,M3.5.0/0,M10.5.0/1|
|Atlantic/Bermuda|AST4ADT,M3.2.0,M11.1.0|
|Atlantic/Canary|WET0WEST,M3.5.0/1,M10.5.0|
|Atlantic/Faroe|WET0WEST,M3.5.0/1,M10.5.0|
|Atlantic/Madeira|WET0WEST,M3.5.0/1,M10.5.0|
|Australia/Adelaide|ACST-9:30ACDT,M10.1.0,M4.1.0/3|
|Australia/Broken_Hill|ACST-9:30ACDT,M10.1.0,M4.1.0/3|
|Australia/Currie|AEST-10AEDT,M10.1.0,M4.1.0/3|
|Australia/Hobart|AEST-10AEDT,M10.1.0,M4.1.0/3|
|Australia/Lord_Howe|<+1030>-10:30<+11>-11,M10.1.0,M4.1.0|
|Australia/Melbourne|AEST-10AEDT,M10.1.0,M4.1.0/3|
|Australia/Sydney|AEST-10AEDT,M10.1.0,M4.1.0/3|
|CET|CET-1CEST,M3.5.0,M10.5.0/3|
|CST6CDT|CST6CDT,M3.2.0,M11.1.0|
|EET|EET-2EEST,M3.5.0/3,M10.5.0/4|
|EST5EDT|EST5EDT,M3.2.0,M11.1.0|
|Europe/Amsterdam|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/Andorra|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/Athens|EET-2EEST,M3.5.0/3,M10.5.0/4|
|Europe/Belgrade|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/Berlin|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/Bratislava|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/Brussels|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/Bucharest|EET-2EEST,M3.5.0/3,M10.5.0/4|
|Europe/Budapest|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/Busingen|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/Chisinau|EET-2EEST,M3.5.0,M10.5.0/3|
|Europe/Copenhagen|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/Dublin|GMT0IST,M3.5.0/1,M10.5.0|
|Europe/Gibraltar|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/Guernsey|GMT0BST,M3.5.0/1,M10.5.0|
|Europe/Helsinki|EET-2EEST,M3.5.0/3,M10.5.0/4|
|Europe/Isle_of_Man|GMT0BST,M3.5.0/1,M10.5.0|
|Europe/Jersey|GMT0BST,M3.5.0/1,M10.5.0|
|Europe/Kiev|EET-2EEST,M3.5.0/3,M10.5.0/4|
|Europe/Lisbon|WET0WEST,M3.5.0/1,M10.5.0|
|Europe/Ljubljana|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/London|GMT0BST,M3.5.0/1,M10.5.0|
|Europe/Luxembourg|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/Madrid|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/Malta|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/Mariehamn|EET-2EEST,M3.5.0/3,M10.5.0/4|
|Europe/Monaco|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/Nicosia|EET-2EEST,M3.5.0/3,M10.5.0/4|
|Europe/Oslo|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/Paris|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/Podgorica|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/Prague|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/Riga|EET-2EEST,M3.5.0/3,M10.5.0/4|
|Europe/Rome|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/San_Marino|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/Sarajevo|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/Skopje|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/Sofia|EET-2EEST,M3.5.0/3,M10.5.0/4|
|Europe/Stockholm|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/Tallinn|EET-2EEST,M3.5.0/3,M10.5.0/4|
|Europe/Tirane|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/Uzhgorod|EET-2EEST,M3.5.0/3,M10.5.0/4|
|Europe/Vaduz|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/Vatican|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/Vienna|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/Vilnius|EET-2EEST,M3.5.0/3,M10.5.0/4|
|Europe/Warsaw|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/Zagreb|CET-1CEST,M3.5.0,M10.5.0/3|
|Europe/Zaporozhye|EET-2EEST,M3.5.0/3,M10.5.0/4|
|Europe/Zurich|CET-1CEST,M3.5.0,M10.5.0/3|
|MET|MET-1MEST,M3.5.0,M10.5.0/3|
|MST7MDT|MST7MDT,M3.2.0,M11.1.0|
|Pacific/Apia|<+13>-13<+14>,M9.5.0/3,M4.1.0/4|
|Pacific/Auckland|NZST-12NZDT,M9.5.0,M4.1.0/3|
|Pacific/Chatham|<+1245>-12:45<+1345>,M9.5.0/2:45,M4.1.0/3:45|
|Pacific/Fiji|<+12>-12<+13>,M11.1.0,M1.3.0/3|
|Pacific/Tongatapu|<+13>-13<+14>,M11.1.0,M1.3.0/3|
|PST8PDT|PST8PDT,M3.2.0,M11.1.0|
|US/Pacific-New|PST8PDT,M3.2.0,M11.1.0|
|WET|WET0WEST,M3.5.0/1,M10.5.0|

or I also write a simple page to generate posix string at http://www.topyuan.top/posix

you can study global timezone rules at:
 
https://en.wikipedia.org/wiki/List_of_tz_database_time_zones

If you have any questions about posix time zone or find bugs on SuperY WiFi Clock , please contact me admin@topyuan.top
