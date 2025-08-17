# Brain-to-Camera Cinema

An expanded cinema experiment that connects a participant's brain activity (both voluntary and involuntary) to camera controls via an open-source brain-computer interface. This system operates in lieu of a traditional cinematographer, where the user's brainwaves dictate the final composition.

## Overview

This project explores a new mode of cinematic production that allows the participant/actor's affect to be transcribed directly into the image itself. Instead of portraying emotions on video, we see the neural state itself as the system weaves emotional output into the construction of the image.

## Project History

### Prototype 002.??.15 (Under Construction)
- **Platform**: Open BCI (open source bio-sensing controller)
- **Development**: Supported by Coca-Cola Critical Difference for Women Graduate Student Grant
- **Location**: The Laboratory Residency
- **Technology Stack**: Max/MSP & Jitter for image control, Arduino for motor control (camera position)
- **Future**: Potential integration with Kinect for brain-to-3D imaging

### Prototype 001.11.14 (Original)
- **Platform**: Neurosky Mindwave EEG Reader Headset
- **Hardware**: Raspberry Pi (Python 3 + OpenCV), Arduino
- **Functionality**: Connected brain activity to camera position and focus
- **Development**: Created at MediaLab-Prado's Interactivos?14 workshop in Madrid, Spain
- **Collaborators**: Gregory Hough and Salud Lopez
- **Documentation**: Complete build instructions available at [Instructables](http://www.instructables.com/id/Biofeedback-Cinema/)

## Repository Contents

### `biofeedback-python/`
The main Python script that:
- Reads brainwave data from the Neurosky Mindwave headset
- Processes attention levels from EEG data
- Applies real-time blur effects to video based on attention
- Controls Arduino servos for camera positioning
- Displays live video with attention level overlay

**Key Features:**
- Real-time attention level monitoring
- Dynamic video blur based on brain activity
- Serial communication with Arduino
- Live video display with brainwave feedback

### `arduino-serial-pi/`
Arduino code for controlling servo motors that:
- Receives serial commands from the Raspberry Pi
- Controls two servo motors for camera positioning
- Responds to different command characters (a, b, c, d)
- Provides precise camera movement control

**Servo Control:**
- Servo 1 (Pin 8): Camera position control
- Servo 2 (Pin 9): Additional camera movement
- Commands trigger specific servo positions and movements

### `cv-blur-test/`
A test script for experimenting with OpenCV blur effects:
- Tests different blur intensities
- Demonstrates camera capture and processing
- Provides a foundation for blur effect implementation

## How It Works

1. **Brainwave Detection**: The Neurosky Mindwave headset captures EEG signals
2. **Attention Processing**: Python processes attention levels from the brainwave data
3. **Video Effects**: OpenCV applies blur effects based on attention levels
4. **Camera Control**: Arduino receives commands to move servos for camera positioning
5. **Real-time Feedback**: Live video display shows the brainwave-controlled effects

## Complete Build Instructions

**📖 Full step-by-step instructions available at: [Biofeedback Cinema Instructables](https://www.instructables.com/Biofeedback-Cinema/)**

### Required Supplies

1. **Neurosky Mindwave Mobile EEG Headset**
2. **Raspberry Pi B+** (B+ recommended for more USB ports, but B Model works with USB hub)
   - Raspberry Pi Power Adapter or Battery Pack
   - Wifi Dongle or Ethernet Connection (setup only)
   - Bluetooth Dongle (see [Raspberry Pi wiki](https://www.raspberrypi.org/documentation/configuration/bluetooth.md) for compatible dongles)
   - SD Card (at least 8GB) with NOOBS
3. **Arduino** (any board, Uno used in this project)
   - Arduino Power Adapter or Battery Pack
   - A-B USB Cable
4. **USB Webcam**
5. **Mini Pan-Tilt Kit**
6. **Monitor with HDMI Input** (or use VNC for remote control)
   - HDMI Cable
7. **USB Keyboard & Mouse** (bluetooth recommended to minimize USB ports)

### Step-by-Step Setup

#### Step 1: Setup Raspberry Pi
1. **Hardware Setup**: Connect keyboard, mouse, bluetooth dongle, wifi dongle, webcam, monitor via HDMI, and power
2. **OS Installation**: Install Raspbian OS via NOOBS
3. **Troubleshooting**: 
   - Fix aspect ratio issues by rebooting or manual configuration
   - Update keyboard configuration if special characters are mismapped
   - Test internet connection for library installation

#### Step 2: Connect Neurosky Headset
1. **Bluetooth Configuration**:
   ```bash
   sudo apt-get update
   sudo apt-get install bluetooth
   sudo apt-get install -y bluetooth bluez-utils blueman
   sudo reboot
   ```

2. **Test Bluetooth Connection**:
   ```bash
   hcitool scan
   ```
   Note the MAC address of your Mindwave headset

3. **Install Neurosky Libraries**:
   ```bash
   sudo apt-get install git-core
   sudo git clone https://github.com/cttoronto/python-mindwave-mobile
   sudo nano /home/pi/python-mindwave-mobile/MindwaveMobileRawReader.py
   ```
   Update the MAC address in the file

4. **Pair and Trust Device**:
   ```bash
   sudo bluez-simple-agent hci0 XX:XX:XX:XX:XX:XX
   sudo bluez-test-device trusted XX:XX:XX:XX:XX:XX yes
   sudo apt-get install python-bluez
   ```

5. **Test Connection**:
   ```bash
   sudo python /home/pi/python-mindwave-mobile/read_mindwave_mobile.py
   ```

#### Step 3: Connect USB Webcam with OpenCV
1. **Install OpenCV**:
   ```bash
   sudo apt-get install libopencv-dev python-opencv
   sudo apt-get -f install
   sudo apt-get install libopencv-dev python-opencv
   ```

2. **Test Installation**:
   ```bash
   python
   >>> import cv2
   ```

3. **Test Webcam**: Use the `cv-blur-test` script to verify camera and OpenCV functionality

#### Step 4: Connect Arduino
1. **Install Arduino IDE**:
   ```bash
   sudo apt-get install arduino
   ```

2. **Load Sketch**: Copy the `arduino-serial-pi` sketch into Arduino IDE and upload to your board

3. **Note Serial Port**: Record the Arduino port (usually `/dev/ttyACM0`)

4. **Disable Serial Console** (for smooth USB serial connection):
   ```bash
   wget https://github.com/wyolum/alamode/blob/master/bundles/alamode-setup.tar.gz?raw=true -O alamode-setup.tar.gz
   tar -xvzf alamode-setup.tar.gz
   cd alamode-setup
   sudo ./setup
   sudo reboot
   ```

#### Step 5: Final Integration
1. **Set Permissions**:
   ```bash
   chmod a=rwx /home/pi/python-mindwave-mobile
   ```

2. **Run Main Script**: Execute the `biofeedback-python` script from the python-mindwave-mobile folder

3. **Expected Results**:
   - Attention level displayed in Python Shell
   - Live webcam feed with dynamic blur based on attention
   - Servo motors moving based on brainwave data

### System Configuration

The Biofeedback Cinema system translates the participant's level of focus/attention (single integer) to:
- **Camera Position**: Pan and tilt via servo motors
- **Camera Focus**: Internal focus via OpenCV blur effects

All processing happens through a bluetooth connection between the Neurosky EEG headset and Raspberry Pi, with the Arduino handling motor control based on signals from the Pi.

## Technical Requirements

### Hardware
- Neurosky Mindwave EEG headset
- Raspberry Pi (or compatible single-board computer)
- Arduino board
- Servo motors for camera positioning
- Webcam or camera module
- USB-to-serial connection

### Software Dependencies
- Python 3
- OpenCV (cv2)
- PySerial
- Bluetooth libraries for Mindwave communication
- MindwaveDataPointReader (custom library)

## Usage

1. **Start the system** and put on the Mindwave headset
2. **Focus your attention** to control video blur effects
3. **Observe real-time changes** in video quality based on your brain activity
4. **Camera positioning** will automatically adjust based on brainwave patterns

## Research Applications

This project explores:
- **Brain-computer interfaces** for artistic expression
- **Affective computing** and emotional state visualization
- **Interactive media** and expanded cinema
- **Non-anthropocentric** approaches to media creation
- **Posthuman** perspectives on embodiment and technology

## Future Development

- Integration with Open BCI for higher resolution brainwave data
- 3D imaging capabilities via Kinect integration
- Advanced video effects and filters
- Machine learning for pattern recognition
- Multi-user collaborative experiences
- Additional brainwave parameters (eye blinks, etc.)
- Extended camera functions (hue, saturation, brightness, etc.)

## Contributing

This is an experimental art project. Contributions are welcome, especially:
- Improvements to brainwave processing algorithms
- New video effects and filters
- Hardware optimization
- Documentation and tutorials

## License

[Add your license information here]

## Acknowledgments

- **Open BCI** community for open-source brain-computer interface technology
- **MediaLab-Prado** for hosting the initial development workshop
- **The Laboratory Residency** for continued development support
- **Gregory Hough** and **Salud Lopez** for collaboration on the original prototype
- **Pedro Peira** for additional workshop collaboration

## Contact

For questions about this project or collaboration opportunities, please reach out through the repository issues or contact the project maintainer.

---

*This project represents ongoing research into the intersection of neuroscience, technology, and artistic expression. It explores how our neural states can become a new form of creative medium.*

**🔗 Complete build guide: [Biofeedback Cinema Instructables](https://www.instructables.com/Biofeedback-Cinema/)**
