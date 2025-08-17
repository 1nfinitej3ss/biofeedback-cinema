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

## Installation & Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/yourusername/biofeedback-cinema.git
   cd biofeedback-cinema
   ```

2. **Install Python dependencies:**
   ```bash
   pip install opencv-python pyserial
   ```

3. **Connect hardware:**
   - Connect Neurosky Mindwave headset via Bluetooth
   - Connect Arduino via USB
   - Connect servos to Arduino pins 8 and 9
   - Connect camera to Raspberry Pi

4. **Upload Arduino code:**
   - Open `arduino-serial-pi` in Arduino IDE
   - Upload to your Arduino board

5. **Run the main script:**
   ```bash
   python biofeedback-python
   ```

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

## Contact

For questions about this project or collaboration opportunities, please reach out through the repository issues or contact the project maintainer.

---

*This project represents ongoing research into the intersection of neuroscience, technology, and artistic expression. It explores how our neural states can become a new form of creative medium.*
