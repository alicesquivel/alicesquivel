---
description: >-
  After you have trained your model, you will need to use rsync again to get it
  onto the car.
---

# Syncing Model to Car

**Syncing the Model to the Cars**

1. To move the model file from the Chameleon Node to the cars, run the following command on the car inside of the donkeycar container:

<pre><code><strong>rsync cc@&#x3C;Chameleon_Floating_Ip_Address>:~/mycar/models/&#x3C;model_name> ~/car/models
</strong></code></pre>

2. Be sure to also sync the my\_config.py file since this could affect how the pi interprets the model

```
rsync cc@<Chameleon_Floating_Ip_Address>:~/mycar/my_config.py ~/car/my_config.py
```

_Note: \~/mycar/models/\<model\_name: is a file path and if the naming of the directories are not within convention, it could lead to errors._&#x20;

\
