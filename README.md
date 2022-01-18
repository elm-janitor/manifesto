# Elm Core Library Maintenance

`elm-janitor` is a group of Elm users that are interested in maintaining the
Elm core packages by applying patches to them. The patch stack will always
be applied on top of the latest official release of the Elm core packages,
with patches removed from the stack if they become part of the official release.

# Git Branch Structure

Using `elm-core` as an example, the following branch structure is used in
the various core patching projects.

The `master` branch of the project is not used.

| Branch | Description |
| --- | --- |
| `stack-1.0.5` | The working branch used to assemble a patch set on top of latest elm/core. |
| `upstream-master` | Tracks upstream elm/core master. |
| `upstream-1.0.5` | Tracks an upstream release tag, in this case 1.0.5 |
| `pr-1033` | Tracks an upstream pull request, in this case \#1033. |

Patches are prepared and maintained with one patch per branch.

? Should a PR also reference its base version in its name. 
