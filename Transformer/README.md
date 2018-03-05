# Transformer


## Transformer Concept
As already mentioned the transformer transforms one JSON object into another. Prior to this transformation a semantic mapping has to take place where the entities of the source model are mapped against the entities of the Open Integration Hub master data model.

A transformer should transform data in both directions (from _source model_ to _Open Integration Hub master data model_ & from _Open Integration Hub master data model_ to _source model_) as can be seen in the [connector overview](https://github.com/openintegrationhub/Connectors/blob/master/Assets/ConnectorsV2.svg).
A transformer expects a JSON object  as an input. Depending on the direction of the transformation the input either represents the structure of the proprieraty data model (direction: _source model_ --> _Open Integration Hub master data model_) or the structure of the Open Integration Hub master data model (direction: _Open Integration Hub master data model_ --> _source model_). Afterwards it transforms the incoming JSON object into another JSON object e.g. via a transformation language (_We suggest JSONata for the transformation_).  Depending on the transformation direction, the transformer's output is then send either to the Open Integration Hub and is validated against a deposited JSON schema or to the corresponding adapter.

## Transformation Language
One way of transforming the JSON objects is the usage of a transformation language. As already mentioned our suggested transformation language is JSONata as it is especially built to transform one JSON object into another.

For detailed information on transformation language and JSONata as well as a general example please have a look at [TransformationLanguage](/TransformationLanguage.md)

## Transformer Evolution
Sometimes there is a need to change the existing data model to adjust to different requirements. In this case, a transformer needs to be adjusted/updated in order to be compatible with the newest version of the data model.

Some changes do not affect existing mappings/transformations and transformers can still be used (although they are not reffering to the newest model version). Thus, backward compatibility is automatically given. According to the [OData specification](http://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part1-protocol/odata-v4.0-errata03-os-part1-protocol-complete.html#_Toc453752210) (shortened/modified list) the following changes do not require a change within a transformer:

- Adding an attribute that is nullable
- Adding an object to the model
- Adding a new complex type to the model
- Adding an option to an enumeration

Apart from this various changes require transformer adjustments as they break existing mappings/transformations. Thus, backward compatibility is not automatically given (in case the Open Integration Hub operator does not run both model versions in parallel). The following list provides an overview of changes that require a transformer adjustment:

- Renaming an existing attribute
- Changing the type of an existing attribute
- Changing the properties of an existing attribute from _nullable_ to _not nullable_
- Deleting an existing attribute
- Renaming an existing object
- Deleting an existing object
- Adding an attribute that is not nullable

If a new version of a model is created, two options exist to create a transformer that is compatible with the newest model version:
1. The existing transformer is adjusted/updated according to the structure of the new data model.
2. A completely new transformer is built.

The following illustrations shows how a transformer works and a possible adjustments that has to be made if a change in a data model occurs:

![TransformerEvolution](Assets/TransformerEvolution.svg)