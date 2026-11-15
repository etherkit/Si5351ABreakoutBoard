# Enclosure

Two-piece, snap-together case for the Si5351A Breakout Board (30 × 50 × 1.6 mm).
Parametric design in SolidCraft, printed in white PETG on an Elegoo Centauri Carbon 2.

![Si5351A board in case, lid ghosted](board_in_case_iso_v8.png)

## Files

| File | What |
|------|------|
| `si5351_case_v8.sc` | Parametric design (SolidCraft). Every dimension is a named parameter — open in SolidCraft, edit, re-export. |
| `base_v8.stl` | Base: pocket, shelf, walls, three SMA bays, lid groove. Print as-is. |
| `lid_v8_print.stl` | Lid: plate, four-side snap skirt, SMA notches, pin-header windows. Print as-is (plate face down). |
| `board_in_case_iso_v8.png` | Isometric render of the board in the case (lid at 22 % opacity). |

## Design

The board sits on a 2.8 mm shelf ledge with 0.4 mm clearance per side; 4.4 mm of
air to the base top, 8.0 mm with the lid on.

- **SMA pass-throughs** — three edge-launch SMAs on the +X wall at
  Y = 12.10 / −0.05 / −12.00 (board-centre origin). Each bay is a single opening
  from a 1.0 mm bay floor up past the wall top: 8.8 mm wide (7.2 mm flange +
  0.8 mm solder margin per side), flange bottom (1.73 mm) clears the bay floor,
  and the lid plate clears the barrel top (6.35 mm).
- **Lid** — snaps on over a 2.0 mm skirt: 0.6 mm ribs riding in 0.5 mm grooves
  (0.2 mm clearance) on all four walls; on the SMA wall the rib splits into four
  ridges passing between the three notches (≈171 of 184 mm engaged). The plate
  carries ⌀2.5 bosses over the four mounting holes at (−11, 21) (7, 21)
  (−11, −21) (7, −21), clamping the board when closed.
- **Headspace** — pin headers pass through lid windows, 4.4 mm above the board.

| Part | Size (mm) |
|------|-----------|
| Base | 35.60 × 55.60 × 8.40 |
| Lid | 38.80 × 58.80 × 6.90 (5.30 mm engaged) |

### Revision history

| Rev | Change |
|-----|--------|
| v2 | First working case (base + lid). Lid snapped on three sides; the SMA edge wall was un-ribbed. |
| v3–v6 | Lid snap-fit iterations (rib depth / groove width). |
| v7 | Lid: fourth snap wall — the SMA edge is now ribbed as four ridges between the notches. All SMA bays widened 7.2 → 8.8 mm (`SMA_MARGIN` = 0.8 mm/side) to absorb hand-soldering misalignment. Base + lid. |
| v8 | Base only: SMA bays and shelf reliefs deepened from the 1.6 mm pocket floor to the 1.0 mm bay floor. A 2.6–2.7 mm ledge under each flange was wedging the board up ≈1.3 mm and stopping the lid from seating; the bays now open floor-to-top and the board sits flat. Lid unchanged (v8 ≡ v7). |

## Printing

Elegoo Slicer · white Rapid PETG (tray 0) · 0.2 mm layers · 3 walls · 15 %
infill · no brim · 250 °C / 70 °C bed (textured PEI) · no supports.

| Part | Layers | Filament | Est. time |
|------|--------|----------|-----------|
| Base v8 | 42 | 7.32 g | 22 min 21 s |
| Lid v8 (plate down) | 35 | ≈5.7 g | ≈25 min |

Both STLs verified watertight before slicing. Post-print check: first layer
flat, no warp or delamination.

## Tools

- **Board geometry** — parsed directly from `pcb/Si5351ABreakout.kicad_pcb`
  (KiCad 10): outline, SMA row centres, mounting-hole positions. No eyeballing.
- **CAD** — [SolidCraft](https://solidcraft.io) 0.42: parametric `.sc` design
  (parameters: `BL`/`BW`, `CLR`, `SMAW`, `SMA_MARGIN`, `SY1..3`, `HX1/2`,
  `HY1/2`, `BOSS_D`, …), board import via `doc.open`, isometric render.
- **Verification** — watertight-mesh checks on every export, point-in-solid
  raycasts through each bay, and per-feature diffs of the `.sc` between
  revisions so only changed parts get reprinted.
- **Printing** — Elegoo Centauri Carbon 2; preflight (machine status, tray
  check, bed photo) and progress monitoring via pycentauri.

To adapt for a board revision: change `BL`/`BW`/`SY*`/`HX*`/`HY*` in the `.sc`
and re-export both parts.
