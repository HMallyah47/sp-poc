This repository contains Proof of Concepts/ Example code for Kafka maintained by the Streaming Platform team.

**Avro Schemas & Schema Registry**

_Schema Evolution_

Modules SchemaRegistryAvroSchemaV1 and SchemaRegistryAvroSchemaV1 demonstrate Schema Evolution, as well as how to produce and consume Avro data and work with the Schema Registry.

The module SchemaRegistryAvroSchemaV1 contains a Producer and Consumer producing and consuming Avro data in the schema as seen in the resources/avro/customer-v1.avsc file. It contains fields such as First Name, Last Name, Age, Height, Weight and Automated Email.

The module SchemaRegistryAvroSchemaV1 contains a Producer and Consumer producing and consuming Avro data in the schema as seen in the resources/avro/customer-v2.avsc file. It contains fields such as First Name, Last Name, Age, Height, Weight and Email. Here, we have 2 new fields Email and Phone Number and the Automated Email field is removed. Since the new fields and the field that was removed have default values, full compatibility is maintained. ConsumerV1 and ConsumerV2 can consumer messages produced by both versions of the Producers.

_Backward Compatibility: A backward compatible change is when a new schema can be used to read old data._

Message produced by ProducerV1 to topic using schema in (old schema)customer-v1.avsc

`{"first_name": "John", "last_name": "Doe", "age": 34, "height": 178.0, "weight": 75.0, "automated_email": false}`

ConsumerV2 using schema customer-v2.avsc consumes the same message as:

`{"first_name": "John", "last_name": "Doe", "age": 34, "height": 178.0, "weight": 75.0, "phone_number": null, "email": "missing@example.com"}`

_Forward: A forward compatible to change is when an old schema can be used to read new data._

Message produced by ProducerV2 to topic using schema in (new schema) customer-v2.avsc

`{"first_name": "John", "last_name": "Doe", "age": 34, "height": 178.0, "weight": 75.0, "phone_number": "(123)-456-7890", "email": "john.doe@gmail.com"}`

ConsumerV1 using schema customer-v2.avsc consumes the same message as:

`{"first_name": "John", "last_name": "Doe", "age": 34, "height": 178.0, "weight": 75.0, "automated_email": true}`







