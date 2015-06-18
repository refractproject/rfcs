- Start Date: 2015-06-18
- RFC PR: (leave this empty)
- Refract Issue: (leave this empty)

# Summary

Provide clarity and additional elements/properites in API Description namespace.

# Motivation

This will make it easier to understand for new users and cover more areas for existing API Description formats.

# Detailed design

I have spent a lot of time thinking about this namespace, and I believe I’m going to keep my suggestions for now mostly to making the namespace clearer to new users. I think we can handle adding state and affordances to this later to accommodate things like the concepts from Resource Blueprints.

This contains mostly questions and thoughts. Would love your thoughts on what you'd like to see addressed in a PR.

## Combine Namespaces

I think we should combine the API Description namespace with the resource namespace. Z is already good with this, but listing it here.

## Elements in Attributes

This is mainly a point for discussion. Refract allows for including elements within the attributes section of an element. Even though it’s possible, would it be helpful to avoid this in such an important namespace? Reason being, this will be one of the first places people interact with Refract, and to use complex features may be too much.

## HREF Variables

I think we should call them “hrefVariables” everywhere instead of parameters in places. I think this will be more consistent and easier to understand for newcomers. This will make more sense in how we handle inheritance.

Question: does it make sense to provide an “in” attribute that defines where in the URI template the variable may be found (e.g. path, query param, etc.)?

## Defining Classes

Swagger provides a way to define tags that can be applied to resources throughout the document. Refract has the “class” attribute that we can use the same way, we only need a way to define a class name and provide the description for it. Of course, this won’t carry over to API Blueprint, but that’s OK.

## Clarify Inheritance

We need to clarify how inheritance works with:

* HREF Variables and HREF values throughout the document
* Content types in payloads
* Methods in transitions
* Resources with schemas (though not in the spec) should be inherited by transitions

I don’t so much mind the inheritance rules, as we can handle this kind of inheritance with Minim by traversing the tree up and down for the correct HREF.

## Transitions at Root

We should be able to define transitions on the root of the document and not require they are nested within a resource. This type of transition, though, should have a URL and a method.

## Transition Attributes

I think it would be helpful to call this something other than attributes, as this will not be obvious to most people. Additionally, it means you have “element.attributes.attributes”, which is not a big deal, but something I think we can avoid. Not sure what to call it.

This seems to me like a data structure for the transition.

## Subclass Asset

I think it would be clearer if we subclass the Asset Element and added one called “messageShema” and another called “messageBody.” I think this will make reading a API Description make more sense than seeing Asset alone with classes.

## Category Element

I still have trouble understanding what “category” means here, but that may just be me. Is there a better name? Is this from the philosophical world? Maybe something like “section” or from the HTML world “div”?

## Provided Media Types

Swagger supports a section that defines what formats the server will respond with. This should be added (already discussed with Z).
