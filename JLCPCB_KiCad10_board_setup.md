# JLCPCB settings for KiCad 10 Board Setup

What eventually seemed best rather than gathering the data and trying to guess what is what and what makes sense myself :

[Cimos kicad-druid repo](https://github.com/Cimos/kicad-druid/tree/main)

# Previously

## 1. Design Rules > Constraints (mm)

| Field | Set to | JLCPCB limit |
|---|---|---|---|
| Minimum clearance |  0.1 | 0.10 |
| Minimum track width | 0.1 | 0.10 |
| Minimum connection width | 0.1 | Not listed; matches track minimum |
| Minimum annular width | 0.05 | Via diameter = hole + 0.1 (+0.15 preferred) |
| Minimum via diameter | 0.4 | 0.25, but small vias can cost more |
| Copper to hole clearance | 0.2 | Via or NPTH hole to track: 0.2 |
| Copper to edge clearance | 0.4 | 0.2 routed, 0.4 V-cut |
| Minimum drill size | 0.3 | 0.15 costs more; 0.2 preferred |
| Hole to hole clearance |0.2 | Via to via: 0.2 |
| Minimum text height | 1.0 | 1.0 |
| Minimum text thickness | 0.15 | 0.15 |

**Minimum item clearance** at 0: it only covers silk-to-silk, and JLCPCB's 0.15 pad-to-silk limit is handled by a custom rule.
The uVia and creepage groove fields can also stay as they are.

### Via cost

JLCPCB charges more for these via sizes:

- 0.1 or 0.15 mm holes, at any via diameter
- 0.2 or 0.25 mm holes with a via diameter under 0.45 mm

Sizes such as 0.6/0.3, 0.45/0.2 and 0.4/0.3 (diameter/hole) avoid the surcharge.

## 2. Other Board Setup pages

- **Solder Mask/Paste:**
  - Solder mask expansion: 0
  - Solder mask minimum web width: 0.1 (0.13 for black or white mask)
  - Solder mask to copper clearance: 0.09
  - Paste clearance: 0
  - Tent vias: leave on
- **Text & Graphics > Defaults:** silkscreen line width to 0.15 and text to 1 × 1 mm with 0.15 thickness.
- **Violation Severity:** "Drilled hole too close to other hole" to Error
- **Net Classes:** Default class (0.2 clearance, 0.2 track, 0.6/0.3 via) complies.
- **Pre-defined Sizes (not a JLCPCB requirement; currently empty):** tracks 0.2, 0.3 and 0.5; vias 0.6/0.3 and 0.45/0.2.
- **Physical Stackup and Board Finish:** 1.6 mm and 1 oz (0.035 mm) copper

## 3. Design Rules > Custom Rules

limits the Constraints page can't express:

```lisp
(version 1)

# JLCPCB rigid FR-4, 2-layer, 1 oz outer copper
# Source: jlcpcb.com/capabilities/pcb-capabilities (read 2026-11-06)
# Limits the Board Setup > Constraints page cannot express on its own.

(rule "JLC PTH annular ring (min 0.18, recommended 0.25)"
	(constraint annular_width (min 0.18mm))
	(condition "A.Type == 'Pad' && A.Pad_Type == 'Through-hole'"))

(rule "JLC pad hole to hole"
	(constraint hole_to_hole (min 0.45mm))
	(condition "A.Type == 'Pad' || B.Type == 'Pad'"))

(rule "JLC pad to pad, different nets"
	(constraint clearance (min 0.15mm))
	(condition "A.Type == 'Pad' && B.Type == 'Pad' && A.Net != B.Net"))

(rule "JLC NPTH minimum hole"
	(constraint hole_size (min 0.5mm))
	(condition "A.Pad_Type == 'NPTH, mechanical'"))

(rule "JLC plated slot minimum width"
	(constraint hole_size (min 0.5mm))
	(condition "A.Pad_Type == 'Through-hole' && A.Hole_Size_X != A.Hole_Size_Y"))

(rule "JLC pad to silkscreen"
	(severity warning)
	(constraint silk_clearance (min 0.15mm))
	(condition "A.Type == 'Pad' || B.Type == 'Pad'"))

(rule "JLC silkscreen minimum line width"
	(severity warning)
	(constraint assertion "A.Line_Width >= 0.15mm")
	(condition "A.Type == 'Graphic' && (A.Layer == 'F.SilkS' || A.Layer == 'B.SilkS')"))

(rule "JLC via surcharge: hole under 0.3 needs diameter 0.45 or more"
	(severity warning)
	(constraint via_diameter (min 0.45mm))
	(condition "A.Type == 'Via' && A.Hole < 0.3mm"))
```

- **Pad spacing:** these rules override the net class between pads, so pads may sit 0.15 apart even though Default says 0.2.
- **PTH to track:** JLCPCB's 0.28 limit needs no rule, because a 0.18 ring plus 0.1 clearance already guarantees it on 2 layers.


## Before order

- **PTH annular ring:** the page says both "≥0.20" and "absolute minimum 0.18" for 2-layer 1 oz. The rule uses 0.18, but aim for the recommended 0.25, which the connector pads already have.
- **Conflicting numbers:** third-party guides quote other figures, such as a 5 mil minimum track or a 0.3 mm minimum via. These settings use JLCPCB's own page.
- **If order 2 oz copper:** 0.16 track and spacing, a 0.254 PTH ring and a 0.2 mask web.
- **Not checked by these rules:** non-plated slots (minimum 1.0 mm) and SMD pad size (minimum 0.25 × 0.25 mm).

## Sources

- [JLCPCB rigid PCB capabilities](https://jlcpcb.com/capabilities/pcb-capabilities)
- [KiCad 10.0 PCB Editor manual](https://docs.kicad.org/10.0/en/pcbnew/pcbnew.html)
- [labtroll/KiCad-DesignRules](https://github.com/labtroll/KiCad-DesignRules)
