# Enclosure for the sensor

I tried something different this time. I usually draw my case using FreeCad so I get exactly what I want. But after seeing a video on YT from Michael Lydick who ask ChatGPT to make a part for him using a photo of the part in question that will be usable in a CAD software and, ultimetly, printable by a 3D printer; I wonder if I could "vibe CAD" the case from scratch using a prompt.

Well, look at the result in the folder and here's below the prompt used in Anthropic Claude (using Opus 5.5 [medium]) to generate all those files. Quite impressive I should say.

## Prompt

Design a 3D-printable enclosure (PLA, FDM) for a Sensirion SEN66 and a small
controller PCB. Deliver STEP files I can open in FreeCAD (body, cover, and an
assembly with dummy parts to check the fit), plus STLs and the parametric script.

SENSOR

- Sensirion SEN66, 55.5 x 25.6 x 21.5 mm. The mechanical drawing is page 56 of
  the attached datasheet. The air inlets and fan outlet are on the large
  55.5 x 25.6 face, which must face the front of the enclosure.
- Follow Sensirion's SEN6x Mechanical Design and Assembly Guidelines: open
  area at least 56 mm² for the inlets and 148 mm² for the outlet, sensor face
  sealed to the front wall with a gasket, openings never facing up, sensor
  below the PCB and isolated from its heat.
- The sensor's 6-pin cable connector is on its LEFT end. Leave room for the
  cable to go up to the PCB.

PCB

- 40 x 24 x 1.6 mm, lying flat above the sensor, 40 mm side parallel to the
  sensor's long side.
- Hold it with slide-in slots along both 40 mm edges (2 mm component-free strip
  on each). No mounting holes.
- USB-C on the RIGHT 24 mm edge, bottom of the connector 4 mm above the board
  top, centred on the edge -> opening in the right side wall.
- Sensor cable connector on the LEFT 24 mm edge, centred -> keep that side
  clear for the cable.
- Clearance: 4 mm under the board, at least 12 mm above.

MECHANICAL

- Two parts: body + back cover, 4 x M3 screws (self-tapping into PLA).
- Must print without supports: body front face down, cover outside face down.
- Protective bars across the front window, vents for the PCB compartment.
- Include an optional TPU gasket.
- Before delivering, check that nothing collides and that the board slides in
  without catching.

## Notes

Attach the PDF file of the sensor in your prompt.
