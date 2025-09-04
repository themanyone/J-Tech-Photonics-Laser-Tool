# J Tech Photonics Laser Tool (Community version)
This Inkscape extension generates gcode for laser cutters and plotting machines from an SVG file.

--------------

This experimental fork enables an option to increase the laser's power level throughout the print by darkening the path's color. And increasing the speed by drawing thinner paths. In other respects it is compatible with earlier plugins.

If you want to test having the darkness of the stroke (line in the svg) controlling laser power, Open the extension at **Extension** > **Generate Laser Gcode** > **J Tech Community Laser Tool**. Insert a `%` sign before the numeric portion of your laser's Tool Power Command. 

For example, if your Power Command is "S1000", change it to "S%1000". Now this extension will emit gcode that varies the laser's power level depending on color. Black is full power.

Thinner lines increase speed. Paths that are 0.10mm in width will be at 90% speed. Paths that are 0.20mm in width will draw at 80% speed. Widths of 1mm or more will use minimum speed.

You will need [this fork of the SvgToGcode](https://github.com/themanyone/SvgToGcode) library for this to work. In this way, you should have full control of the laser's power and speed throughout a print.

If the various line widths and colors are not desirable to see in Inkscape, go to **View** > **Display Mode** > **Outline**. 

--------------

Our SvgToGcode library (above) is a fork of the original [svg_to_gcode](https://github.com/PadLex/SvgToGcode) library, found here.

## Installation

Download the latest release [here](https://github.com/themanyone/J-Tech-Photonics-Laser-Tool).
Inkscape versions below 1.0 are not supported. Use legacy releases if you are using Inkscape < 1.0.

Copy laser/laser.* into the Inkscape **user extensions folder**. Inkscape lists the location
of your user extensions folder under **Edit/Inkscape** > **Preferences** > **System**.

Restart Inkscape and you're done.

## Tutorial

### Document Setup
Before using the extension, we need to make sure the document is setup correctly. Open **File** > **Document Properties**.

Set the document's **display units** to `mm` or `in`.
Then set **Scale x**, **Scale y** to `1` and **Viewbox > X**, **Viewbox > Y** to `0`.

<img src="./images/document_setup_properties.png" alt="document_setup_properties.png" width="600" />

Lastly, you can move and rescale your drawing to make it look like it did before. 

### Basic Usage

This extension will parse all svg paths and ignore everything else. 

**Step 1 is to convert all other shapes to paths.** In this case I want to convert the whole drawing to gcode.
So I select everything `ctr+A` and convert the drawing to paths 
**Path** > **Object to Path** (Ctrl-Shift-C).

Open the extension at **Extension** > **Generate Laser Gcode** > **J Tech Community Laser Tool**

It should default to the **same unit** you used in the **Document Settings**. If not, then change it. Then choose an appropriate output directory, leave the file name blank, and hit apply.

<img src="./images/important_settings.png" alt="important_settings.png" width="600" />

If Live preview is checked, you'll notice two layers were added to your document:
* `debug reference points` contains the black corners. They 
represent the four corners of your machine's bed. You can use them to eyeball whether the gcode is scaled and placed 
correctly.
* `debug traces` contains the red paths which trace all generated gcode commands.

Note: debug layers are reset everytime you run the extension. So make sure you don't accidentally add any objects to them 
or they will be deleted.

## Contribute

* As a user you can contribute by suggesting features, testing the library and reporting any bugs you encounter in a 
detailed issue.
* As a developer of any skill level you can make pull requests which close issues or introduce useful features. 
Just make sure to create an issue describing what features you want to add before taking the time to implement them.
