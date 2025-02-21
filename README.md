﻿# REM-Cloud Message Bus API
[REM](https://www.garaio-rem.ch/) (Real Estate Management) is a suite of products and systems developed by GARAIO AG. The REM-Cloud Message Bus connects
these systems and enables other organisations to integrate with REM. The REM-Cloud Message Bus is a [RabbitMQ Message Bus](https://www.rabbitmq.com/).
RabbitMQ itself implements [AMQP](https://www.amqp.org/).
## Access
If you wish to access the REM-Cloud Message Bus please contact us on [garaio-rem@garaio.com](mailto:youraddress@ucsc.edu).

Once you're granted access, credentials and access details are sent to you. The access details contain:

Detail | Description
---|---
app id | An app id (Unique Application ID) (e.g: 'YourService'). The app id is also the name of your queue from which you can retrieve your messages
userid / password | Login  credentials for RabbitMQ
exchange name | The name of the exchange to which you can send messages

## About this specification
Certain parts of this specification can have a specification status. These status are:

Status | Meaning
---|---
Draft| The information may become effective but can change without further notice|
Official| The information is effective and will not change without further notice|
Deprecated| The information may still be effective but can become invalid in future|

If no status is mentioned the information is "Official".

## Messages
### Message Properties

All messages must specify at least the following AMQP message properties:

Property | Value | Example | Description
---|---|---|---
app_id| \<app_id> | 'YourService' or 'REMCustomerA'  | Uniquely identifies the sender of a message
content_type| application/json || The content type must always be JSON |
content_encoding | UTF-8 || The message encoding must always be UTF-8 |
message_id | \<app_id>-\<app_specific_uid>| 'YourService-7712897' | Uniquely identifies a message. The app specific uid is an alphanumeric, app wide unique key
timestamp | Unix timestamp | '1553245964' | A timestamp to indicate when the message was created

### Headers

The headers are part of the message properties and must specify at least the app id

Property | Value | Example | Description
---|---|---|---
app_id | \<app_id> | headers: { app_id: 'YourService' }  | In order to be able to route the messages we need the app id in the headers, too

Some events require additional header properties. They are documented in the event description where needed.

### Events

Events are messages that can be received by multiple subscribers. The message body contains a json data structure.  

## Contexts
Events are grouped by contexts. A context relates to a certain subdomain within the domain of property management,
or to a domain outside of property management.

Context | Description
---|---|
[Masterdata](masterdata_context.md)| Informs about changed data in the context of Property, Buildings and Units |
[Letting](letting_context.md)| Events related to the letting process | 
[Tenancy Application](tenancy_application_context.md)| Events related to tenancy applications |
[Tenant Portal](tenant_portal.md)| Events that occur on a Tenant Portal |
