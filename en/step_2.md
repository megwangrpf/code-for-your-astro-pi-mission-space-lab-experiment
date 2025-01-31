## Getting started

If you have received an official Astro Pi kit from ESA, you have everything you need to develop and test your Phase 2 program for Mission Space Lab (MSL). If you want to, you could even [create your own Astro Pi flight case](https://projects.raspberrypi.org/en/projects/astro-pi-flight-case-mk2), but don't worry, that's not essential, and completion of Mission Space Lab **does not** rely on having the flight case.

### Assembling the hardware

--- task ---
Unpack everything from your kit.

--- /task ---

--- task ---
Take the black hexagonal spacer columns from the small bag that comes with the Sense HAT. Use the accompanying screws to connect them to the bottom of the Raspberry Pi 4.

![Photo of the Raspberry Pi 4 with attached HAT spacers.](images/assembly_spacers.JPG)
--- /task ---

--- task ---
Insert the camera cable into the CSI (Camera Serial Interface) socket on the Raspberry pi.  

[[[rpi-picamera-connect-camera]]]

![Photo of Raspberry Pi with camera cable attached.](images/assembly_cam.JPG)
--- /task ---

--- task ---
Take the Sense HAT and remove the short header if it is attached.

![Photo of the Sense HAT with small header removed.](images/assembly_small_header.JPG)
--- /task ---

--- task ---
Line up the tall header with the corresponding holes on the Sense HAT.  

![Photo of tall header lined up with the Sense HAT.](images/assembly_insert_header.JPG)
--- /task ---

--- task ---
Push the header all the way through. Make sure none of the pins are obstructed and that they are lined up correctly so that they do not become bent.  

![Photo of tall header inserted through the Sense HAT.](images/assembly_sh_header.JPG)
--- /task ---

--- task ---
Feed the camera cable through the slot on the Sense HAT and then sit the Sense HAT onto the Raspberry Pi device. Make sure that all 40 GPIO pins line up with the corresponding holes in the tall header.   

<iframe width="560" height="315" src="https://www.youtube.com/embed/VzYGDq0D1mw" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

![Photo of a Sense HAT fitted on to a Raspberry Pi device with a tall header and camera cable passed through the slot on the HAT.](images/assembly_cam_spacers_sh.JPG)
--- /task ---

--- task ---
Use the four remaining black screws to secure the Sense HAT stack to the spacers. 

![Photo of the Sense HAT with screws securing it to the spacers.](images/assembly_spacer_top.JPG)
--- /task ---

--- task ---
Now take the PIR and remove the foam pin protector block. 

![Photo of PIR with foam pin protector block removed.](images/assembly_PIR.JPG)
--- /task ---

--- task ---
Connect three wires to the pins on the PIR. Note the labels on the back of the PIR circut board which indicate the use of each pin: 

- The GND needs to be connected to corresponding ground pin on the Raspberry Pi
- The VCC needs to be connected to a 3V3 pin on the Raspberry Pi
- The OUT should be connected to [GPIO pin 12](https://projects.raspberrypi.org/en/projects/physical-computing/1) on the Raspberry Pi

![Photo of PIR with wires attached to pins.](images/assembly_PIR_wires.JPG)
--- /task ---

--- task ---
Connect the wires from the PIR to the appropriate GPIO pins on the Raspberry Pi. You can use [the diagrams here](https://www.raspberrypi.org/documentation/usage/gpio/) to help you make sure that you connect the wires to the correct pins. 

![Photo of a Raspberry Pi with wires from the PIR connected to the correct pins.](images/assembly_wires.JPG)
--- /task ---


#### Converting a camera for IR-sensitive Life on Earth experiments

The high-quality camera sensor can detect infrared (IR) light. However, the sensor housing contains an IR filter, which is used to greatly reduce the camera’s sensitivity to IR light.  This is so that the images captured by the high-quality camera sensor look the same as what we see with our eyes (which are not sensitive to IR light). 

If your Life on Earth experiment requires an IR-sensitive camera (like the one on Astro Pi IR), then you will need to convert the high-quality camera sensor you received in your kit by removing the IR filter. If you are programming a Life in Space experiment, or your Life on Earth experiment requires photos to be taken in the visible light spectrum only, then you should not convert your high-quality camera sensor. Please skip to the final assembly steps below. 


--- collapse ---
---
title: Converting a camera for IR-sensitive experiments
---

**Note**: This process cannot be reversed or undone once completed.

--- task ---

Please ensure that you need the IR-sensitive camera before following the [instructions here](https://www.raspberrypi.org/documentation/accessories/camera.html#raspberry-pi-hq-camera-filter-removal).
--- /task ---

Now you can add the DB660/850-25.4 red/NIR dual band pass filter. This been designed primarily for NDVI (Normalized Difference Vegetation Index) imaging applications. By adding it to the High Quality Camera sensor, only reflected red light (660nm) and reflected near-infrared light (850nm) will be captured by the sensor.  See our [NDVI project](https://projects.raspberrypi.org/en/projects/astropi-ndvi) for more information. 

--- task ---
 
Make sure the back focus ring is screwed all the way in. 
![Photo of the high-quality camera sensor with the back focus ring screwed all the way in.](images/filter_backfocus.JPG)

--- /task ---

--- task ---
 
Unscrew the high-quality camera sensor lens cap and the C/CS adapter. 
![Photo of the high-quality camera sensor with C/CS adapter and cap removed.](images/filter_caps.JPG)

--- /task ---

--- task ---
 
Take the filter and sit it onto the hole in the centre of the high-quality camera sensor. 

![Photo of the high-quality camera sensor with the red filter sitting on top prior to installation.](images/filter_rest.JPG)
--- /task ---

--- task ---
 
Gently start turning the filter clockwise using just your fingers, so that the filter screws down into the high-quality camera sensor. Take care not to touch the glass part of the lens and leave greasy fingerprints!

![Photo of the high-quality camera sensor with the red filter being turned by hand.](images/filter_fingers.JPG)

--- /task ---

--- task ---
 
Take the tool provided with the filter and line up the two knobbly bits at each end with the corresponding dimples in the filter. If you have a 3D printer, you might like to print a handle for the tool to make it easier to grip. One of these handles has been printed and sent to the ISS for the astronauts to use when completing the task — but it isn't required. 

![Photo of the high-quality camera sensor showing the filter tool aligned with the filter itself.](images/filter_tool_align.JPG)
--- /task ---

--- task ---
 
Continue gently turning the filter using the tool. Take care not to touch the glass part of the lens with the tool — it will scratch it!

![Photo of the high-quality camera sensor with the red filter being turned using the tool.](images/filter_tool.JPG)

--- /task ---

--- task ---
 
You should start to feel increasing resistance as the filter gets lower. After about nine full turns, the filter should be as low as it can go and you won't be able to turn it any further. Be careful not to over-tighten. 

![Photo of the high-quality camera sensor with the red filter being turned using the tool.](images/filter_turning.JPG)

--- /task ---
--- /collapse ---

#### Final assembly steps 

--- task ---
Insert the other end of the camera cable into the CSI socket on the high-quality camera sensor. 

![Photo of camera cable connected to the High Quality Camera sensor](images/assembly_cable.JPG)
--- /task ---

--- task ---
Remove the cap from the high-quality camera sensor. 

![Photo of camera cable connected to the High Quality Camera sensor, with the cap removed](images/assembly_cap.JPG)
--- /task ---

--- task ---
Remove the C/CS adapter ring from the high-quality camera sensor. 

![Photo of camera cable connected to the High Quality Camera sensor, with the cap and C/CS adapter ring removed](images/assembly_adapt_cap.JPG)
--- /task ---

--- task ---
Remove the caps from the end of the 6mm lens and screw the lens onto the high-quality camera sensor. 

![Photo of lens mounted on the High Quality Camera sensor](images/assembly_6mm.JPG)
--- /task ---

**Note**: The camera sensor in the ESA kit is the same high-quality camera as the one found in the new Astro Pis on the ISS. You can read the [documentation about the HQ camera](https://www.raspberrypi.org/documentation/hardware/camera/), and a lot of detailed technical information can also be found in [the relevant section of the PiCamera library documentation](https://picamera.readthedocs.io/en/latest/fov.html#camera-hardware).

Your Astro Pi kit should now be complete. Insert your SD card, connect to a monitor, keyboard, and mouse and finally plug in the USB-C power lead. For more details on using your Raspberry Pi, take a look at [this guide](https://projects.raspberrypi.org/en/projects/raspberry-pi-getting-started).

![Photo of all the components in the ESA Astro Pi kit assembled together](images/assembly_all.JPG)

#### Performance

The ESA kits for Astro Pi 2020/21 contain Raspberry Pi 4 devices with 4GB of memory (RAM). They are almost identical to the new Astro Pis on the ISS, except that those have 8GB of memory. This means there should be very little difference in performance between the computer on which you develop and test your code and the computer where it actually runs, unless your experiment requires a lot of memory.


### Software and your development environment

After assembling your hardware, you will need to set up your development environment. If you received a kit from ESA, it will contain an SD card with the Desktop version of the Flight OS: a custom-built version of the Raspberry Pi Operating System that you will need.

The packages available in the Desktop Flight OS closely match the ones in the actual Flight OS, the operating system installed on the Astro Pi units on the ISS. However, the Flight OS is a "command-line only" environment that is not really convenient for developing programs and that is why the ESA kits provide a Desktop version that also includes a host of programming tools. Here is a [video tour](https://youtu.be/i57kwOiR7UM) of the 2020 version!

![Screenshot of the Desktop version of the Flight Operating System.](images/os-desktop.png)

You will use this environment to **develop** and **test** the code for your experiment. Making sure that your program runs successfully in this environment is the best way to ensure that your experiment passes our testing procedure and can run on the Astro Pis on the ISS without any modifications.

Please, **do not perform any upgrades or install any additional packages or Python libraries** in this environment as these will not be available when your experiment runs.

--- collapse ---
---
title: Accessing the Desktop Flight OS remotely
---

The Desktop Flight OS runs the VNC Server from RealVNC, so you can use the [compatible VNC client](https://www.realvnc.com/en/connect/download/viewer/) to connect to your desktop from another computer.

You can also connect to the Desktop Flight OS using just a browser. On a machine that is connected to the same network as your Astro Pi kit, open up a browser and type `http://astro-pi-kit.local/vnc.html` in the address bar. This should lead you to the noVNC connection page. Click on the `Connect` button, enter `raspberry` as the password, and you should see the Flight OS desktop in your browser!

![The Desktop Flight OS accessed remotely through a browser window on an Ubuntu machine.](images/noVNC.png)

--- /collapse ---


--- collapse ---
---
title: Downloading Operating System images (optional)
---

If you want to create additional SD cards to use for Astro Pi, you can download the [Desktop Flight OS image file](https://downloads.raspberrypi.org/AstroPi_latest) used in the ESA kits. After downloading, you can use any software tool to write the image file to your own SD card. See [this guide](https://www.raspberrypi.org/documentation/installation/installing-images/) for instructions on how to do this.

--- /collapse ---

--- collapse ---
---
title: Sample data
---

The Desktop version of the Flight OS also contains a `Data` folder with sample data from a previous mission, which can be used to help test and refine your code. You can also download this [sample data](https://rpf.io/ap-sample-data) separately.

#### Sensor readings

There is a comma-separated values (CSV) file with 3 hours worth of data from all of the Sense HAT sensors. The columns in this file are in this order:

Date
Time
Humidity
Temperature
Pressure
Pitch (as measured by gyroscope)
Roll (as measured by gyroscope)
Yaw (as measured by gyroscope)
Pitch (as measured by accelerometer)
Roll (as measured by accelerometer)
Yaw (as measured by accelerometer)
Raw accelerometer X value
Raw accelerometer Y value
Raw accelerometer Z value
Raw magnetometer X value
Raw magnetometer Y value
Raw magnetometer Z value
Latitude degrees
Latitude minutes
Latitude seconds
Longitude degrees
Longitude minutes
Longitude seconds

LibreOffice Calc is a spreadsheet program similar to Microsoft Excel and is installed on the Desktop Flight OS. You can use this to look at the data and plot charts.

#### Images

There is also a sequence of photos taken by the Mark I Astro Pi IR camera. The sequence starts at 'night', and so the first few photos are black.

![Completely black photo taken during the "night" using a Mark I Astro Pi IR camera](images/zz_astropi_1_photo_116.jpg)

Then, the window gradually appears as light starts to flood in.

![A photo taken at "dawn" using a Mark I Astro Pi IR camera. The Earth is not visible yet and the Astro Pi is reflected on the nadir window](images/zz_astropi_1_photo_133.jpg)

By image 150, the Earth below becomes visible.

![A photo of the Earth becoming visible after "dawn", taken using a Mark I Astro Pi IR camera. The sun is still reflected on the sides of the nadir window.](images/zz_astropi_1_photo_159.jpg)

And eventually, the area surrounding the window cannot be seen at all.

![A photo of the Earth taken using a Mark I Astro Pi IR camera](images/zz_astropi_1_photo_193.jpg)

You could use these images to train a machine learning algorithm to recognise different types of views. However, please note that there is no guarantee that the location, view, and orientation of the Astro Pi will be exactly the same when your program runs on the ISS. Therefore, your program should be flexible enough to adapt to any changes.

--- /collapse ---
