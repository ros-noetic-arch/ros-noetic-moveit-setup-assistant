pkgdesc="ROS - Generates a configuration package that makes it easy to use MoveIt!."
url='https://moveit.ros.org'

pkgname='ros-noetic-moveit-setup-assistant'
pkgver='1.1.13'
arch=('i686' 'x86_64' 'aarch64' 'armv7h' 'armv6h')
pkgrel=1
license=('BSD')

ros_makedepends=(ros-noetic-srdfdom
  ros-noetic-moveit-core
  ros-noetic-catkin
  ros-noetic-moveit-ros-planning
  ros-noetic-moveit-resources
  ros-noetic-moveit-ros-visualization)
makedepends=(cmake ros-build-tools
  ${ros_makedepends[@]}
  yaml-cpp
  log4cxx
  ompl)

ros_depends=(ros-noetic-srdfdom
  ros-noetic-xacro
  ros-noetic-moveit-core
  ros-noetic-moveit-ros-planning
  ros-noetic-moveit-ros-visualization)
depends=(${ros_depends[@]}
  yaml-cpp
  log4cxx
  ompl)

_dir="moveit-${pkgver}/moveit_setup_assistant"
source=("${pkgname}-${pkgver}.tar.gz"::"https://github.com/ros-planning/moveit/archive/${pkgver}.tar.gz")
sha256sums=('91735df0ec1a7bdbcdad9028352a0d78d44fad2076584319120e2e10ecb5882c')

build() {
  # Use ROS environment variables
  source /usr/share/ros-build-tools/clear-ros-env.sh
  [ -f /opt/ros/noetic/setup.bash ] && source /opt/ros/noetic/setup.bash

  # Create build directory
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build

  # Build project
  cmake ${srcdir}/${_dir} \
        -DCATKIN_BUILD_BINARY_PACKAGE=ON \
        -DCMAKE_INSTALL_PREFIX=/opt/ros/noetic \
        -DPYTHON_EXECUTABLE=/usr/bin/python \
        -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
