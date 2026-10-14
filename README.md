# PeakPeek terrain data

Offline elevation tiles downloaded by the PeakPeek iOS app, which labels the
mountains in its camera view. The tiles live on this repository's
[releases](../../releases); there is no code here.

## What is in a release

Each release is one region at one data version, for example `colorado-v1`:

- `manifest.json` lists every tile with its bounds, byte sizes and SHA-256.
- `<tile>.ppdem.deflate` is one 1°×1° tile of 1 arc-second (about 30 m)
  terrain, raw-DEFLATE compressed. Tiles are named for their north-west corner
  in the USGS style (`n40w106` spans 39–40° N, 106–105° W) and carry a
  one-cell margin of their neighbours' data so they join seamlessly.

Unpacked, a tile is a PPDEM grid: a 48-byte little-endian header (magic
`PPDEM1\0\0`, south, west and cell size as doubles, row and column counts as
UInt32, an Int16 no-data value, 6 reserved bytes), then Int16 elevations in
metres, row-major, southernmost row first.

## Source and licence

Elevations come from the U.S. Geological Survey's 3D Elevation Program
(3DEP) 1 arc-second DEM, a public-domain U.S. Government work. The tiles are
cut and re-packed from it without other changes. They are likewise offered
without restriction.
