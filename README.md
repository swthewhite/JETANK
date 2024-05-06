# JETANK
JETANK is an open-source robot based on NVIDIA Jetson Nano

## Introduction

JETANK AI Kit is an AI Tracked Mobile Robot and AI Vision Robot based on the Jetson Nano Developer Kit. This intelligent crawler robot is specially designed for the NVIDIA JetBot AI project. The expansion board integrates various components like OLED, motor drive circuit, servo drive circuit, power supply circuit, and battery protection circuit, making circuit welding unnecessary. It supports unloading charging without the need to repeatedly remove the battery. The software is fully compatible with the NVIDIA JetBot AI project, enabling capabilities such as intelligent obstacle avoidance, autonomous line patrol, motion detection, color recognition tracking, and more. Additionally, the robot is equipped with a four-degree-of-freedom mechanical arm, controlled through a three-dimensional coordinate system, and can be flexibly controlled by a wireless gamepad.

### Expansion Board Features

- Supports three 18650 batteries (not included), providing up to 12.6V voltage output and enhanced motor power.
- Features S-8254AA + AO4407A lithium battery protection circuit onboard with anti-overcharge, anti-over-discharge, anti-over-current, and short-circuit protection functions.
- The onboard APW7313 voltage regulator chip ensures a stable 5V voltage supply to the Jetson Nano.
- The onboard SY8286 voltage regulator chip can provide a maximum current of 5A to the steering gear.
- Includes a TB6612FNG dual H-bridge motor driver chip onboard to operate the left and right motors.
- Equipped with a 0.91-inch 128×32 resolution OLED to display real-time information like the car IP address, memory, power, etc.
- The onboard INA219 acquisition chip facilitates real-time monitoring of battery voltage and charging current.

## Assembly Guides

### Step 1: Download and Prepare the Image

- Download the latest jetbot image from [jetbot.org](http://jetbot.org) provided by NVIDIA for Jetson Nano (4GB).
- Optionally, use a pre-configured image to skip Step 4.
- Flash the JetBot image onto an SD card:
  - Unzip the zip archive to retrieve the .img file.
  - Insert an SD card into your PC.
  - Use Win32DiskImager software to write the .img file onto the SD card.
  - Eject and remove the SD card from the PC.

### Step 2: Boot the Jetson Nano

- Insert the SD card into your Jetson Nano.
- Connect an HDMI display, keyboard, and mouse to the Nano.
- Connect a Power adapter to Jetson Nano (5V/4A) and start.
- Note: Test the Jetson Nano before assembling the JETANK and conducting tests.

### Step 3: Connect to WiFi

- Boot the Jetson Nano, enter the password (default is 'jetbot'), which directly opens the terminal as the Desktop IU is disabled to reduce CPU usage.
- Connect to WiFi using the following command: `sudo nmcli device wifi connect <SSID> password <PASSWORD>`.
  - Modify `<SSID>` to your actual WiFi SSID and `<PASSWORD>` to the correct password.
- Reboot the Jetson Nano; it should auto-connect to the WiFi, with the IP displayed on the OLED of JETANK.

### Step 4: Access JETANK by Web Browser

- Ensure your PC is connected to the same network as the JETANK.
- Assemble the JETANK according to the instructional video.
- Connect the 12.6V power adapter to the power interface of the JETANK.
- The Jetson Nano starts and connects to WiFi automatically, displaying the IP address on the OLED.
- Open a Chrome browser and navigate to `<jetson_ip>:8888` to access the Jupyter lab (e.g., `192.168.1.76:8888`).
- The default password for the Jupyter lab is 'jetbot'.
- Open a terminal and install the JETANK codes:
  ```bash
  git clone https://github.com/waveshare/JETANK.git

  cd JETANK
  cd config
  chmod +x config.sh
  sudo ./config.sh
  ```


  ```bash
  cd JETANK
  cd SCSCtrl
  chmod +x install.sh
  sudo ./install.sh
  
  cd ..
  cd config
  python3 servoInt.py
  ```
- The JETANK will auto-reboot.

### Accessing Different Modules

#### Servo Control

- Navigate to `http://<jetank_ip_address>:8888`.
- Go to `/JETANK/docs/en` and open the `servos_en.ipynb` file.
- Follow the guides and run the cell one by one to see how the servo works.

#### Arm and Camera Control

- Navigate to `http://<jetank_ip_address>:8888`.
- Go to `/JETANK/docs/en` and open the `ctrl_en.ipynb` file.
- Follow the guides and run the cell

 one by one to control the arm and move the camera.

#### Motion Detection

- Navigate to `http://<jetank_ip_address>:8888`.
- Go to `/JETANK/docs/en` and run the `motionDetect_en.ipynb`.
- Follow the guides and run the cell one by one to detect motion or changes in objects using OpenCV.

#### Color Recognition

- Navigate to `http://<jetank_ip_address>:8888`.
- Go to `/JETANK/docs/en` and run the `colorRecognition_en.ipynb`.
- Follow the guides and run the cell one by one to recognize the HSV value of the image captured by the camera.

#### Color Tracking

- Navigate to `http://<jetank_ip_address>:8888`.
- Go to `/JETANK/docs/en` and run the `colorTracking_en.ipynb`.
- Follow the guides and run the cell one by one to recognize and track a specified color, defaulting to yellow.

#### Gamepad Control

- Navigate to `http://<jetank_ip_address>:8888`.
- Go to `/JETANK/docs/en` and run the `gamepadCtl_en.ipynb`.
- Follow the guides and run the cell one by one, and connect the USB adapter of the gamepad to the Jetson Nano to control the JETANK.

## Resources

### Documentation

- Schematic of JETANK Expansion board
- Datasheet Links
  - [Ina219.pdf](#)
  - [PCA96_datasheet.pdf](#)
  - [S-8254AA.PDF](#)
  - [Ads1115.pdf](#)
  - [TB6612FNG_datasheet_en.pdf](#)

### Related Tutorials

- Motor Driver
- Teleoperation
- Collision Avoidance
- Line Tracking
- Servo Driver
- JETANK Control
- JETANK AI Kit-Motion Detection
- JETANK AI Kit-Color Recognition
- JETANK AI Kit-Color Tracking
- JETANK AI Kit-Gamepad Control

## FAQ

### What batteries does JETANK AI Kit use?

Supports three 18650 batteries (Not included). The voltage per battery is 3.7V, reaching 4.2V when fully charged. Use batteries without a protective plate. If the system voltage drops close to 9V, it is recommended to charge the batteries if the voltage displayed is lower than 10V. High-quality batteries like Sanyo or Panasonic are recommended.

### What is the power adapter used for?

The 12V power adapter is used to charge the batteries and should not be directly connected to the Jetson Nano Developer board.

### Charging indicator?

The charger has a charging indicator: green light when full, red light when charging.

### What are the system account and passwords?

Both are 'jetbot'.

### I am prompted to enter my password, but I cannot enter it, or I get an error?

The Linux system does not display the input when entering passwords, meaning you need to type blindly. Enter 'jetbot' directly on the keyboard and press enter.

### The battery is in full state, but the car cannot be powered on time?

If you are installing the battery for the first time, or have disassembled the battery, ensure you connect the distributed power supply to charge the cart for a few seconds and open the protection circuit before normal use.

### After burning the image of Jetson Nano, the TF card is not recognized on Windows PC?

Due to partitioning issues, the TF card with the Jetson Nano image burned on a Windows computer might not recognize the disk letter normally. If you need to reformat, search for disk management in the search bar of Windows and open the disk management interface. Find the removable disk where the TF card is located (be careful not to mistake it for another disk), right-click and select 'Delete Volume', then create a new volume and format it by default. After the default format, the TF disk will be re-identified. If the TF card memory space is incorrect, use formatting software to quickly format the new disk letter again. After formatting, if the TF card memory space is normal, you can re-burn the new image normally.

### What is the approximate movable arm length of a tracked robot?

The farthest reach is 235mm and the nearest is about 90mm.