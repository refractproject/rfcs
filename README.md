# Refract and Refract Libraries RFCs

> Hat tip to the [Ember RFC process] and [Rust RFC process].

Many changes, including bug fixes and documentation improvements can be
implemented and reviewed via the normal GitHub pull request workflow.

Some changes though are "substantial", and we ask that these be put
through a bit of a design process and produce a consensus among the Refract
core team.

The "RFC" (request for comments) process is intended to provide a
consistent and controlled path for new features to enter the framework.

## Active RFC List

- [0004 Clarity on API Description Namespace](text/0004-clarify-api-namespace.md)
- [0005 Embedded Refract](text/0005-embedded-refract.md)

## Completed RFC List

- [0001 MSON Rename](text/0001-mson-rename.md)
- [0002 Clarity on API Description Format](text/0002-clarity-api-description.md)
- [0003 Rename `class` meta property](text/0003-class-rename.md)

## When you need to follow this process

You need to follow this process if you intend to make "substantial"
changes to Refract, Refract libraries, or related documentation. What
constitutes a "substantial" change may vary depending on how Refract progresses.

If you submit a pull request without going through the RFC process, it may be
closed with a polite request to submit an RFC first.

## What the process is

In short, to propose a major change or to simply discuss design ideas and
proposals, here are the steps to do so:

* Fork the RFC repo http://github.com/refractproject/rfcs
* Copy `0000-template.md` to `text/0000-my-feature.md` (where
'my-feature' is descriptive. don't assign an RFC number yet).
* Fill in the RFC with as many details as possible.
* Submit a pull request. The pull request is where the feedback will be given
about the RFC.
* Build consensus and integrate feedback.
* Eventually, someone on the Refract core team will either accept the RFC by
merging the pull request, at which point the RFC is 'active', or reject it by
closing the pull request.

## The RFC life-cycle

Once an RFC becomes active then authors may implement it and submit the
change as a pull request to the relevant repository. An 'active' is not a rubber
stamp, and in particular still does not mean the feature will ultimately
be merged; it does mean that the core team has agreed to it in principle
and are amenable to merging it.

Furthermore, the fact that a given RFC has been accepted and is
'active' implies nothing about what priority is assigned to its
implementation, nor whether anybody is currently working on it.

Modifications to active RFC's can be done in followup PRs.  We strive
to write each RFC in a manner that it will reflect the final design of
the feature; but the nature of the process means that we cannot expect
every merged RFC to actually reflect what the end result will be at
the time of the next major release; therefore we try to keep each RFC
document somewhat in sync with the language feature as planned,
tracking such changes via followup pull requests to the document.

An RFC that makes it through the entire process to implementation is
considered 'complete' and is moved to the 'complete' folder; an RFC
that fails after becoming active is 'inactive' and moves to the
'inactive' folder.

## Implementing an RFC

The author of an RFC is not obligated to implement it. Of course, the
RFC author (like any other developer) is welcome to post an
implementation for review after the RFC has been accepted.

If you are interested in working on the implementation for an 'active'
RFC, but cannot determine if someone else is already working on it,
feel free to ask (e.g. by leaving a comment on the associated issue).

## Reviewing RFCs

Each week the Refract core team will attempt to review some set of open RFC
pull requests.

[Rust RFC process]: https://github.com/rust-lang/rfcs
[Ember RFC process]: https://github.com/emberjs/rfcs
