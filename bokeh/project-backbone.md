# Bokeh project backbone

[Bokeh](http://bokeh.pydata.org/en/latest/) is a Python interactive
visualization library that targets web browsers for presentation. Not sure how
it compares to [mpld3](http://mpld3.github.io/index.html), but it seems
intuitive so far and it's perfect for backend visualizations.

The basic steps to creating plots with the `bokeh.plotting` interface are:

* prepare the data.
* specify where to generate the output
* call `figure()` to create a plot with options like title, tools and labels.
* add renderers with visual customizations like colors and legends.
* `show()` or `save()` the results.

Here is an example from the [Bokeh documentation](http://bokeh.pydata.org/en/latest/docs/user_guide/quickstart.html#userguide-quickstart):

    from bokeh.plotting import figure, output_file, show
    import numpy as np

    # prepare the data
    SIZE = 4000
    X_DATA = np.random.random(size=SIZE) * 100
    Y_DATA = np.random.random(size=SIZE) * 100
    RADII = np.random.random(size=SIZE) * 1.5
    COLORS = ["#%02x%02x%02x" % (int(r), int(g), 150) for r, g in zip(50 + 2*X_DATA, 30 + 2*Y_DATA)]
    TOOLS = 'resize,crosshair,pan,wheel_zoom,box_zoom,reset,box_select,lasso_select'

    # specify where to generate the output
    output_file('index.html', title='color scatter example', mode='cdn')

    # call figure() to create a plot
    PLOT = figure(tools=TOOLS, x_range=(0, 100), y_range=(0, 100))

    # add renderers with visual customizations
    PLOT.circle(X_DATA, Y_DATA, radius=RADII, fill_color=COLORS, fill_alpha=0.6, line_color=None)

    # show the results
    show(PLOT)

`show()` creates or overwrites the output file `index.html`, and automatically
opens a new tab to display it.

And here is the result:

![Bokeh color scatter](https://github.com/marcolagi/today-i-learned/resources/bokeh_1.png)

A few core concepts of this library are:

* **plots**: containers that hold all the various objects (renderers, guides, data,
and tools) that comprise the final visualization. The `Figure` class helps with
assembling a plot, and the function `figure()` creates `Figure` objects.

* **glyphs**: basic visual marks that Bokeh can display. At the lowest level
(`bokeh.models`), there are glyph objects such as `Circle`. To make life easier,
the `bokeh.plotting` interface exposes higher level glyph methods (see
`Figure.circle` method above).

* **guides and annotations**: visual components that aid presentation.
**guides** are visual aids that help users judge distances, angles, etc.
(grid lines, bands, axes, ticks). **annotations** are visual aids that label or
name parts of the plot (titles, legends).

* **ranges**: describe the data-space bounds of a plot. By default, plots
try to automatically set the bounds to encompass all the available data, but
this can be modified (see `x_range` and `y_range` above)

* **resources**: by default, the `output_file()` function will configure Bokeh
to generate static HTML files with `BokehJS` resources embedded directly inside.
One can also generate output that loads `BokehJS` from a Content Delivery
Network (CDN), by passing the argument `mode="cdn"`.









