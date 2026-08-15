# Changelog

## 0.2.0

Mobile support.

- Added the viewport meta tag. Without it phones rendered the page at desktop
  width and zoomed out.
- Replaced HTML5 drag-and-drop with pointer events, which fire for mouse and
  touch alike. HTML5 drag events never fire on a touchscreen, so on a phone
  nothing could be dragged at all.
- Added an Armed bar: tap a module to arm it, tap a unit to place it. Movement
  under 8px counts as a tap, so dragging and tapping coexist. In Stage 3 this
  lets you arm a module, scroll sideways to the right column, then place it.
- Unit numbers are pinned to the left edge while the chart scrolls horizontally.
- Responsive layout under 860px: bin becomes a wrapping chip row above the rack,
  stage rail goes two-up, tap targets raised to 44px, hint buttons enlarged.

## 0.1.1

Fixed: in Stage 3, labels valid in more than one column (Transport, Application,
Network) were built as separate column-bound tiles that looked identical in the
bin. Dropping the OSI "Transport" tile into the TCP/IP column scored a fault
even though Transport is correct at 4U in both models.

Shared labels now merge into a single tile carrying one slot per column, and a
drop is judged by its destination column rather than by which tile was grabbed.
The tile shows how many columns still need it, and the span it fills is decided
by where it lands: Application fills 7/6/5 in TCP/IP but only 7 in OSI.

Genuine errors are still rejected. Network at TCP/IP 3U is wrong (Internet lives
there) and Internet at OSI 3U is wrong (OSI calls it Network).

## 0.1.0

Initial release.

- Four gated stages: Stack Builder, Attribute Sort, Full Chart, Bins & Triage
- Snap-back on wrong drops with a per-drop explanation
- Tiered hints: mnemonic word, first letter, answer reveal
- Blanking plates for the chart's N/A cells
- Spanning modules (TCP/IP Application over 7/6/5, Network Access over 2/1, NIC over 2/1)
- 38 protocol cards and 18 fault-triage tickets
- Per-layer accuracy tracked across sessions
- Progress persisted via window.storage with a localStorage fallback
