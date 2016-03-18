# Catch all URLs

The `route()` decorator is used in Flask to bind a function to a URL. Variable
parts of a URL can be marked as
`<variable_name>`. Such parts are then passed as a keyword argument to the
function. Optionally a **converter** can be used by specifying a rule with
`<converter:variable_name>`. For example:

    @app.route('/user/<username>')
    def show_user_profile(username):
        return 'User %s' % username

    @app.route('/post/<int:post_id>')
    def show_post(post_id):
        return 'Post %d' % post_id

The following converters exist:

| type   | description                               |
| -----  | ----------------------------------------- |
| `int`  | accepts integers                          |
| `float`| like `int` but for floating point values  |
| `path` | like the default but also accepts slashes |

A [simple way](http://flask.pocoo.org/snippets/57/) to create a catch-all
function which serves every URL including `/` is to chain two route filters.
One for the root path `/`, and one including a path placeholder for the rest.

    from flask import Flask
    app = Flask(__name__)

    @app.route('/', defaults={'this_path': ''})
    @app.route('/<path:this_path>')
    def catch_all(this_path):
        return 'Path %s' % this_path

    app.run()

Just the path placeholder is not enough, each placeholder must at least catch
one character.
