### Fixed

#### `.standards` was pinned 11 weeks behind — including the Go 1.26 rule this repo just cited

`CLAUDE.md` names `.standards/instructions/` authoritative and points
contributors and agents at it. A git submodule is a **pinned commit, not a live
link**, and this one had not moved since 2026-06-12.

The clearest proof it was misleading people is in this repo's own history. The
previous commit on `main`, `chore(go): raise minimum to Go 1.26`, justified
itself with "Org standards set Go 1.26 as the mandatory minimum and the default
(`.standards/instructions/go.md`)." That rule is real upstream — but it is
**not in the copy this repo had checked out**. At pin `664ae68`,
`instructions/go.md` is 55 lines and does not mention a Go version anywhere.
The change was correct; the citation pointed at a file that could not support
it.

The pin now moves to `7bdfd13` (2026-08-30), nine commits ahead. `go.md` goes
from 55 lines to 384 and from unversioned to 1.3.0, carrying:

- the Go version policy — 1.26 mandatory minimum, prefer 1.27 where every
  dependency allows it, plus the `toolchain`-below-`go` inversion trap
- the `io/ioutil` ban and the rest of the deprecated-stdlib table
- the `wg.Go(fn)` rule — never `Add(1)` + `defer Done()`
- the testing-isolation table (`t.Setenv`, `t.Chdir`, `t.TempDir`,
  `testing/synctest` instead of `time.Sleep`)
- `omitempty` vs `omitzero` under `encoding/json/v2`

`file-headers.md`, `commit-messages.md` and `typescript.md` also become
versioned, so drift is visible next time instead of silent, and
`templates/executive-summary.md` is new.

So this bumps the pin *and* removes the need to remember it: a `gitsubmodule`
entry in `.github/dependabot.yml` puts `.standards` on the same weekly
multi-ecosystem schedule as the Go, Docker and Actions dependencies. Falling
behind now opens a PR instead of going quietly unnoticed.

Nothing in CI or any script reads `.standards`. Workflows check out submodules
recursively, but no step consumes the contents — it is documentation read by
humans and agents — so the bump carries no build risk. Verified by grepping
every workflow, Makefile and script before making the change.
