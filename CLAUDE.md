# CLAUDE.md

Guidance for Claude Code working **on** the rerddap package source (drop
this at the repo root of `ropensci/rerddap`; it currently lives beside
`SKILL.md` because no local checkout exists in this environment).
rerddap is the rOpenSci R client for ERDDAP(TM) servers —
[`info()`](https://docs.ropensci.org/rerddap/reference/info.md),
[`griddap()`](https://docs.ropensci.org/rerddap/reference/griddap.md),
[`tabledap()`](https://docs.ropensci.org/rerddap/reference/tabledap.md),
search, caching, conversions. R \>= 4.0.

## Skill vs. this file

`SKILL.md` in this same directory is LLM-targeted guidance for *writing
user code that calls rerddap*. When helping a user *use* rerddap, defer
to the skill. **This file is for working on the package source itself.**

## Commands

``` r

devtools::document()     # roxygen2 -> man/, NAMESPACE
devtools::load_all()     # load for interactive testing
devtools::run_examples(run = TRUE)   # exercise @examples (see Testing note below)
```

``` bash
R CMD build .
_R_CHECK_CRAN_INCOMING_=FALSE R CMD check --as-cran --no-manual rerddap_*.tar.gz
```

`Makefile` targets wrap these (`make doc`, `make build`, `make check`,
`make test`, `make readme`). CI (`.github/workflows/R-CMD-check.yaml`,
`R-check.yml`, `rhub.yaml`, `test-coverage.yaml`) runs `R CMD check`
across platforms plus `test-coverage.yaml` — despite that workflow’s
name, there is **no `tests/testthat` directory in this repo**.
Coverage/testing currently comes entirely from roxygen `@examples`, most
of which are wrapped in `\dontrun{}` or gated by a
[`try()`](https://rdrr.io/r/base/try.html)/server-availability check so
`R CMD check` doesn’t fail when a live ERDDAP server is unreachable.
Treat `devtools::test()` as a no-op until a real suite exists.

## Codebase Shape (`R/`)

- `grid.R` / `table.R` —
  [`griddap()`](https://docs.ropensci.org/rerddap/reference/griddap.md)
  /
  [`tabledap()`](https://docs.ropensci.org/rerddap/reference/tabledap.md),
  by far the largest and densest files; each also carries the private
  helpers that build/parse the request URL (`parse_args`, `check_dims`,
  `fix_dims`, `field_handler`) and do the actual HTTP fetch + disk cache
  lookup (`erd_up_GET` / `erd_tab_GET`, `gen_key`).
- `info.R` —
  [`info()`](https://docs.ropensci.org/rerddap/reference/info.md), the
  required first call for any
  [`griddap()`](https://docs.ropensci.org/rerddap/reference/griddap.md)/[`tabledap()`](https://docs.ropensci.org/rerddap/reference/tabledap.md)
  request; also `table_or_grid()`, which auto-detects a dataset’s
  protocol type by checking whether its ID is in the server’s tabledap
  index.
- `search.R` / `search_adv.R` / `global_search.R` —
  [`ed_search()`](https://docs.ropensci.org/rerddap/reference/ed_search.md),
  [`ed_search_adv()`](https://docs.ropensci.org/rerddap/reference/ed_search_adv.md),
  [`global_search()`](https://docs.ropensci.org/rerddap/reference/global_search.md)
  (search across a list of servers).
- `estimate_griddap_size.R` — metadata-only request-size estimator; see
  “Duplicated in rerddapUtils” below.
- `cache_setup.R` / `cache_list.R` / `cache_details.R` /
  `cache_delete.R` / `cache_paths.R` — disk cache built on `hoardr`;
  `.onLoad` (in `on_load.R`) creates the package-level `rrcache` object
  (default: a tempdir).
- `default-url.R` —
  [`eurl()`](https://docs.ropensci.org/rerddap/reference/eurl.md), the
  default-server resolver (`RERDDAP_DEFAULT_URL` env var override).
- `convert_time.R` / `convert_units.R` / `fipscounty.R` / `keywords.R` —
  thin wrappers around ERDDAP’s `/convert/*` web services.
- `colors.R` — bundled `cmocean` palette data (`colors` object), used by
  downstream packages (plotdap) more than by rerddap itself.
- `utils.R` — `dimvars()`, `getvar()`, `getvars()`, etc. **This exact
  helper set is independently re-implemented (copy, not shared) in
  rerddapXtracto’s and rerddapUtils’s own `utils.R`.** A bug fix here
  doesn’t propagate — check the sibling packages’ repos too.
- `version.R` —
  [`version()`](https://docs.ropensci.org/rerddap/reference/version.md),
  queries `/erddap/version`; gates `fmt = "parquet"` support (requires
  ERDDAP \>= 2.25) in `grid.R`/`table.R`.

## Known Landmine: `quit()` in Network Error Handlers

Several functions wrap their `crul` GET call in
[`tryCatch()`](https://rdrr.io/r/base/conditions.html) and call
**`quit(save = "no", status = 1)`** in the `error` handler instead of
[`stop()`](https://rdrr.io/r/base/stop.html)/returning an error object —
currently in `grid.R` (x2), `table.R` (x2), `fipscounty.R`,
`keywords.R`, `convert_time.R`, `convert_units.R`, and `servers.R`. This
means a transient network failure or unreachable server **terminates the
caller’s entire R session**, not just the function call — a serious
landmine for interactive use, Shiny apps, or any long-running script. If
you touch any of these functions, strongly consider replacing
[`quit()`](https://rdrr.io/r/base/quit.html) with a normal
[`stop()`](https://rdrr.io/r/base/stop.html)/condition and flagging it
for a fix; don’t copy the pattern into new code.

## Duplicated in rerddapUtils

[`estimate_griddap_size()`](https://docs.ropensci.org/rerddap/reference/estimate_griddap_size.md)
is near-byte-identical between this package and `rerddapUtils` — the two
definitions have already drifted from a shared original. If you fix a
bug or add a feature here, check `rerddapUtils::estimate_griddap_size()`
for the same issue.

## Packaging Notes

- `Roxygen: list(markdown = TRUE)` — docs use markdown roxygen syntax.
- No formatter/linter config (no `air.toml`, no `.lintr`) — match
  surrounding style by hand.
- `codemeta.json` is present and should be regenerated
  (`codemetar::write_codemeta()`) after DESCRIPTION changes, per
  rOpenSci convention.
- This is an rOpenSci-reviewed package — non-trivial API changes should
  consider backward compatibility and CRAN policy (see
  `cran-comments.md` for the current submission’s notes).
