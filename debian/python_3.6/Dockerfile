FROM python:3.6-slim-stretch

RUN apt-get update \
 && ln -sf /usr/share/zoneinfo/UTC /etc/localtime \
 && apt-get install -y --no-install-recommends \
     cmake \
     davix-dev \
     dcap-dev \
     fonts-freefont-ttf \
     g++ \
     gcc \
     gfal2 \
     gfortran \
     git \
     libafterimage-dev \
     libavahi-compat-libdnssd-dev \
     libcfitsio-dev \
     libfftw3-dev \
     libfreetype6-dev \
     libftgl-dev \
     libgfal2-dev \
     libgif-dev \
     libgl2ps-dev \
     libglew-dev \
     libglu-dev \
     libgraphviz-dev \
     libgsl-dev \
     libjemalloc-dev \
     libjpeg-dev \
     libkrb5-dev \
     libldap2-dev \
     liblz4-dev \
     liblzma-dev \
     default-libmysqlclient-dev \
     libpcre++-dev \
     libpng-dev \
     libpq-dev \
     # libpythia8-dev \
     libqt4-dev \
     libsqlite3-dev \
     libssl-dev \
     libtbb-dev \
     libtiff-dev \
     libx11-dev \
     libxext-dev \
     libxft-dev \
     libxml2-dev \
     libxpm-dev \
     libz-dev \
     locales \
     lsb-release \
     make \
     r-base \
     r-cran-rcpp \
     r-cran-rinside \
     srm-ifce-dev \
     unixodbc-dev \
 && localedef -i en_US -f UTF-8 en_US.UTF-8 \
 && rm -rf /var/lib/apt/lists/*

RUN pip install --no-cache-dir numpy

ARG ROOT_VERSION=6-14-04
RUN cd /tmp \
 && git clone --branch v${ROOT_VERSION} https://github.com/root-project/root /usr/src/root \
 && cmake /usr/src/root \
 	-Dall=ON \
 	-Dcxx14=ON \
 	-Dfail-on-missing=ON \
 	-Dgnuinstall=ON \
 	-Drpath=ON \
 	-Dbuiltin_afterimage=OFF \
 	-Dbuiltin_ftgl=OFF \
 	-Dbuiltin_gl2ps=OFF \
 	-Dbuiltin_glew=OFF \
 	-Dbuiltin_unuran=ON \
 	-Dbuiltin_vc=ON \
 	-Dbuiltin_vdt=ON \
 	-Dbuiltin_veccore=ON \
 	-Dbuiltin_xrootd=ON \
 	-Darrow=OFF \
 	-Dcastor=OFF \
 	-Dchirp=OFF \
 	-Dgeocad=OFF \
 	-Dglite=OFF \
 	-Dhdfs=OFF \
 	-Dmonalisa=OFF \
 	-Doracle=OFF \
 	-Dpythia6=OFF \
  -Dpythia8=OFF \
 	-Drfio=OFF \
 	-Dsapdb=OFF \
 	-Dsrp=OFF \
 && cmake --build . -- -j$(nproc) \
 && cmake --build . --target install \
 && rm -rf /tmp/* /usr/src/root

ENV PYTHONPATH /usr/local/lib
CMD root -b
