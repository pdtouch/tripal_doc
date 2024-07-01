
Deprecations in tripal_chado.cv.api.inc
==========================================

Previous database storage and access functions are all replaced by Tripal DBX. 
For example, to replace **db_select** one should move to 

**\Drupal::service('tripal_chado.database')->select()**

See below the table of the deprecated functions with their new alternatives in 
tripal_chado/src/api/tripal_chado.cv.api.inc

.. table:: List of deprecated functions and corresponding new method

    +----------------------------------+---------------------+
    | Deprecated function              |    New method       |
    +==================================+=====================+
    |                                  |                     |
    +----------------------------------+---------------------+
    |                                  |                     |
    +----------------------------------+---------------------+

For general information on deprecations in Tripal 4.x refer to 

 - :ref:`Deprecations in Tripal 4.x`
