- Start Date: 2015-10-16
- RFC PR: (leave this empty)
- Refract Issue: (leave this empty)

# Summary

The goal of this RFC is to formalize and document the various serialization formats used by Refract, as well as explicitly list how to handle ambiguity in refracted metadata and attributes.

# Motivation

1. Currently they are not defined in the specification. There is one RFC for Embedded Refract but it is not visible to people looking at the Refract specification repository.
2. Optionally refracted element metadata and attributes cause ambiguity issues with some serialization formats. We need to formally document how to avoid these ambiguities.
3. Doing this could help us to remove some domain and element-specific knowledge from the parser because it removes ambiguity. For example, in the API Description namespace a resource may have HTTP headers as an attribute, which is always an element. If we remove the ambiguity we can remove special logic for this attribute and treat it like any other, in this case seeing it is refracted and loading the `httpHeaders` element.

# Detailed design

At the time of this writing there are three serialization formats in use to save and load Refract structured data. They are:

- Full JSON
- Compact (list-based) JSON
- Embedded

The [Embedded Refract](https://github.com/refractproject/rfcs/blob/master/text/0005-embedded-refract.md) RFC contains information about when and how to make element metadata and attributes into refract elements, and explains how the parser knows how to handle them. This RFC will focus on the other two formats, which should be described in the Refract specification.

## Full JSON

The full JSON refract serialization will serialize each element as a JSON object with up to four keys: `element`, `meta`, `attributes`, and `content`.

- `element`: The name of the element, e.g. `'string'`
- `meta`: An object containing element metadata
- `attributes`: An object containing element attributes
- `content`: The element's content, which can be any type.

### Example

The following example describes an array named `My array` which looks like `['Hello, world!', 123]`:

```js
{
  "element": "array",
  "meta": {
    "title": "My array"
  },
  "content": [
    {
      "element": "string",
      "content": "Hello, world!"
    },
    {
      "element": "number",
      "content": 123
    }
  ]
}
```

### Refracted Metadata & Attributes

If the array's title from the example above needs to contain extra information, for example an encoding, then it can be refracted:

```js
{
  "element": "array",
  "meta": {
    "title": {
      "element": "string",
      "attributes": {
        "encoding": "utf-8"
      },
      "content": "My array"
    }
  },
  "content": [
    {
      "element": "string",
      "content": "Hello, world!"
    },
    {
      "element": "number",
      "content": 123
    }
  ]
}
```

## Compact (list-based) JSON

The short-form of the full JSON described above is based on lists. Each element is represented by a four item list in which the position of the item determines its semantic meaning. Each list consists of [`element`, `meta`, `attributes`, `content`].

- `element`: The name of the element, e.g. `'string'`
- `meta`: An object containing element metadata
- `attributes`: An object containing element attributes
- `content`: The element's content, which can be any type.

### Example

The following example describes an array named `My array` which looks like `['Hello, world!', 123]`:

```js
["array", {"title": "My array"}, {}, [
  ["string", {}, {}, "Hello, world!"],
  ["number", {}, {}, 123]
]]
```

### Refracted Metadata & Attributes

If the array's title from the example above needs to contain extra information, for example an encoding, then it can be refracted:

```js
["array", {
    "title": ["string", {}, {"encoding": "utf-8"}, "My array"]
  }, {}, [
  ["string", {}, {}, "Hello, world!"],
  ["number", {}, {}, 123]
]]
```

## Preventing Ambiguity

Because an element's metadata and attributes can contain both refracted elements and any other data, as well as fields which may be one or the other depending on content, we must prevent ambiguity. This can be accomplished by **always refracting ambiguous cases**. For example, given this **raw attribute** data:

```js
// Ambiguous raw content for full JSON serialization
{
  "element": "string",
  "content": "foo"
}

// Ambiguous raw content for compact JSON serialization
['foo', {}, {}, 0]
```

It must be serialized so that the parser knows it is **not an element**:

```js
// Unambiguous full JSON version
{
  "element": "object",
  "content": [
    {
      "element": "member",
      "content": {
        "key": {
          "element": "string",
          "content": "element"
        },
        "value": {
          "element": "string",
          "content": "string"
        }
      }
    },
    {
      "element": "member",
      "content": {
        "key": {
          "element": "string",
          "content": "content"
        },
        "value": {
          "element": "string",
          "content": "foo"
        }
      }
    }
  ]
}

// Unambiguous compact JSON version
['array', {}, {}, ['foo', {}, {}, 0]]
```

The expanded serialized form above can now be set in the element's attributes and will be unambiguously interpreted as a refracted data structure in the parser.

# Drawbacks

- Optionally refracting complicates parsing. Using a tool like Minim this isn't a huge problem, but if you expect to use the serialized JSON directly it could be.

# Alternatives

- Always refract metadata and attributes, but where does it stop? This would increase the requirement on domain and element-specific knowledge in the parser and may introduce subtle bugs in parsing for edge cases.

# Unresolved questions

- Should it be up to the serializer how it determines what an ambiguous case is? For example, is any list ambiguous to the compact format, or just a list with four items? Or a list with four items where the first item is a string and the next two are objects?
- Have I missed any ambiguous cases?
