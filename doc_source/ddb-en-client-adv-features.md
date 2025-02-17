# Advanced table schema features<a name="ddb-en-client-adv-features"></a>

Learn about advanced table schema features in the DynamoDB Enhanced Client API\.

## Schema overview<a name="ddb-en-client-adv-features-schm-overview"></a>

`[TableSchema](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/enhanced/dynamodb/TableSchema.html)` is the interface to the mapping functionality of the DynamoDB Enhanced Client API\. It can map a data object to and from a map of [AttributeValues](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/services/dynamodb/model/AttributeValue.html)\. A `TableSchema` object needs to know about the structure of the table it is mapping\. This structure information is stored in a [https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/enhanced/dynamodb/TableMetadata.html](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/enhanced/dynamodb/TableMetadata.html) object\.

The enhanced client API has several implementations of `TableSchema`, which follow\. 

### Table schema generated from annotated classes<a name="ddb-en-client-adv-features-schema-mapped"></a>

It is a moderately expensive operation to build a `TableSchema` from annotated classes, so we recommend doing this once, at application startup\.

 [ BeanTableSchema ](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/enhanced/dynamodb/mapper/BeanTableSchema.html)   
This implementation is built based on attributes and annotations of a bean class\. An example of this approach is demonstrated in the [Get started section](ddb-en-client-gs-tableschema.md#ddb-en-client-gs-tableschema-anno-bean)\.  
If a `BeanTableSchema` is not behaving as you expect, enable debug logging for `software.amazon.awssdk.enhanced.dynamodb.beans`\.

[ImmutableTableSchema](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/enhanced/dynamodb/mapper/ImmutableTableSchema.html)  
This implementation is built from an immutable data class\. This approach is described in the [Work with immutable data classes](ddb-en-client-use-immut.md) section\.

### Table schema generated with a builder<a name="ddb-en-client-adv-features-schema-static"></a>

The following `TableSchema`s are built from code by using a builder\. This approach is less costly than the approach that uses annotated data classes\. The builder approach avoids the use of annotations and doesn't require JavaBean naming standards\.

[StaticTableSchema](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/enhanced/dynamodb/mapper/StaticTableSchema.html)  
This implementation is built for mutable data classes\. The getting started section of this guide demonstrated how to [generate a `StaticTableSchema` using a builder](ddb-en-client-gs-tableschema.md#ddb-en-client-gs-tableschema-builder)\.

[StaticImmutableTableSchema](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/enhanced/dynamodb/mapper/StaticImmutableTableSchema.html)  
Similarly to how you build a `StaticTableSchema`, you generate an implementation of this type of `TableSchema` using a [builder](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/enhanced/dynamodb/mapper/StaticImmutableTableSchema.html) for use with immutable data classes\.

### Table schema for data without a fixed schema<a name="ddb-en-client-adv-features-schema-document"></a>

[DocumentTableSchema](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/enhanced/dynamodb/document/DocumentTableSchema.html)  
Unlike other implementations of `TableSchema`, you don't define attributes for a `DocumentTableSchema` instance\. Usually, you specify only primary keys and attribute converter providers\. An `EnhancedDocument` instance provides the attributes that you build from individual elements or from a JSON string\.