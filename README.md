All-in-one Self-adaptive Computing Platform for Smart City

![image](https://github.com/hassaanEssex/xohw23-114/assets/138205555/6b4457a2-710c-4442-aa2d-6fbd9878f8a8)

Team number: xohw23-114

Project name: All-in-one Self-adaptive Computing Platform for Smart City

Link to YouTube Video(s):

Link to project repository: https://github.com/hassaanEssex/xohw23-114

 

University name: University of Essex

Participant(s): Hassaan ur Rahman, Syed Muhammad Shariq Ali, Morgan Greenhill, Foteini Papadogianni, Akshay Gopinath

Email: hr22581@essex.ac.uk

Supervisor name: 1. Dr. Xiaojun Zhai. 2. Dr. Yun Wu

Supervisor e-mail: xzhai@essex.ac.uk

 
Board used: Xilinx Kria KV260

Software Version: 2.0

Brief description of project: 
The "All-in-one Self-adaptive Computing Platform for Smart City" project presents a comprehensive solution for efficient and intelligent human detection in smart city environments. It utilizes the Xilinx Kria KV260 Vision AI Starter Kit,

![image](https://github.com/hassaanEssex/xohw23-114/assets/138205555/41d53143-4072-4bcb-bb31-591544df8b3e)

which combines the Zynq UltraScale MPSoC architecture with 4 GB of DDR4 memory for AI-accelerated applications such as smart cameras and face detection. The software component employs PetaLinux and Vitis Video Analytics SDK (VVAS)to create a streamlined development environment for seamless integration of hardware and software.

![image](https://github.com/hassaanEssex/xohw23-114/assets/138205555/c73bf10c-7604-437a-bdaf-a72e4c807bbf)
By incorporating image classification models like YOLO and ResNet, the project enables real-time person detection from video input, contributing to enhanced security and safety in smart cities. Overall, the "All-in-one Self-adaptive Computing Platform for Smart City" project offers a comprehensive solution that combines powerful hardware, advanced software frameworks, and cutting-edge AI models for efficient and accurate human detection in smart city environments.

 ![image](https://github.com/hassaanEssex/xohw23-114/assets/138205555/55aab0d5-2124-41a1-a86f-fa933914c088)


Description of archive (explain directory structure, documents and source files):

Instructions to build and test project:

Kria KV260 setup
What you’ll need:
•	KV260 Power supply and Adapter (12V, 3A)

•	MicroSD Card 16GB or Above

•	USB-A to micro-B Cable

•	Raspberry Pi Camera

•	Ethernet Cable


PetaLinux installation
•	Download the Kria KV260 image from the Xilinx webpage to your PC.
•	Download the Balena Etcher image flashing tool
•	Follow the instructions within Balena Ethcher to flash the image to the SD card

Hardware setup
•	Insert the microSD card containing the boot image in the microSD card slot (J11)
•	Connect the micro-B end of the USB-A to micro B cable to J4
•	Connect the Raspberry Pi Camera Module to J9
•	Connect to a monitor/display with the the HDMI cable
•	Connect the DC power supply to J12

![image](https://github.com/hassaanEssex/xohw23-114/assets/138205555/86aaab4e-b4fc-495f-9c14-310ac86d74e5)

Booting the board
•	Using a terminal emulator of your choice such as Putty, open a terminal with a baud rate of 115200.
•	Power up the KV260 board and observe the power LEDs illuminate and the Linux boot response appear on the UART.
•	Once the board has booted to the Linux command prompt, enable the root user with the command ‘sudo su -l root’.
•	Verify internet connectivity with the command ‘ping 8.8.8.8’

Building and installing VVAS
•	Clone the following repository containing the VVAS file structure onto the host PC with the following command: ‘git clone --recurse-submodules https://github.com/Xilinx/VVAS.git’
•	Build VVAS with the following command within the repository folder: ‘./build_install_vvas.sh Edge’
•	Copy VVAS to the KV260 board using either a USB stick or the following network transfer command:
‘scp install/vvas_installer.tar.gz <board ip>:/’
•	On the KV260 board, run the following commands to install VVAS:
‘cd /’
‘tar -xvf vvas_installer.tar.gz’
•	VVAS should now be installed and ready to run on the KV260 board.

Then we deploy the quantized YOLO model on the board using VVAS. Once the YOLO and ResNet models are deployed and integrated into the Vitis Video Analytics SDK (VVAS) application, they will provide outputs in the form of classifications for the input video frames.

![image](https://github.com/hassaanEssex/xohw23-114/assets/138205555/27e99065-cf02-4336-9665-7156f91ecafe)

For YOLO (You Only Look Once) model:
1. Input: Each video frame is passed as input to the YOLO model.
2. Processing: The YOLO model performs object detection by dividing the input frame into a grid and predicting bounding boxes and class probabilities for each grid cell.
3. Output: The model generates bounding box coordinates, class labels, and confidence scores for the detected objects in the frame.
4. Post-processing: The bounding boxes are post-processed to filter out overlapping or low-confidence detections. Non-maximum suppression (NMS) is often applied to eliminate redundant or overlapping bounding boxes.
5. Visualizing the Output: The final output typically includes bounding boxes drawn around the detected objects in the video frame, along with the corresponding class labels and confidence scores. These visual indicators highlight the presence and location of humans in the video footage.

For ResNet (Residual Network) model:
1. Input: Each video frame is fed as input to the ResNet model.
2. Processing: The ResNet model performs deep convolutional neural network-based image classification, analyzing the features within the frame.
3. Output: The model provides a probability distribution over different classes for the input frame, indicating the likelihood of the frame containing a human or other predefined classes.
4. Post-processing: Depending on the application, a threshold may be set to classify the frame as containing a human if the predicted probability exceeds a certain threshold value.
5. Visualizing the Output: The output can be visualized by displaying the predicted class label along with the probability score, indicating the presence of a human or other objects in the frame.

For now, the model wasn't able to run on the hardware directly but was added into a similar environment server with Vitis AI on it. To do that we simply connect remotely to the server and operate through the command line. Install all the dependencies for YOLO and ResNet and can run the model.
The VVAS application, incorporating both the YOLO and ResNet models, can provide visual representations of the detected objects (humans) in the video frames by overlaying bounding boxes and labels. These visual indicators aid in understanding and analyzing the output of the models.
