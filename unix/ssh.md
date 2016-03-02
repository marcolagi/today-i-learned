# How to keep ssh connections alive

It often happens that when connecting from home, coffee shops, or hotels,
ssh sessions break after a few minutes of being idle:

    user@hostname [12:52] [~] ::
    packet_write_wait: Connection to [HOST]: Broken pipe

Using `screen` can make this less painful, but you still have to reconnect many
times. This is usually the result of a router timing
out inactive connections. Why?

* home routers are cheap, and maintaining the connection table costs limited
resources.
* the timeout cleans up what the router considers to be stale or hung
connections. The connection table of a router at a popular coffee shop can have
many active connections, so in general it's a good idea.

The ssh client provides a `ServerAliveInterval` setting, which allows the client
to send ssh null commands on a set interval, to fool routers into thinking the
session is active even when idle. Using this setting will
ensure that the connection is kept fresh in the router connection table. From
the ssh client man page,

> ServerAliveInterval

> Sets a timeout interval in seconds after which if no data has been received from
> the server, ssh(1) will send a message through the encrypted channel to request a
> response from the server. The default is 0, indicating that these messages will
> not be sent to the server.

**nb**: the same thing can be done on the server with the `ClientAliveInterval`
setting.

So one just needs to add these two lines to `~/.ssh/config`:

    Host *
        ServerAliveInterval 60



