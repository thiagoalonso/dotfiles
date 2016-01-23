SoundWire Server for Linux
--------------------------

For installation instructions please see INSTALL.txt.
For license information please see license.txt and any additional license files.

1) Start the SoundWire Server application. You should see the green message
"Audio capture running at 44.1 kHz" in the GUI, or similar console message. If not then
there is a problem, check the console for details. To see the complete console
output start SoundWireServer from the command line with the -verbose option,
this will display messages from Portaudio. Note that most error messages generated
by Portaudio do not indicate a problem.

2) Press the large button to launch Pulse Audio Volume Control. If it doesn't
start then it may not be installed, or pavucontrol may not be in your search
path. You can also start it from your GUI or from the command line.
If you have no GUI then skip ahead to step 6 (you should configure Pulse
Audio as required manually if SoundWire doesn't work).

3) In Pulse Audio Volume Control go to the Configuration tab, select Internal
Audio profile "Analog Stereo Duplex" or a similar name. Alternatively, try
different configuration profiles if you have problems. SoundWire can also work
with no audio hardware present, in which case the Configuration tab may be
empty. You can also simulate having no audio hardware by selecting profile
"Off", SoundWire should still work properly by monitoring Pulse's dummy output.

4) In Pulse Audio Volume Control go to the Recording tab. Find "SoundWireServer"
(it must be running) and select "Monitor of Internal Audio" or a similar name.
To use other audio inputs such as microphone make another selection as appropriate.
If no selections are possible then there's no audio hardware, or you've selected
the profile "Off" in the Configuration tab.

5) Check the meter (horizontal bar just below the volume controls) for presence
of audio and correct audio level. SoundWire Server is now ready to use!
If you don't see the meter move you must correct your Linux system's audio
configuration and/or make your music player use Pulse Audio.

Summary of Command Line Options
-------------------------------
-nogui     Run SoundWire Server as a daemon (no GUI window, no X server connection).
-p NNNNN   Use the indicated network port number. The next port number (one higher)
           is used for auto-locate. You can also specify the port number by setting
           environment variable SOUNDWIRE_SERVER_PORT. 
-verbose   Write all messages to the console, including those from Portaudio.

48 kHz Audio
------------

SoundWire supports both 44.1 kHz and 48 kHz sample rate audio. The server GUI
displays the sample rate currently being used. The default is usually 44.1 kHz,
however if Portaudio reports a device sample rate of 48 kHz then SoundWire Server
will use 48 kHz. To change the SoundWire Server sample rate, define environment
variable SOUNDWIRE_SERVER_SAMPLE_RATE giving it the value 48000 or 44100.
Make sure to configure the Pulse Audio sample rate to match, otherwise sample rate
conversion may be required, reducing audio quality and placing extra load on the CPU
(see 'man pulse-daemon.conf' and the 'default-sample-rate' setting for more info).
Ideally your audio source material, Pulse Audio, and SoundWire Server should all use
the same sample rate.

Additional Notes
----------------

Pulse Audio Volume Control main volume / mute may affect audio transmitted to
your phone, adjust as needed. You can silence your computer audio by turning the
main volume down but not all the way down (in Output Devices tab). If you can't
turn down main volume without losing SoundWire audio on laptops plug something into
the audio output (headphone) jack.
You may also be able to silence your computer by selecting profile "Off" in
the Pulse Audio Volume Control Configuration tab.

If you have trouble connecting or the IP address indicated by SoundWireServer is
wrong check the beginning of the console output for possible alternate IP addresses
to try.

If you experience audio dropouts caused by poor server performance or when running
other applications we recommend using nice level -19, e.g.
    /bin/nice --19 ./SoundWireServer
This will probably require root privilege. Should show up as level -19 in 'top'.

Please send any feedback to soundwire@georgielabs.net
(c)2012-2015 GeorgieLabs and Georg Feil
