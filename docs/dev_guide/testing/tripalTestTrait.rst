
Tripal Testing Environment
===========================

Tripal uses the Drupal testing environment to automate our tests using `PHPUnit <https://phpunit.de/>`_. This means that when you run tests on any Tripal site, the following will happen **FOR EACH TEST**:

1. Drupal will setup a virtual Drupal site whose level of functionality depends on whether you are running a Kernel or Functional Test. This will actually setup a full drupal database schema within your current site temporarily. Note: This is not a new postgresql schema but rather creates all the tables used by Tripal in the same public schema but with prefixes in the table names.

  - Kernel tests will give you a fully functional site that cannot be interacted with through the browser and that only has the specific modules, tables, etc. that you specify in your test `setUp()`
  - Functional tests will have a fully functional site with methods to explore the fully rendered pages within the test. It will still only have the modules you specify enabled but it will run the entire install for those modules whereas kernel tests do not.

2. Tripal does not yet do any additional preparing of the Drupal test environment so as not to include any more than you need for your tests. This means there are no content types, no fields, no TripalTerms, etc. However, we do provide a number of methods to complement the Drupal methods in helping you setup the environment exactly as you want to. These will be described in the next section.
3. The code inside your tests `setUp()` is now run to setup the environment for this test. The same setup will be run for all tests in the same test class.
4. Finally your test method is called. Note: any services, plugins, etc you use here will only have the test environment available. You will not have access to any data in your main site, nor should this long term affect your main site. **That said, we do not recommend running tests on production sites!**
5. Once your test is complete, the `tearDown()` method is called to clean the entire development environment up. This includes dropping the development drupal tables including any changes made by your test.

Setting up Content Types
-------------------------

As mentioned above, there are no content types in the testing environment. That means to do any testing related to content types or fields, you will first need to setup content types in your environment. **Tripal has provided helper methods to make this easier! These are available in any test that extends the `TripalTestBrowserBase`, `TripalTestKernelBase`, `ChadoTestKernelBase`, and `ChadoTestBrowserBase`.**

For example, the following example creates the organism Tripal Term and then the organism content type:

.. code-block:: php

  /**
   * {@inheritdoc}
   */
  protected function setUp(): void {
    parent::setUp();

    // Create the TripalTerm used for the organism content type.
    $this->createTripalTerm([
      'vocab_name' => 'obi',
      'id_space_name' => 'OBI',
      'term' => [
        'name' => 'organism',
        'definition' => '',
        'accession' =>'0100026',
      ]],
      'chado_id_space', 'chado_vocabulary'
    );

    // Create the Organism Content Type
    $this->createTripalContentType([
      'label' => 'Organism',
      'termIdSpace' => 'OBI',
      'termAccession' => '0100026',
      'category' => 'General',
      'id' => 'organism',
      'help_text' => 'A material entity that is an individual living system, ' .
        'such as animal, plant, bacteria or virus, that is capable of replicating ' .
        'or reproducing, growth and maintenance in the right environment. An ' .
        'organism may be unicellular or made up, like humans, of many billions ' .
        'of cells divided into specialized tissues and organs.',
    ]);
  }

The above will work just fine on its own in a functional test as long as you have tripal listed in your `$modules` array. However, you will need to make additional parts available in kernel tests. Specifically, add the following install calls to the top of your setUp method:

.. code-block:: php

  /**
   * {@inheritdoc}
   */
  protected function setUp(): void {
    parent::setUp();

    // Make the TripalTerm database tables available.
    $this->installSchema('tripal_terms');
    $this->installSchema('tripal_terms_vocabs');
    $this->installSchema('tripal_terms_idspaces');

    // Make the User, Tripal Content and Tripal Content Type entities available.
    $this->installEntitySchema('user');
    $this->installEntitySchema('tripal_entity');
    $this->installEntitySchema('tripal_entity_type');

.. warning::

  The above content type will **NOT have any fields attached** to it yet! See the following section for adding fields.

Adding Fields to Content Types
-------------------------------

Now that we have a Tripal Content type, we will want to add fields to it. Again, Tripal provides an easy to use function to create field instances and attach them to your entity in the test environment!

The following code snippet shows how to add a single field to an existing content type in the test environment. This should go in your `setUp()` method after the content type is already created.

.. code-block:: php

    // Create the term used by the field.
    // This is the term that would normally get set
    // in the form when adding a field through the UI.
    $genus_term = $this->createTripalTerm([
      'vocab_name' => 'taxonomic_rank',
      'id_space_name' => 'TAXRANK',
      'term' => [
        'name' => 'genus',
        'definition' => '',
        'accession' =>'0000005',
      ]],
      'chado_id_space', 'chado_vocabulary'
    );
    // Create the field instance.
    $this->createTripalField(
      // The machine name of the content type to attach the field to.
      'organism',
      // The field settings + details.
      [
        // This can be anything.
        'field_name' => 'organism_taxrank_0000005',
        // This is the machine name of the field type you want to create.
        'field_type' => 'chado_string_type_default',
        'term' => $genus_term,
        'is_required' => TRUE,
        'cardinality' => 1,
        // This indicates the base chado table and column to use for this field.
        // You would include anything here that you would normally supply on
        // the storage settings form.
        'storage_plugin_settings' => [
          'base_table' => 'organism',
          'base_column' => 'genus'
        ],
      ]
    );

If we later want to create content, you will need to create at least all required fields in order for the content to be saved properly. You will also likely need to create tripal terms for any properties that this field has as well.
