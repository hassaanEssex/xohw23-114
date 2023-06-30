All-in-one Self-adaptive Computing Platform for Smart City

![image](https://github.com/hassaanEssex/xohw23-114/assets/138205555/aa3ea57d-2804-4321-aaf1-c822d67fc0f1)


Team number: xohw23-114

Project name: All-in-one Self-adaptive Computing Platform for Smart City

Link to YouTube Video(s):

Link to project repository: https://github.com/hassaanEssex/xohw23-114

 

University name: University of Essex

Participant(s): Hassaan ur Rahman , Syed Muhammad Shariq Ali , Morgan Greenhill Foteini Papadogianni, Akshay Gopinath

Email: hr22581@essex.ac.uk

Supervisor name: 1. Dr. Xiaojun Zhai. 2. Dr. Yun Wu

Supervisor e-mail: xzhai@essex.ac.uk

 
Board used: Xilinx Kria KV260

Software Version: Version 2.0

Brief description of project: 
The "All-in-one Self-adaptive Computing Platform for Smart City" project presents a comprehensive solution for efficient and intelligent human detection in smart city environments. It utilizes the Xilinx Kria KV260 Vision AI Starter Kit,

![image](https://github.com/hassaanEssex/xohw23-114/assets/138205555/41d53143-4072-4bcb-bb31-591544df8b3e)

which combines the Zynq UltraScale MPSoC architecture with 4 GB of DDR4 memory for AI-accelerated applications such as smart cameras and face detection. The software component employs PetaLinux and Vitis Video Analytics SDK (VVAS)to create a streamlined development environment for seamless integration of hardware and software.

![image](https://github.com/hassaanEssex/xohw23-114/assets/138205555/c73bf10c-7604-437a-bdaf-a72e4c807bbf)
By incorporating image classification models like YOLO and ResNet, the project enables real-time person detection from video input, contributing to enhanced security and safety in smart cities. Overall, the "All-in-one Self-adaptive Computing Platform for Smart City" project offers a comprehensive solution that combines powerful hardware, advanced software frameworks, and cutting-edge AI models for efficient and accurate human detection in smart city environments.

 ![image](https://github.com/hassaanEssex/xohw23-114/assets/138205555/55aab0d5-2124-41a1-a86f-fa933914c088)


Description of archive (explain directory structure, documents and source files):

Instructions to build and test project:

Connect the raspberry pi camera and run the board.

1.	Clone the repo: https://github.com/Xilinx/VVAS , by following instructions in the link
2.	Before building, you need to setup the cross compiler environment
a.	Clone this entire repo: https://github.com/Xilinx/Vitis-AI/tree/master 

b.	Run: ./Vitis-AI/board_setup/mpsoc/host_cross_compiler_setup.sh
This will install petalinux environment to compile for the correct target
(installed in /home/user in Linux)
c.	Source the environment: 
source /home/akshay/petalinux_sdk_2022.2/environment-setup-cortexa72-cortexa53-xilinx-linux
d.	Now from the VVAS repo root, if you try to build using: ./build_install_vvas.sh TARGET-Edge
you will get an error because a key dependency is missing, which is libjansson
i.	To fix its quite tedious but here are the steps:
ii.	Download another petalinux target: https://www.xilinx.com/member/forms/download/xef.html?filename=xilinx-zynqmp-common-v2022.2_10141622.tar.gz
This contains the dependencies that we can copy to our target. This by default installed /opt in Linux (the tar.gz file has an installer script)
iii.	You need to copy some files from the /opt one to our target one (in /home/user). These files are:
- sdk/sysroots/cortexa72-cortexa53-xilinx-linux/usr/lib/libjansson.so.4.14.0 libjansson.so.4 libjansson.so 
- sdk/sysroots/cortexa72-cortexa53-xilinx-linux/usr/lib/pkgconfig/jansson.pc
- copy sdk/sysroots/cortexa72-cortexa53-xilinx-linux/usr/include/jansson_config.h jansson.h
Note: This just a standard linux directory structure to these files we are copying go to the exact same place inside our target petalinux environment
e.	After this is done, we can build from VVAS repo root: ./build_install_vvas.sh TARGET=Edge 
f.	There will be a folder created called install after building

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

The VVAS application, incorporating both the YOLO and ResNet models, can provide visual representations of the detected objects (humans) in the video frames by overlaying bounding boxes and labels. These visual indicators aid in understanding and analyzing the output of the models.
