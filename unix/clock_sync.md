# Time synchronisation

The clock of AWS instances running Ubuntu 14.04, more often than not, tends to
be out of sync. This is a common problem for clocks on virtual servers.
Sometimes this is the cause of bugs that are hard to pin down, e.g. AWS not
being able to validate a user's credentials when these are provided with the
AWS CLI. This is due to the fact that the date in the signature may not match
the date of the request, and AWS rejects it.

To update the clock, on Ubuntu:

    sudo ntpdate -s time.nist.gov

NTP is a TCP/IP protocol for synchronising time over a network: a
client requests the current time from a server, and uses it to set its own
clock.
