- Start Date: 2016-01-15
- RFC PR: (leave this empty)
- Refract Issue: (leave this empty)

# Summary

This RFC is for starting the conversation to move all namespaces and profiles out of the core spec repository and move to their own repositories.

Please note that I am wanting to open this RFC as a way to discuss this and the alternatives. I am not necessarily proposing we do this, but wanting to hear what others have in mind. Once we have the discussion and consensus, I'll update or close this PR.

# Motivation

We have the spec and several namespace documents in the same repository. I am starting to see ways in which this may be confusing things, and in the future see where this may confuse things more.

Currently, as we are versioning and tagging the base specification, it is unclear how we version and tag these namespaces in the same repository. Additionally, it is unclear how we handle discussions, issues, and other roadmap discussions in the same space as the base specification.

All of this tends to blur things together, where the API Description namespace is sometimes seen as the same as Refract. We want to make sure that we keep these ideas separate as we move forward.

We have also accepted that we are moving away from calling these namespaces and calling them profiles instead. Because renaming to profiles breaks links, if we do decide to rename these files, this would be a good discussion to have on whether or not to move elsewhere.

# Detailed design

The idea with this would be to move namespaces and profiles to their own repositories, either one repository per namespace/profile or one repository for all registered namespaces/profiles.

If we put into the separate repositories, it means that each profile has its own issues, pull requests, and potential roadmaps. They can also be version and tagged separately. In this situation, we'll want some list in the main specification repository that can act as a profile registry page.

If we put them into the same repository, it means that all of the profiles make up a kind of registry for profiles, but it lends itself to many of the same issues of keeping profiles and the base specification together in the same repository, namely that tagging and versioning is an issue. It's also hard to see what issues in that single repository go along with an individual profile, along with issues that go along with managing the repository itself.

# Drawbacks

Separating things into their own repositories breaks links. It also moves things away from the current repository, making them less visible.

# Alternatives

The alternative is keeping everything in the same repository and coming up with some way of handling multiple things that need versioning/tagging.

# Unresolved questions

None at this moment.
