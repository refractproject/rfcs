- Start Date: 2015-08-10
- RFC PR: https://github.com/refractproject/rfcs/pull/10

# Summary
Clarify API description namespace and iron out issues which rose during API Blueprint serialization to API description namespace.

# Motivation
The purpose of this document is to clear inconsistencies in the format and make it easier to build tools around it.

# Detailed design

## Data Structure
Correct the `Data Structure` in API description namespace to the following:

```apib
# Data Structure (Element)
+ element: dataStructure (string, fixed)
+ content (Data Structure Element)
```

## Transition Example
Value of `content` should be changed to `[]` instead of `null`.

## Category
Remove the "reserved" word from the description of `scenario` since it can be used as category semantics.

## Copy
The relation between copy elements in `content` and `description` in `attributes` should be clarified. Unless specified otherwise, a copy element's content represents the description of it's parent element and SHOULD be used instead of parent element's description metadata. `Copy Element` should be added to `content` of the following elements in API description namespace:

- Category Element
- Resource Element
- Transition Element
- HTTP Transaction Element
- HTTP Message Payload Element

## HTTP Transaction Example
Value of `content` should be changed to `[]` instead of `null`.

## HTTP Headers
The `content` should be corrected to be an `array[Member Element]`.
