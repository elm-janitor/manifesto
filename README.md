# Work in progress.

Topics this README needs to cover or direct the reader to are:

How to use an elm-janitor patched core package in an Elm project. Peters
instructions. Future plans in this area - someone needs to write a tool to
automate distribution/install of these patched versions.


# Elm Core Library Maintenance

`elm-janitor` is a group of Elm users that are interested in maintaining the
Elm core packages by applying patches to them. The patch stack will always
be applied on top of the latest official release of the Elm core packages,
with patches removed from the stack if they become part of the official release.

# Is this a fork of Elm?

This is a *release branch* of Elm. It will only apply patches to Elm core
packages that do not change their APIs. The aim of this GitHub organization is
to keep Elm core packages up to date with their pull requests. This is so that

  * Elm users can get the core packages with fixes applied.
  * Elm users have a process for getting PRs into these packages, without being
    blocked on the official releases.

The difference between a fork and a release branch, is that the release branch
will not try to lead the design of these packages. It will be ahead of the
upstream in terms of patches. All patches will be made available to the upstream
for consideration for inclusion. The main aim of a release branch is to fix
defects that are fed back from real world use of the packages, in a timely
manner.

# What will get fixed here?

Pull requests to the Elm core packages, are evaluated to assign them to one of
the following level. The level names are hopefully self explanatory, see the
Appendix at the end of this README for some more detailed notes.

1. Doc Fixes
2. Performance Improvements
3. Runtime Bug Fixes
4. API Changes to Implementation
5. API New Functions
6. API Changes
7. Language Semantics

A sheet of analysed PRs is maintained here,
[Elm Bug Fixes](https://docs.google.com/spreadsheets/d/12Jz3CI4CFomF6aS0blMeQIzDpAh2PiqgxlxkJhn7mOg/edit?usp=sharing).

There is a column in the sheet to mark some PRs as "Controversial", which might
happen if Evan has commented that a particular solution may be undesirable. This
flag is used to mark things that are too controversial to merge.

Anything at levels 1-4 is acceptable for fixing as part of this maintenance work.
Level 1 is regarded as low priority.
Level 5 is backwards compatible, but code using it would not be able to revert
to the original APIs without change. Level 5 is therefore currently out of scope.

# How do I get my patch included?

Make a PR against whichever elm/ core project you want to make a change to.

Post a link to your PR to the
[Incremental Elm #elm-janitor](https://discord.com/channels/534524278847045633/933054571981471755)
channel. If you need an invite to join the Discord server, use this link here to
sign up:
[Incremental Elm Discord Invite](https://discord.com/invite/NZUYqYPYnh)

We will assess your PR and assign it a level as described above, and add it to
the bug tracking sheet.

To keep the patches clean, please ensure your patch follows the style of the
code being modified, and does not include any changes to whitespace of code
outside of the code being modified. In particular, note that Evan does not
use elm-format on the core packages, but prefers to use a 2 space indent.

# How do I get involved in reviewing and merging patches?

This github organization will be managed through dicussion on the
[Incremental Elm #elm-janitor](https://discord.com/channels/534524278847045633/933054571981471755)
channel. Anyone on that channel can ask to join the org as a patch maintainer.

This [guide to reviewing and merging patches for maintainers](git-help.md)
should be followed.


# Appendix - Bug Fix Impact Levels

### 1. Doc Fixes

Changes to the docs only, no code changes.

### 2. Performance Improvements

Changes that only affect runtime performance. Ideally a benchmark would also be
provided to back up the claim.

### 3. Runtime Bug Fixes

Changes that eliminate one or more runtime exceptions.

### 4. API Changes to Implementation

Changes to the implementation that fix some bug other than a runtime exception.
Sometimes it can be debatable if something if a bug or a feature. This can be
discussed on the #elm-janitor channel.

### 5. API New Functions

Changes that add new functions to elm/ core APIs, but do not change any existing
APIs.

### 6. API Changes

Changes to elm/ core APIs that would require a bump to the major version.

### 7. Language Semantics

Changes to the Elm language itself.
