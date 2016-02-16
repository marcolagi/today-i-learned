# Change datetime timezone

AWS Linux instances are, by default, set on Coordinated Universal Time (UTC),
i.e. time at 0° longitude and disregarding daylight saving time. So
`datetime.datetime.now()` will return UTC time, unless the machine's time zone
was changed.

In order to have it return the desired time zone, say EST, without updating
`/etc/sysconfig/clock`, one has to use `pytz`, a port of the Olson tz database:

    import pytz
    import datetime

    print datetime.datetime.now(pytz.timezone('US/Eastern'))


