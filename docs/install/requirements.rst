
Requirements
===============

- Drupal (see supported versions below)
- Drupal core modules: Search, Path, Views, and Field.
- PostgreSQL 13+
- PHP 8 (tested with 8.1, 8.2, 8.3)
- Apache 2+
- Composer 2+
- UNIX/Linux

.. note::

  Apache 2+ is recommended as the webserver but Drupal is also known to work well with Nginx. You may have limited support for Nginx from the Tripal community.

  PostgreSQL is required by Chado to function properly, rather than MySQL or any other database management system.

Supported Drupal Versions
---------------------------

The following table shows the current status of automated testing on the versions
of Drupal we currently support.

=========== ================ ================
Drupal      10.2.x           10.3.x
=========== ================ ================
**PHP 8.1** |PHP8.1D10.2.x|  |PHP8.1D10.3.x|
**PHP 8.2** |PHP8.2D10.2.x|  |PHP8.2D10.3.x|
**PHP 8.3** |PHP8.3D10.2.x|  |PHP8.3D10.3.x|
=========== ================ ================


.. |PHP8.1D10.2.x| image:: https://github.com/tripal/tripal/actions/workflows/MAIN-phpunit-php8.1_D10_2x.yml/badge.svg
   :target: https://github.com/tripal/tripal/actions/workflows/MAIN-phpunit-php8.1_D10_2x.yml
.. |PHP8.2D10.2.x| image:: https://github.com/tripal/tripal/actions/workflows/MAIN-phpunit-php8.2_D10_2x.yml/badge.svg
   :target: https://github.com/tripal/tripal/actions/workflows/MAIN-phpunit-php8.2_D10_2x.yml
.. |PHP8.3D10.2.x| image:: https://github.com/tripal/tripal/actions/workflows/MAIN-phpunit-php8.3_D10_2x.yml/badge.svg
   :target: https://github.com/tripal/tripal/actions/workflows/MAIN-phpunit-php8.3_D10_2x.yml

.. |PHP8.1D10.3.x| image:: https://github.com/tripal/tripal/actions/workflows/MAIN-phpunit-php8.1_D10_3x.yml/badge.svg
   :target: https://github.com/tripal/tripal/actions/workflows/MAIN-phpunit-php8.1_D10_3x.yml
.. |PHP8.2D10.3.x| image:: https://github.com/tripal/tripal/actions/workflows/MAIN-phpunit-php8.2_D10_3x.yml/badge.svg
   :target: https://github.com/tripal/tripal/actions/workflows/MAIN-phpunit-php8.2_D10_3x.yml
.. |PHP8.3D10.3.x| image:: https://github.com/tripal/tripal/actions/workflows/MAIN-phpunit-php8.3_D10_3x.yml/badge.svg
   :target: https://github.com/tripal/tripal/actions/workflows/MAIN-phpunit-php8.3_D10_3x.yml
