- Start Date: 2015-11-24
- RFC PR: (leave this empty)
- Refract Issue: (leave this empty)

# Summary

The RFC outlines adding hyperlinking into the base Refract specification.

# Motivation

As we encounter more real-world Refract situations, we are noticing that we seem to need namespaces for domain-specific uses. To provide a general way to extend Refract documents, this document proposes using hyperlinking.

# Design

This proposal is for adding a Link Element to the base spec.

- `element`: link (string, fixed)
- `attributes`
    - `relation` (string) - Link relation type as specified in [RFC 5988][].
    - `href` (string) - The URI for the given link

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
        element: 'link',
        attributes: {
          relation: 'edit',
          href: '/bar/1'
        }
      },
      {
        element: 'link',
        attributes: {
          relation: 'self',
          href: '/bar/1'
        }
      }
    ]
  }
}
```

## Embeddeding Links

While not addressed in this PR, embedding links may be possible by including the [Asset Element](https://github.com/refractproject/refract-spec/blob/master/namespaces/api-description-namespace.md#asset-element) in the base specification and making it available as content for this Link Element.

## Additional Benefits

Additionally, if hyperlinks are used in this way, we may be able to remove the concept of namespaces from the base Refract specification. This change is out of scope of this RFC, but mentioning so we keep it in mind.

## Transition in the API Description Namespace

If we do this, the [Transition element](https://github.com/refractproject/refract-spec/blob/master/namespaces/api-description-namespace.md#transition-element) in the API Description will inherit from this element.

# Drawbacks

While this direction is very flexible and usable, it may be seen as more complex than simple adding domain-specific namespaces.

# Alternatives

The alternative would be creating more namespaces, media types, and namespace-specific libraries.

# Unresolved questions

* Whether to do this or continue creating namespaces
