# opencv3.3.0-install-ubuntu16.04
help to install opencv for your whole linus system

first,install CMake(if done,ignore this step)
on official website download: cmake-3.12.0.tar.gz
(
  sudo tar -zxvf cmake-3.12.0.tar.gz
  cd 
  sudo ./bootstrap
  sudo make
  sudo make install
)

second,install opncv
on official website download: opencv-3.3.0.tar.gz
(
  tar -zxvf opencv-3.3.0.tar.gz
  cd opencv-3.3.0
  mkdir build
  cd build
  cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local ..
  make -j7
  make install
)

then,add library path
(
  vi /etc/ld.so.conf.d/opencv.conf
  input:   /usr/local/lib ,save and quit
)

add environment variables
(
  vi /etc/profile
  in the end,add :  export PKG_CONFIG_PATH=/usr/local/lib/pkgconfig:$PKG_CONFIG_PATH
                    export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib
  update it :       source /etc/profile
)

add extra environment variables
(
  vi /etc/bash.bashrc
  in the end,add :  export PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/lib/pkgconfig
                    export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib
  update it :       source /etc/profile
)

Update system library cache
(
  sudo ldconfig
)

last,check out if installed successfilly
(
    pkg-config --cflags opencv
    pkg-config --libs opencv
)
no errors,done
