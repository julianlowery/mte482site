## SoundAssist

### Project

SoundAssist is a wearable device to assist the hearing impaired. It sits around the wearer's neck constantly monitors the ambient noise to classify important sounds that may occur. It provides immediate haptic feedback to the user to notify them that an important sound has occurred, and sends a notification to their mobile device for more detailed information.

The device will replace hearing dogs, who currently play a very similar role, but are much expensive, difficult to obtain, and limiting to the user.

### Group

|Patrick Liu     | Julian Lowery | Bilun Sun     |
|:--------------:|:-------------:|:-------------:|
| <img src="/lake.jpg" width="200" height="150"> |  <img src="/lake.jpg" width="200" height="150"> | <img src="/lake.jpg" width="200" height="150"> |

### Weekly Log

#### Week of Jan 10

- Software infrastructure was created.
- A detailed exploration of options for bluetooth connectivity between the SoundAssist and mobile device was conducted.
- _some applicable AI stuff. Got quantization working for the first time?_
- Jetson nano was selected over its alternantive, the Raspberry Pi.

#### Week of Jan 17

- Some hardware arrived! The nRF52840 module that will be integrated into the PCB for BLE connectivity, as well as an Adafruit nRF52840 Feather Express. This development board integrates the nRF52840 and can be used for early prototyping and testing.
- The Arduino programming environment was configured and tested for the Feather, and initial tests of BLE capabilities were successful.
- Progress on configuring the Jetson/Raspberry Pi was made, particularly in installing (and running) Pytorch and the plethora of dependencies required for the neural network inference processing. Read this short article, [Arm's Funny Bone](/software-updates/jetson-nano-environment.md), by Patrick Liu on some of the quircks and difficulties with using an ARM Single-Board Computer (SBC) as our compute platform.
- An interesting setback is that CUDA will likely be unavailable on the Jetson for a quantized neural net, posing a new dilema of whether to run a quantized model on the CPU, or a non-quantized model on the NVIDIA GPU.

### Source Code

The project software can be found on our [HearingAId Github repository](https://github.com/bilunsun/HearingAId).
