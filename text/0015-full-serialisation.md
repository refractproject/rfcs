- Start Date: 2017-03-27
- RFC PR: (leave this empty)
- Refract Issue: (leave this empty)

# Refract Full JSON Serialisation

## Summary

Full Refract serialisation is not clearly defined in the Refract specification
and there are a few ambiguities that may occur when parsing a Refract document.

## Motivation

It should be clear to consumers how to serialise and de-serialise refracted
elements.

At the moment there are no formal rules for full serialisation and some
implementations are inconsistent. Many Refract serialisers support embedding
both refracted and raw JSON data in a Refract document, however many
de-serialisers and consumers of Refract do not support both forms in all
places.

Since an element does not need to be refracted, that leads to unrefracted
elements being used in some cases causing ambiguity and leads to consumers
having to know details about a Refract namespace to be able to truely parse it.

It should be possible for a Refract consumer to consume a Refract document
without knowing about specific elements from a namespace. There should be no
ambiguities when parsing a Refract document.

## Detailed design

We should provide a full specification on how Refract elements can be
serailised as JSON and recommendations on how to consume Refract elements in
JSON.

### JSON Serialisation

A Refract element MUST be serialised as JSON as follows:

- element (required, string)
- meta (optional)
- attributes (optional)
- content (optional)

The name of the element is always required, however other JSON values may be
omitted, for example if there is no meta keys then it SHOULD be omitted from
the JSON object.

#### Content

The content inside JSON Serialisation MUST always be a Refracted element, an
array of Refracted element or a primitive type such as string, number, boolean
or none. The only exceptions to this rule is for any element types described
within the Refract specification.

These same rules would apply to meta and attribute values of an Element. They
must also always be Refracted.

For example, it is NOT possible to serialise an arbitrary object inside the
content value for elements not defined within the base Refract specification.
Otherwise it can be ambiguous for consumers whether the JSON object is another
element or JSON data.

As example, the following is NOT permitted:

```json
{
  "element": "custom",
  "content": {
    "content": "abc"
  }
}
```

Instead, a `custom` element with the content of an object with `content` =
`abc` should be serialised as follows where the content is a Refract element:

```json
{
  "element": "custom",
  "content": {
    "element": "object",
    "content": [
      {
        "element": "member",
        "content": {
          "key": {
            "element": "string",
            "content": "content"
          },
          "value": {
            "element": "string",
            "content": "abc"
          }
        }
      }
    ]
  }
}
```

Another example of a serialisation that is NOT permitted would be an array of a
primitive type. For example:

```json
{
  "element": "custom",
  "content": [
    "abc"
  ]
}
```

Instead, a `custom` element with the content of a array of primitive types
should be an array of Refracted elements as follows:

```json
{
  "element": "custom",
  "content": [
    {
      "element": "string",
      "content": "abc"
    }
  ]
}
```

## Drawbacks

Forcing all elements to be fully refracted can lead to bloated documents and
increase document sizes for Refract. We should offer compact Refract
serialisation when size is important.

## Alternatives

Another design in https://github.com/refractproject/rfcs/pull/17 has been
proposed, this RFC is similar except it has addressed some feedback from other
Refract developers and does not cover compact Refract serialisation.
