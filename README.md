# Telepresence System for Remote Participant

## Overview

![Alt text](telepresence_system.png?raw=true "System Architecture")

This system allows remote users to participate in live events (football matches, concerts) from their homes as if they were in the real places.
360 video/audio captured from a 360 camera located at a remote site are streamed to the user's location using ``WebRTC protocol``, which are watched by users using VR Headsets. The user can interact with people in the remote site using his/her voice. When testing in local networks, the one-way delay of the system is approximately 0.3-0.5 sec for 2K video at 30fps.

For ``WebRTC``, the signalling between the local and remote peers are carried out using a ``WebSocKet``-based server. Ricoh Theta V camera is used to record 360-degree video. At the user side, HTCV Vive Pro Eye VR Headset is used to display 360 video.

 - Remote Agent: Google Chrome on Windows 10 (It is OK to use MacOS, but you will nedd to manually compile and install the driver (https://github.com/ricohapi/libuvc-theta/tree/theta_uvc). Tested on Ubuntu 20.04 but currently not working)
 - Local Agent: Google Chrome / Firefox on Windows 10 (in order to support HTC Vive Pro Eye Headset)
 - Signalling Server: Same PC as the remote agent

## How to use
### 1. Install driver for the camera
Connect the camera to a Windows 10 PC via USB cable. Run file ``UVC4K_setup64_en.exe`` and follow instructions to install driver for Ricoh Theta V camera.

### 2. Install required softwares for remote agent
Download and install ``Python`` (version 3.9), then using ``pip`` to install ``WebSockets`` package.

``
pip install WebSockets
``

Download and install ``Node.js`` (https://nodejs.org/en/download/).

Download and install ``Google Chrome`` browser.

### 3. Install required softwares for local agent
Connect HTC Vive Pro headset to the computer.
Download and install ``Google Chrome`` browser.

### 4. Start servers (on the remote agent)
Change the default ip adress at line 323 of file ``signalling\simple_server.py`` to the ip address of the remote agent, then start the WebSocket server:

``
cd telepresence_VR\signalling
python simple_server.py
``
Open Google Chrome on the remote agent, then go to: https://websocket-server-ip-address:8443 and accept self-signed certificates for this site. Do the same thing on the local agent.

