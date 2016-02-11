Thumbor Universal Image Prototype
=================================

This is a proof of concept prototype and not production ready.

Installation
------------

Set up a production server.

Install Pyexiv2 and the Thumbor dependencies (Without OpenCV):

    apt-get install ffmpeg libjpeg-dev libpng-dev libtiff-dev libncurses5-dev libjasper-dev libgtk2.0-dev python-numpy python-pycurl webp python-dev python-pip libcurl4-openssl-dev
    apt-get install python-pyexiv2
    
On Ubuntu 14.04 ffmpeg is not available. Install [Libav](https://wiki.ubuntuusers.de/Libav/) and 
and create a symlink: `sudo ln -s /usr/bin/avconv /usr/bin/ffmpeg`

Install all dependencies including Thumbor itself.
Currently the filter requires a custom branch of thumbor which supports xmp metadata.

    sudo pip install -r requirements.txt


Create a `.env` file in the root directory that contains the following line:

    SECURITY_KEY=<your secret key>
    
Create a file `/etc/nginx/conf.d/thumbor.conf` with the following content:
    
    upstream thumbor {
        server 127.0.0.1:8000;
    }
    server {
        listen 80;
        server_name <server name, e.g. *.compute-1.amazonaws.com>;
        location / {
            proxy_pass http://thumbor;
        }
    }


Start Thumbor with 

    thumbor -c thumbor.conf -p 8000
