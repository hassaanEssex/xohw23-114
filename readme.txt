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

Brief description of project: The All-in-one Self-Adaptive Computing Platform for Smart City project presents a comprehensive solution for smart cities using a Raspberry Pi camera and the Xilinx Kria KV260 Vision AI Starter Kit. This project integrates hardware, software, and artificial intelligence components to enable efficient human detection from video footages. The methodology involves utilizing the powerful Zynq UltraScale MPSoC architecture, along with PetaLinux and Vitis Video Analytics SDK, to develop a robust and adaptable system. An image classification Convolutional Neural Network (CNN) model is employed, although with certain layers split into subgraphs due to DPU limitations. The system achieves real-time video analytics and demonstrates accurate human detection in various smart city scenarios. The project report encompasses the project's title, introduction, methodology, results, conclusion, recommendations, and limitations. It provides valuable insights into the development of selfadaptive computing platforms for smart cities, laying the groundwork for further advancements in this domain.

 

Description of archive (explain directory structure, documents and source files):

 

Instructions to build and test project

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