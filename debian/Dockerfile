FROM tianon/debian-devel

# start by adding just "debian/control" so we can get mk-build-deps with maximum caching
ADD control /usr/src/hy/debian/
WORKDIR /usr/src/hy

# get all the build deps of _this_ package in a nice repeatable way
RUN apt-get update && mk-build-deps -irt'apt-get --no-install-recommends -yq' debian/control

# need our debian/ directory to compile _this_ package
ADD . /usr/src/hy/debian

# go download and unpack our upstream source
RUN uscan --force-download --verbose --download-current-version
RUN origtargz --unpack

# tianon is _really_ lazy, and likes a preseeded bash history
RUN echo 'origtargz --unpack && dpkg-buildpackage -us -uc && lintian -EvIL+pedantic' >> /root/.bash_history
