- Start Date: 2015-08-10
- RFC PR: (leave this empty)
- Refract Issue: (leave this empty)

# Summary
Clarify API description namespace and Iron out issues which rose during API Blueprint serialization to API description namespace.

# Motivation
The purpose of this document is to clear inconsistencies in the format and make it easier to build tools around it.

# Detailed design

## HREF Variables
We need to clarify about the value of the `content` in the `hrefVariables` element.

## Data Structure
We don't need a `Data Structure` because an element which is an `object`, `extend` or `array` can be considered as a data structure element.

*(The current spec is a lot confusing. What is the `Data Structure Element`? Why is `Data Structure` inheriting from it?)*

## Resource
Since `hrefVariables` is an element, we should move it to be under `content` rather than leave it under `attributes`.

## Transition
Similarily to the Resource, we need to move `hrefVariables` to be under `content`. `Data Structure` in Resource is under `content`, but it is under `attributes` in Transition. To resolve this inconsistency, we need to move `Data Structure` to be under `content`. Another reason for it is that `Data Structure` is an element.

## Transition Example
Value of `content` should be changed to `[]` instead of `null`.

## Category
We need to clarify what `transitions` category is about. If it is being reserved for future use, we need to add reserved keyword.

## Copy
We need to clarify what the relation between copy elements in `content` and `description` in `attributes` is. Is `description` just an aggregator of all `copy` elements? Why does some examples contain `description` without any `copy` elements and some examples contain `copy` elements but doesn't contain `description`. Since `copy` element is superior, why do we need `description` if we can use `copy` elements everywhere?

## HTTP Transaction Example
Value of `content` should be changed to `[]` instead of `null`.

## HTTP Headers
We need to change the base type from `Array Type` to `Element`. We also need to correct the `content` to be an `array[Member Element]`.

## HTTP Message Payload
Since `httpHeaders` is an element, we need to move it to be under `content`.

# Drawbacks

## Data Structure
It can be tough for tools to get the data structure from the format.

# Unresolved questions

## Asset
What is the `href` in `attributes`? What does it represent? Maybe we need to have an example there.

## HTTP Transaction
Why does it contain exactly 1 request and 1 response? A transaction example in API Blueprint can contain 1 request and many responses.

## HTTP Request Message
What about the name of a request from API Blueprint? How will it be represented?
