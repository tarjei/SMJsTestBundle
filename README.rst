JsTestBundle
~~~~~~~~~~~~

The goal of this bundle is to provide a simple way to inject some qunit tests into a Symfony2 page.

Usage example
-------------

Let's say you got a page with some js stuff you want to test, but it is tied to your markup. So in your page you got:

.. raw:: twig

    <html>
        <head>
            ..
            <script type="text/javascript" src="{{ asset('bundles/mybundle/js/moduleHandler.js') }}"></script>
            ..
        </head>
    </html>

Then you add in the body of the template for the page you want to test:

.. raw:: html

        <body>
            ... 
            {{ qunit_tests("ModuleHandler", 'bundles/mybundle/js/moduleHandler_tests.js') }}
            ...
        </body>

And request the page with an extra request parameter: /mypage?fpgJsTest=true.

Then the module will inject the complete Qunit markup as well as the qunit.js script ++ and the tests inmoduleHandler_tests.js will be run.

Todo
----

* Add support for phanthom.js runner.
* Add support for including extra mock libs etc.
* Improve security.




Instalation
-----------

Add to deps::

    [SMJsTestBundle]
        git=git://github.com:tarjei/JsTestBundle.git
        target=/bundles/SM/JsTestBundle

Then register the bundle with your kernel::

    
    // app/AppKernel.php
    // in AppKernel::registerBundles()
    if (in_array($this->getEnvironment(), array('dev', 'test'))) {
        // do not use this bundle in production!
        $bundles[] = new SM\JsTestBundle\SMJsTestBundle();
    }

Make sure that you also register the namespaces with the autoloader::

    // app/autoload.php
    $loader->registerNamespaces(array(
        // ...
        'SM\\JsTestBundle' => __DIR__ . '/../vendor/bundles',
    ));

Configuration
-------------

No config yet. 
