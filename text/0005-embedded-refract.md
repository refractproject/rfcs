- Start Date: 2015-08-29
- RFC PR: https://github.com/refractproject/rfcs/pull/14
- Refract Issue: (leave this empty)

# Summary

This document outlines a new serialization format for embedding Refract.

# Motivation

1. Our current formats either look like XML, the DOM, or Lisp
1. People already "get" JSON
1. Other serializations we have are verbose

# Detailed design

## Overview

For this serialization, there are two basic concepts:

1. There is a reserved property name of `_refract`
1. There is a Refract Object with properties:
    - element
    - meta
    - attributes
    - content

All valid JSON that adheres to reserved property is valid Embedded Refract.

## Basic JSON

We'll start with a basic JSON example, which we'll say is a person and their bowling scores.

```json
{
  "first_name": "John",
  "last_name": "Doe",
  "age": 28,
  "scores": [150, 202, 145]
}
```

## Refracting Object Elements

In Refract, this is an object with four members. With Embedded Refract, I can annotate by embedding refract using the `refract` property.

```json
{
  "_refract": {
    "element": "object",
    "meta": {
      "id": "bowler-103"
    }
  },
  "first_name": "John",
  "last_name": "Doe",
  "age": 28,
  "scores": [150, 202, 145]
}
```

This is what this would like in full Refract.

```json
{
  "element": "object",
  "meta": {
    "id": "bowler-103"
  },
  "content": [
    {
      "element": "member",
      "content": {
        "key": {
          "element": "string",
          "content": "first_name"
        },
        "value": {
          "element": "string",
          "content": "John"
        }
      }
    },
    {
      "element": "member",
      "content": {
        "key": {
          "element": "string",
          "content": "first_name"
        },
        "value": {
          "element": "string",
          "content": "Doe"
        }
      }
    },
    {
      "element": "member",
      "content": {
        "key": {
          "element": "string",
          "content": "age"
        },
        "value": {
          "element": "number",
          "content": 28
        }
      }
    },
    {
      "element": "member",
      "content": {
        "key": {
          "element": "string",
          "content": "scores"
        },
        "value": {
          "element": "array",
          "content": [
            {
              "element": "number",
              "content": 150
            },
            {
              "element": "number",
              "content": 202
            },
            {
              "element": "number",
              "content": 145
            }
          ]
        }
      }
    }
  ]
}
```

## Refracting Value Elements

If values do not have any meta values or attributes, there is no need to represent them as refracted. If I were to add some annotation to one of the values, it would show up as Refract and would be defined as Refracted by use of the `refract` property keyword.

```json
{
  "first_name": "John",
  "last_name": "Doe",
  "age": {
    "_refract": {
      "element": "number",
      "meta": {
        "id": "bowler-103-age"
      },
      "content": 28
    }
  },
  "scores": [150, 202, 145]
}
```

Above, I've added an ID to the age of the bowler. Notice how I just refracted that value in that specific place. This is also the same as:

```json
{
  "_refract": {
    "element": "object",
    "meta": {
      "id": "bowler-103"
    },
    "content": {
      "age": {
        "element": "number",
        "meta": {
          "id": "bowler-103-age"
        },
        "content": 28
      }
    }
  },
  "first_name": "John",
  "last_name": "Doe",
  "scores": [150, 202, 145]
}
```

This will also support full member elements, so even this below is equivalent (note that it's a slight modification from the full Refract):

```json
{
  "_refract": {
    "element": "object",
    "meta": {
      "id": "bowler-103"
    },
    "content": [
      {
        "element": "member",
        "content": {
          "key": "age",
          "value": {
            "_refract": {
              "element": "number",
              "meta": {
                "id": "bowler-103-age"
              },
              "content": 28
            }
          }
        }
      }
    ]
  },
  "first_name": "John",
  "last_name": "Doe",
  "scores": [150, 202, 145]
}
```

In full Refract, you would have to also provide the element for the key "age" in the previous example, but since we can rely on the `refract` keyword, we can leave it unrefracted. We could Refract it more later if necessary.

## Refracting Array and Array Items

Array items can be embedded without refracting the entire array.

```json
{
  "first_name": "John",
  "last_name": "Doe",
  "age": 28,
  "scores": [
    {
      "_refract": {
        "element": "number",
        "meta": {
          "id": "bowler-103-game-1"
        },
        "content": 150
      }
    },
    202,
    145]
}
```

Full arrays can also be refracted.

```json
{
  "first_name": "John",
  "last_name": "Doe",
  "age": 28,
  "scores": {
    "_refract": {
      "element": "array",
      "meta": {
        "id": "bowler-103-scores"
      },
      "content": [150, 202, 145]
    }
  }
}
```

## Refracting Attributes

This makes it nice for refracting attributes, because now you know what attributes have been refracted. This could become:

```json
{
  "_refract": {
    "element": "object",
    "meta": {
      "id": "bowler-103"
    },
    "attributes": {
      "foo": "baz"
    }
  },
  "first_name": "John",
  "last_name": "Doe",
  "age": 28,
  "scores": [150, 202, 145]
}
```

```json
{
  "_refract": {
    "element": "object",
    "meta": {
      "id": "bowler-103"
    },
    "attributes": {
      "foo": {
        "_refract": {
          "element": "string",
          "content": "baz"
        }
      }
    }
  },
  "first_name": "John",
  "last_name": "Doe",
  "age": 28,
  "scores": [150, 202, 145]
}
```

## Edge cases

### Properties in Value Elements

What would this mean, where we have the `foo` property?

```json
{
  "first_name": "John",
  "last_name": "Doe",
  "age": {
    "_refract": {
      "element": "number",
      "content": 28
    },
    "foo": "bar"
  },
  "scores": [150, 202, 145]
}
```

We SHOULD ignore these properties.

# Drawbacks

"Don't we have more important things to do right now?" you may say. Sure! But it's the weekend and I'm doing some free-time thinking.

# Alternatives

We have alternatives already, so the idea would be that we don't do this if the current ones are enough.

# Unresolved questions

None at this point.
