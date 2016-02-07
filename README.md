Thumbor Universal Image Prototype
=================================

This is a proof of concept prototype and not production ready.

Installation
------------

Set up a production server.

Install Pyexiv2 and the Thumbor dependencies (Without OpenCV):

    apt-get install ffmpeg libjpeg-dev libpng-dev libtiff-dev libjasper-dev libgtk2.0-dev python-numpy python-pycurl webp python-dev python-pip
    apt-get install python-pyexiv2
    
On Ubuntu 14.04 ffmpeg is not available. Install [Libav](https://wiki.ubuntuusers.de/Libav/) and 
and create a symlink: `sudo ln -s /usr/bin/avconv /usr/bin/ffmpeg`

Create and activate a virtualenv and install all dependencies including Thumbor itself.
Currently the filter requires a custom branch of thumbor which supports xmp metadata.

    pip install -r requirements.txt


Create a `.env` file in the root directory that contains the following line:

    SECURITY_KEY=<your secret key>
    

Start Thumbor with 

    thumbor -c thumbor.conf -p <port>
