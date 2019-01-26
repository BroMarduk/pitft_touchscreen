# EVDEV event queue for Touchscreens on the Rasperry Pi

## Overview

This fork of the PrzemoF/pitft_touchscreen project is designed to provide support for capacitive Adafruit PiTFT screens in the latest version of Stretch, where the former Adafruit capacitive drivers have been removed.   In addition, support for resistive Adafruit PiTFT touchscreens

## Features

* Threaded message queue processing
* Support for Adafruit capacitive PiTFTs

## Features over original repository

* Support for SYN_DROPPED messages
* Support for Adafruit resistive PiTFTs (3.5 support working, 2.8 being tested)

## Notes

The EVDEV library is stateful, so messages only include changes from previous state.  This means that at times only a ABS_X or ABS_Y (or sometimes neither) event will be queued on a move or a touch.   When only one is present, it means the previous value did not change.  If the event occurs at the exact same coordinate, neither will be present.   The application using the queue will need to keep this state in order to make sure messages occur at the correct coordinates.

## Usage
```
@raspberrypi:~/pitft_touchscreen $ python3 example_usage.py 
Input device /dev/input/touchscreen found
Do whaterer you want to do while waiting for touchscreen events
Do whaterer you want to do while waiting for touchscreen events
Event received: {'touch': 1, 'id': 67, 'y': 215, 'time': 1533721688.999557, 'x': 102}
Event received: {'touch': 1, 'id': 67, 'y': 213, 'time': 1533721689.030115, 'x': 102}
Event received: {'touch': 1, 'id': 67, 'y': 211, 'time': 1533721689.054368, 'x': 102}
Event received: {'touch': 1, 'id': 67, 'y': 208, 'time': 1533721689.066565, 'x': 103}
Event received: {'touch': 1, 'id': 67, 'y': 206, 'time': 1533721689.078685, 'x': 103}
Event received: {'touch': 1, 'id': 67, 'y': 202, 'time': 1533721689.090849, 'x': 103}
Event received: {'touch': 1, 'id': 67, 'y': 199, 'time': 1533721689.102968, 'x': 104}
Event received: {'touch': 1, 'id': 67, 'y': 195, 'time': 1533721689.115151, 'x': 103}
Event received: {'touch': 1, 'id': 67, 'y': 192, 'time': 1533721689.127282, 'x': 103}
Event received: {'touch': 1, 'id': 67, 'y': 188, 'time': 1533721689.139474, 'x': 102}
Event received: {'touch': 1, 'id': 67, 'y': 185, 'time': 1533721689.151614, 'x': 101}
Event received: {'touch': 1, 'id': 67, 'y': 182, 'time': 1533721689.163759, 'x': 100}
Event received: {'touch': 1, 'id': 67, 'y': 180, 'time': 1533721689.175889, 'x': 99}
Event received: {'touch': 1, 'id': 67, 'y': 178, 'time': 1533721689.20014, 'x': 97}
Event received: {'touch': 0, 'id': -1, 'y': 97, 'time': 1533721689.297147, 'x': 97}
Do whaterer you want to do while waiting for touchscreen events
Event received: {'touch': 1, 'id': 68, 'y': 206, 'time': 1533721690.48638, 'x': 110}
Event received: {'touch': 1, 'id': 68, 'y': 204, 'time': 1533721690.536405, 'x': 110}
Event received: {'touch': 1, 'id': 68, 'y': 202, 'time': 1533721690.572857, 'x': 110}
Event received: {'touch': 1, 'id': 68, 'y': 200, 'time': 1533721690.585048, 'x': 110}
Event received: {'touch': 1, 'id': 68, 'y': 198, 'time': 1533721690.59718, 'x': 109}
Event received: {'touch': 1, 'id': 68, 'y': 196, 'time': 1533721690.609346, 'x': 109}
Event received: {'touch': 1, 'id': 68, 'y': 193, 'time': 1533721690.621493, 'x': 108}
Event received: {'touch': 1, 'id': 68, 'y': 190, 'time': 1533721690.633648, 'x': 108}
Event received: {'touch': 1, 'id': 68, 'y': 187, 'time': 1533721690.645795, 'x': 107}
Event received: {'touch': 1, 'id': 68, 'y': 185, 'time': 1533721690.657941, 'x': 107}
Event received: {'touch': 1, 'id': 68, 'y': 183, 'time': 1533721690.682163, 'x': 107}
Event received: {'touch': 0, 'id': -1, 'y': 107, 'time': 1533721690.791378, 'x': 107}
Do whaterer you want to do while waiting for touchscreen events
pi@raspberrypi:~/pitft_touchscreen $

