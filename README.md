## Building the Modules

### Build Mesos with some unbundled dependencies

First, build mesos out of its source tree. Let us assume you did extract/clone the repo into `~/mesos`. Let us also assume that you build mesos in a subfolder called `build` (`~/mesos/build`). Do a full build (`configure` and `make`) - you may optionally also want to run a `make check`.

Due to the fact that modules will need to have access to a couple of libprocess dependencies, mesos itself should get built with unbundled dependencies to reduce chances of problems introduced by varying versions (libmesos vs. module library). 

`--with-glog=/usr/local`
`--with-protobuf=/usr/local`
`--with-boost=/usr/local`
`--with-picojson=/usr/local`

### Build Mesos-Modules

Once that is done, extract/clone the mesos-modules package. For the sake of this example, that could be in `~/mesos-modules`. Note that you should not put `mesos-modules` into the `mesos` folder.

You may now run start building the modules.

The configuration phase needs to know some details about your mesos package location, hence the following are used:
`--with-mesos-root`
For allowing access to the internal headers which modules may still rely on. 

`--with-mesos-build`
For allowing access to the protobuf compilation results and for other generated sources like version.hpp.


### Example
```
./bootstrap
mkdir build && cd build
../configure --with-mesos-root=~/mesos  --with-mesos-build=~/mesos/build
make
```
