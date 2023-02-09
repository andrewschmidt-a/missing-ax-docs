Types
=====

.. _primatives:

Primatives
------------

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

