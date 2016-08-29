Undebt_: Command Line Interface
===============================

.. _Undebt: index.html
.. default-role:: code

Install it
----------

.. code-block:: bash

    $ git clone https://github.com/Yelp/undebt.git
    $ cd undebt
    $ pip install .

Read it
-------

.. code-block:: bash

    $ undebt --help
    usage: undebt [-h] --pattern path [--extension ext]
                  [--multiprocess processes] [--verbose] [--dry-run]
                  FILE [FILE...]

    positional arguments:
      FILE [FILE...]
                            paths to files or directories (searched recursively
                            for extension) to be modified (if not passed uses
                            stdin)

    optional arguments:
      -h, --help            show this help message and exit
      --pattern path, -p path
                            paths to pattern definition files
      --extension ext, -e ext
                            extensions of files to be modified when searching a
                            directory (exclude ".", e.g. "py" instead of ".py")
      --multiprocess processes, -m processes
                            number of processes to run in parallel (default is 16)
      --verbose
      --dry-run, -d         only print to stdout; do not overwrite files

Try it out
----------

.. code-block:: bash

    $ undebt -p ./undebt/examples/method_to_function.py ./tests/inputs/method_to_function_input.txt
    $ git diff
    diff --git a/tests/inputs/method_to_function_input.txt b/tests/inputs/method_to_function_input.txt
    index f268ab9..7681c63 100644
    --- a/tests/inputs/method_to_function_input.txt
    +++ b/tests/inputs/method_to_function_input.txt
    @@ -1,13 +1,14 @@
    +from function_lives_here import function
     something before code pattern
     @decorator([Class])
     def some_function(self, abc, xyz):
         """herp the derp while also derping and herping"""
         cde = fgh(self.l)
         ijk = cde.herp(
    -        opq_foo=FOO(abc).method()
    +        opq_foo=function(FOO(abc))
         )['str']
         lmn = cde.herp(
    -        opq_foo=FOO(xyz).method()
    +        opq_foo=function(FOO(xyz))
         )['str']
     bla bla bla
         for str_data in derp_data['data']['strs']:
    @@ -16,8 +17,8 @@ bla bla bla
                 rst.uvw(
                     CTA_BUSINESS_PLATFORM_DISABLED_LOG,
                     "derp {derp_foo} herp {herp_foo}".format(
    -                    derp_foo=FOO(derp_foo).method(),
    -                    herp_foo=FOO(herp_foo).method(),
    +                    derp_foo=function(FOO(derp_foo)),
    +                    herp_foo=function(FOO(herp_foo)),
                     ),
                 )
     something after code pattern
