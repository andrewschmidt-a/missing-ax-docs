Global functions
================



.. _conversionFunctions:

Conversion runtime functions
--------------------

.. seealso::
   For more information about conversion runtime functions see the `Official AX docs <https://learn.microsoft.com/en-us/dynamics365/fin-ops-core/dev-itpro/dev-ref/xpp-conversion-run-time-functions>`_

.. _any2Date:

any2Date
++++++++

Although this is `any2Date` the output is most helpful when the input is a str or int.

.. code-block:: X++

   // Signature
    date any2Date(anytype object)

   // Usage
    str dateAsString = "1995 5 5";
    int dateAsInt = 45;
    date myDate = any2Date(dateAsString);
    myDate = any2Date(dateAsInt);

.. _any2Enum:

any2Enum
++++++++

Although this is `any2Enum` the output is most helpful when the input is an int or str.

.. code-block:: X++

   // Signature
    int any2Int(anytype object)

   // Usage
    str intAsString = "1";
    int enumAsInt = 0;

    NoYes myEnum = any2Enum(intAsString); // Yes
    myEnum = any2Enum(enumAsInt); // No

.. _any2Guid:

any2Guid
++++++++

.. _any2Int:

any2Int
+++++++

Although this is `any2Int` the output is most helpful when the input is a real, enum or str.

.. code-block:: X++

   // Signature
    int any2Int(anytype object)

   // Usage
    str intAsString = "1995";
    real intAsReal = 1.024e3;
    NoYes isAlive = NoYes::Yes;

    int myInt = any2Int(intAsString); // 1995
    myInt = any2Int(intAsReal); // 1024
    myInt = any2Int(isAlive); // 1

.. _any2Int64:

any2Int64
+++++++++
Although this is `any2Int64` the output is most helpful when the input is a real, enum or str.

.. code-block:: X++

   // Signature
    int64 any2Int(anytype object)

Usage is similar to `any2Int <any2Int_>`_

.. _any2Real:

any2Real
++++++++

Although this is `any2Real` the output is most helpful when the input is a real, enum or str.

.. code-block:: X++

   // Signature
    real any2Real(anytype object)

   // Usage
    str realAsString = "1995";
    int realAsInt = 10;
    NoYes isAlive = NoYes::Yes;

    real myReal = any2Real(intAsString); // 1.995e3
    myReal = any2Real(intAsReal); // 1e1
    myReal = any2Real(isAlive); // 1e0

.. _any2Str:

any2Str
+++++++