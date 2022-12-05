# docker-protobuf-renovate-repro
Renovate minimal reproduction to try to understand how to update git hashes with regex manager

# Description

I am trying to update Line 4 of `deps.list`. The `currentValue` is in
the format of a git commit hash, but not part of any particular package
management system, so I am using the `regex` manager to update versions.
Most versions of this file are in semver and work fine, but
https://github.com/googleapis/googleapis does not use branches, tags or
releases when they release updates. The `HEAD` of `master` branch is
always the latest version.

Full repo: https://github.com/strophy/docker-protobuf
Minimal reproduction repo: https://github.com/strophy/docker-protobuf-renovate-repro

Possible related issues:
- https://github.com/renovatebot/renovate/issues/5640
- https://github.com/renovatebot/renovate/discussions/15005
- https://github.com/mui/mui-x/pull/3500

Possible solutions:
- https://github.com/visualon/renovate-config/blob/bf8c1b72e7580fdec98373058a82cab157d0ddce/shared.json#L133-L144

# Current behaviour

I am unable to get Renovate to recognise that a change/update is needed.
I have tried `git`, `loose` and `docker` versioning, as well as not
specifying any versioning. I'm not sure if `docker` is the right
approach here, but since only `docker` seems to handle digests, maybe
this is the best way of doing it?

# Expected behaviour

I would like Renovate to check the default branch of the repo, get the
latest commit hash, and update it in the file.
