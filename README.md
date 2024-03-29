# ARCATOR
MacOS Application that extends the functionality of the Midi Fighter Twister.  
By running this application you can use the  **“push”** functionality separate from the **“push&rotate”** functionality.  
The app listens if you turn the encoder while pushing it. If not, it sends an midi AND OSC signal on release. 

Programmed in [VUO](https://vuo.org), but it can easily be replicated in other programming languages which offer support/have a library for Midi.

## Setting up your Midi Fighter Twister
For this to work, inside the [Midi Fighter Utility.app](https://store.djtechtools.com/pages/midi-fighter-utility) you need to set the Encoder settings > Switch Action Type to "Shift Encoder Hold"

## Making it work with VDMX
As default, the midi changes are send to VDMX. So it should work out of the box.    

Example .vdmx5 file is included  
I have the "push" linked to the sliders presets, the "push&rotate" to that sliders min envelope and the normal rotate to that sliders max envelope.

## Making it work with other software
- Broadcasts OSC messages to the entire localhost. Listen to port 7000 and to addresses **/midifighter_0** till **/midifighter_15** (or higher)
- You can edit the .vuo file so it sends midi to other apps instead of "To VDMX"

## How it works
The app listens to the midi signals send from the Midi Fighter Twister.
These signals are:
- Rotate encoder: sends CC messages over channel 1
- Push encoder: sends CC messages over channel 2, 127 on push, 0 on release (if encoder is set to "Shift Encoder Hold")
- Push AND rotate encoder: sends CC messages over channel 5 (so you can control another thing with the same encoder, so handy!)  

When the app detects that the encoder is pushed (channel 2) without rotating (no midi received on channel 5), on release of the encoder, **two things happen**:
- the app cycles through sending a midi CC message on channel 14,15,16 with a value of 60 at "To VDMX"
- the app shoots out a OSC message on the localhost at port 7000 with the message address of /midifighter_\[CC number\] and a value of 60

The \[CC number\] number in the OSC message address corresponds to the incomming CC. As default, this is 0 to 15, which corresponds to the 16 encoders of the Midi Fighter Twister.

## Dependencies
- Programmed in [VUO](https://vuo.org), so you'll need it installed to open, rund or edit the compositions.

## To Do
- Configuring a "dead zone" so that micro rotations when pushing also trigger the "push" functionality

