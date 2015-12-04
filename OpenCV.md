# How_To_Install_OpenCV
Install OpenCV and Python on your Raspberry Pi

Make sure Raspbian update :
    sudo apt-get update
    sudo apt-get upgrade
    sudo rpi-update
    
Install Dependecies
First you must update
    sudo apt-get -y install build-essential cmake cmake-curses-gui pkg-config libpng12-0 libpng12-dev libpng++-dev libpng3 libpnglite-dev zlib1g-dbg zlib1g zlib1g-dev pngtools libtiff4-dev libtiff4 libtiffxx0c2 libtiff-tools libeigen3-dev

Then do you must download These packages allow you to load various image file formats such as JPEG, PNG, TIFF, etc.
    sudo apt-get -y install libjpeg8 libjpeg8-dev libjpeg8-dbg libjpeg-progs ffmpeg libavcodec-dev libavcodec53 libavformat53 libavformat-dev libgstreamer0.10-0-dbg libgstreamer0.10-0 libgstreamer0.10-dev libxine1-ffmpeg libxine-dev libxine1-bin libunicap2 libunicap2-dev swig libv4l-0 libv4l-dev python-numpy libpython2.6 python-dev python2.6-dev libgtk2.0-dev 

Install the GTK development library. This library is used to build Graphical User Interfaces (GUIs)
    sudo apt-get install libgtk2.0-dev
    
Install the necessary video I/O packages. These packages are used to load video files using OpenCV:
    sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
    
Install libraries that are used to optimize various operations within OpenCV:
    sudo apt-get install libatlas-base-dev gfortran
    
Install pip :
    wget https://bootstrap.pypa.io/get-pip.py
    sudo python get-pip.py
    
Install  virtualenv  and virtualenvwrapper :
    sudo pip install virtualenv virtualenvwrapper
    sudo rm -rf ~/.cache/pip
    
Then, update your ~/.profile  file to include the following lines:
    # virtualenv and virtualenvwrapper
    export WORKON_HOME=$HOME/.virtualenvs
    source /usr/local/bin/virtualenvwrapper.sh
    
Reload your .profile  file:
    source ~/.profile
    
Create your computer vision virtual environment:
     mkvirtualenv cv
     
  Now we can install the Python 2.7 development tools:
      sudo apt-get install python2.7-dev
      
  Note: Yes, we are going to use Python 2.7. OpenCV 2.4.X does not yet support Python 3 and OpenCV 3.0 is still in beta. 
  It’s also unclear when the Python bindings for OpenCV 3.0 will be complete so I advise to stick with OpenCV 2.4.X for the time being.
  
  We also need to install NumPy since the OpenCV Python bindings represent images as multi-dimensional NumPy arrays:
      pip install numpy
      
  Download OpenCV and unpack it:
      wget -O opencv-2.4.10.zip http://sourceforge.net/projects/opencvlibrary/files/opencv-unix/2.4.10/opencv-2.4.10.zip/download
       unzip opencv-2.4.10.zip
       cd opencv-2.4.10
       
  Setup the build :
      mkdir build
      cd build
      cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D BUILD_NEW_PYTHON_SUPPORT=ON -D INSTALL_C_EXAMPLES=ON -D INSTALL_PYTHON_EXAMPLES=ON  -D BUILD_EXAMPLES=ON ..
  
  Compile OpenCV:
      make
      
  Important: Make sure you’re in the  cv  virtual environment so OpenCV is compiled against the virtual environment Python and NumPy. Otherwise, OpenCV will be compiled against the system Python and NumPy which can lead to problems down the line.
  
  Finally, we can install OpenCV:
      sudo make install
      sudo ldconfig
      
  If you’ve gotten this far in the guide, 
  OpenCV should now be installed in  /usr/local/lib/python2.7/site-packages
  
  But in order to utilize OpenCV within our cv  virtual environment, we first need to sym-link OpenCV into our site-packages  directory:
      cd ~/.virtualenvs/cv/lib/python2.7/site-packages/
      ln -s /usr/local/lib/python2.7/site-packages/cv2.so cv2.so
      ln -s /usr/local/lib/python2.7/site-packages/cv.py cv.py
      
  Finally, we can give our OpenCV and Python installation a test drive:
      workon cv
      python
      >>> import cv2
      >>> cv2.__version__
      '2.4.10'
      
  Reference : http://www.pyimagesearch.com/2015/02/23/install-opencv-and-python-on-your-raspberry-pi-2-and-b/ http://www.pyimagesearch.com/2015/07/27/installing-opencv-3-0-for-both-python-2-7-and-python-3-on-your-raspberry-pi-2/http://robertcastle.com/2014/02/installing-opencv-on-a-raspberry-pi/http://www.robopapa.com/Projects/InstallOpenCVOnRaspberryPi
