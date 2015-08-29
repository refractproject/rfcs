- Start Date: 2015-08-29
- RFC PR: (leave this empty)
- Refract Issue: (leave this empty)

# Summary

The document provides some thoughts on how we can move forward to version 1.0.0 of Refract. This document is not proposing we move to 1.0.0 immediately, but to rather start putting steps in place to get us there quickly and being intentional about it.

# Motivation

As Refract is moving into production environments, we need to keep the following in mind:

1. We want to have as a concise of a spec as necessary for newcomers
1. We want to introduce breaking changes thoughtfully, which is what SemVer encourages. We currently can't do SemVer correctly without moving to 1.0.0.
1. We want to start registering media types for Refract representations
1. Moving this to production means people are actually going to start using this spec in the wild, and we need to prepare for feedback

With this in mind, I'd like to start now thinking through the steps on how to prepare. This design outlines some small steps. Additionally, this document is open to additional suggestions in what we can do.

# Detailed design

## Versioning Namespace Documents

In addition to moving to 1.0.0, we need to actually start versioning namespace documents. The reason for this is that we do not want a breaking change in a namespace to require a major version bump for the entire spec.

**Proposal**: Start versioning current and future namespaces and move each namespace to their own repo. We can do this immediately.

## Namespace Functionality

The one area of Refract that we have not implemented in our implementations is namespaces. Currently, the design of namespaces mimics that of XML, but the way we have implemented it does not follow. In Refract, each element can have its own lexically-scoped elements as defined in its own namespace. This allows for namespaces to be defined and used deep within a data structure.

Our implementations have diverted from this concept, and are rather relying on the document itself to define the elements includes. We still have namespaces, but the namespaces are not scoped within elements inside the document and are not explicitly defined in the documents.

In order to get to 1.0.0, we need to think about whether we want to leave these kinds of things in the spec and change to them, or if we want to align the spec with what we've practically done.

**Proposal**: Consider removing ability for namespaces to be lexically scoped on each element and make namespaces rather document-defined as we've done in our implementations.

## Separating Out Serialization Formats

An important concept of Refract is that it is a model for representing data structures and is not a JSON format. With that said, we do have two current formats as defined in the spec, and all examples in the spec use one of these formats.

This decoupling I think is important, because it gives freedom to implementors to implement the best way they see fit in their language/platform, and it allows for other serialization formats to spring up that may be helpful to others.

**Proposal**: Explain the difference in the conceptual model and the serialization formats, and potentially move these serialization descriptions to their own file in the spec repo, separating them from the main spec.

# Drawbacks

This could be considered to be premature. I am open to that discussion, and also to the idea of doing some of the things outlined above without having 1.0.0 in mind.

# Alternatives

We can extend the time we spend in pre-1.0.0 days.

# Unresolved questions

This document does not specifically address how we define namespaces, only to start the discussion on what to do about them.
