﻿# Amcrest-Camera

Amcrest IPM-721 & IP2M-841 DeviceType, now with LIVE Video!

The Amcrest 720P and 1080P cameras are packed with an impressive feature set for their relatively low cost. This Device Type allows for some integration into the ST platform and will hopefully help out other community members.

This is my first Groovy coding attempt, so do not be surprised if I have to make a number of bug fixes. I will be making adjustments/fixes as I continue to develop this further, so feel free to ask for other features and I will try to accomodate them. I am planning to eventually create a SmartApp for my cameras using this DeviceType.
Features:

    LIVE Video Streaming (as of version 2.0.0)!
    Snapshot Image Capture and Carousel Display
    Full PTZ (Pan-Tilt-Zoom) Functionality (Up/Down/Left/Right/Zoom In/Zoom Out)
    Adjust PTZ Speed (range slowest <1> to fastest <8>)
    Toggle Motion Detection On/Off
    Adjust Motion Detection Sensitivity (range of least sensitive <1> to highest sensitivity <6>)
    Set Night Vision On/Off/Auto
    Move to Preset ¹ (available presets 1 -> 6)
    Toggle Camera Image Flipping On/Off
    Toggle Camera Image Mirroring On/Off
    Set Camera Image Rotation Clockwise/Counter-Clockwise/Off
    Remote Camera Reboot
    Supports either a Local IP Address or a Public DNS entry
    Switch Video Recording Off/On/Auto ²
    Verbose Debugging Switch On/Off
    Exposed commands that can be access via Rule Machine (RM)

Please Note:

    If either the Hostname/IP or Port are changed after executing any request, you may have to edit the devices in the IDE and change the Device Network Id to some string (e.g. "TEST01") before attempting a new action.
    If you receive a partial image, or no image at all, and you are using a local IP address, this is most likely occurring because of a ST timeout waiting for a HubAction response.
    When using a local IP (HubAction), reduce the Snapshot Quality to lessen the likelihood of a timeout occurring ³ (see Amcrest Web View configuration).

¹ Presets:

    Preset buttons 1 -> 6 must first be defined in the camera (see Amcrest Web View configuration).

² Video Recording:

    Recording to the Camera MicroSD Card only, which must be configured in the camera (see Amcrest Web View configuration).
    All camera actions (PTZ, Zoom, etc.) perform during recording will appear in the recorded video.

³ Image Quality:

    For the IP2M-841B a snapshot at the highest Quality setting (6) is approximately 200 KB in size and at the lowest setting (1) it is approximately 50 KB in size, in my experience.
    It has been speculated that most images over 40 KB begin to have problems with local IP communication with ST.
    While the timeout may still occur with a lower Quality_ setting, especially with the 1080P version of the camera, this is much less likely to occur when using a public IP. I experienced no issues grabbing an image at the highest setting (6) when using a public IP.
    In all honesty, using a local IP failed to return an image more times than not, so I use a public IP (DDNS) for all of my cameras.
    In addition, you may need to restart the Hub (unplug for 10 seconds, plug back in, wait for the green light) between failed image attempts while adjust the Quality setting.

Exposed Commands

The following device commands are exposed by the DTH:

    appVersion
    changeNvLED
    changeRecord
    changeRotation
    moveDown
    moveLeft
    moveRight
    moveUp
    presetCmd1
    presetCmd2
    presetCmd3
    presetCmd4
    presetCmd5
    presetCmd6
    rebootNow
    setLevelSpeed
    setLevelSensitivity
    toggleFlip
    toggleMirror
    toggleMotion
    zoomIn
    zoomOut

Amcrest Web View configuration

The following steps will guide you to the correct settings within the Amcrest Web View applications for the specified topic. These steps assume that you have logged in under the admin user account or an account with equivalent permissions.

    Set Presets: Live (Header) -> PTZ (Footer) -> PTZ Settings (Right Panel) -> Preset (Dropdown) -> Position view to desired point -> Enter # -> Select + Add
    Set Snapshot Quality: Setup -> Camera -> Video -> Snapshot -> Quality (Dropdown)
    Set SD Card for Video Record: Setup -> Storage -> Destination -> Path -> SD Card (check the box)

Installation:

(These installation/setup notes are purposely very detailed to help ST newcomers... a picture is worth a 1,000 words!)

1) Sign in to the SmartThings IDE and select My Device Handlers.
2) Click the Settings button:

3) Click on Add new repository and fill in the highlighted fields:

4) Click on Save.
5) Click on Update from Repo and then select Amcrest-Camera (master):

6) Check the box next to New (only in GitHub) item:

7) Check the Publish box then click the Execute Update button.
8) Click on My Devices then click the + New Device button:

9) Fill in the device fields similar to these values (Type is the only fields that must match):
Create_Device.PNG446x700 36.3 KB

10) Click the Create button.
11) Go into the SmartThings mobile app and select Marketplace where you should see and select:

12) Fill in the fields below and select Next when finished with page 1, then select Done:
Install_Screen.PNG1601x2025 607 KB

NOTE: The camera default "Video Channel" is usually set to 0.

You should now see your new device available in your Things list. Enjoy!

A final word of thanks to the ST Community for all of their non-code-related help (@JDRoberts that's a nod to you) and to all of the coders who help make this platform a fun hobby, with specific nods related to this DTH going to:

    @pstuart For the efforts he put into his Generic Camera device and various posts. Very educational!
    @tgauchat and @RBoy : For the "convertHostnameToIPAddress" macro.
    @slagle, @eparkerjr and @scottinpollock For their efforts on the great Foscam & D-Link device types.
    RBoy again: For the code making the JPEG image available to other apps.
