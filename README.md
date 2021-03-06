# What is wavedeck?

Wavedeck turns a Raspberry Pi into a portable multi-track recording device. 

Connect a multi-channel audio interface and a MIDI device via USB to a Raspberry Pi (or similar) to start recording your band or dawless jams. Send a MIDI note to toggle the recording mode. This will record multi-channel wave files onto your SD card. Some audio interfaces even have integrated MIDI functionality, which eliminates the need for a separate MIDI device. The current recording toggle state is indicated back to the MIDI device to light up a status LED.

# Example setup diagram

![wavedeck-diagram](https://user-images.githubusercontent.com/692826/104786417-8bac4a80-5795-11eb-9c7a-b68e2ef0fb5a.png)


Note that in this setup the audio interface is a Keith McMillen K-Mix, which has a MIDI mode and a "record" button.

# Web interface of wavedeck

You can easily access and download audio files through a built-in web interface directly from a phone or computer. Use the LAN port of your Raspberry Pi or configure its built-in wifi module to connect. Once you are in the same network you should be able to surf to http://raspberry.local.

![wavedeck-web-interface](https://user-images.githubusercontent.com/692826/104780426-77625080-5789-11eb-8891-54cbfe9e81c6.png)

Web interface features:
- display available storage space
- just-in-time zipping and downloading sessions 
- listen back to recordings
- delete recordings and sessions

# Installation and execution

## Installing on Raspberry Pi 3 and above

Run installation script:
`sh install.sh`

## Configure the recorder 

Edit `recorder.py` and configure to your needs. 
Note that if you just run `python3 recorder.py`, it will print out all connected MIDI and audio devices to help you with the configuration. By the way, it is enough to just use a part of the printed name for referencing a device.

Example config:
```
#
# initialize midi
#
midi_portname = "K-Mix Control Surface"
note_rec_button = 84

#
# initialize soundcard 
#
soundcard_name = "K-Mix"
channels = 8
```

## Running wavedeck recorder

The recorder will listen to MIDI notes and start / stop the audio recording.

To start the recorder run 
```
python3 recorder.py
```

## Running wavedeck web interface

To enable the web interface you need to start the server script
```
python3 server.py
```

## How to take care of alsa warnings?

To get rid of alsa warnings, edit this config file:
`sudo nano /usr/share/alsa/alsa.conf`

Comment out these sections as such:

```
#
#  PCM interface
#

# redirect to load-on-demand extended pcm definitions
pcm.cards cards.pcm

pcm.default cards.pcm.default
pcm.sysdefault cards.pcm.default
#pcm.front cards.pcm.front
#pcm.rear cards.pcm.rear
#pcm.center_lfe cards.pcm.center_lfe
#pcm.side cards.pcm.side
#pcm.surround21 cards.pcm.surround21
#pcm.surround40 cards.pcm.surround40
#pcm.surround41 cards.pcm.surround41
#pcm.surround50 cards.pcm.surround50
#pcm.surround51 cards.pcm.surround51
#pcm.surround71 cards.pcm.surround71
#pcm.iec958 cards.pcm.iec958
#pcm.spdif iec958
#pcm.hdmi cards.pcm.hdmi
pcm.dmix cards.pcm.dmix
#pcm.dsnoop cards.pcm.dsnoop
#pcm.modem cards.pcm.modem
#pcm.phoneline cards.pcm.phoneline
```

# MIT License

Copyright (c) 2021 Karl Pannek

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
