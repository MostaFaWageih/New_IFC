# Image locations on the IFC model (AI estimate)

Every location below is an **AI estimate** (visual reading of the photo + sun heading), not a survey. Edit `Analysis/locations.csv`, then re-run `python report.py` and `python compare.py` to regenerate this file.

## 1. Source IFC entities

- File: `New_REPO/2-1319-HAC-MOD-SSC-00-GL-BS-01_detached--STRUCTRE-MODEL_detached.ifc` - schema IFC4X3 in header, read as IFC4X3_ADD2, length unit 0.001 m (mm).
- `#28` IfcProjectedCRS: **EPSG:22992** (Egypt 1907 / Red Belt).
- `#29` IfcMapConversion: Eastings **1031135.2671632987**, Northings **1208737.2173774764**, OrthogonalHeight **168.22345511726195**, XAxisAbscissa 1.0, XAxisOrdinate 6.123031769111886e-17, Scale 1.0.
- `#87` IfcSite `1hpgWBKdT1ewmJZcftP8IU`: RefLatitude/RefLongitude [33.514927, 35.477237] - **not used**. IfcSite RefLatitude/RefLongitude and the model origin lie ~530 km from the building; the building location is computed from element geometry + IfcMapConversion.
- IfcGrid / IfcGridAxis (2280 entities, repeated per IfcGrid; merged into the unique labelled axes in out/grids.csv): polylines used for the grid references.
- Element positions: every column shares one ObjectPlacement, so element XY is taken from the triangulated geometry bounding box (ifcopenshell.geom, world coords), not from ObjectPlacement.

### Storeys (IfcBuildingStorey)

| Storey | Entity | GlobalId | Elevation (mm) | Placement Z (m) |
|---|---|---|---|---|
| HAC-SSL-FL1 | `#39` | `1e5lafjSHAghj4kuu0ZMl8` | -12250 | 150.5265 |
| HAC-SSL-FL2 | `#43` | `12f1l24kT8d9RBml7$P4Yu` | -11950 | 150.8265 |
| HAC-SSL-SG | `#47` | `3Plbe07H16wxCxq3w7K7Cr` | -9200 | 153.5765 |
| 01-F.P | `#51` | `2Q0$OZmMnF59jLfgg1N1l4` | -8800 | 153.9765 |
| HAC-SSL-U1SG | `#55` | `1E5LY37rnCnRmSlFD56Tx2` | -8750 | 154.0265 |
| HAC-SSL-U2SG | `#59` | `1IOALYxP5Fs9iT8iO9CiKF` | -6900 | 155.8765 |
| HAC-SSL-B1 | `#63` | `1Jdpcnsr96JO2WmiJEXcXn` | -4700 | 158.0765 |
| HAC-SSL-ST1 | `#67` | `1E5LY37rnCnRmSlFD56Tvj` | -3300 | 159.4765 |
| HAC-SSL-ST2 | `#71` | `1IOALYxP5Fs9iT8iO9CiNx` | -2300 | 160.4765 |
| HAC-SSL-GF | `#75` | `0pudd0TGPB4OiLkwVCfEhC` | -250 | 162.5265 |
| HAC-SSL-UGF | `#79` | `1E5LY37rnCnRmSlFD56TZe` | 1900 | 164.6765 |
| 01-F.O | `#83` | `20bAMCNeH0RQtIJo2MBUDL` | 2000 | 164.7765 |

## 2. Coordinate chain

- Site frame used in this analysis (m): `x = X_ifc/1000 - (-343771.0)`, `y = Y_ifc/1000 - (-402380.0)`, `z = Z_ifc/1000` (project Z, not AMSL).
- IFC project coordinates (file units, mm): `X_ifc = (x + ox) * 1000`, `Y_ifc = (y + oy) * 1000`, `Z_ifc = z * 1000`.
- Map: `E = Eastings + Scale*(XAxisAbscissa*X - XAxisOrdinate*Y)`, `N = Northings + Scale*(XAxisOrdinate*X + XAxisAbscissa*Y)`, X and Y in metres.
- WGS84 lat/lon: pyproj EPSG:22992 -> EPSG:4326.
- Camera eye Z = storey placement Z + 1.5 m (tripod) + offset_z_m from locations.csv.

## 3. Location of each image

| Pos | Photos | Storey | Grid ref | Site x, y, z (m) | IFC X, Y, Z (mm) | Easting, Northing | Lat, Lon | Heading |
|---|---|---|---|---|---|---|---|---|
| P01 | IMG_20261031_121515_00_004<br>IMG_20261031_121515_00_005<br>IMG_20261031_121515_00_006 | HAC-SSL-FL2 | AFX.A-11/B | 62.271, 82.974, 153.027 | -343708729, -402297026, 153027 | 687426.538, 806440.191 | 29.965911, 31.752042 | 359.58° (sun) |
| P02 | IMG_20261031_121630_00_007<br>IMG_20261031_121630_00_008<br>IMG_20261031_121630_00_009 | HAC-SSL-FL2 | B/AFX.A-11 | 64.271, 81.974, 153.027 | -343706729, -402298026, 153027 | 687428.538, 806439.191 | 29.965902, 31.752063 | 93.16° (sun) |
| P03 | IMG_20261031_122113_00_013 | HAC-SSL-FL2 | 16/C | 56.871, 52.374, 153.027 | -343714129, -402327626, 153027 | 687421.138, 806409.591 | 29.965636, 31.751984 | 311.64° (sun) |
| P04 | IMG_20261031_122144_00_014 | HAC-SSL-FL2 | 16/C | 58.871, 52.374, 153.027 | -343712129, -402327626, 153027 | 687423.138, 806409.591 | 29.965636, 31.752005 | 333.61° (sun) |
| P05 | IMG_20261031_122204_00_015 | HAC-SSL-FL2 | 17/C | 56.871, 43.974, 153.027 | -343714129, -402336026, 153027 | 687421.138, 806401.191 | 29.965560, 31.751984 | 15.56° (sun) |
| P06 | IMG_20261031_122324_00_016 | HAC-SSL-FL2 | 18/C | 56.871, 38.174, 153.027 | -343714129, -402341826, 153027 | 687421.138, 806395.391 | 29.965508, 31.751983 | 346.47° (sun) |
| P07 | IMG_20261031_122347_00_017 | HAC-SSL-FL2 | 18/C | 53.871, 38.174, 153.027 | -343717129, -402341826, 153027 | 687418.138, 806395.391 | 29.965508, 31.751952 | 309.33° (sun) |
| P08 | IMG_20261031_123214_00_024 | HAC-SSL-B1 | 20/B | 67.671, 21.374, 163.577 | -343703329, -402358626, 163577 | 687431.938, 806378.591 | 29.965355, 31.752094 | 9.03° (sun) |
| P09 | IMG_20261031_123234_00_025 | HAC-SSL-B1 | 20/B | 67.671, 23.374, 163.577 | -343703329, -402356626, 163577 | 687431.938, 806380.591 | 29.965373, 31.752094 | 279.49° (sun) |
| P10 | IMG_20261031_123305_00_026 | HAC-SSL-B1 | B/AFX.A-17 | 67.671, 25.374, 163.577 | -343703329, -402354626, 163577 | 687431.938, 806382.591 | 29.965391, 31.752094 | 341.88° (sun) |

## 4. Camera view set per image

Directions are unit vectors in IFC project axes (+X east, +Y north; TrueNorth = +Y; grid vs true north differ by ~0.37 deg, ignored). Target = eye + 10 m along the view direction. To rebuild the view in Revit / Navisworks: perspective camera at Eye looking at Target, up = +Z, FOV 90 deg per cube face.

### P01 - HAC-SSL-FL2, grid AFX.A-11/B - confidence low, verified no

- Taken: 2026-10-31 12:15:15+02:00; photos: IMG_20261031_121515_00_004, IMG_20261031_121515_00_005, IMG_20261031_121515_00_006
- Eye (IFC mm): `(-343708729, -402297026, 153027)`
- Target (IFC mm): `(-343708802, -402287027, 153027)`
- View direction (pano centre): `(-0.0073, 1.0000, 0.0000)`, true bearing 359.58 deg from sun
- Up vector: `(0.0000, 0.0000, 1.0000)`; pitch 0, roll 0
- Google Maps: https://maps.google.com/?q=29.96591,31.75204
- Nearest columns (plan distance from eye):

  - `055sdm20rEqP0eKf$zgR_F` RC_Rectangular Columns:C(800x800)mm:627098 (HAC-SSL-FL2) - 4.24 m
  - `26KqgdbaD3EQ2JpeUjZOr1` RC_Rectangular Columns:C(800x800)mm:1153294 (HAC-SSL-B1) - 4.24 m
  - `26KqgdbaD3EQ2JpeUjZOmM` RC_Rectangular Columns:C(1000x2100)mm:1153113 (HAC-SSL-B1) - 4.93 m

- Why here: Sun heading 360 deg: finished government buildings and the excavation sand bank are due E/NE, so the camera is near the east edge of the basement; on the raft rebar mat with column cages starting (lowest storey with column starters = FL2); tower-crane mast cased in a concrete column ~8 m SE; red column formwork ~6 m NW. Grid chosen on the east side of the orthogonal block; exact grid unconfirmed. Model 360 compared: the model has no raft slab immediately E of the camera, consistent with the raft edge and open ground E in the photo; the grid itself is not confirmed.

### P02 - HAC-SSL-FL2, grid B/AFX.A-11 - confidence low, verified no

- Taken: 2026-10-31 12:16:30+02:00; photos: IMG_20261031_121630_00_007, IMG_20261031_121630_00_008, IMG_20261031_121630_00_009
- Eye (IFC mm): `(-343706729, -402298026, 153027)`
- Target (IFC mm): `(-343696744, -402298578, 153027)`
- View direction (pano centre): `(0.9985, -0.0552, 0.0000)`, true bearing 93.16 deg from sun
- Up vector: `(0.0000, 0.0000, 1.0000)`; pitch 0, roll 0
- Google Maps: https://maps.google.com/?q=29.96590,31.75206
- Nearest columns (plan distance from eye):

  - `055sdm20rEqP0eKf$zgR_F` RC_Rectangular Columns:C(800x800)mm:627098 (HAC-SSL-FL2) - 4.12 m
  - `26KqgdbaD3EQ2JpeUjZOr1` RC_Rectangular Columns:C(800x800)mm:1153294 (HAC-SSL-B1) - 4.12 m
  - `055sdm20rEqP0eKf$zgR_u` RC_Rectangular Columns:C(800x800)mm:627117 (HAC-SSL-FL2) - 4.51 m

- Why here: Taken 75 s after P01 showing the same red formwork (now NW) and crane mast (now SE, closer): same spot moved ~2 m east along the raft edge. Sun heading 93 deg. Model 360 compared: inconclusive - many identical column bays, so the grid stays an estimate.

### P03 - HAC-SSL-FL2, grid 16/C - confidence low, verified no

- Taken: 2026-10-31 12:21:13+02:00; photos: IMG_20261031_122113_00_013
- Eye (IFC mm): `(-343714129, -402327626, 153027)`
- Target (IFC mm): `(-343721602, -402320982, 153027)`
- View direction (pano centre): `(-0.7473, 0.6645, 0.0000)`, true bearing 311.64 deg from sun
- Up vector: `(0.0000, 0.0000, 1.0000)`; pitch 0, roll 0
- Google Maps: https://maps.google.com/?q=29.96564,31.75198
- Nearest columns (plan distance from eye):

  - `26KqgdbaD3EQ2JpeUjZOmf` RC_Rectangular Columns:C(1000x2100)mm:1153126 (HAC-SSL-B1) - 4.45 m
  - `2Ip7HNHkH8QuUSM6MpN0dp` RC_Rectangular Columns:C(1000x2100)mm:617999 (HAC-SSL-FL2) - 4.45 m
  - `26KqgdbaD3EQ2JpeUjZOme` RC_Rectangular Columns:C(1000x1000)mm:1153127 (HAC-SSL-B1) - 7.68 m

- Why here: 4.7 min walk after P02 (~100-250 m reach). Sun heading 312 deg: government buildings E/NE, flat raft rebar fields W/NW with a recessed pit (lift/pile cap) NW, column cages S and E. Long open raft area suggests mid-east part of the orthogonal block south of P01. Model 360 compared: inconclusive - many identical column bays, so the grid stays an estimate.

### P04 - HAC-SSL-FL2, grid 16/C - confidence low, verified no

- Taken: 2026-10-31 12:21:44+02:00; photos: IMG_20261031_122144_00_014
- Eye (IFC mm): `(-343712129, -402327626, 153027)`
- Target (IFC mm): `(-343716573, -402318668, 153027)`
- View direction (pano centre): `(-0.4445, 0.8958, 0.0000)`, true bearing 333.61 deg from sun
- Up vector: `(0.0000, 0.0000, 1.0000)`; pitch 0, roll 0
- Google Maps: https://maps.google.com/?q=29.96564,31.75201
- Nearest columns (plan distance from eye):

  - `26KqgdbaD3EQ2JpeUjZOmf` RC_Rectangular Columns:C(1000x2100)mm:1153126 (HAC-SSL-B1) - 6.18 m
  - `2Ip7HNHkH8QuUSM6MpN0dp` RC_Rectangular Columns:C(1000x2100)mm:617999 (HAC-SSL-FL2) - 6.18 m
  - `3061ju5N94YvDiTWXiyN7i` RC_Rectangular Columns:C(800x800)mm:615965 (HAC-SSL-FL2) - 6.84 m

- Why here: 31 s after P03 with the same pit, compressor and workers in view rotated: same area ~2 m away. Sun heading 334 deg. Model 360 compared: inconclusive - many identical column bays, so the grid stays an estimate.

### P05 - HAC-SSL-FL2, grid 17/C - confidence low, verified no

- Taken: 2026-10-31 12:22:04+02:00; photos: IMG_20261031_122204_00_015
- Eye (IFC mm): `(-343714129, -402336026, 153027)`
- Target (IFC mm): `(-343711447, -402326393, 153027)`
- View direction (pano centre): `(0.2682, 0.9634, 0.0000)`, true bearing 15.56 deg from sun
- Up vector: `(0.0000, 0.0000, 1.0000)`; pitch 0, roll 0
- Google Maps: https://maps.google.com/?q=29.96556,31.75198
- Nearest columns (plan distance from eye):

  - `26KqgdbaD3EQ2JpeUjZOme` RC_Rectangular Columns:C(1000x1000)mm:1153127 (HAC-SSL-B1) - 5.38 m
  - `2Ip7HNHkH8QuUSM6MpN0cb` RC_Rectangular Columns:C(1000x1000)mm:618073 (HAC-SSL-FL2) - 5.38 m
  - `26KqgdbaD3EQ2JpeUjZOmy` RC_Rectangular Columns:C(1000x1000)mm:1153139 (HAC-SSL-B1) - 5.75 m

- Why here: 20 s after P04; compressor now NNE and pit to the W, column cage with crane hook E: moved a few metres south along the same raft strip. Sun heading 16 deg. Model 360 compared: inconclusive - many identical column bays, so the grid stays an estimate.

### P06 - HAC-SSL-FL2, grid 18/C - confidence low, verified no

- Taken: 2026-10-31 12:23:24+02:00; photos: IMG_20261031_122324_00_016
- Eye (IFC mm): `(-343714129, -402341826, 153027)`
- Target (IFC mm): `(-343716469, -402332104, 153027)`
- View direction (pano centre): `(-0.2340, 0.9722, 0.0000)`, true bearing 346.47 deg from sun
- Up vector: `(0.0000, 0.0000, 1.0000)`; pitch 0, roll 0
- Google Maps: https://maps.google.com/?q=29.96551,31.75198
- Nearest columns (plan distance from eye):

  - `26KqgdbaD3EQ2JpeUjZOmy` RC_Rectangular Columns:C(1000x1000)mm:1153139 (HAC-SSL-B1) - 2.43 m
  - `2Ip7HNHkH8QuUSM6MpN1SN` RC_Rectangular Columns:C(1000x1000)mm:618731 (HAC-SSL-FL2) - 2.43 m
  - `2Ip7HNHkH8QuUSM6MpN0WM` RC_Rectangular Columns:C(1000x2100)mm:618474 (HAC-SSL-FL2) - 6.25 m

- Why here: 80 s after P05; compressor now N close by, long raft strip W/NW with workers tying rebar, column cages E: continued south ~5-8 m. Sun heading 346 deg. Model 360 compared: inconclusive - many identical column bays, so the grid stays an estimate.

### P07 - HAC-SSL-FL2, grid 18/C - confidence low, verified no

- Taken: 2026-10-31 12:23:47+02:00; photos: IMG_20261031_122347_00_017
- Eye (IFC mm): `(-343717129, -402341826, 153027)`
- Target (IFC mm): `(-343724864, -402335489, 153027)`
- View direction (pano centre): `(-0.7736, 0.6337, 0.0000)`, true bearing 309.33 deg from sun
- Up vector: `(0.0000, 0.0000, 1.0000)`; pitch 0, roll 0
- Google Maps: https://maps.google.com/?q=29.96551,31.75195
- Nearest columns (plan distance from eye):

  - `2Ip7HNHkH8QuUSM6MpN0WM` RC_Rectangular Columns:C(1000x2100)mm:618474 (HAC-SSL-FL2) - 3.59 m
  - `26KqgdbaD3EQ2JpeUjZOmX` RC_Rectangular Columns:C(1000x2100)mm:1153134 (HAC-SSL-B1) - 3.59 m
  - `26KqgdbaD3EQ2JpeUjZOmy` RC_Rectangular Columns:C(1000x1000)mm:1153139 (HAC-SSL-B1) - 5.40 m

- Why here: 23 s after P06 with the same compressor (NE) and raft strip: ~3 m west of P06. Sun heading 309 deg. Model 360 compared: inconclusive - many identical column bays, so the grid stays an estimate.

### P08 - HAC-SSL-B1, grid 20/B - confidence low, verified no

- Taken: 2026-10-31 12:32:14+02:00; photos: IMG_20261031_123214_00_024
- Eye (IFC mm): `(-343703329, -402358626, 163577)`
- Target (IFC mm): `(-343701760, -402348750, 163577)`
- View direction (pano centre): `(0.1569, 0.9876, 0.0000)`, true bearing 9.03 deg from sun
- Up vector: `(0.0000, 0.0000, 1.0000)`; pitch 0, roll 0
- Google Maps: https://maps.google.com/?q=29.96536,31.75209
- Nearest columns (plan distance from eye):

  - `3061ju5N94YvDiTWXiyN8c` RC_Rectangular Columns:C(800x800)mm:615895 (HAC-SSL-FL2) - 2.40 m
  - `26KqgdbaD3EQ2JpeUjZOm2` RC_Rectangular Columns:C(800x800)mm:1153101 (HAC-SSL-B1) - 2.40 m
  - `3EiCjDjFHBo9ianunvkuX7` RC_Rectangular Columns:C(800x800)mm:608902 (HAC-SSL-FL2) - 5.60 m

- Why here: Camera on a timber/shoring deck about one storey above the raft: retaining wall and excavation bank close by to the E with the bank top near deck level, so a slab formwork deck near the east perimeter. Taken 9 min after P07. Sun heading 9 deg. Model 360 compared (uncast GF slab hidden): B1 columns below and perimeter walls to the E/NE, consistent with the retaining wall E in the photo; the grid itself is not confirmed.

### P09 - HAC-SSL-B1, grid 20/B - confidence low, verified no

- Taken: 2026-10-31 12:32:34+02:00; photos: IMG_20261031_123234_00_025
- Eye (IFC mm): `(-343703329, -402356626, 163577)`
- Target (IFC mm): `(-343713192, -402354978, 163577)`
- View direction (pano centre): `(-0.9863, 0.1648, 0.0000)`, true bearing 279.49 deg from sun
- Up vector: `(0.0000, 0.0000, 1.0000)`; pitch 0, roll 0
- Google Maps: https://maps.google.com/?q=29.96537,31.75209
- Nearest columns (plan distance from eye):

  - `3061ju5N94YvDiTWXiyN8c` RC_Rectangular Columns:C(800x800)mm:615895 (HAC-SSL-FL2) - 3.12 m
  - `26KqgdbaD3EQ2JpeUjZOm2` RC_Rectangular Columns:C(800x800)mm:1153101 (HAC-SSL-B1) - 3.12 m
  - `3061ju5N94YvDiTWXiyN8N` RC_Rectangular Columns:C(800x800)mm:615910 (HAC-SSL-FL2) - 5.91 m

- Why here: 20 s after P08 on the same deck (same crane N, retaining wall E): ~2 m further along the deck. Sun heading 279 deg. Model 360 compared: inconclusive - many identical column bays, so the grid stays an estimate.

### P10 - HAC-SSL-B1, grid B/AFX.A-17 - confidence low, verified no

- Taken: 2026-10-31 12:33:05+02:00; photos: IMG_20261031_123305_00_026
- Eye (IFC mm): `(-343703329, -402354626, 163577)`
- Target (IFC mm): `(-343706439, -402345122, 163577)`
- View direction (pano centre): `(-0.3110, 0.9504, 0.0000)`, true bearing 341.88 deg from sun
- Up vector: `(0.0000, 0.0000, 1.0000)`; pitch 0, roll 0
- Google Maps: https://maps.google.com/?q=29.96539,31.75209
- Nearest columns (plan distance from eye):

  - `3061ju5N94YvDiTWXiyN8N` RC_Rectangular Columns:C(800x800)mm:615910 (HAC-SSL-FL2) - 4.16 m
  - `26KqgdbaD3EQ2JpeUjZOm1` RC_Rectangular Columns:C(800x800)mm:1153102 (HAC-SSL-B1) - 4.16 m
  - `3061ju5N94YvDiTWXiyN8c` RC_Rectangular Columns:C(800x800)mm:615895 (HAC-SSL-FL2) - 4.66 m

- Why here: 31 s after P09, same deck walkway: ~2 m further. View S over formwork decks of the neighbouring bays. Sun heading 342 deg. Model 360 compared: inconclusive - many identical column bays, so the grid stays an estimate.

## 5. Model 360 render settings (out/model_pano/Pxx.jpg)

- Renderer: pyvista/VTK off-screen, 6 cube faces 1024 px at 90 deg FOV, order right, left, up, down, front, back, stitched with ffmpeg `v360=c6x1:e` to a 4096x2048 equirectangular image.
- Front face = view direction above; right = `(cos h, -sin h, 0)`; clipping 0.05-2000 m.
- Elements drawn: within 80 m plan radius and starting at or below eye Z + 0.3 m; slabs/beams whose top is above the camera feet + 0.05 m are hidden (treated as not cast yet).
- Colours: column orange, wall grey, slab blue, beam green, proxy purple, stair yellow, other light grey; sky #9cc3e6.
- Real pano heading: sun found in the image (yaw) vs NOAA sun azimuth at photo time (UTC+2): `heading = (sun_azimuth - sun_yaw) mod 360`. Viewer northOffset = heading.
