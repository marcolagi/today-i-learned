# Bokeh server setup

Today the goal is to serve a website with Bokeh. The
[command](http://bokeh.pydata.org/en/latest/docs/user_guide/server.html) to run
a standalone Bokeh server is:

    bokeh serve dashboard.py --port [PORT] --host [HOST]:[PORT]

The application is now accessible at

    http://[HOST]:[PORT]/dashboard

`nginx` or other web servers have to be used if password authentication, load
balancing etc. are needed.