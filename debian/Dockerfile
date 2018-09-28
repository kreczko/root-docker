FROM python:2.7-slim-stretch


COPY packages packages

RUN apt-get update -qq \
 && ln -sf /usr/share/zoneinfo/UTC /etc/localtime \
 && apt-get -y install --no-install-recommends $(cat packages) \
 && localedef -i en_US -f UTF-8 en_US.UTF-8 \
 && rm -rf /packages /var/lib/apt/lists/*

RUN pip install --no-cache-dir numpy

ARG ROOT_VERSION=6-14-04
RUN cd /tmp \
 && git clone --branch v${ROOT_VERSION} https://github.com/root-project/root /usr/src/root \
 && cmake /usr/src/root \
 	-Dminimal=ON \
 	-Dcxx14=ON \
 	-Dfail-on-missing=ON \
 	-Dgnuinstall=ON \
 	-Drpath=ON \
  -Dpython=ON \
 	-Dbuiltin_afterimage=OFF \
 	-Dbuiltin_ftgl=OFF \
 	-Dbuiltin_gl2ps=OFF \
 	-Dbuiltin_glew=OFF \
 	-Dbuiltin_unuran=OFF \
 	-Dbuiltin_vc=OFF \
 	-Dbuiltin_vdt=OFF \
 	-Dbuiltin_veccore=OFF \
 	-Dbuiltin_xrootd=OFF \
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
