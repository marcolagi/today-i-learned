# Basic Authentication for a Flask app

`flask-basicauth` is a `flask` extension that provides an easy way to protect
an application with HTTP basic access authentication. Here is the scheleton:

    from flask import Flask, current_app
    from flask.ext.basicauth import BasicAuth

    def check_users(user, pass):
        return {user: pass} in current_app.config['BASIC_AUTH_USERS']

    def main():
        app = Flask(__name__)
        app.config['BASIC_AUTH_FORCE'] = True
        app.config['BASIC_AUTH_USERS'] = [{'username1': 'password1',
                                           'username2': 'password2'}]
        basic = BasicAuth(app)
        basic.check_credentials = check_users

        @app.route('/')
        def login():

            ... what to do after login ...

        app.run()

In order to protect the whole application, `BASIC_AUTH_FORCE` is set to `True`.
The `check_credentials` method of BasicAuth needs to be overwritten if the app
allows multiuser authentication.