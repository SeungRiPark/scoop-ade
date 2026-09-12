# scoop-ade — the Scoop bucket for ADE

[ADE](https://github.com/SeungRiPark/AdeTool) runs many AI coding agents side by
side from one static Go binary: each agent gets its own git worktree, and ADE
owns the terminals, the diffs, the approvals and the hand-offs — through a
native desktop app (pure Go + [Gio](https://gioui.org), no WebView), a CLI and
an MCP endpoint.

## Install

```powershell
scoop bucket add ade https://github.com/SeungRiPark/scoop-ade
scoop install ade
```

That gives you both binaries on `PATH` and an **ADE** entry in the Start menu:

| Binary | Subsystem | Use |
|---|---|---|
| `ade-app.exe` | GUI (no console) | The desktop app. The Start menu entry runs this one. |
| `ade` | console | The CLI and daemon (`ade doctor`, `ade worktree …`, `ade daemon …`). |

Installing also runs `ade app register` for you (per user, `HKCU` only, no
elevation): Explorer's **Open in ADE** context menu and `ade://open?path=…`
links. Requires **Windows 10 1809 (build 17763)** or newer, the same floor as
ConPTY.

The binaries are **not code-signed**, so SmartScreen may ask once on first run:
*More info → Run anyway*. Scoop verifies the sha256 of the archive it downloads
against the hash in the manifest either way.

## Update

```powershell
scoop update             # refresh this bucket
scoop update ade         # install the newest manifest
```

## Uninstall

```powershell
ade app unregister       # first: removes the Explorer / ade:// keys
scoop uninstall ade
```

`ade app unregister` is a separate step because Scoop manifests written by
GoReleaser carry no uninstall hook; skipping it leaves three harmless but stale
`HKCU\Software\Classes` keys behind.

## How this bucket is maintained

`bucket/ade.json` is **generated**. Every ADE release runs
[GoReleaser](https://goreleaser.com), which rewrites the manifest (version, URLs
and sha256 hashes for `amd64` and `arm64`, the shortcut and the post-install
hook) and pushes it here. **Do not edit it by hand** — the next release
overwrites whatever you change. Prereleases (`v0.1.0-rc.1` and friends) are
skipped on purpose, so this bucket only ever points at final releases.

Issues and pull requests about ADE itself belong in
[SeungRiPark/AdeTool](https://github.com/SeungRiPark/AdeTool).

## License

MIT — see [LICENSE](LICENSE). Same license as ADE.
