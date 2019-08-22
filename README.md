# ORB_SLAM2-D435

## 1. Pangolin install
* __install grew__
    
      sudo apt-get install libglew-dev
* __Pangolin download__

      git clone https://github.com/stevenlovegrove/Pangolin.git
      cd Pangolin
      mkdir build
      cd build
      cmake ..
      sudo make install

## 2. Opencv(3.2.0) install 
* __prev package update__

      sudo apt-get update
      sudo apt-get upgrede
    
* __package install__
    
      sudo apt-get install build-essential cmake pkg-config libjpeg-dev libtiff5-dev libjasper-dev libpng12-dev libavcodec-dev libavformat-dev libswscale-dev libxvidcore-dev libx264-dev libxine2-dev libv4l-dev v4l-utils libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev libqt4-dev mesa-utils libgl1-mesa-dri libqt4-opengl-dev libatlas-base-dev gfortran libeigen3-dev python2.7-dev python3-dev python-numpy python3-numpy
      
* __opencv install__

      mkdir opencv
      cd opencv
      wget -O opencv.zip https://github.com/Itseez/opencv/archive/3.2.0.zip
      unzip opencv.zip
      wget -O opencv_contrib.zip https://github.com/Itseez/opencv_contrib/archive/3.2.0.zip
      unzip opencv_contrib.zip
      
* __opencv build__ (만약 에러나면 아래 참고)

      cd opencv-3.2.0/
      mkdir build
      cd build
      cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_TBB=OFF -D WITH_IPP=OFF -D WITH_1394=OFF -D BUILD_WITH_DEBUG_INFO=OFF -D BUILD_DOCS=OFF -D INSTALL_C_EXAMPLES=ON -D INSTALL_PYTHON_EXAMPLES=ON -D BUILD_EXAMPLES=OFF -D BUILD_TESTS=OFF -D BUILD_PERF_TESTS=OFF -D ENABLE_NEON=ON -D WITH_QT=ON -D WITH_OPENGL=ON -D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib-3.2.0/modules -D WITH_V4L=ON -D WITH_FFMPEG=ON -D WITH_XINE=ON -D BUILD_NEW_PYTHON_SUPPORT=ON -D PYTHON_INCLUDE_DIR=/usr/include/python2.7 -D PYTHON_INCLUDE_DIR2=/usr/include/x86_64-linux-gnu/python2.7 -D PYTHON_LIBRARY=/usr/lib/x86_64-linux-gnu/libpython2.7.so ../
      make -j
      sudo make install
      
* __check install__
      
      pkg-config --modversion opencv
      pkg-config --libs --cflags opencv
      
* __build error due to [CUDA 9.0]__

     https://stackoverflow.com/questions/46584000/cmake-error-variables-are-set-to-notfound
      
## 3. eigen 3.1.0
* __Download 3.1.0 version__

     https://bitbucket.org/eigen/eigen/downloads/?tab=tags
     
## 4. ORB-SLAM install

      git clone https://github.com/raulmur/ORB_SLAM2.git ORB_SLAM2
      cd ORB_SLAM2
      chmod +x build.sh
      ./build.sh
    
* __[usleep(3000);] error ./build.sh__

    Find file and add the following codes.
    
    (LocalMapping.cc / LoopClosing.cc / Tracking.cc / System.cc / Viewer.cc
    System.cc / mono_euroc.cc / mono_kitti.cc / mono_tum.cc / rgbd_tum.cc
    stereo_kitti.cc / stereo_euroc.cc)
	
	  #include <unistd.h>
	  #include <stdio.h>
	  #include <stdlib.h>
      
 ## 5. ORB_SLAM ROS
 
__Move ORB_SLAM file to catkin_ws/src/ and Remove build file__

	./build.sh
	./build_ros.sh
	
* __if error ./build_ros.sh__

	https://github.com/raulmur/ORB_SLAM2/issues/535
 
 
## 6. Realsense setting

   * https://github.com/IntelRealSense/realsense-ros#installation-instructions
   
* __Register the server's public key:__

      sudo apt-key adv --keyserver keys.gnupg.net --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE || sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE
    
* __Add the server to the list of repositories  (Ubuntu 16 LTS):__
    
      sudo add-apt-repository "deb http://realsense-hw-public.s3.amazonaws.com/Debian/apt-repo xenial main" -u
    
* __Install the libraries__

      sudo apt-get install librealsense2-dkms
      sudo apt-get install librealsense2-utils
      sudo apt-get install librealsense2-dev
      sudo apt-get install librealsense2-dbg
 
* __check install__
   
      realsense-viewer
      
