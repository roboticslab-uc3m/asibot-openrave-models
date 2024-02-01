## Basic installation

Dependencies:

- [Install CMake 3.12+](https://github.com/roboticslab-uc3m/installation-guides/blob/master/docs/install-cmake.md)
- [Install YCM 0.11+](https://github.com/roboticslab-uc3m/installation-guides/blob/master/docs/install-ycm.md)
- [Install YARP 3.2+](https://github.com/roboticslab-uc3m/installation-guides/blob/master/docs/install-yarp.md) (CMake modules)

Installation steps:

```bash
cd  # go home
mkdir -p repos; cd repos                                                  # create $HOME/repos and enter it
git clone https://github.com/roboticslab-uc3m/asibot-openrave-models.git  # download repository
cd asibot-openrave-models; mkdir build; cd build; cmake ..                # configure the build
sudo make install                                                         # install
```

For additional (advanced) options, use `ccmake` command instead of `cmake`.

See also:

* [asibot-main](https://github.com/roboticslab-uc3m/asibot-main)
