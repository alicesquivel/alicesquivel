---
description: >-
  After collecting a large sample of data, you will likely have some bad data
  consisting of mistakes while driving. It is important that bad data is removed
  before training.
---

# Cleaning Data

**Cleaning the Data Process**

_The following steps can be done from either the raspberry pi or the baremetal Chameleon instance. If using the baremetal instance, the steps will be the same except you will have to use the ip address associated with that instance instead of the ip address of the pi_

1. Run the following command in your car's directory

```
donkey tubclean <data_filepath>
```

example:

```
donkey tubclean ~/car/data
```

2. Open a web browser and enter the ip address with port 8886 as the URL

```
<edge_device_ip_address>:8886
```

3. This should open the tubclean user interface. You should see links to the subdirectories within your data folder. If you instead see a list of your catalog files, you will have to rerun the command with the path to just the car as your file path.

```
donkey tubclean ~/car
```

4. In the tubclean user interface, click on one of the data subdirectories. Here you can watch the data you recorded as a movie and select portions to be deleted. Here is the usual workflow:
   1. Watch through the video until you see a mistake
   2. Right before a mistake happens, press (c) on the keyboard to split the video. The top video now consists of all frames before the split and the bottom video is all frames from the split until the end.
   3. Watch the bottom video until the mistake is over.
   4. Press (c) to split the video again, now leaving the mistake contained within the middle video.
   5. Repeat this process for all mistakes in the video. When you are done, check the boxes next to all videos containing mistakes. Then, select the save and delete button a the bottom.
