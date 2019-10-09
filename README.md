# crow-max-and-m4l
Max + M4L for crow (monome/whimsical raps)

## Max installation
After downloading the entire `crow-max-and-m4l` repo, extract the zip file and you should get two unique folders: `crow_max` and `crow_m4l`.

Open `Max` > `Options` > `File Preferences` > highlight `User Library` > the rightmost icon in the bottom bar should illuminate. Clicking this icon will open the User Library folder, where you can drop the `crow_max` folder.

If you are performing an update of an existing `crow_max` installation, you can simply allow the system to replace the existing files. If you somehow have previous **beta** crow files in your User Library (or anywhere along your Max search path), please delete them and start fresh with `crow_max`.

Restart Max and you should be able to instantiate the `crow` abstraction as a regular object!

### Getting started with crow + Max
A detailed Max help patcher is included with the `crow`abstraction:

![help_ss](/images/help_ss.png)

To access, instantiate `crow` and right-click the object. Select "Open crow Help".

- **anatomy**: demonstration of the necessary signal flow to start patching with crow in Max.
- **cv input**: showcases reading CV through crow's 2 hardware inputs either on-demand, as a stream, or when a signal crosses a specified threshold.
- **basic cv output**: setting CV slew and specifying target voltages for crow's 4 hardware outputs. introduces `sprintf` techniques to help assign values dynamically.
- **cv notes**: showcases MIDI-to-CV translation for v/8 notemaking. also introduces *pulse* and *ar* commands.
- **cv shapes**: introduction to *actions* as user-definable envelopes/lfo's.
- **i2c**: demonstrates i2c connectivity + simple interactions with Just Friends (Whimsical Raps). this seemed the most interesting application, though the fundamental approach is translatable to any i2c device that has pre-defined Teletype interactions (w/, ER-301, Ansible, etc).
- **^^**: an index of system commands that report on connected hardware + flash new scripts to the module.

### The standalone ^^bootloader patch
To help make flashing new crow firmware easy, we've included a straightforward Max patch that walks through the necessary steps:

![bootloader_ss](/images/bootloader_ss.png)

You can either open it from inside the `crow_max` folder **or** by opening a new patcher in Max and instantiating a `^^bootloader` object (lock the patch and double-click the object to open the bootloader helper).

After loading new firmware, you will need to re-establish the connection between Max and the crow module but there is no need to reboot your modular.

## Max for Live installation

nb. Max installation is **not** required to use the devices in `crow_m4l`.

After downloading the entire `crow-max-and-m4l` repo, extract the zip file and you should get two unique folders: `crow_max` and `crow_m4l`.

Open Live (9 or 10) Suite, running at least Max 7.3.6. Place `crow_m4l` wherever you'd prefer it living longterm on your hard drive. Open Live and drag the folder into Live's browser, under `PLACES`.

If you are updating a previous installation, just replace the previous `crow_m4l` folder's contents with the new files.

### Getting started with crow + Max for Live
The `crow_m4l` folder holds a suite of devices to help integrate your modular with Live:

![row](/images/m4l_row.png)

There is also a series of [video walkthroughs](https://youtu.be/TaEGzWsFVQc) available, which explore setup and basic parameters of each device.

---

### **^^command_center**
![command-center](/images/m4l_command-center.png)

nb. the m4l devices that follow will not connect to crow unless `^^command_center` is properly initialized.

nb. (pt 2) currently only one crow is addressable at a time. Multi-crow support will be added in the future.

- a *connector* between crow and Live
- load onto any MIDI track
- select your connected crow device from the dropdown
- don't see your crow? hit 'refresh'

---

#### **^^dual**

![dual](/images/m4l_dual.png)

- an *output* device to translate MIDI data from Live to v/8 and envelope voltages
- load onto any MIDI track + either arm it for record or set the monitoring to "in"
- expand the `(outs)` dropdown to identify which duo of outputs you'd like **^^dual** to use for v/8 and envelope voltage: ouputs 1+2 or outputs 3+4
- output 1/3 will send v/8
- output 2/4 will send either an envelope or a trigger for every note-on event

~~

- *base*: the central point for MIDI-to-CV conversion, default is MIDI note 60
- *slew*: adds glide between notes, default is none
- *attack*: shapes the start of the envelope, default is nearly zero
- *decay*: shapes the end of the envelope, default is very snappy / trigger-style

---

#### ^^ins

![ins](/images/m4l_ins.png)

- an *input* device to translate incoming CV to useful MIDI data
- load onto any MIDI track
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
- *(trig src)*: identify whether you would like the CV conversion to take place synced to Live's clock (arpeggiator) or if you'd like the conversion to take place every time a trigger is received through the *other* input of crow
- *low*: set the desired floor for CV-to-MIDI, default is lowest note at 36
- *high* set the desired ceiling for CV-to-MIDI, default is highest note at 127

---

#### ^^jf_synth

![jf-synth](/images/m4l_jf-synth.png)

an i2c output device to play a connected Just Friends module as a 6-voice polyphonic synth through Live

- as always, you must first choose a crow device with the ^^command_center

- ^^jf_synth requires Just Friends (Whimsical Raps) to be connected to crow via i2c cable or through powered-bus

- load onto any MIDI track + either arm it for record or set the monitoring to "in"

- if crow is NOT connected to an i2c powered-bus (ie, if it's just connected directly to Just Friends via an i2c cable with no Teletpe/TXb/powered-bus in between), toggle 'enable pullups' on the m4l interface

- on your Just Friends module's panel, engage 'sound' and 'transient'

- on the m4l device, engage the big toggle in the middle-bottom to connect to Just Friends

- you will see the 6 lights blink on Just Friends

- you should now be able to play Just Friends through MIDI!

---
#### ^^outs

![outs-setup](/images/m4l_outs-setup.png)

nb. you can instantiate this device up to four times in a Live set, to speak to each of the four hardware outputs on crow

- an *output* device that collects multiple utilities in a single interface
- load onto any MIDI track + either arm it for record or set the monitoring to "in"
- expand the `(out)` dropdown to identify which hardware output you'd like to use
- the device will display the selected output in the top right corner of the following screens:

~~

*v/8*

![outs-v-8](/images/m4l_outs-v-8.png)

- *base*: the central point for MIDI-to-CV conversion, default is MIDI note 60
- *slew*: adds glide between notes, default is none

~~

*clock*

![outs-clock](/images/m4l_outs-clock.png)

- *rate*: the rate of clock pulses, synced to Live's transport + tempo, default quarter notes
- *trigger*: set the max voltage for the trigger signal, default 5V
- *gate*: toggle behavior for *trigger* which will reveal % duty cycle of current clock rate, default 50%
- *polarity*: whether triggers are a burst of voltage or an absence of voltage in a continuous on-state, default is + (burst)

~~

*lfo*

![outs-lfo](/images/m4l_outs-lfo.png)

- *rate*: the rate of a positive LFO, synced to Live's transport + tempo, default 1 bar
- *level*: the high voltage for the LFO to reach before falling to 0V, default 5V

~~

*remote*

![outs-remote](/images/m4l_outs-remote.png)

- *knob*: an automatable knob which sends any movement out as CV
- *min*: the minimum CV the knob can put out when the needle is far-left, default -5V
- *max* the maximum CV the knob can put out when the needle is far-right, default 5V
- *bias*: adds an offset to the knob's current position, default 0V
- *smooth*: adds glide between knob values, default 50ms

---

#### ^^derwydd

This device gives you access to crow's Lua [read-eval-print loop](https://en.wikipedia.org/wiki/Read–eval–print_loop).  Send Lua code to Crow to execute on the fly, allowing you to modify crow's behavior in your real time.  You can also use it to upload new scripts, erase scripts, and more.

![derwydd](/images/m4l_derwydd.png)

- as always, you must first choose a crow device with the ^^command_center

- load onto any MIDI track.
- use the yellow-bordered box to type in lua code to send to crow.
- choose between how the 'enter' key on your keyboard functions using the switch
  - *execute* mode: pressing enter will send the entered code to crow for execution
  - *carriage-return* mode: pressing enter will move you to a new line, allowing you to send more complex multi-line code snippets to crow
- printouts and error messages from crow are displayed to the right of the text entry box
- use the up and down arrow keys to scroll through your recently entered code snippets
- use the ^^ buttons to give crow special commands; hover over the buttons and read Ableton's info box to find out more

---

#### ^^bridges

![bridges](/images/m4l_bridges.png)

Use this device to translate multiple mappable knobs in ableton into data for crow; the primary use case is taking remote control over variables in a script that crow is currently running.

- as always, you must first choose a crow device with the ^^command_center

- load onto any MIDI track
- use the yellow-bordered box to type in a name matching a variable in your script; the corresponding knob will now act as a remote control for that variable
- press enter to confirm your selection.
- adjust the min and max values of the knob as desired
- try automating the knob
- try MIDI mapping the knob with a MIDI controller
- try mapping the knob with another Max For Live Device
- adjust the number of bridges using the *bridge count* controller
- you may have an arbitrary number ^^bridges devices instantiated in a given set

---

#### ^^macros

![macros](/images/m4l_macros.png)

Store code snippets which can be sent to crow as macros on the fly.  Each snippet can be sent by selecting the device and pressing the corresponding number key on your keypad, or by sending the device the corresponding MIDI note.

- as always you must first choose a crow device the ^^command_center
- load onto any MIDI track
- use the numbered, yellow-bordered boxes to type in lua code to send to crow
- to execute the code in each box, you may either send the corresponding MIDI note to the device, or press the corresponding key on your keyboard *nb: when using your number keys, make sure the device is highlighted*
- macros are saved with your live set
