Two Step Validation (with Google Authenticator)
===============================================

The SonataUserBundle provides an optional layer of security by including a support for a Two Step Validation process.

When the option is enabled, the login process is done with the following workflow :

* the user enters the login and password
* if the user get the correct credentials, then
* a code validation form is diplayed
* at this point the user must enter a time based code provided by the Google Authenticator application
* the code is valid only once per minute

So if your login and password are compromised then the hacker must also hold your phone!


Installation
------------

Add the following lines to the file ``deps``::

    [SonataUserBundle]
        git=git://github.com/sonata-project/SonataUserBundle.git
        target=/bundles/Sonata/UserBundle

Update the autoload.php file::

    // app/autoload.php
    $loader->registerNamespaces(array(
        // ...
        'Google'            => __DIR__.'/../vendor/google-authenticator/lib'
        // ...
    ));

Edit the configuration file

.. code-block:: yaml

    # app/config/config.yml

    sonata_user:
        google_authenticator:
            enabled: true
            server:  yourserver.com

Now if the ``User::twoStepVerificationCode`` property is not null, then a second form will be displayed.
