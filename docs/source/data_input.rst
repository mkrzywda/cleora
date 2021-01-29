.. _data-input:

Data input 
========== 

CSV 
----



TSV (tab-separated values) 
--------------------------

For TSV datasets containing composite fields (categorical array), multiple items within a field are then separated by space.

The specification of an input format is as follows:

    --columns="[column modifiers, ::]<column_name> [column modifiers, ::]<column_name> [column modifiers, ::]<column_name> ..."

The allowed column modifiers are:

 - *transient* - the field is virtual - it is considered during embedding process, no entity is written for the column
 - *complex* - the field is composite, containing multiple entity identifiers separated by space in TSV or an array in JSON
 - *reflexive* - the field is reflexive, which means that it interacts with itself, additional output file is written for every such field
 - *ignore* - the field is ignored, no output file is written for the field

Allowed combinations of modifiers are:

- `transient`
- `complex`
- `transient::complex`
- `reflexive::complex`

Combinations which don't make sense are:

- `reflexive` - this would represent an identity relation
- `transient::reflexive` - this would generate no output
- `reflexive::transient::complex` - this would generate no output

JSON 
-------- 

TODO

