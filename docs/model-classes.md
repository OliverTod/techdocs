---
id: model-classes
title: Classes
---

## Concepts

Concepts are similar to class declarations in most object-oriented languages, in that they may have a super-type and a set of typed properties:

```js
abstract concept Animal {
  o DateTime dob
}

concept Dog extends Animal {
 o String breed
}
```

A concept can be declared as an `abstract concept` if it is not intended to be instantiated. Any such `abstract concept` must have one or more subclasses.

Concepts are typically used to structure data, based on shared properties.

## Identity

Concepts may optionally declare an identifying field, using either the `identified by` (explicitly named identity field) or `identified` (`$identifier` system identity field) syntax.

`Person` below is defined to use the `email` property as its identifying field.

```
concept Person identified by email {
  o String email
  o String firstName
  o String lastName
}
```

While `Product` below will use `$identifier` as its identifying field.

```
concept Product identified {
  o String name
  o Double price
}
```

Identity is typically used to establish [relationships](https://docs.accordproject.org/docs/model-relationships.html) between concerto objects.

## Assets

An asset is a class declaration that has at least one `String` property which acts as the identifier. An asset may have other properties, but will only have one identifier. You can use the `modelManager.getAssetDeclarations` API to look up all assets.

```js
asset Vehicle identified by vin {
  o String vin
}
```

Assets are typically used in your models for the long-lived identifiable Things (or nouns) in the model: cars, orders, shipping containers, products, etc.

## Participants

Participants are class declarations that have at least one `String` property acting as the identifier. A participant may have other properties, but will only have one identifier. You can use the `modelManager.getParticipantDeclarations` API to look up all participants.

```js
participant Customer identified by email {
  o String email
}
```

Participants are typically used for the identifiable people or organizations in the model: person, customer, company, business, auditor, etc.

## Transactions

Transactions are similar to participants in that they are also class declarations that have a single `String` property acting as an identifier. A transaction may have other properties, but will only have one identifier. You can use the `modelManager.getTransactionDeclarations` API to look up all transactions.

```js
transaction Order identified by orderId {
  o String orderId
}
```
Transactions are used to model the [interactions between a contract or clause and the real world](https://docs.accordproject.org/docs/spec-execution.html). Transactions are used for both inbound messages (requests) and as the synchronous return values (responses) from the logic of clauses or contracts.

## Events

Events are similar to participants in that they are also class declarations that have a single `String` property acting as an identifier. An event may have other properties, but will only have one identifier. You can use the `modelManager.getEventDeclarations` API to look up all transactions.

```js
event LateDelivery identified by eventId {
  o String eventId
}
```

Events are typically used in models for the identifiable business events or messages that are emitted by logic to signify that something of interest has occurred or to indicate that some asynchronous action should occur in the real-world, such as notifying a party to the contract that they need to take some action.
