![Edisyn Splash Banner](https://raw.githubusercontent.com/eclab/edisyn/master/pics/Banner.png)

# Edisyn
Synthesizer Patch Editor (Version 7)

By Sean Luke (sean@cs.gmu.edu)


## About

Edisyn is a synthesizer patch editor library written in pure Java.   It runs on OS X, Linux, and (probably) Windows.  

Edisyn presently supports:

* Waldorf Blofeld and Waldorf Blofeld Keyboard (Single and Multi Modes)
* Waldorf Microwave II, XT, and XTk (Single and Multi Modes)

Ultimately Edisyn will have some more written for it as well as I get time; and of course the patch editors I can write are restricted to the synths I own and can test on!  Edisyn has no graphical interface editor system like Ctrlr, but it's designed to make the GUI pretty easy to write (well, for me anyway).

## Pictures!

* Blofeld Single: [Oscillators and Filters](https://raw.githubusercontent.com/eclab/edisyn/master/pics/BlofeldSingle1.png), 
[LFOs and Envelopes](https://raw.githubusercontent.com/eclab/edisyn/master/pics/BlofeldSingle2.png), 
[Modulation and Effects](https://raw.githubusercontent.com/eclab/edisyn/master/pics/BlofeldSingle3.png), 
[Arpeggiator](https://raw.githubusercontent.com/eclab/edisyn/master/pics/BlofeldSingle4.png)

* Blofeld Multi: [Multi and Parts 1-4](https://raw.githubusercontent.com/eclab/edisyn/master/pics/BlofeldMulti1.png), 
[Parts 5-10](https://raw.githubusercontent.com/eclab/edisyn/master/pics/BlofeldMulti2.png), 
[Parts 11-16](https://raw.githubusercontent.com/eclab/edisyn/master/pics/BlofeldMulti3.png)

* Microwave II/XT/XTk Single: [Oscillators and Filters](https://raw.githubusercontent.com/eclab/edisyn/master/pics/XTSingle1.png), 
[Envelopes](https://raw.githubusercontent.com/eclab/edisyn/master/pics/XTSingle2.png), 
[Modulation](https://raw.githubusercontent.com/eclab/edisyn/master/pics/XTSingle3.png), 
[Other](https://raw.githubusercontent.com/eclab/edisyn/master/pics/XTSingle4.png)

* Microwave II/XT/XTk Multi: [Multi and Instruments 1-2](https://raw.githubusercontent.com/eclab/edisyn/master/pics/XTMulti1.png), 
[Instruments 3-5](https://raw.githubusercontent.com/eclab/edisyn/master/pics/XTMulti2.png), 
[Instruments 6-8](https://raw.githubusercontent.com/eclab/edisyn/master/pics/XTMulti3.png)


## Install and Run Edisyn

Edisyn is cross-platform and will run on a variety of platforms (Windows, Linux) but I am personally developing on and for OS X.  I'd appreciate feedback and screenshots of it running on Windows and Linux so I can tweak things.


### Installation and Running on OS X 

First install Edisyn from the [Edisyn.dmg](https://github.com/eclab/edisyn/raw/master/install/Edisyn.dmg) file located in the "install" directory.  Sadly, it's a whopping 70MB because it includes the Java VM.  :-(


Sierra has really locked down the ability to run an application that's not from a paid-up Apple Developer.  And I'm not one.  So you will have to instruct Sierra to permit Edisyn to run.

Let's assume you stuck Edisyn in the /Application directory as usual.  Then:

1. Run the Terminal Program (in /Applications/Utilities/)
2. Type the following command and hit RETURN: `   sudo spctl --add /Applications/Edisyn.app`
4. Enter your password and hit RETURN.
5. Quit the Terminal Program

Now you should be able to run Edisyn.  Let me know if this all works.


### Installation and Running on Windows

I don't know.  But you may be able to download the [jar file](https://github.com/eclab/edisyn/raw/master/jar/edisyn.jar) located in the "jar" directory and double-click on it.  Tell me if this works.


### Installation and Running on Linux

I'm told that this works on Ubuntu:

1. Install Java if you don't have it yet (openjdk probably).

2. Download [Edisyn's jar file](https://github.com/eclab/edisyn/raw/master/jar/edisyn.jar) located in the "jar" directory.

3. Right-click on the jar file icon and choose "Properties".  Then select the "Open With" tab, and select your Java VM (for example "Open JDK Java 8 Runtime").  
The press "Set as Default".  This makes the Java VM the default application to launch jar files.

4. Thereafter you should be able to just double-click on the file to launch Edisyn.


### Running from the command line (OS X, Windows, Linux)

1. Make sure Java is installed.

2. Download [Edisyn's jar file](https://github.com/eclab/edisyn/raw/master/jar/edisyn.jar) located in the "jar" directory.

3. Run Edisyn as:   `java -jar edisyn.jar`



## Using Edisyn

### The Editor Pane

The editor pane should be self-explanatory.  There are four tabs which together cover all of the parameters of 
the synthesizer.  The first tab, *Oscillators and Filters*, also contains an area called *Waldorf Blofeld* (or
some other synth) which
lets you set the patch name and category, bank, number, and Device ID.   The bank, number, and ID are mostly
for saving out to sysex files: whenever you upload or download patch to/from the synth, you'll be prompted
to revise those if necessary.

### The File Menu

* *New* creates a new editor pane, set to the default (the synth's Init patch setting).  Note that only the frontmost editor pane will receive MIDI.  So if you for
some reason set up both editor panes with the same interface, then request MIDI from one pane, then quickly
switch to the other pane, you could in theory get the MIDI sent to the other pane.  So don't do that.

* *Load...* loads a sysex file into the existing editor pane.  It's called Load instead of Open because it 
doesn't open a new window.

* *Close Window* closes, well, you know, it closes, um, the window.

* *Save* and *Save As...* save to a sysex file.


### The MIDI Menu

Note that you can *send* a patch to the synthesizer and you can *write* a patch to the synthesizer.  The former
just temporarily updates the synth's current patch memory so you can play it.  The latter actually writes the 
patch to an address in the synth, replacing whatever is there.

* *Request Current Patch* asks the synthesizer to load the current patch memory into the editor.  Note that on
some machines (like the Waldorf Blofeld) when the patch is loaded, the bank and patch number are invalid and will
be reset to some defaults, which might be confusing!

* *Request Patch...* asks the synthesizer to load a specific patch into the editor.  If the synthesizer complies,
once the patch is loaded, Edisyn will then send the patch to the synthesizer.

* *Request Merge* asks the synthesizer to load a specific patch into the editor.  If the synthesizer complies,
then the patch is *merged* with the existing patch, meaning that some *percentage* of parameters in the existing
patch are replaced with the old patch.  Then Edisyn will then send the patch to the synthesizer.

* *Randomize* randomizes the editor's current patch, then sends it to the synthesizer.

* *Reset* resets the editor's current patch to its initialized state, then sends it to the synthesizer.

* *Send Patch* sends the current patch to the synthesizer.  This isn't actually used much since other commands
send the patch automatically.

* *Write Patch...* writes the patch to a given location in the synthesizer.

* *Change MIDI* sets or updates the MIDI interface.

* *Disconnect MIDI* disconnects the MIDI interface.

* *Send All Sounds Off* sends the All Sounds Off message to all channels.

* *Send Test Note* sends a 1/2 second test note to the primary channel.

* *Map CC* (or *End Map CC*) toggles CC Mapping mode, which enables you to map a CC message from your controller keyboard to almost any Edisyn
editor widget.  See "CC Mapping" below.

* *Clear CCs* clears all mapped CCs.  See "CC Mapping" below.

### The Tabs Menu

The Tabs menu lets you quickly move between tabs.

* *Previous Tab* moves one tab to the left.

* *Next Tab* moves one tab to the right.

* *Tab 1* through *Tab 8* select the first through the eighth tab respectively.

### The MIDI Interface

Edisyn makes up to three MIDI device connections.  The *Receiving Device* is the MIDI device from which we will accept
patches.  This is usually your synthesizer.  The *Sending Device* is the MIDI device to which we will send 
patches and parameter changes.  We'll also need a *Channel* for the Sending Device so we can send test notes.

Optionally you can route your controller keyboard through Edisyn to play the sounds directly if you wish.  To do this,
the *Controller* is the MIDI Device of your controller keyboard.  You'll also specify an incoming *Controller Channel*
channel of course.  This can be set to "Any" for any channel (Omni).

Additionally, if you're sick of using your mouse, you can map *CC MIDI Commands* from your Controller Keyboard to 
directly manipulate dials and other widgets in Edisyn.  See "CC Mapping" below.

### Sending and Recieving Parameters

If you change a widget in the editor, Edisyn will send the appropriate sysex command to the synthesizer to change it on
the synth as well.  Additionally, if you change a parameter on the synthesizer and it forwards a *sysex* command to Edisyn,
then Edisyn will update the appropriate widget in the editor.  At present Edisyn does't support CC commands from the
synthesizer (maybe later).  So (for example) on the Blofeld you'll need to change the machine to *send sysex* -- not CC only -- when changing parameters on the synth.

### CC Mapping

If you select *Map CC*, you can map a CC controller to a widget.  This is done as follows:

1. Make sure you told Edisyn the correct MIDI device and channel for your controller.
2. Choose *Map CC*
3. Edisyn will change the window to say "LEARNING"
4. Tweak the widget to change its value.  This informs Edisyn that it's the widget you want to map.
5. Edisyn will change the window to say "LEARNING parameter[range]=cc" (*range* and *cc* might not show up)
where *parameter* is the name of the parameter the widget is controlling, *range* is the range of the parameter (if any),
and *cc* is the current CC assigned to that parameter (if any).
6. Send the CC message from your controller (turn a knob or press a button).
7. It'd now be a good idea to set your controller to only send CC values within the provided range.  For example, if *range* was 7, you might set your controller
to only send values from 0..6.  If *range* was 2, you'd set it to send values 0..1.  And so on.

Every *Tab* on every *Synthesizer Panel type* has its own unique set of CCs.
Mapped CCs for a given Synthesizer panel type are permanent until you clear all CCs for the synth by choosing *Clear CCs*, which clears them for all tabs for that Synthesizer.

### Per-Synth Specific Notes and Bugs

Gotchas and important things to know are contained in the <b>About</b> Tab in each synth editor window.  You should read it before using the editor for that synth.

## Caveats

To work around some bugs in OS X Midi and CoreMIDI4J, Edisyn's architecture at present does not let you
plug in new devices (or remove them) after Edisyn has been launched.  If you need to do so, restart Edisyn
(for now). 

Randomize isn't very useful right now.  I'm working on it.

Everything has to be sent via sysex for the moment: I don't have code written to make it easy to send CC or NRPN
if you wanted to build a patch which did that.

Popping up a new panel is slow.  Profiling suggests that the primary reason for this is that JComboBox construction
is slow.  So I can't get around it.

