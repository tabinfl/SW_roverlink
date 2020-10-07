# SW_roverlink
Audio input and output testing on pi3

Dev setup: Pi3 Model B V1.2  and standard headset connected to a MPOW HC ADC USB adapter.

Notes: 
- pyaudio-record.py and usb-audio-input.py do not run with python3, only pyhton and python 2


1. Connecting USB I/O device
    - The pi audio input/output is default set to ...rpi_simple_soundcard, which i believe is the GPIO pins and/or moniter in which it is connected depending on what the media player/method of playing audio decides.
    - You will need to configure the default device to our USB so that we don't have to manually change it everytime we connect and disconnect it
    https://makersportal.com/blog/2018/8/23/recording-audio-on-the-raspberry-pi-with-python-and-a-usb-microphone
    - check the usb is connected
    - setting up pyaudio
3. Checking the status of the devices
    - "cat /proc/asound/modules" should display 0 snd_usb_audio is what we are looking for, it will display as (index)(name of device)
    - if configurations edited correctly running "alsamixer", hitting the F6 sound card key will display as option 0
    - if the device index can not be changed, edit the program variables to match index of audio input device
4. Running the scripts requires a few more libraries and installs
    https://www.raspberrypi.org/forums/viewtopic.php?t=25173
    - another helpful link for setting up pyaudio aand streaming data
    https://code.google.com/archive/p/pygalaxy/wikis/SoundAnalyse.wiki
    - for import analyse
    - SoundAnalyse measures the loudness/pitch of the USB input in the example
    - Note: this converts the sound data into NumPy 16-bit mono array
    
    
    - pyaudio-record.py r
        - requires pyaudio, wave libraries
        - records audio for a brief moment and outputs to 'output.wav' file
    - usb-audio-input.py requires numpy, pyaudio, analyse
 
 5. Checking the audio that was recorded
    - because my usb audio did not have output, I used the headphone jack and forced the audio to be player thru it using "omxplayer -local xxx.mp3"

 
 More Information:
    https://people.csail.mit.edu/hubert/pyaudio/docs/
    - the pyaudio documentation containing the original examle code
    - Input overflow error occured, resolved in 'usb-audio-input.py' 
 

 
 Common Issues/Solutions:
 - updating the system using "sudo apt-get update" or "sudo rpi-update"
 - IOError: [Errno -9996] Invalid input device means the audio device is not physically connected properly 
 - Input overflow error addressed in comments of 'usb-audio-input.py' 
 - Invalid number of channels is and easy fix: check the number of channels of the device and update the variable in the code accordingly, more at https://www.raspberrypi.org/forums/viewtopic.php?t=71062
 
