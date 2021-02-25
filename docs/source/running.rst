.. _running:

Running
========== 

Run parameters 
--------------

input 
******
A parameter that defines path for input file. You can use also absolute path or relative path.
     

file type
*********
This parameter is responsible for defining the input file extension to the algorithm. Cleora supports two kinds of input files **.tsv**(tab-separated values) and **.json**.

dimension
**********
Embedding dimension size.

number of iterations
*********************
Max number of iterations.

columns
********
Column names (max. 12), with modifiers from list: [transient::, reflexive::, complex::]

.. list-table::
   :widths: 20 80
   :header-rows: 1

   * - Modifiers
     - Description
   * - transient
     - The field is virtual - it is considered during embedding process, no entity is written for the column
   * - reflexive   
     - The field is composite, containing multiple entity identifiers separated by space in TSV or an array in JSON
   * - complex  
     - The field is reflexive, which means that it interacts with itself, additional output file is written for every such field
   * - ignore
     - The field is ignored, no output file is written for the field


Allowed combinations of modifiers are:  
    - `transient`
    - `complex`
    - `transient::complex`
    - `reflexive::complex`



For TSV datasets containing composite fields (categorical array), multiple items within a field are then separated by space.

The specification of an input format is as follows:

    .. code-block:: none

        --columns="[column modifiers, ::]<column_name> [column modifiers, ::]<column_name> [column modifiers, ::]<column_name> ..."


Combinations which don't make sense are:

.. list-table::
   :widths: 40 80
   :header-rows: 1

   * - Modifiers
     - Description
   * - reflexive
     - This would represent an identity relation
   * - transient::reflexive   
     - This would generate no output
   * - reflexive::transient::complex
     - This would generate no output

Picture below representation how works column modifiers:

.. figure:: _static/cleora-columns.png
    :figwidth: 100 %
    :width: 60 %
    :align: center
    :alt: examples use case of column modifiers


relation name
**************
Name of the relation, for output filename generation.

prepend field name
*******************
Prepend field name to entity in output.

log every n
************
Log output every N lines

in memory embedding calculation
*******************************
Parameter that responsible for using calculate embeddings in memory or with memory-mapped files. Default is on (setting -e 0). If you want off use -e 1.

output dir
***********
Output directory for files with embeddings.

output format
**************
A parameter that defines the format of the output file. Possible output format are textfile (.txt) and numpy (.npy)


Examples run configuration
---------------------------
#. Run 

    .. code-block:: none

        $ python -c "import torch; print(torch.__version__)"
        >>> 1.7.0