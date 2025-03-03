
Automated Testing
===================

Tripal 4 is being developed with automated testing as it is upgraded. This greatly improves the stability of our software and our ability to fix any bugs. We highly recommend developing automated testing alongside any extension modules you create! This guide is intended to explain how automated testing is working for Tripal 4 and help you develop similar tests for your extensions.

How run automated tests locally
---------------------------------

See the `Drupal "Running PHPUnit tests" guide <https://www.drupal.org/node/2116263>`_ for instructions on running tests on your local environment. In order to ensure our Tripal functional testing is fully bootstrapped, tests should be run from Drupal core.

If you are using the docker distributed with this module, then you can run tests using:

.. code:: bash

  docker exec --workdir=/var/www/drupal/web/modules/contrib/tripal tripal phpunit

Tripal-focused Testing
------------------------

The following automated testing documentation and tutorials are focused on testing Tripal-specific functionality within Tripal Core and Extension modules. If there is a topic you would like covered that is not yet documented, please add an issue on our github at https://github.com/tripal/tripal_doc/issues!

.. toctree::
   :maxdepth: 2

   testing/tripalTestTrait
   testing/chadoTestTrait
   testing/fields

Additional Resources
----------------------

 - `Official Drupal: Testing Documentation <https://www.drupal.org/docs/testing>`_
 - `Official Drupal: PHPUnit file structure, namespace, and required metadata <https://www.drupal.org/docs/testing/phpunit-in-drupal/phpunit-file-structure-namespace-and-required-metadata>`_
 - `Official Drupal: Running PHPUnit Tests <https://www.drupal.org/docs/testing/phpunit-in-drupal/running-phpunit-tests>`_
 - `Official Drupal: PHPUnit Browser test tutorial <https://www.drupal.org/docs/testing/phpunit-in-drupal/phpunit-browser-test-tutorial>`_
 - `Official Drupal: PHPUnit JavaScript test writing tutorial <https://www.drupal.org/docs/automated-testing/phpunit-in-drupal/phpunit-javascript-test-writing-tutorial>`_
 - `Drupal 8, 9, 10 Functional and Unit Testing (Automation Testing) <https://gurinderpal.medium.com/drupal-8-9-10-functional-and-unit-testing-462993c3ce14>`_
 - `Writing Automated Tests in Drupal 8, Part 4: Kernel tests <https://deninet.com/blog/2019/02/10/writing-automated-tests-drupal-8-part-4-kernel-tests>`_
 - `Writing Automated Tests in Drupal 8, Part 3: Unit tests <https://deninet.com/blog/2019/01/27/writing-automated-tests-drupal-8-part-3-unit-tests>`_
 - `Drupal 8: Writing Your First Unit Test With PHPUnit <https://www.axelerant.com/resources/team-blog/drupal-8-writing-your-first-unit-test-with-phpunit>`_
