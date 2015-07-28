- Start Date: 2015-06-18
- RFC PR: (leave this empty)
- Refract Issue: (leave this empty)

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

## Defining Classes

Swagger provides a way to define tags that can be applied to resources throughout the document.
Refract has the “class” attribute that we can use the same way, we only need a way to define a class name and provide the description for it.
Of course, this won’t carry over to API Blueprint, but that’s OK.

## Clarify Inheritance

We need to clarify how inheritance works by defining the behavior for:

* HREF Variables and HREF values throughout the document
* Content types in payloads
* Methods in transitions
* Resources with schemas (though not in the spec) should be inherited by transitions

## Transitions at Root

We should be able to define transitions on the root of the document and not require they are nested within a resource.
This type of transition, though, should have a URL and a method.

## Subclass Asset

We should subclass the Asset Element and add one called “messageShema” and another called “messageBody.”
This will make reading a API Description make more sense than seeing Asset alone with classes.

## Provided Media Types

We should add a section that defines what media types the server will respond with.

## Add Schema to Resource

A resource should be able to have its own schema, whereas now it cannot.

# Unresolved questions

## Category Element

What is a "category"?
Does this word make sense used here?
Maybe something like “section” or from the HTML world “div”?

## Transition Attributes

I think it would be helpful to call this something other than attributes, as this will not be obvious to most people.
We have parameters, variables, and attributes throughout the document, which seems confusing.
What should this be called?
