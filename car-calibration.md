---
description: >-
  Calibrating your car's steering and throttle pwm values are important so that
  it can drive correctly
---

# Car Calibration

**Calibrating the Cars**

1. Connect your personal computer to the car and go into the donkeycar container: (steps as of Jun 29, 2023; hope to have ssh in future)
   1. log into Chi@Edge dashboard
   2. Go to containers and find your container
   3. Click on the console tab
2. Run the following command to calibrate the steering:

```
donkey calibrate --pwm-pin=PCA9685.1:40.0
```

This will prompt you to input pin values for steering. Test out 360 and then 300 and 400 (etc.) in order to test the optimal number, it can be different for every car, note the optimal number for left and right turns.

3. Make sure that the numbers remembered for left and right turns are not causing the car to “whine.”
   1. Remember which values correspond to the wheels turning all the way to the right and all the way to the left
   2. For reference, our value for maximum left steering was 520 and maximum right steering was 260
4. Run the following command to calibrate the throttle:

```
donkey calibrate --pwm-pin=PCA9685.1:40.1
```

_This will prompt you to input pin values for the throttle. Test out 360 and then 300 and 400 in order to test the optimal number, it can be different for every car, not the optimal number for throttle speed. For reference, our throttle pwm values were 410 for forward, 370 for stopped, and 300 for reverse. Yours might be different depending on what you want the max speed of your car to be._

5. Change the pwm steering values within the myconfig.py with the optimal ones found in steps 1 and 2:
   1. nano myconfig.py
      1. The variable is named PWM\_STEERING\_THROTTLE and various steering parameters can be modified.
   2. example:

```
PWM_STEERING_THROTTLE = {
     "PWM_STEERING_PIN": "PCA9685.1:40.1",   # PWM output pin for steering servo
     "PWM_STEERING_SCALE": 1.0,              # used to compensate for PWM frequency differents from 60hz; NOT for adjusting steering range
     "PWM_STEERING_INVERTED": False,         # True if hardware requires an inverted PWM pulse
     "PWM_THROTTLE_PIN": "PCA9685.1:40.0",   # PWM output pin for ESC
     "PWM_THROTTLE_SCALE": 1.0,              # used to compensate for PWM frequence differences from 60hz; NOT for increasing/limiting spe>
     "PWM_THROTTLE_INVERTED": False,         # True if hardware requires an inverted PWM pulse
     "STEERING_LEFT_PWM": 520,               #pwm value for full left steering
     "STEERING_RIGHT_PWM": 260,              #pwm value for full right steering
     "THROTTLE_FORWARD_PWM": 410,            #pwm value for max forward throttle
     "THROTTLE_STOPPED_PWM": 370,            #pwm value for no movement
     "THROTTLE_REVERSE_PWM": 320,            #pwm value for max reverse throttle
}
```
