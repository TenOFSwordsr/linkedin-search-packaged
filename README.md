# LinkedIn Dataset Search - Packaged Executable

A self-contained build output of the `linkedin-search` project: a compiled Windows executable, its
launcher, a seed dataset, a SQLite database, and UI screenshots. There is no source here - this
folder exists to run and show off the packaged app, not to develop it. Build the real thing from
the `linkedin-search` repository, which owns the Go source and already documents itself.

**Suggested repo name:** `linkedin-search-bin`
**Stack:** Prebuilt Go binary (`linkedin-search.exe`, from a gin + modernc.org/sqlite app); SQLite data
**Status:** build output
**Last modified:** 2026-09-02

## What it does

Runs the LinkedIn-profile search web app that was compiled elsewhere:

- `linkedin-search.exe` - the packaged server. Byte-identical (same MD5) to the `linkedin-search.exe`
  committed in the source project, confirming it is that build copied here for testing.
- `Start.bat` - double-click launcher. `cd`s to its own folder, prints the URL and stop
  instructions, runs the exe, and on exit prints likely failure causes (port 8080 already in use, or
  antivirus blocking the exe).
- Serves a local web UI at `http://localhost:8080` for searching/importing LinkedIn profile records.
- `data/profiles.json` and `linkedin.db` - the sample dataset and the SQLite database the app reads
  and seeds from (the source project embeds `data/profiles.json` at build time via `internal/assets`).
- `ui-*.png` - screenshots of the running UI (dialog, results, final states), kept as visual evidence.

## Layout

```
linkedin-search.exe   packaged Go server (identical to the source project's build)
Start.bat             double-click launcher for the web UI
linkedin.db           SQLite database used by the running app
data/profiles.json    seed dataset the app imports
ui-*.png              UI screenshots (dialog/results/final)
```

## Running it

```
Double-click Start.bat        # or run linkedin-search.exe from this folder
```

Then open `http://localhost:8080`. Free port 8080 if another copy is already running.

## Notes

- **This is not the project - `../linkedin-search` is.** The source, README, build script and
  re-embed step live there (`build.bat` syncs `data/profiles.json` and `web/static/` into
  `internal/assets` and runs `go build`). Make that repository the canonical GitHub project; do not
  publish this folder as if it were source.
- The two `linkedin.db` files (here vs in `linkedin-search/`) differ in content but the executables
  are identical, so this folder is just a run/test snapshot with its own working database copy.
- Committing a 13 MB `.exe` and a populated `.db` is build/data output, not something to track in the
  source repo - add both to the source project's `.gitignore` (its README notes this) and treat this
  directory as disposable.
