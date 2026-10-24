# Documentation and hardware evidence

This file covers `docs/`: user documentation and the hardware evidence that
driver changes depend on.

## Evidence per wheel

New wheels get their own directory `docs/wheels/<model>/`, for example
`docs/wheels/t500rs/`, with:

+ `README.md`: USB IDs, `bcdDevice`, firmware versions seen, values returned by
  the attachment query, how the wheel is told apart from other wheels with the
  same ID, and which effects are supported and tested.
+ `rdesc.md`: report descriptor dumps, with source (Linux or Windows, kernel or
  driver version, firmware) and length.
+ `effects.md`: the packet format of each effect, format first, then dissected
  example packets, in the style of `docs/FFBEFFECTS.md`.

The existing `docs/FFBEFFECTS.md` for the T300RS stays where it is.

## Rules

+ Preserve raw data exactly: descriptor dumps and packet bytes are copied, not
  retyped or reconstructed.
+ Record how the data was obtained: tool (`usbmon`/Wireshark, `fedit`,
  `ffbsdl`, `ffbwrap`), which parameter was changed, wheel, firmware, kernel or
  Windows driver version.
+ Separate measured facts from assumptions. Name unknown fields as unknown.
+ Don't generalize from one wheel or firmware to all Thrustmaster wheels
  without evidence from more devices.
+ Raw capture files don't go into the repository, only annotated excerpts.
+ Remove personal data (serial numbers, user names, paths) from dumps.
+ ASCII only, consistent example format throughout a document.

## Verification

+ Re-check every stated ID, length, firmware version and packet byte against
  the source material.
+ Check that the driver code and the documentation agree (constants, field
  names, packet order).
