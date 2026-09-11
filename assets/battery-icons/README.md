# Battery icons

21 PNG battery-status icons (18×18, RGBA), extracted from the embedded
`data:image/png;base64,...` URIs in `Battery_Icons_offline.html` (a
self-contained bundled page whose original page template carried a
`<script type="application/json" id="icon-uris">` block mapping short
IDs to inline data URIs).

`source-icon-uris.json` is that original ID → data-URI mapping, kept
verbatim for provenance/traceability. The PNGs in this folder are the
same bytes, decoded to files and given descriptive names per the
source page's `SERIES` definition:

| Series (`SERIES.key`) | Display name  | Color     | Source IDs                          | Files |
|---|---|---|---|---|
| `empty` | SHARED EMPTY | `#4b5158` | `empty-0` | `shared-empty.png` |
| `off`   | OFF          | `#FF7A2E` | `off-1`…`off-5` | `off-1.png` … `off-5.png` |
| `dfs`   | DEFF SLOW    | `#4C92FF` | `dfs-1`…`dfs-5` | `deff-slow-1.png` … `deff-slow-5.png` |
| `dff`   | DEFF FAST    | `#3BF29A` | `dff-1`…`dff-5` | `deff-fast-1.png` … `deff-fast-5.png` |
| `fort`  | FORT         | `#B77CFF` | `fort-1`…`fort-5` | `fort-1.png` … `fort-5.png` |

Each series' 5 files are levels 1 (lowest charge) through 5 (full),
sharing the single empty-state icon.

## Metadata stripping

The source data URIs carried two nonstandard ancillary PNG chunks —
`caBX` (a 5758-byte C2PA content-credentials manifest) and `deBG` —
wrapped around ~394 bytes of actual image data. Spec-compliant decoders
skip unknown ancillary chunks, but stricter/embedded ones may reject the
file outright, so these chunks are removed here: only `IHDR`, `IDAT` and
`IEND` remain. Decoded pixel arrays were compared before and after and
are identical for all 21 files; the set went from 130,363 to 8,605 bytes.

`source-icon-uris.json` still holds the untouched originals if the
C2PA provenance manifest is ever needed.
