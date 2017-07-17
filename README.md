Chipy.org
=========

The code for the Chipy.org website
This project is open source and the license can be found in LICENSE.


Installation
============

To get setup with chipy.org code it is recommended that you use the following:

 * Python 2.7.x
 * virtualenv
 * [Autoenv](https://github.com/kennethreitz/autoenv)
 * C compiler (for PIL)

Setting up a Local environment
------------------------------

Chipy.org is setup using [12factor](http://12factor.net), which means that it takes local settings from the environment. For this reason it is recommended that you use autoenv and a .env file. The example .env is::

    export DEBUG=True
    export ALLOWED_HOSTS="chipy.org,www.chipy.org"
    export GITHUB_APP_ID=youridhere
    export GITHUB_API_SECRET=supersecretkeyhere
    export SECRET_KEY=somesecretkeyfordjangogoeshere
    export ADMINS=admin@example.com
    export ENVELOPE_EMAIL_RECIPIENTS=admin@example.com
    export NORECAPTCHA_SITE_KEY=your_recaptcha_public_key
    export NORECAPTCHA_SECRET_KEY=your_recaptcha_private_key
    export DATABASE_URL=postgres://USER:PASSWORD@HOST:PORT/NAME

    # settings needed for social authentication
    export GITHUB_API_SECRET=""
    export GITHUB_APP_ID=""
    export GOOGLE_OAUTH2_CLIENT_ID=""
    export GOOGLE_OAUTH2_CLIENT_SECRET=""

    # optional email settings and their defaults
    export EMAIL_BACKEND='django.core.mail.backends.smtp.EmailBackend'
    export EMAIL_HOST='smtp.sendgrid.net'
    export EMAIL_PORT=587
    export EMAIL_USE_TLS=True
    export EMAIL_HOST_USER=""
    export EMAIL_HOST_PASSWORD=""

    # to enable S3, do the following
    export USE_S3="True"
    export AWS_ACCESS_KEY_ID=""
    export AWS_SECRET_ACCESS_KEY=""
    export AWS_STORAGE_BUCKET_NAME=""

Note that the only required config is the github stuff. The secret key will be random by default which will cause your session to wipe on every restart.

If using autoenv, the above will be in your environment when you cd to the project directory

Create a virtual environment where your dependencies will live::

    $ virtualenv venv
    $ source venv/bin/activate
    (venv)$

Clone the repo

    (venv)$ git clone git://github.com/chicagopython/chipy.org.git chipy.org

Make the project directory your working directory::

    (venv)$ cd chipy.org

Install project dependencies::

    (venv)$ pip install -r requirements.txt

Setting up the database
-----------------------

I recommend keeping your development DB as close to production as possible. If you're on a Mac, I recommend using [Postgress.app](http://postgresapp.com)

You will need to run::

    (venv)$ python manage.py migrate

Running a web server
--------------------

In development you should run::

    (venv)$ python manage.py runserver


Heroku Commands
-------------------------------

    # Deploy changes to master
    git push heroku master

    # Deploy feature branch  
    git push heroku feature/mybranch:master

    # Collectstatic
    heroku run python manage.py collectstatic --noinput

    # Set sync and migrate the database
    heroku run python manage.py migrate

    # Set environment variable on Heroku
    heroku config:set DEBUG=True
