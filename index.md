## SoundAssist

### Project

SoundAssist is a wearable device to assist the hearing impaired. It rests around the wearer's neck and constantly monitors ambient noise to classify important sounds that may occur. It provides immediate haptic feedback to the user to notify them that an important sound has occurred, and sends a notification to their mobile device for more detailed information.

The device will replace hearing dogs, who currently play a very similar role, but are much expensive, difficult to obtain, and limiting to the user.

### Group

|Patrick Liu     | Julian Lowery | Bilun Sun     |
|:--------------:|:-------------:|:-------------:|
| <img src="/lake.jpg" width="200" height="150"> |  <img src="/lake.jpg" width="200" height="150"> | <img src="/bilun_sun.png" width="200" height="150"> |

### Weekly Log

#### Week of Jan 10

- Software infrastructure was created.
- A detailed exploration of options for bluetooth connectivity between the SoundAssist and mobile device was conducted.
- Continued iteration of training neural network adjusting hyperparameters, experimenting with both Mel spectogram and time domain data representation.
- Jetson nano was selected over its alternantive, the Raspberry Pi.

#### Week of Jan 17

- Some hardware arrived! The nRF52840 module that will be integrated into the PCB for BLE connectivity, as well as an Adafruit nRF52840 Feather Express. This development board integrates the nRF52840 and can be used for early prototyping and testing.
- The Arduino programming environment was configured and tested for the Feather, and initial tests of BLE capabilities were successful.
- Progress on configuring the Jetson/Raspberry Pi was made, particularly in installing (and running) Pytorch and the plethora of dependencies required for the neural network inference processing. Read this short article, [Arm's Funny Bone](/software-updates/jetson-nano-environment.md), by Patrick Liu on some of the quircks and difficulties with using an ARM Single-Board Computer (SBC) as our compute platform.
- An interesting setback is that CUDA will likely be unavailable on the Jetson for a quantized neural net, posing a new dilema of whether to run a quantized model on the CPU, or a non-quantized model on the NVIDIA GPU.

#### Week of Jan 24

- With the resolution of our software dependencies for the Jetson Nano and Raspberry Pi, we were finally able to run some performance benchmarks to get an idea on how much performance we can expect with our system. We're working on summarzing our results in an article.

#### Week of Jan 31

- Began app development for testing bluetooth connection to mobile device within a custom application. The initial app will only have the essential functionality for verifying blueooth connection.

#### Week of Feb 7

- Preliminary success in connecting to the Feather development board via BLE from the custom application. Early success was somewhat finicky but promising. The goal on this front is to iron out a more full featured application to connect/disconnect, display data, and send push notifications, as well as to implement a proper program on the Feather to send ascii data that can be used to communicate arbitrary sound classifications.

#### Week of Feb 14

- Focus was turned to the bluetooth module in charge of forwarding classifcations over bluetooth. The Bluetooth Low Energy (BLE) protocol stack was investigated so it could be properly utilized for our specific purpose. With that, a new program was written to advertise, connect, and transmit necessary data over bluetooth.
- It was also necessary to set up communication between the Jetson and the bluetooth module. I2C was used and built into the program on the bluetooth module such that as the bluetooth module receives a classification from the I2C connection, it would immediately forward the classifcation over bluetooth.
- At this point, the mobile application and user interface remain rudimentary.

#### Week of Feb 21

- The mobile application was further developped to include a better display of the detected audio classifcation, more detailed and user friendly connection status information, as well as alerts and vibrations for when a classification is detected.
- A python program was created to interface with microphone on the device to collect audio data.
- A separate python module was created to send data from the Jetson over I2C to the bluetooth module (for relaying to the mobile application).


#### Week of Feb 28

- The neural network was refined, and the form of audio data used for classifcations was changed from a Mel Spectrogram to the time domain representation.
- The neural network was retrained on our own data collected on the device and a python program was written to filter the output of the neural network. Since the neural net would output a classifcation for every input, a low pass filter was created to smooth the output. More logic was added so that the classification would only be transferred to the bluetooth module in the event that a classification _changed_ since for one detection, the neural net would produce multiple classifications in a row.

### Source Code

The project software can be found on our [HearingAId Github repository](https://github.com/bilunsun/HearingAId).
