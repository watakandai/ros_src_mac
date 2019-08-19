# ROS src Directory for mac
## Before you start
Follow instructions in [Official ROS Install Tutorial](http://wiki.ros.org/kinetic/Installation/OSX/Homebrew/Source).

Replace with src directory installed by ``wstool init -j8 src kinetic-desktop-full-wet.rosinstall`

```
rosdep install --from-paths src --ignore-src --skip-keys "python-wxtools google-mock boost" --rosdistro kinetic -y
```

## Installing Boost
Uninstall boost installed by brew
```
brew uninstall boost
```

download [boost 1.64.0](https://www.boost.org/users/download/#live).
```
tar -xzf boost_1_64_0.tar.gz
cd boost_1_64_0
./bootstrap.sh
./b2
./b2 install
```

include following to `~/ros_catkin_ws/src/roscpp_core/cpp_common/CMakeLists.txt`

```
SET (Boost_INCLUDE_DIR "/usr/local/include")
SET (Boost_LIBRARY_DIR "/usr/local/lib")
```

## Change versions for following brew packages
- cmake (3.15.1 bottle)
- opencv (3.4.5_2)
- ogre (1.9)

## Tell cmake where to find following libraries
- `/usr/local/Cellar/pcl/1.9.1_4/share/pcl-1.9/Modules/FindFLANN.cmake`
Add following lines at the top

```
set(FLANN_LIBRARIES /usr/local/lib/libflann.dylib /usr/local/lib/libflann_cpp.dylib)
set(FLANN_FOUND TRUE)
```

# Build and Install
change <NAME>

```
cd ~/ros_catkin_ws
./src/catkin/bin/catkin_make_isolated --install -DCMAKE_MACOSX_RPATH=ON -DCMAKE_INSTALL_RPATH="/Users/<NAME>/ros_catkin_ws/install_isolated/lib" -DCMAKE_BUILD_TYPE=Release
```

