# `wired` add-on shield — PARKED (not currently built)

This shield adds ZMK's **full-duplex wired UART** split transport on top of the
`lily58_left` / `lily58_right` shields. It is **not built or published right now** —
the matrix entries in `../../../lily58.yaml` are commented out.

## Why it's parked

ZMK's wired split currently supports **full-duplex only**, which needs **two
data wires** between the halves. The keebd Lily58 routes a **single shared data
conductor** over the TRRS, and ZMK's **half-duplex (single-wire)** support is
**not implemented yet** (see https://zmk.dev/docs/features/split-keyboards —
"Full Duplex vs Half Duplex"). So wired split cannot function on the current
hardware. These boards use the **Bluetooth (wireless)** transport.

Additional hardware conflict on the current revision: the nice!view display
**CS is on pro_micro D1**, which is also the default UART **TX** pin — so even
full-duplex would clobber the display. A hardware revision that lands wired on
the default UART pins (D0=RX, D1=TX) must also move the nice!view CS off D1.

## Re-enabling later

When ZMK ships half-duplex single-wire support (or a board revision adds a
second TRRS data wire and relocates the display CS):
1. Uncomment the wired entries in `lily58.yaml`.
2. Set the UART pins in `wired.overlay` to the TRRS data pin(s) for the revision.
3. Re-add the download links in the keebd-docs firmware page.
