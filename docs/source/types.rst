Types
=====

.. _primatives:

Primatives
------------

.. seealso::
   For more information about the primitive types see the `Official AX docs <https://learn.microsoft.com/en-us/dynamics365/fin-ops-core/dev-itpro/dev-ref/xpp-data-primitive>`_

anytype
+++++++

Anytypes are used as placeholders for any type of data. When it is assigned a value it then is converted to that type.

.. code-block:: X++
   :caption: Example of automatic type assignment

    anytype placeholder;
    placeholder = "this is a str"; // Automatically assigns a str literal.
    placeholder = 0; // Runtime Error! -- this is not allowed since it is now assigned to a str

.. warning::
   Anytype variables can only be assigned one type. If you attempt to assign a different type after initial assignment, you may experience undesired behaviour

In this example from the AtlPersonnel module, the primary key value that is being returned is not known so anytype must be used as a placeholder.

.. code-block:: X++
   :caption: Example of using anytype as a placeholder

   [SysGeneratedCode('ATLGenerator', '1.0.0.0')]
	protected final Common getRecordByPrimaryKey(anytype _primarykeyValue)
    {
        HcmGoalTemplate hcmGoalTemplate;

        select firstonly hcmGoalTemplate where hcmGoalTemplate.RecId == _primarykeyValue;

        return hcmGoalTemplate;
    }

Helpful conversion functions:

* `any2date <any2date_>`_
* `any2enum <any2enum_>`_
* `any2int <any2int_>`_
* `any2int64 <any2int64_>`_
* `any2real <any2real_>`_
* `any2str <any2str_>`_

boolean
+++++++
Booleans are simple binary structures, which can be either true or false. Booleans are represented as integers and due to this, you can also assign integer values to them.

.. code-block:: X++

    boolean isTrue; // false
    isTrue = true; // true
    boolean isFalse = false; // false
    boolean isZero = 0; // false
    boolean isOne = 1; // true
    boolean isTwo = 2; // true

int and int64
+++++++++++++
Integers are used to represent whole numbers (both negative and positive). By default these are represented with 32-bits but a 64 bit integer type is also available for larger numbers. 

.. note ::
   Most RecIds for tables in X++ are stored as an Int64

.. code-block:: X++

    int myInt = 1334;
    int64 myLargeInt = 19299990878787999;

real
++++
Real literals are numbers that can hold decimals. In other languages this may be called a float, decimal or double.

.. code-block:: X++

    int myInt = 1334;
    int64 myLargeInt = 19299990878787999;

.. note ::
   If you are using the CLRInterop layer for your code, you will want to make sure to use .NET Decimal type between C# and X++ code as that is what X++ uses.

date
++++
Date types are used only to refer to the day, month and year component of time. The date literal is set with the format {day}\\{month}\\{year}. 

Min date: 01\\01\\1900

Max date: 31\\12\\2154

.. code-block:: X++

    date d = 03\05\1997; // Date literal d is initialized to May 3rd, 1997
    d = d-729; // d is now May 5th, 1995
    date secondDay = 1; // secondDay is January 2nd, 1990

