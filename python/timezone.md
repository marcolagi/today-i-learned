# Change datetime timezone

AWS Linux instances are set by default on Coordinated Universal Time (UTC),
i.e. time at 0° longitude that doesn't take into account daylight saving time.
Unless the machine's time zone was changed, `datetime.datetime.now()` will
return UTC time.

In order to have it return the desired time zone, say **EST**, without updating
`/etc/sysconfig/clock`, one has to use `pytz`, a Python port of the Olson tz
database:

    >>> import pytz, datetime
    >>> datetime.datetime.now()
    datetime.datetime(2016, 2, 16, 20, 22, 57, 463343)
    >>> datetime.datetime.now(pytz.timezone('US/Eastern'))
    datetime.datetime(2016, 2, 16, 15, 23, 9, 709983, tzinfo=<DstTzInfo 'US/Eastern' EST-1 day, 19:00:00 STD>)

