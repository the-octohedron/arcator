# ARCATOR
MacOS Application that extends the functionality of the Midi Fighter Twister.  
By running this application you can use the “push” functionality separate from the “push&rotate” functionality.  
The app listens if you turn the encoder while pushing it. If not, it sends an midi signal on release. 

Programmed in VUO, but it can easily be replicated in other programming languages which offer support/have a library for Midi.

## Setting up your Midi Fighter Twister
For this to work, inside the [Midi Fighter Utility.app](https://store.djtechtools.com/pages/midi-fighter-utility) you need to set the Encoder settings > Switch Action Type to "Shift Encoder Hold"

## Making it work with VDMX
As default, the midi changes are send to VDMX. So it should work out of the box.  
In VDMX, I have the "push" linked to a sliders presets, the "push&rotate" to that sliders min envelope and the normal rotate to that sliders max envelope.  

Example .vdmx5 file is included

## Releases
Future compiled versions will be made available as releases, once Resolume support is up and running.

## How it works
The app listens to the midi signals send from the Midi Fighter Twister.
These signals are:
- Rotate encoder: sends CC messages over channel 1
- Push encoder: sends CC messages over channel 2, 127 on push, 0 on release (if encoder is set to "Shift Encoder Hold")
- Push AND rotate encoder: sends CC messages over channel 5 (so you can control another thing with the same encoder, so handy!)  
When the app detects that the encoder is pushed (channel 2) without rotating (no midi received on channel 5), on release of the encoder, the app shoots a midi CC message on channel 15 with value 60


## Dependencies
- Programmed in [VUO](https://vuo.org), so you'll need it installed to open, rund or edit the compositions.


## To Do
- build a release
- Configuring a "dead zone" so that micro rotations when pushing also trigger the "push" functionality

