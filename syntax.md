# Syntax

## Cardinality

The documentation contains tables of attributes for requests and responses. For each of those attributes, a cardinality is given. This then defines, which attributes are mandatory or optional, and which elements will be contained within an json array (with at least 0 or 1 or more elements).

The following table defines the possible values for cardinality use within this documentation:

| Cardinality | Description 
|-------------|----------------------------------------------------------------------------|
| 1           | The attribute is mandatory. A non null value must be provided
| ?           | The attribute is optional. Both, ommitting the attribute or setting a null value is ok
| +           | The attribute contains an array of values with at least one element
| *           | The attribute contains an array of values with at least zero elements (that is, the array is optional)

