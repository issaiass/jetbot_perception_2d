# JETBOT_PERCEPTION_2D

<details open>
<summary> <b>Brief Review<b></summary>

This project add perception to your ros project.  We used a deep learning approach based on TFOD API and using the SSD model of mobilenet.   

Below an image example of the outcome:

<p align="center">
<img src = "https://github.com/issaiass/jetbot_perception/blob/master/doc/imgs/jetbot_detection.gif?raw=true" width="80%"/>
</p>

</details>

<details open>
<summary> <b>Launching the application<b></summary>

- Create a ROS ros workspace and compile an empty package:
~~~
    cd ~
    mkdir -p catkin_ws/src
    cd catkin_ws
    catkin_make
~~~
- Open the `.bashrc` with nano:
~~~
    nano ~/.bashrc
~~~    
- Insert this line at the end of the `~/.bashrc` file for sourcing your workspace:
~~~
    source ~/catkin_ws/devel/setup.bash
~~~
- Clone this repo in the `~/catkin_ws/src` folder by typing:
~~~ 
    cd ~/catkin_ws/src
    git clone https://github.com/issaiass/jetbot_perception_2d.git --recursive
    cd ..
~~~
- Go to the root folder `~/catkin_ws` and make the folder running `catkin_make` to ensure the application compiles.
- [Download the ssd mobilenet object detection model](http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v2_coco_2018_03_29.tar.gz) and place the *frozen_inference_graph.pb* file into the folder *models/ssd_mobilenet_v2_coco_2018_03_29*
- Change the path paramters of the *configfile*, *modelfile* and *classfile* in the *config/ssd_mobilenet.yaml* configuration.
- Finally, in three separate windows launch the commands.
~~~
    roslaunch jetbot_perception perception_detection.launch
    rosrun jetbot_perception perception_subscriber
    rostopic echo /detected_objects_info    
~~~
- If you want, you could see the image in rviz, just add Image and select the /detected_objects topic.

<details open>
<summary> <b>Nodes and Parameters<b></summary>

#
## Node: usb_cam

### Node function

    This node opens the video camera input and publish to a topic.

### Node parameters

    For usb_cam please visit the ros wiki from http://wiki.ros.org/usb_cam.

#
## Node: perception_detection
### Node function

    This node publishes using opencv the image and also the object boxes properties like position, class id and probability.

### Node parameters

 * **`/opencv/enable_floating_window`**
     
    If you set it to true/false you could see the floating window created by opencv.

 * **`/opencv/image_width`**

    The width of the opencv window.

 * **`/opencv/image_height`**
   
    The height of the opencv window.
     
 * **`/opencv/window_name`**

    The name of the flating window

 * **`/opencv/wait_key`**
  
    The time for waiting frames
  
 * **`/neuralnet/imawidth of ge_width`**

    The input size of width of the image that will be the input of the neural network.  By default, if you are using mobilenet, set it to 300.

 * **`/neuralnet/image_height`** 
 
    The input size of height of the image that will be the input of the neural network.  By default, if you are using mobilenet, set it to 300.

 * **`/neuralnet/scale_factor`**

    The factor relatd to the scaling of the image in the neural network.  Set it between 0.2 to 0.98 to get good results.

 * **`/neuralnet/confidenceThreshold`**

    The minimal probability value to consider a proper detection.  By default, a good value could be 0.7.  Range of values are between 0.0-1.0.

 * **`/neuralnet/meanValR`**
 * **`/neuralnet/meanValG`**
 * **`/neuralnet/meanValB`**

    Those are the mean values of the dataset, this values are calculated by the data scientist that made the model because are related to the dataset, by default, in mobilenet are [127.5, 127.5, 127.5].

 * **`/neuralnet/configfile`**

    The configuration file path of the TFOD API neural network.  It contains information of the layers and how to process each one

 * **`/neuralnet/modelfile`**

    The TFOD API *.pb file that contains the computatinal graph serialized in that format, in other words, the model weights and biases.

 * **`/neuralnet/classfile`**

    The path of the class file that matches the object, is a relation between lines and object id.

#### Published Topics

  sub_topic: /usb_cam/image_raw

* **`/detected_objects`** ([sensor_msgs/Image])

    The perception output of the labeled image.

* **`/detected_objects_info`** ([jetbot_msgs/BoundingBoxes])

    The perception output that consts of the list of objects with its class id, label, probability and boxes in format (x,y,w,h).

#### Subscribed Topics

* **`/usb_cam/image_raw`** ([sensor_msgs/Image])

    Subscribes to the usb_cam topic for get the image of the webcam or camera.

#
## Node: perception_subscriber

### Node function

This node is an example of how to extract information of the resulting node.

### Node parameters

#### Published Topics

* **`/usb_cam/image_raw`** ([sensor_msgs/Image])

    Subscribes to the usb_cam topic for get the image of the webcam or camera.

#### Subscribed Topics

* **`/detected_object_info`** ([jetbot_msgs/BoundingBoxes])

    Subscribes to the /detected_objects_info topic for get the image information of the published detected objects from the perception_detection node.

</details>


<details open>
<summary> <b>Results<b></summary>

You could see the results on this youtube video.  

<p align="center">

Jetbot Perception using SSD Mobilenet

[<img src= "https://img.youtube.com/vi/5O2olvxdjiI/0.jpg" />](https://youtu.be/5O2olvxdjiI)

</p>

</details>

<details open>
<summary> <b>Video Explanation<b></summary>

<p align="center">

Explaining Jetbot Perception using SSD Mobilenet

[<img src= "https://img.youtube.com/vi/lRG9W_d8x5Y/0.jpg" />](https://youtu.be/lRG9W_d8x5Y)

</p>

</details>

<details open>
<summary> <b>Issues<b></summary>

- No issues present in this release

</details>

<details open>
<summary> <b>Future Work<b></summary>

- :x: Add services
- :x: Add actions
- :x: Add dynamic_reconfigure 
- :heavy_check_mark: Publish topic of objects information
- :heavy_check_mark: Publish topic of image

</details>

<details open>
<summary> <b>Contributing<b></summary>

Your contributions are always welcome! Please feel free to fork and modify the content but remember to finally do a pull request.

</details>

<details open>
<summary> :iphone: <b>Having Problems?<b></summary>

<p align = "center">

[<img src="https://img.shields.io/badge/linkedin-%230077B5.svg?&style=for-the-badge&logo=linkedin&logoColor=white" />](https://www.linkedin.com/in/riawa)
[<img src="https://img.shields.io/badge/telegram-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white"/>](https://t.me/issaiass)
[<img src="https://img.shields.io/badge/instagram-%23E4405F.svg?&style=for-the-badge&logo=instagram&logoColor=white">](https://www.instagram.com/daqsyspty/)
[<img src="https://img.shields.io/badge/twitter-%231DA1F2.svg?&style=for-the-badge&logo=twitter&logoColor=white" />](https://twitter.com/daqsyspty) 
[<img src ="https://img.shields.io/badge/facebook-%233b5998.svg?&style=for-the-badge&logo=facebook&logoColor=white%22">](https://www.facebook.com/daqsyspty)
[<img src="https://img.shields.io/badge/linkedin-%230077B5.svg?&style=for-the-badge&logo=linkedin&logoColor=white" />](https://www.linkedin.com/in/riawe)
[<img src="https://img.shields.io/badge/tiktok-%23000000.svg?&style=for-the-badge&logo=tiktok&logoColor=white" />](https://www.linkedin.com/in/riawe)
[<img src="https://img.shields.io/badge/whatsapp-%23075e54.svg?&style=for-the-badge&logo=whatsapp&logoColor=white" />](https://wa.me/50766168542?text=Hello%20Rangel)
[<img src="https://img.shields.io/badge/hotmail-%23ffbb00.svg?&style=for-the-badge&logo=hotmail&logoColor=white" />](mailto:issaiass@hotmail.com)
[<img src="https://img.shields.io/badge/gmail-%23D14836.svg?&style=for-the-badge&logo=gmail&logoColor=white" />](mailto:riawalles@gmail.com)

</p

</details>

<details open>
<summary> <b>License<b></summary>
<p align = "center">
<img src= "https://mirrors.creativecommons.org/presskit/buttons/88x31/svg/by-sa.svg" />
</p>
</details>