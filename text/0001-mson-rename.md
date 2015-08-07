- Start Date: 2015-07-29
- RFC PR: https://github.com/refractproject/rfcs/pull/5
- Refract Issue: https://github.com/refractproject/refract-spec/pull/35

# Summary

Rename the MSON Refract Namespace to "Data Structures Namespace" to greater
represent what the namespace is used for.

# Motivation

The current name of the MSON namespace is confusing since it references
Markdown. The namespace is called "MSON" for historical reasons, and
ultimately Markdown is a serialization form for this namespace, but should not
be the name for this namespace.

The namespace purpose is to allow consumers to define recursive data structures.

# Detailed design

The namespace purpose is to allow consumers to define recursive data
structures, and therefore the proposed new name for this namespace is
"Data Structure Namespace".

# Drawbacks

Currently, the MSON refract namespace references, and heavily depends on the
MSON specification. It might be difficult to change this as it would require
substancially changing the refract namespace. I propose we change the name, but
we will reference the MSON specification.
