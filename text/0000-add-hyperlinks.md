- Start Date: 2015-11-24
- RFC PR: (leave this empty)
- Refract Issue: (leave this empty)

# Summary

The RFC outlines adding hyperlinking into the base Refract specification.

# Motivation

As we encounter more real-world Refract situations, we are noticing that we seem to need namespaces for domain-specific uses. To provide a general way to extend Refract documents, this document proposes using hyperlinking.

# Design

This proposal is for adding a `links` property to the `meta` object in Refract elements.

- `links` (array)
    - (object)
        - `rel` - Link relation of the link
        - `href` - Resolvable URL for the link

The `rel` property MAY be any defined [link relation](http://www.iana.org/assignments/link-relations/link-relations.xhtml), a resolvable URL to documentation on the link relation, or defined in a `profile` link.

## Use Cases

As mentioned, it is becoming common to need to add domain-specific information into documents. Providing hyperlinks allows to convey this kind of information without adding additional namespace specifications. The downside of additional namespaces is that they require new media types and new libraries. Baking in hyperlinks can provide an avenue that does not require new namespaces.

This shows up when trying to convey state of an element or resource. For instance, the presence of an `edit` link relation in an element tells the client not only how to edit the element, but also that it can edit it. If the link is not there, the client knows it cannot edit that given element or resource.

Additionally, it is common to provide properties that couple the format with certain state and functionality. In the above example, a designer may include `canEdit: true` as a property in an element's attributes. To accomplish this, the designer needs to document this somewhere, but that documentation is now out of band.

## Example

This example shows a `foo` element with two links. The presence of the `edit` link tells the client the user can edit the given element or document, and the `self` link provides a link to the actual resource.

```js
{
  element: 'foo',
  meta: {
    links: [
      {
        rel: 'edit',
        href: '/bar/1'
      },
      {
        rel: 'self',
        href: '/bar/1'
      }
    ]
  }
}
```

## Embeddeding Links

In some situations, it may be advantageous to embed the resources themselves that would be found when the link was resolved. This current proposal is not addressing this yet, though it may be something we should look into in this RFC. This would happen if the design would go better together.

## Additional Benefits

Additionally, if hyperlinks are used in this way, we may be able to remove the concept of namespaces from the base Refract specification. The namespace options allowed for including additional elements, but so far no library is using or has implemented this functionality. Since we've been using content types for extending Refract documents, we could use the `profile` link relation to define additional functionality.

# Drawbacks

While this direction is very flexible and usable, it may be seen as more complex than simple adding domain-specific namespaces.

# Alternatives

The alternative would be creating more namespaces, media types, and namespace-specific libraries.

# Unresolved questions

* Whether to do this or continue creating namespaces
* Whether to include the ability to embed links
