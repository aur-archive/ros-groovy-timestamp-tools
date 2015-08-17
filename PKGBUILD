pkgdesc="ROS - timestamp tools."
url='http://www.ros.org/'

pkgname='ros-groovy-timestamp-tools'
pkgver='1.6.6'
arch=('i686' 'x86_64')
pkgrel=1
license=('BSD')
makedepends=('ros-build-tools')

depends=(
  ros-groovy-catkin
  ros-groovy-roslib
  ros-groovy-roscpp
  boost)

build() {
  [ -f /opt/ros/groovy/setup.bash ] && source /opt/ros/groovy/setup.bash
  if [ -d ${srcdir}/timestamp_tools ]; then
    cd ${srcdir}/timestamp_tools
    git fetch origin --tags
    git reset --hard release/groovy/timestamp_tools/${pkgver}-0
  else
    git clone -b release/groovy/timestamp_tools/${pkgver}-0 git://github.com/ros-gbp/driver_common-release.git ${srcdir}/timestamp_tools
  fi
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build
  /usr/share/ros-build-tools/fix-python-scripts.sh ${srcdir}/timestamp_tools
  cmake ${srcdir}/timestamp_tools -DCATKIN_BUILD_BINARY_PACKAGE=ON -DCMAKE_INSTALL_PREFIX=/opt/ros/groovy -DPYTHON_EXECUTABLE=/usr/bin/python2 -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
