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

### Getting started with crow + Max for Live
The `crow_m4l` folder holds a suite of devices to help integrate your modular with Live:

<img src="https://github.com/monome/crow-max/blob/master/images/m4l_row.png" width="800">

---

#### **^^dual**
- an *output* device to translate MIDI data from Live to v/8 and envelope voltages
- load onto any MIDI track + either arm it for record or set the monitoring to "in"
- click the `^^` button in the bottom left corner to link a connected crow to **^^dual**
- expand the `(outs)` dropdown to identify which duo of outputs you'd like **^^dual** to use for v/8 and envelope voltage: ouputs 1+2 or outputs 3+4
- output 1/3 will send v/8
- output 2/4 will send either an envelope or a trigger for every note-on event

~~

- *base*: which MIDI note represents middle-C, default is 60
- *slew*: adds glide between notes, default is none
- *attack*: shapes the start of the envelope, default is nearly zero
- *decay*: shapes the end of the envelope, default is very snappy / trigger-style

---

#### ^^jf_synth
- an *i2c output* device to play a connected Just Friends module as a 6-voice polyphonic synth through Live
- requires Just Friends (Whimsical Raps) to be connected via i2c cable
- load onto any MIDI track + either arm it for record or set the monitoring to "in"
- click the `^^` button in the middle of the m4l device to link a connected crow to **^^jf_synth**
- on your Just Friends module's panel, engage `sound` and `transient`
- on the m4l device, engage the toggle in the bottom left corner to connect to Just Friends
- you should now be able to play Just Friends through MIDI

---

#### ^^ins
- an *input* device to translate incoming CV to useful MIDI data
- load onto any MIDI track
- click the `^^` button in the top-left of the m4l device to link a connected crow to **^^ins**
- expand the `(input)` dropdown to identify which hardware input you'd like to monitor / control Live: 1 or 2
- *input cv*: real-time streaming monitor of voltage incoming through the input specified

~~

*CV-to-CC*: this section will translate incoming voltage to MIDI CC data
- *low*: set the desired floor for voltage-to-CC, default is 0V
- *high*: set the desired ceiling for voltage-to-CC, default is 10V
- *map*: map the incoming voltage to any MIDI-controllable parameter in Live
- *%'s*: adjust the range of CC expression for each individual map channel

~~

*CV-to-note*: this section will translate incoming CV to MIDI pitch data
- *(trig src)*: identify whether you would like the CV conversion to take place synced to Live's clock (arpeggiator) or if you'd like the conversion to take place every time a trigger is received through the *other* input of crow.
- *low*: set the desired floor for CV-to-MIDI, default is lowest note at 36
- *high* set the desired ceiling for CV-to-MIDI, default is highest note at 127

---
#### ^^outs
- an *output* device that collects multiple utilities in a single interface
- load onto any MIDI track + either arm it for record or set the monitoring to "in"
- click the `^^` button in the center-bottom of the m4l device to link a connected crow to **^^outs**
- expand the `(out)` dropdown to identify which hardware output you'd like to use (nb. you can instantiate this device up to four times in a Live set)
- 
