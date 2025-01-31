## A big worked example

Here is an example of an Astro Pi Mission Space Lab experiment idea: the team from CoderDojo Tatooine wants to investigate whether the environment on the ISS is affected by the surface of the Earth it is passing over. Does the ISS get hotter when it passes over a desert, or wetter when it is above the sea?

This example will serve as a template, to illustrate how you can combine all the elements described so far in this guide to plan and write your computer program.

For this particular example, the program for the experiment should:
- Take regular measurements of temperature and humidity every 30 seconds, and log the values in a CSV file
- Calculate the ISS’s latitude and longitude and log this information in the CSV file
- Take a photo using the camera on Astro Pi IR, which is pointing out of a window towards Earth, to gather data on whether cloud cover might also be a factor
- Write the latitude and longitude data in the CSV file and also into the EXIF tags of the images, which have sequentially numbered file names
- Handle any unexpected errors and log the details

### Planning your coding sessions

To help with planning, we've put together some useful tips for Phase 2 that will facilitate your team's coding.

--- collapse ---
---
title: Tips for planning and running coding sessions
---

### How to approach writing the program for Phase 2 of Mission Space Lab

+ Read through this guide. Familiarise yourself with the requirements that your program must meet so that it can advance to the next phase and run smoothly on the Astro Pis on the ISS. Read the useful tips provided throughout on how to best to develop your program and make the most of your experimental results.

### Work out the key tasks

+ Get your team together and start to map out the rough outline of how your program will work. You could do this as a group and have everyone call out their ideas, or all team members could work individually and then get together to compare results.

+ Use a whiteboard or big sheet of paper to list all of the key tasks that your program will need to perform. You don’t need to worry about the order or the actual functions and commands at this stage — just note down the specific things that need to be achieved. This is what that would look like for the example scenario above:

![The key tasks for the Mission Space Lab experiment idea by the team from CoderDojo Tatooine](images/Astro_Pi_Educator_Focus_Graphics_V6a.png)

+ Have a closer look at each task and think about whether it can be split into smaller subtasks. Moreover, are there any actions that can be sensibly combined with one another? Also, see if there are any tasks that need to be repeated.

![Some of the key tasks that involve writing data to a file can be combined together](images/Astro_Pi_Educator_Focus_Graphics_V6b.png)

+ Try to put everything into a logical order, using lines to connect the various tasks. It will start to get messy, but that’s good! You will probably discover that there are some obvious repeated tasks. This is a good time to introduce or reinforce the programming concepts of repetition and loops.

![Arrange the key tasks into a logical order](images/Astro_Pi_Educator_Focus_Graphics_V6c.png)

+ If there are any repeated tasks, do they appear just once in your diagram, with flow lines passing through many times, or do they fit in in multiple places? Talk with your team about how repeated tasks should only be coded once, so that parts of the program can be reused.

### Create a flow chart

+ Take a fresh sheet of paper or find a clean area on your whiteboard (be sure to copy or take a photo of your first picture before you erase anything). Reconfigure the steps and flow into a more ordered diagram, maybe running clockwise around the paper or starting at the top and working downwards. Try a few different versions and see which one is the easiest to follow. Include a ‘start’ and ‘end’ block to make it very clear where the program begins and finishes. Are there any actions that you need to perform at these stages? The final result is what is called a flow chart: a diagram of all of a program’s tasks, in the right order, but doesn’t contain any actual programming language commands.

![Create a flow chart](images/Astro_Pi_Educator_Focus_Graphics_V6d.png)

+ Work through your task list and try to identify any missing pieces. Add any missing functionality into your flow chart.

+ You should also think about where in your program you should be looking to handle exceptions and errors. Most experiments will have a main loop that runs repeatedly over the 3-hour period. An unexpected error encountered in this loop could be disastrous if it causes the program to stop or stall and prevent further data collection. So, think of some ‘what if’ scenarios. For example, if you’re reading data from a sensor, what will happen if it gives you an unexpected result? Will your program cope with this? How are you dealing with hardware errors?

### Assign tasks to members of the team

+ Give descriptive names to each task block.

+ Assign responsibility for each block to different members of the team. Try to think about the individual team members’ experience levels and programming ability and allocate tasks accordingly. Depending on the number of people in your team and the complexity of your program, it may be sensible to have more than one person allocated to a specific block or function.

+ Remember that someone needs to be responsible for the scaffold of the final program that will contain the various function calls in the right order.

### Get coding!

+ You will probably discover that some functions are really easy to create using the recommended Python libraries, perhaps even with only a single line. Others will be more complex, and we have included some useful code snippets in the coding requirements document (e.g. for adding latitude and longitude information to the EXIF data of a photo) that you can copy into your project. To design more complicated functions, if needed, you can use the same pseudocode approach that you used with the program as a whole.

+ Remind your team that they cannot install additional Python libraries or access the internet on the Astro Pi computers aboard the ISS, so they should not use any commands that make a web request or look up something from an online source.

+ Encourage each team member or subteam responsible for a specific part of the program to code their section so that it works by itself, just like the examples in the coding requirements document. Suggest that they add comments and docstrings as they go along.

+ Get together regularly to discuss progress and work through any major challenges as a group. It is useful to update your pseudocode flow diagram to reflect any changes that your team realise are necessary as they write the actual program.

![Update the flow chart to reflect changes that become necessary as the program evolves](images/Astro_Pi_Educator_Focus_Graphics_V6e.png)

+ Keep the deadline for submitting your program in mind. If time is running out, are there any parts of your program that can be left out? If you are planning on performing analysis of results in real time, can this instead be done after your program has run, when you’ve got your results back?

### Test your program

+ Don’t forget to test your program in the Desktop version of the Flight OS: open a terminal, type `python3 main.py` and make sure your program terminates after 3 hours without generating any errors (including any exceptions that may have been caught and recorded in the log). 
+ Check that the data and images captured by your program match what you would expect. 
+ Make sure you go through the requirements checklist in the last step of this guide. 

--- /collapse ---

### The experiment code

Here is what the final code that implements the experiment idea might look like:

```python
from pathlib import Path
from logzero import logger, logfile
from sense_hat import SenseHat
from picamera import PiCamera
from orbit import ISS
from time import sleep
from datetime import datetime, timedelta
import csv

def create_csv_file(data_file):
    """Create a new CSV file and add the header row"""
    with open(data_file, 'w') as f:
        writer = csv.writer(f)
        header = ("Counter", "Date/time", "Latitude", "Longitude", "Temperature", "Humidity")
        writer.writerow(header)

def add_csv_data(data_file, data):
    """Add a row of data to the data_file CSV"""
    with open(data_file, 'a') as f:
        writer = csv.writer(f)
        writer.writerow(data)

def convert(angle):
    """
    Convert a `skyfield` Angle to an EXIF-appropriate
    representation (rationals)
    e.g. 98° 34' 58.7 to "98/1,34/1,587/10"

    Return a tuple containing a boolean and the converted angle,
    with the boolean indicating if the angle is negative.
    """
    sign, degrees, minutes, seconds = angle.signed_dms()
    exif_angle = f'{degrees:.0f}/1,{minutes:.0f}/1,{seconds*10:.0f}/10'
    return sign < 0, exif_angle

def capture(camera, image):
    """Use `camera` to capture an `image` file with lat/long EXIF data."""
    location = ISS.coordinates()

    # Convert the latitude and longitude to EXIF-appropriate representations
    south, exif_latitude = convert(location.latitude)
    west, exif_longitude = convert(location.longitude)

    # Set the EXIF tags specifying the current location
    camera.exif_tags['GPS.GPSLatitude'] = exif_latitude
    camera.exif_tags['GPS.GPSLatitudeRef'] = "S" if south else "N"
    camera.exif_tags['GPS.GPSLongitude'] = exif_longitude
    camera.exif_tags['GPS.GPSLongitudeRef'] = "W" if west else "E"

    # Capture the image
    camera.capture(image)


base_folder = Path(__file__).parent.resolve()

# Set a logfile name
logfile(base_folder/"events.log")

# Set up Sense Hat
sense = SenseHat()

# Set up camera
cam = PiCamera()
cam.resolution = (1296, 972)

# Initialise the CSV file
data_file = base_folder/"data.csv"
create_csv_file(data_file)

# Initialise the photo counter
counter = 1
# Record the start and current time
start_time = datetime.now()
now_time = datetime.now()
# Run a loop for (almost) three hours
while (now_time < start_time + timedelta(minutes=178)):
    try:
        humidity = round(sense.humidity, 4)
        temperature = round(sense.temperature, 4)
        # Get coordinates of location on Earth below the ISS
        location = ISS.coordinates()
        # Save the data to the file
        data = (
            counter,
            datetime.now(),
            location.latitude.degrees,
            location.longitude.degrees,
            temperature,
            humidity,
        )
        add_csv_data(data_file, data)
        # Capture image
        image_file = f"{base_folder}/photo_{counter:03d}.jpg"
        capture(cam, image_file)
        # Log event
        logger.info(f"iteration {counter}")
        counter += 1
        sleep(30)
        # Update the current time
        now_time = datetime.now()
    except Exception as e:
        logger.error(f'{e.__class__.__name__}: {e}')
```

Here's a snippet from the `data.csv` file that is produced:

```
Counter,Date/time,Latitude,Longitude,Temperature,Humidity
1,2021-02-24 10:46:39.399823,39.740617143761526,3.3473845489216094,27.4958,42.934
2,2021-02-24 10:47:10.221346,38.53934241569049,5.26367913685018,27.6456,42.7503
3,2021-02-24 10:47:40.890616,37.309551077336856,7.1032053271899365,27.7018,42.5886
4,2021-02-24 10:48:11.571371,36.047429941325575,8.879601929060437,27.5894,42.6544
```

Note that exception handling in this program is rather crude: all raised exceptions will be caught and logged. This means that such a program is very unlikely to terminate abruptly and display an error. Even if errors are generated and the program fails to achieve its goal, this will only become apparent by checking the log files for errors. When testing your program, make sure you also check any log files it generates.
