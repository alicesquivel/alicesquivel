---
description: Your device must be enrolled to Chi@Edge before it can be accessed.
---

# Adding Pi to Chi@Edge

**Requirements**

Before you begin, you will need to have an SD card and SD card reader in order to flash the Chi@Edge image onto your device. You will also need an SD flashing application installed. The [Chi@Edge docs](https://chameleoncloud.gitbook.io/chi-edge/) recommend using [Balena Etcher](https://etcher.balena.io/) and that is what we used as well. You will also need to have access to Chi@Edge, which requires being added to a project.

**Enrolling your Raspberry PI in Chi@Edge**

It is highly recommended that, in addition to our steps below, you should also read the [Chi@Edge docs](https://chameleoncloud.gitbook.io/chi-edge/). The docs are thorough enough so that you could add your Pi successfully without any assistance, but we also supply some additional tips and help below for each step.

1. Installing the SDK

```
# create a virtualenv
python3 -m venv .venv

# activate it
source .venv/bin/activate

# install the SDK
pip install python-chi-edge
```

This step uses a Python virtual environment so that the chi-edge package can be installed using the correct dependencies. You will need to be in this virtual environment whenever you want to use chi-edge commands. To reactivate the virtual environment, run the second command again.

2. Authenticating to Chi@Edge

It is required that you use an application credential when registering your device. You can create an application credential on the Chi@Edge dashboard in Identity->Application Credentials or by clicking this [link](https://chi.edge.chameleoncloud.org/identity/application\_credentials/). Once on the application credentials page, click the button to "Create Application Credential". Set the name and expiration date for the application credential. You can also set the secret. If you do not set the secret, a complicated one will be generated for you, so you can set it to "123" or something easy to remember. Click the blue "Create Application Credential" at the bottom right of the page. After this, you should click the button to download the application credential. Take note of where this is saved on your computer. Once this is done, run this command in your terminal.

```
source <path to credential>
```

example:

```
source ~/Downloads/app-cred-edge-openrc.sh
```

3. Registering Your Device

You can use the following command to register the device. You will have to use the id and secret from the application credential you created. The device name should be something descriptive so that you can identify it easily on Chi@Edge. The name should include information about your location or project, as well as the type of the device. For example, our device name was uc-rpi4-racer.

```
chi-edge device register \
  --contact-email <contact_email> \
  --application-credential-id <application_credential_id> \
  --application-credential-secret <application_credential_secret> \
  --machine-name raspberrypi4-64 \
  <device_name>
```

4. Viewing Your Registered Devices

You can see your device on the list by running the following command. You should keep this screen up, since you will need the device's uuid later.

```
# List all devices
chi-edge device list
```

5. Imaging Your Device

After you download the image for raspberry pi 4 off of the docs, take note of where it is saved. You will need to replace \<image> in the following command with the path to the image file. You should also copy the device's uuid from the output of the previous command and replace \<uuid> with that. You must bake the image using the following command before you can flash it to the pi.

```
chi-edge device bake --image <image> <device_uuid>
```

6. Flashing the Image

Place the SD card into your SD card reader. Open Blanea Etcher or your choice of SD card flashing software. You will need to select the image that you downloaded to be flashed onto the car.

7. Wi-Fi Configuration

Note: This step is not covered in the Chi@Edge docs and it is very important so that your pi can connect to wifi.

On your computer, create a new file called "resin-wifi"

```
nano resin-wifi
```

In this file, you will include information on the Wi-Fi network you want the pi to connect to. The contents of this file will almost certainly be different because it depends on your own Wi-Fi network. Below, we provide the contents of the file if you plan to connect to the eduroam Wi-Fi network. Eduroam is a network found at many colleges and universities across the country, so it may be available for you to use. If you don't have access to eduroam, you will have to look up the details for your own network.

Resin-wifi for eduroam:

```
[connection]
id=eduroam
type=wifi

[wifi]
ssid=eduroam
mode=infrastructure
security=802-11-wireless-security

[wifi-security]
key-mgmt=wpa-eap

[802-1x]
eap=peap;
identity=<EDU_EMAIL>
phase2-auth=mschapv2
password=<EDU_Password>
private-key-password-flags=1
phase2-private-key-password-flags=1

[ipv4]
method=auto

[ipv6]
method=auto
```

Now, you will need to copy this file onto your SD card. The file will need to go in the system-connections folder. You can do this by opening your file browser and dragging the resin-wifi file into the proper location in the SD card, or you can run this command in the terminal.

```
cp resin-wifi /Volumes/resin-boot/system-connections
```

After this has been done, you can eject the SD card. Making sure you pi is turned off, place the SD card into the SD slot of the pi. After the SD card is in place, you can turn your pi on.

8. Manage Which Projects can use Your Devices

Back in the terminal of your computer, you can set your project as authorized to use your pi.

```
chi-edge device set \
    --authorized-projects <project_name> \
    --authorized-projects-reason "special reason here" \
    <device_name_or_uuid>
```

9. Wait for Pi to be Active on Chi@Edge

It will take some time before your pi is active on Chi@Edge. You can check its status by running:

```
chi-edge device list
```

When the device is ready, its health should be at 4/4. You can also check if it is ready by looking on the Chi@Edge device calendar for the name of your pi.
