---
description: >-
  Before you can train a self-driving model, you must drive it around yourself
  to collect training data.
---

# Collecting Data

**Collecting Data with the Cars**

1. Inside the donkeycar container running on the car start the driving program:

```
cd ~/car
python3 manage.py drive
```

2. Open up a window and input the device’s public IP into the search bar with port 8887. You can find the public ip by navigating back to the Chi@Edge dashboard and looking under Network->Floating Ips

```
<devic_public_ip_address>:8887
```

This should open a browser where you can view the output of the camera and drive with a joystick/gamepad

3. To drive with the physical game controller, you will need to click on gamepad. Depending on the pwm value you set for forward throttle, you may need to set the maximum throttle percentage to less than 100% in order to control the car.

**Data Collection Tips**

1. Trash folder to store practice data

When you begin driving, you may make some mistakes like going off of the track. We want to make sure that the data we use to train the model is good data without mistakes. The next page will explain how to clean up bad data. However, if you want to just drive around and not worry about filling up the data directory with bad data, you can create a new subdirectory within data.

```
cd ~/car/data
mkdir trash
```

Then you can edit the myconfig.py file to store newly collected data in this subdirectory.

```
cd ~/car
nano myconfig.py
```

Uncomment these top three lines and change the directory of DATA\_PATH

```
import os
# 
# #PATHS
CAR_PATH = PACKAGE_PATH = os.path.dirname(os.path.realpath(__file__))
DATA_PATH = os.path.join(CAR_PATH, 'data/trash')
```

2. Amount of data needed

When the data is collected and stored as records in the data directory or whatever path you are telling it to save the data. These records consist of .catalog files, images directory, and manifest files. Catalog files are where your steering and throttle values are recorded while driving. Each of these corresponds to an image in the images directory based on their id number. Catalog\_manifest files store information about each catalog file and the manifest.json file is where certain records are marked for deletion. The number of records you have can be discerned from the number of catalog files since each catalog file can only contain up to 1,000 records. In order to see any kind of behavior from your model, it is recommended that you collect 10,000 records. We found that in order to train a working model, almost 30,000 records are needed.
