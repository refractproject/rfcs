- Start Date: 2017-03-24
- RFC PR: (leave this empty)
- Refract Issue: (leave this empty)

# Summary

Fix the type of `meta` and `attributes` collection of a Refract element to `array[Member Element]`.

# Motivation

Currently, `meta` and `attributes` collection of a Refract element can be either written in an object form or in the form of array containing Member Elements. Most of the times, it can be very confusing for the end users. Additionally, there are conceptual differences between both forms of representation and they are not equivalent to each other.

# Detailed design

This allows `meta` and `attributes` collection to be directly typed as `array[Member Element]` instead of the `enum` it currently is. In the case of `meta`, we would still need to talk about the key of each of the member elements being restricted.

A String Element with a `meta` item `id` would be represented in the following form:

```
{
	"element": "string",
	"meta": [
		{
			"element": "member",
			"content": {
				"key": {
					"element": "string",
					"content": "id"
				},
				"value": {
					"element": "string",
					"content": "User"
				}
			}
		}
	],
	"content": "Pavan"
}
```

An attribute item being a Member Element will allow it's key to have their own `meta` and `attributes` while being the property of an object doesn't.

# Drawbacks

We are representing `meta` and `attributes` collection as an array while conceptually they are more similar to an object. This also makes it more verbose and will seem complex.

# Alternatives

We can fix the type of `meta` and `attributes` collection to be an `object` where each item's key is a string and value is an element. But that would disable us from attaching `meta` and `attributes` to the key of the items.

Another alternative of making them an Object Element has been discarded since it would mean that an Element's `meta` and `attributes` collection would itself have it's own `meta` and `attributes`.
