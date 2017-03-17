## Basic installation

Dependencies:

- [Install CMake](https://github.com/roboticslab-uc3m/installation-guides/blob/develop/install-cmake.md)
- [Install YARP](https://github.com/roboticslab-uc3m/installation-guides/blob/develop/install-yarp.md) (CMake modules)

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
