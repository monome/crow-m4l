# crow-max
Max + M4L for crow (monome/whimsical raps)

## Max installation
After downloading the entire `crow-max` repo, extract the zip file and you should get two unique folders: `crow_max` and `crow_m4l`.

Open `Max` > `Options` > `File Preferences` > highlight `User Library` > the rightmost icon in the bottom bar should illuminate. Clicking this icon will open the User Library folder, where you can drop the `crow_max` folder.

If you are performing an update of an existing `crow_max` installation, you can simply allow the system to replace the existing files. If you somehow have previous **beta** crow files in your User Library (or anywhere along your Max search path), please delete them and start fresh with `crow_max`.

Restart Max and you should be able to instantiate the `crow` abstraction as a regular object!

### Getting started with crow + Max
A detailed Max help patcher is included with the `crow`abstraction:

<img src="https://github.com/monome/crow-max/blob/master/images/help_ss.png" width="500">

To access, instantiate `crow` and right-click the object. Select "Open crow Help".

- **anatomy**: demonstartion of the necessary signal flow to start patching with crow in Max.
- **cv input**: showcases reading CV through crow's 2 hardware inputs either on-demand, as a stream, or when a signal crosses a specified threshold.
- **basic cv output**: setting CV slew and specifying target voltages for crow's 4 hardware outputs. introduces `sprintf` techniques to help assign values dynamically.
- **cv notes**: showcases MIDI-to-CV translation for v/8 notemaking. also introduces *pulse* and *ar* commands.
- **cv shapes**: introduction to *actions* as user-definable envelopes/lfo's.
- **i2c**: demonstrates i2c connectivity + simple interactions with Just Friends (Whimsical Raps). this seemed the most interesting application, though the fundamental approach is translatable to any i2c device that has pre-defined Teletype interactions (w/, ER-301, Ansible, etc).
- **^^**: an index of system commands that report on connected hardware + flash new scripts to the module.

## Max for Live installation
nb. Max installation is **not** required to use the devices in `crow_m4l`.

After downloading the entire `crow-max` repo, extract the zip file and you should get two unique folders: `crow_max` and `crow_m4l`.

Open Live (9 or 10) Suite, running at least Max 7.3.6. Place `crow_m4l` wherever you'd prefer it living longterm on your harddrive. Open Live and drag the folder into Live's browser, under `PLACES`.

If you are updating a previous installation, just replace the previous `crow_m4l` folder's contents with the new files.
