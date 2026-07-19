### Added

#### Adopt changelog fragments (`changelog.d/`) and a CHANGELOG.md

Introduce a `CHANGELOG.md` assembled from per-change Markdown fragments under
`changelog.d/` by `scriv`, rather than hand-editing. Contributors add a fragment
with `scriv create`; a CI check requires one on each PR, and the fragments are
folded into `CHANGELOG.md` when a release is published. This removes changelog
merge conflicts across parallel PRs.
