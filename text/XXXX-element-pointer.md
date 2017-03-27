- Start Date: 2017-03-28
- RFC PR: (leave this empty)
- Refract Issue: (leave this empty)

# Element Pointer

## Summary

Element Pointer is currently a special case and the only type that does not
extend from an element which means it has special rules when it comes to
serialisation and de-serialisations.

## Motivation

To aid simplicity and to remove complexity of Refract serialisation, we should
move Element Pointer to be an element itself. This would be more consistent
with other elements such as the Link element.

## Detailed design

The Element Pointer should become an Element Pointer element which can be
described as follows:

### Element Pointer

+ element: elementPointer (fixed)
+ attributes
    + path (enum) - Path of the referenced element to transclude instad of element itself
        + element (default)
        + meta
        + attributes
        + content
+ content (string) - A URL to an ID of an element in the current document
