- Start Date: 2015-06-18
- RFC PR: https://github.com/refractproject/rfcs/pull/1
- Refract Issue: https://github.com/refractproject/refract-spec/pull/36

# Summary

Provide clarity and additional elements/properites in API Description namespace.

# Motivation

The purpose of this document is to make it easier for newcomers to understand the format and build tools around it.

# Detailed design

## Combine Namespaces

We should combine the API Description namespace with the resource namespace.
Right now they are separate and it would be clearer if they were not.

## HREF Variables

We should call them “hrefVariables” everywhere instead of parameters in places (specifically transitions).
I think this will be more consistent and easier to understand for newcomers.
This will make more sense in how we handle inheritance as well, because parameters inheriting from hrefVariables does not seem optimal.

## Clarify Inheritance

We need to clarify how inheritance works by defining the behavior for:

* HREF Variables and HREF values throughout the document
* Content types in payloads
* Methods in transitions
* Resources with schemas (though not in the spec) should be inherited by transitions

## Transitions at Root

We should be able to define transitions on the root of the document and not require they are nested within a resource.
This type of transition, though, should have a URL and a method.

## Provided Media Types

We should add a section that defines what media types the server will respond with.

## Transition Attributes

We should rename transition attributes to "data" to prevent confusion because the term "attributes" is already used within Refract.
