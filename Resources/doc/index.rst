Bundle for Symfony3 for basic authentication of HTTP users listed in the file created by htpasswd utility

Installation
============

Add adem-enuygun/HtpasswdBundle to composer.json
-------------------------------------------

::

    "require": {

        "adem-enuygun/HtpasswdBundle": "dev-master"

    }

Add Ksn135HtpasswdBundle to your application kernel
---------------------------------------------------

::

    // app/AppKernel.php
    public function registerBundles()
    {
        $bundles = [
            // ...

            new Ksn135\HtpasswdBundle\Ksn135HtpasswdBundle(),
            
            // ...
        ];
    }

Update your security.yml configuration
--------------------------------------

::

    # app/config/security.yml

    parameters:
        htpasswd_user_provider.filename: /etc/nagios3/htpasswd.users

    security:
        encoders:
            Ksn135\HtpasswdBundle\Security\User\HtpasswdUser: 
                id:            htpasswd_encoder

        providers:
            htpasswd:
                id:            htpasswd_user_provider

        firewalls:
            dev:
                pattern:       ^/(_(profiler|wdt)|css|images|js)/
                security:      false

            secured_area:
                pattern:       ^/
                http_basic:
                    provider:  htpasswd
                    realm:     "Secured Area"

        access_control:
            - { path: ^/, roles: ROLE_USER }

.. note::
    Modify 'htpasswd_user_provider.filename' parameter to suit your needs.
