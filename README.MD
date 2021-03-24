<h2>Steps for Installing Open-CV on Windows Subsystem for Linux(WSL1) from Source:</h2>

<b><u>Step-0</u></b>:<br>
If you are already using WSL-1 proceed to Step-3.

<b><u>Step-1</u></b>:<br>
Enable the Windows Subsystem for Linux optional feature.For this open <b>Windows Powershell</b> and run the following command as Administrator.

```C
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

Now <b>restart the system</b> and open Microsoft Store.Install a linux distro preferably Debian.<br>
[Debian Linux/GNU](https://www.microsoft.com/en-in/p/debian/9msvkqc78pk6?rtc=1#activetab=pivot:overviewtab)

<b><u>Step-2</u></b>:<br>
Create a unix username and password.Your distro will be in the home directory by default .To navigate to your current user in Windows use the following command.

```C
mnt/c/Users/"Your Windows username"/desktop
```

For ease of convenience use Windows Terminal that can be downloaded from this link.<br>
[Windows Terminal](https://www.microsoft.com/en-in/p/windows-terminal/9n0dx20hk701?rtc=1#activetab=pivot:overviewtab)

<b><u>Step-3</u></b>:<br>
Open your terminal and run the following commands to install Git,GNU-Make and GCC-Compiler. Enter your unix password created earlier when prompted to enter.

```C
sudo apt-get update
sudo apt-get upgrade
```

```C
sudo apt-get install git
sudo apt-get install make
sudo apt install build-essential
```

<b><u>Step-4A</u></b>:<br>
Since there is no GUI Support for WSL directly,we will use an X-Server preferably XLaunch which can be downloaded from this link.<br>
[Xserver](https://sourceforge.net/projects/vcxsrv/)

Open the Linux-Terminal and type the following command for supporting X-Server.

```C
sudo apt-get install x11-apps
```

<b><u>Step-4B</u></b>:<br>
To check whether the X-server is working or not open the X-Launch app.You will see the following screen.<br>
[Screen-1](http://i.imgur.com/V0BpaA5.png?1)<br>
Change the number -1 to 0 and press on next button.<br>
You will see the following screen.<br>
[Screen-2](https://lh3.googleusercontent.com/proxy/xZBOO6GL79i8NTAeBMKykL_5ugR-oc9CKWoZ22UDQdiidaaz5Yi2Pg4AGcnJ9TQAen1zl9Qxg5qcfF1pWZiBNNoGVpAzrQgOd5o8SLq8Sg)<br>
Press next and you will see the following screen.<br>
[Screen-3](https://miro.medium.com/max/998/1*d8ArTA3ISw1skKU0HMWIow.png)<br>
Press next and you will see the following screen.<br>
[Screen-4](https://linustechtips.com/uploads/monthly_2018_10/image.png.a6c5330fd54e484006cc748cb93c5554.png)<br>
Now press <b>Finish</b>.<br>
Now open the terminal and press the commands.<br>

```C
export DISPLAY=:0
xeyes
```

You will see the following image.
[xeyes](https://seanthegeek.net/wp-content/uploads/2017/06/xeyes-bash-ubuntu-windows-10.png).<br>

<b><u>Step-5</u></b>:<br>

Install required and optional dependencies.<br>

```C
sudo apt install build-essential cmake git pkg-config libgtk-3-dev 
    libavcodec-dev libavformat-dev libswscale-dev libv4l-dev \
    libxvidcore-dev libx264-dev libjpeg-dev libpng-dev libtiff-dev \
    gfortran openexr libatlas-base-dev python3-dev python3-numpy \
    libtbb2 libtbb-dev libdc1394-22-dev
```

<b><u>Step-6A</u></b>:<br>

Clone the git repos of OPEN-CV.This method by default installs latest version which can possibly be in development stages.<br>
For installing particular version say 4.5.1 directly go to Step-6B.Follow only 6A or 6B<br>

```C
mkdir ~/opencv_build && cd ~/opencv_build
git clone https://github.com/opencv/opencv.git
git clone https://github.com/opencv/opencv_contrib.git
```

<b><u>Step-6B</u></b>:<br>

For some other version say 4.2.1,replace 4.5.1 by 4.2.1 in both the checkout commands.<br>

```C
mkdir ~/opencv_build && cd ~/opencv_build
```

```C
git clone https://github.com/opencv/opencv.git
cd ~/opencv_build/opencv
git checkout 4.5.1
cd ~/opencv_build
```


```C
git clone https://github.com/opencv/opencv_contrib.git
cd ~/opencv_build/opencv_contrib
git checkout 4.5.1
cd ~/opencv_build
```


<b><u>Step-7</u></b>:<br>

Create a temporary build system.<br> 

```C
cd ~/opencv_build/opencv
mkdir build && cd build
```

Set the build system with CMake.<br>
```C
cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D INSTALL_C_EXAMPLES=ON \
    -D INSTALL_PYTHON_EXAMPLES=ON \
    -D OPENCV_GENERATE_PKGCONFIG=ON \
    -D OPENCV_EXTRA_MODULES_PATH=~/opencv_build/opencv_contrib/modules \
    -D BUILD_EXAMPLES=ON ..
```

<b><u>Step-8</u></b>:<br>
After the build is over you will see <br>

```C
...
Output
-- Configuring done
-- Generating done
-- Build files have been written to: /home/pi/opencv_build/opencv/build
```

<b><u>Step-9</u></b>:<br>
Compile the build using

```C
make -j4 
```

j4 denotes that build will be compiled on 4 cores.<br>
Depending on the number of cores in processor and your wish change the number to j2 or j6 or j8.<br>
After compilation you will see 

```C
...
Output
[100%] Linking CXX executable ../../bin/example_tutorial_imgcodecs_imwrite
[100%] Built target example_tutorial_goodFeaturesToTrack_Demo
[100%] Built target example_tutorial_imgcodecs_imwrite

```

<b><u>Step-10</u></b>:<br>
Now install opencv using<br>

```C
sudo make install 
```

After installation you will see<br>

```C
...
Output
-- Installing: /usr/local/share/opencv4/samples/python/video_threaded.py
-- Installing: /usr/local/share/opencv4/samples/python/video_v4l2.py
-- Installing: /usr/local/share/opencv4/samples/python/watershed.py
```


<b><u>Step-11</u></b>:<br>
Check whether opencv is properly installed or not using<br>

```C
pkg-config --modversion opencv4
```

If you have installed version 4.5.1,you will see<br>
```C
Output
4.5.1
```


<b><u>Step-12</u></b>:<br>
For testing opencv open the Xlaunch and follow step-4B for setting display number and open the terminal to type<br>

```C
export DISPLAY=:0
```
Use the polygon.cpp in this repository to test and you will see output.jpg and output1.jpg provided in this repo.<br>

Compile and execute the code using following commands<br>
```C
g++ polygon.cpp -o a -pthread -std=c++11 `pkg-config --cflags --libs opencv4`
./a
```

If above command doesn't work use<br>

```C
g++ polygon.cpp -o a -pthread -std=c++11 `pkg-config --cflags --libs opencv`
./a
```
If you see any error like <b>cannot open shared object file Error</b> use the command<br> 
```C
sudo /sbin/ldconfig -v
```
and then compile the code.<br>
 


