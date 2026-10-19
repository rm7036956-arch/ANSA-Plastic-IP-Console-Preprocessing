# ANSA-Plastic-Preprocessing ( Project 2 ) 

Mid-Mesh Generation of a Plastic Car IP Console (ANSA)

A project that converts the CAD of a plastic car instrument panel (IP) console / dashboard into a clean, variable-thickness mid-mesh (shell mesh) ready for structural, NVH or crash analysis.

1. Project Summary
Item	Details
Component	Car IP console / dashboard (instrument cluster area, music-system area, full dashboard)
Material type	Plastic (injection moulded), variable wall thickness
Input file	Dash Board Sub Parts-Final.IGS (IGES)
Software	ANSA (Checks Manager, Mesh, Align Manager, Casting)
Method	Casting method for mid-mesh generation (not mid-surface)

Why mid-mesh? Plastic parts have changing wall thickness around ribs, bosses and clips. The casting method finds the mid-plane directly from the solid and generates the shell mesh and its thickness together, which is faster and more accurate than building a constant-thickness mid-surface.

2. Files in This Package
File	Description
IP_Console_MidMesh_Project_Report.docx	Full project report (editable)
IP_Console_MidMesh_Project_Report.pdf	Same report as PDF (14 pages, ready to share)
DogHouse_Tapered_Before_After.png	Before/after: tapered dog house
DogHouse_Cylindrical_Before_After.png	Before/after: angled cylindrical dog house
DogHouse_Triple_Before_After.png	Before/after: group of three dog houses
DogHouse_4_Tapered_v2_Before_After.png	Before/after: tapered dog house (second example)
DogHouse_5_Twin_Cylinders_Before_After.png	Before/after: twin cylindrical bosses
DogHouse_6_Angled_Flat_Before_After.png	Before/after: angled dog house (curves vs mesh)
README.md	This file
3. Workflow
Import the IGES geometry into ANSA.
Geometry checks with the Checks Manager (Geometry). 371 errors were found.
Geometry cleanup (see Section 4).
Mid-mesh generation with the Casting method (see Section 5).
Dog house capture: features the automatic method missed were rebuilt manually (see Section 6).
Alignment: Align Manager for perimeters, areas and imprints; white lines removed.
Mesh repair and quality: FEM Topo, Smooth, Reshape, Reconstruct, Sweep, Split.
Quality check against the project criteria (see Section 7).
4. Geometry Errors and Fixes
Code	Error	Meaning
E5102	Problematic Surface	Surface with bad mathematical shape
E4068	Unchecked Faces	Faces the checker could not evaluate (26)
E4071	Needle Face	Very thin, sliver-like face
E4072	Overlapping Faces	Two faces in the same place
E4073	Crack Between Cons	Tiny gap between neighbouring faces
E4070	Triple Cons	Three faces sharing one edge
E4074	Single Cons	Free edge belonging to only one face

Fixes used: ANSA auto-fix, Cons to Curve, curve editing (Create, Connect, Modify, Project, Delete), Fill to rebuild faces, then re-running the checks.

5. Casting Parameters
Parameter	Value
Minimum thickness	0.5 mm
Target length	4 mm
Minimum length	2 mm
Maximum length	6 mm
Thickness result (T result)	Taken and treated
6. Dog House Capture

Dog houses are solid, hollow-from-inside features with no wall thickness of their own, so they are captured in the mid-mesh as a cross pattern.

Workflow for each dog house:

Create curves along its edges using Cons to Curve (plus Connect / Create / Modify / Project / Delete).
Build the missing faces with Fill.
Align perimeters and areas to the wall mesh using Align Manager.
Fill remaining gaps with FEM Topo.
Check quality, then Freeze the finished area.

Freeze / Unfreeze: aligning one perimeter can disturb a neighbouring area. Freezing a finished area protects it from later changes; Unfreeze is used when it needs editing again.

7. Results
Mesh statistics (ANSA Quality Monitor)
Item	Count	Share
Total shells	50,641	100 %
Quads	48,167	95.11 %
Trias	2,474	4.89 %
Quality criteria
#	Criterion	Required	Status
1	Target length	4 mm	Pass
2	Minimum length	2 mm	Pass
3	Maximum length	6 mm	Pass
4	Aspect ratio	≤ 3	Pass
5	Warpage	≤ 15°	Pass
6	Skewness	≤ 45°	Pass
7	Jacobian	≥ 0.7	Pass
8	Minimum quad angle	≥ 45°	Pass
9	Maximum quad angle	≤ 135°	Pass
10	Minimum tria angle	≥ 30°	Pass
11	Maximum tria angle	≤ 120°	Pass
12	Tria percentage	≤ 15 %	Pass (4.89 %)

A few failed elements may remain near triple cons or in very small regions bounded by two triple cons; these are kept as they are when they cannot be solved.

8. Tools and Commands Used
Tool	Purpose
Checks Manager (Geometry)	Find geometry errors
Cons to Curve	Convert edges to curves, capture dog houses
Curves: Create / Connect / Modify / Project / Delete	Build and edit boundaries
Faces / Fill	Create faces; convert cons into mesh
Casting	Generate variable-thickness mid-mesh
Extrusion	Mid-surface generation in selected areas
Align Manager	Align perimeters, areas, imprints; remove white lines
Smooth / Reshape / Reconstruct	Improve element quality
FEM Topo	Fill holes and gaps in the mesh
Sweep, Split	Create and split elements
Freeze / Unfreeze	Protect finished areas
9. Editing the Report
Open the .docx in Microsoft Word to edit text, tables and images.
Fill in the Prepared by name on the cover page.
To update quality values with exact measured numbers, edit the "Result" column in Section 9.2.
Export to PDF from Word after editing.
10. Skills Demonstrated
Geometry cleanup and topology repair in ANSA
Variable-thickness mid-mesh generation for plastic parts
Manual capture of complex features (dog houses, clips, bosses)
Mesh quality control to OEM-style criteria





