# Digital Civics FM

This repository contains the codebase for Colin, Stuart and Helen's Technologies for Digital Civics project.

# Overview

A focus group of older people expressed a desire for Newcastle University's digital communications to be made accessible to people with low levels of I.T. literacy. We developed Digital Civics FM as a response. This centres on a modified traditional radio which reads out the University's digital communications to the user, along with communications relating to a research area of personal interest to the user. Additionally, the radio features a screen which can display images and text. 

## Features

The radio has a dial to allow the user to select one of four streams:

* Newcastle University's Twitter communications
* Twitter activity relating to the user's research area of interest.
* Newcastle University's Facebook activity
* Newcastle University's Instagram activity

The radio has three buttons - play, stop, and eject.
+ The play button reads out tweets if one of the two Twitter streams is selectd
+ The stop button ends audio playback
+ The eject button toggles the screen in and out of the radio. 

## Using the software

The repository contains two folders; 'forRadioPi' and 'forServerPi'. Two Raspberry Pi computers are required to fully recreate our system.

+ The code within the forRadioPi folder should be loaded onto a Raspberry Pi and placed within the modified radio. The job of this code is to look for user interactions with the radio and then play the appropriate audio files, display the appropriate images on the screen, and/or eject/withdraw the screen. To use this code start with: `python physicalInputs.py`

+ The code within the forServerPi folder should be loaded onto a Pi which does not need to be placed within the radio. The job of this code is to run scripts at regular intervals which:
    - for the Twitter streams: scrapes Twitter and returns tweets including the @uniofnewcastle address, and tweets with a hash tag relating to the user's research interests (which in this case was #breastfeeding). These tweets are parsed to make them clearer then fed into a text to speech convertor. The audio files which are returned are then pushed onto the Pi within the radio.
    - for the Instagram stream: Stuart to complete
    - To use this code ensure you follow the dependencies info below, then simply start the Pi. The Cron file will call all the python scripts as appropriate. 

## Installing dependancies

### serverPi dependencies

Twython is used to scrape Twitter. It must be installed. 
    
    sudo pip install twython
  
You must modify both twythonTool.py and twythonSpecialInterestTool.py (lines 8 to 12 in both files) to include your own Twitter app key, app secret, oauth token, and oauth token secret. 

CereProc is used for the text to speech conversion. To apply for an academic license and to download the code visit: https://www.cereproc.com/en/products/academic 
+ You must include a voice file (heather.voice in our case), a licence file, and the cerevoice_eng python library. These are not included within this repository for copyright reasons. 
+ Within the txt2wavTool.py file (line 41) you must point to the cerevoice_eng/pylib folder. 
+ Within scrapeTwitter.py (line 12) you must point to the licence file and the voice file on your system.

You must modify your Pi's cron file so that the Python files are called at regular intervals.

    crontab -e

Add the lines:

    Stuart to complete
    
### radioPi dependencies

There are no dependencies for this Pi.



## License
The txt2wavTool.py file contains code written by CereProc and is thus subject to their license (contained within the file). All other files were written by Colin, Stuart or Helen for the purpose of this project and are licensed under the MIT license (see below)

Copyright (c) <2016> <Colin Dodds, Stuart Nicholson, Helen Rice>

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
