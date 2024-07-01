
Deprecations in tripal_chado.variables.api.inc
==============================================

Previous database storage and access functions are all replaced by Tripal DBX. 
For example, to replace **db_select** one should move to 

**\Drupal::service('tripal_chado.database')->select()**

See below the table of the deprecated functions with their new alternatives in 
tripal_chado/src/api/tripal_chado.variables.api.inc

.. table:: List of deprecated functions and corresponding new method

    +----------------------------------+---------------------+
    | Deprecated function              |    New method       |
    +==================================+=====================+
    | chado_generate_var               |                     |
    +----------------------------------+---------------------+
    | chado_expand_var                 |                     |
    +----------------------------------+---------------------+

For general information on deprecations in Tripal 4.x refer to 

 - https://tripaldoc.readthedocs.io/en/latest/dev_guide/deprecations.html

Tripal 4.x deprecations issue
-----------------------------

 - `Issue 1343 <https://github.com/tripal/tripal/issues/1343>`_ Deprecated Functions in Tripal 4