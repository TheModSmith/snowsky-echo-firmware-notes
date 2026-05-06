# Snowsky/FiiO Echo Firmware Notes

Research notes for the **full-size Snowsky/FiiO Echo** firmware.

This is for the **Echo non-mini**, currently focused on firmware:

```text
Firmware version: 1.3.0
Firmware image: ECHOV130.IMG
```

## Status

This repo is currently documentation only.

It is not a firmware editor, flashing guide, or finished modding tool.

## Current findings

The Echo 1.3.0 firmware contains a UI image resource block named:

```text
ROCK26IMAGERES
```

So far:

```text
Resource block offset: 0x009a8648
Image/resource count: 817
Image format: raw bgr565_be
```

The images are not stored as normal PNG, JPEG, or BMP files. They are raw 16-bit image resources.

## Image format

The extracted UI images use:

```text
BGR565, big-endian
```

Each pixel is 2 bytes:

```text
bits 15..11 = blue
bits 10..5  = green
bits 4..0   = red
```

All 817 extracted PNG previews have been validated to round-trip back to the original firmware bytes.

## What the images include

The image resources appear to include:

- playback backgrounds
- cassette-style UI skins
- turntable-style UI skins
- boot/logo screens
- power-off/shutdown animation frames
- menu/settings panels
- icons and small UI elements
- test/color-bar images

## Important note

Echo Mini firmware research may be useful as reference material, but the full-size Echo should be treated as a separate device.

We should not reuse Echo Mini offsets, tools, or make assumptions without verifying them against the full-size Echo firmware.

## Safety

This research is read-only unless clearly stated otherwise.

Do not flash modified firmware unless the firmware structure, checksums/signatures, update process, and recovery method are understood.
