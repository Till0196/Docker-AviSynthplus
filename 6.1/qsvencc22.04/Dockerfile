FROM        ubuntu:22.04 AS base

WORKDIR     /tmp/workdir

RUN     apt-get -yqq update && \
        apt-get install -yq --no-install-recommends ca-certificates expat libgomp1 && \
        apt-get autoremove -y && \
        apt-get clean -y

FROM base as build

ENV         FFMPEG_VERSION=6.1.1 \
            AVISYNTHPLUS_VERSION=v3.7.3 \
            LSMASHSOURCE_VERSION=20220505 \
            AOM_VERSION=v3.8.1 \
            CHROMAPRINT_VERSION=1.5.0 \
            FDKAAC_VERSION=0.1.5 \
            FONTCONFIG_VERSION=2.15.0 \
            LIBBZIP2_VERSION=1.0.8 \
            FREETYPE_VERSION=2.13.2 \
            FRIBIDI_VERSION=1.0.13 \
            KVAZAAR_VERSION=2.0.0 \
            LAME_VERSION=3.100 \
            LIBASS_VERSION=0.13.7 \
            LIBPTHREAD_STUBS_VERSION=0.4 \
            LIBVIDSTAB_VERSION=1.1.0 \
            LIBXCB_VERSION=1.15 \
            XCBPROTO_VERSION=1.15 \
            OGG_VERSION=1.3.2 \
            OPENCOREAMR_VERSION=0.1.5 \
            OPUS_VERSION=1.2 \
            OPENJPEG_VERSION=2.1.2 \
            THEORA_VERSION=1.1.1 \
            VORBIS_VERSION=1.3.5 \
            VPX_VERSION=1.8.0 \
            WEBP_VERSION=1.0.2 \
            X264_VERSION=20170226-2245-stable \
            X265_VERSION=3.4 \
            XAU_VERSION=1.0.9 \
            XORG_MACROS_VERSION=1.19.2 \
            XPROTO_VERSION=7.0.31 \
            XVID_VERSION=1.3.4 \
            LIBXML2_VERSION=2.9.12 \
            LIBBLURAY_VERSION=1.3.4 \
            LIBZMQ_VERSION=4.3.2 \
            LIBSRT_VERSION=1.4.1 \
            LIBARIBB24_VERSION=1.0.3 \
            LIBPNG_VERSION=1.6.9 \
            LIBVMAF_VERSION=2.1.1 \
            LIBVA_VERSION=2.16.0 \
            LIBPCIACCESS_VERSION=0.18 \
            LIBDRM_VERSION=2.4.120 \
            ZIMG_VERSION=3.0.5 \
            GMMLIB_VERSION=22.3.11 \
            INTEL_MEDIA_DRIVER_VERSION=24.1.5 \
            INTEL_MEDIA_SDK_VERSION=22.5.4 \
            INTEL_VAAPI_DRIVER_VERSION=2.4.1 \
            INTEL_GRAPHICS_COMPILER_VERSION=1.0.15985.7 \
            INTEL_OPENCL_ICD_VERSION=24.05.28454.6 \
            VAPOURSYNTH_VERSION=66 \
            ONEVPL_INTEL_GPU_VERSION=24.1.5 \
            LIBVPL_VERSION=2.10.2 \
            INTEL_LIBVA_UTILS_VERSION=2.16.0 \
            QSVENCC_VERSION=7.62 \
            SRC=/usr/local

ARG         FREETYPE_SHA256SUM="5eab795ebb23ac77001cfb68b7d4d50b5d6c7469247b0b01b2c953269f658dac freetype-2.10.4.tar.gz"
ARG         FRIBIDI_SHA256SUM="3fc96fa9473bd31dcb5500bdf1aa78b337ba13eb8c301e7c28923fea982453a8 0.19.7.tar.gz"
ARG         LIBASS_SHA256SUM="8fadf294bf701300d4605e6f1d92929304187fca4b8d8a47889315526adbafd7 0.13.7.tar.gz"
ARG         LIBVIDSTAB_SHA256SUM="14d2a053e56edad4f397be0cb3ef8eb1ec3150404ce99a426c4eb641861dc0bb v1.1.0.tar.gz"
ARG         OGG_SHA256SUM="e19ee34711d7af328cb26287f4137e70630e7261b17cbe3cd41011d73a654692 libogg-1.3.2.tar.gz"
ARG         OPUS_SHA256SUM="77db45a87b51578fbc49555ef1b10926179861d854eb2613207dc79d9ec0a9a9 opus-1.2.tar.gz"
ARG         THEORA_SHA256SUM="40952956c47811928d1e7922cda3bc1f427eb75680c3c37249c91e949054916b libtheora-1.1.1.tar.gz"
ARG         VORBIS_SHA256SUM="6efbcecdd3e5dfbf090341b485da9d176eb250d893e3eb378c428a2db38301ce libvorbis-1.3.5.tar.gz"
ARG         XVID_SHA256SUM="4e9fd62728885855bc5007fe1be58df42e5e274497591fec37249e1052ae316f xvidcore-1.3.4.tar.gz"
ARG         LIBBLURAY_SHA256SUM="a3dd452239b100dc9da0d01b30e1692693e2a332a7d29917bf84bb10ea7c0b42 libbluray-1.1.2.tar.bz2"
ARG         LIBZMQ_SHA256SUM="02ecc88466ae38cf2c8d79f09cfd2675ba299a439680b64ade733e26a349edeb v4.3.2.tar.gz"
ARG         LIBARIBB24_SHA256SUM="f61560738926e57f9173510389634d8c06cabedfa857db4b28fb7704707ff128 v1.0.3.tar.gz"


ARG         MAKEFLAGS="-j2"
ARG         PKG_CONFIG_PATH="/opt/ffmpeg/share/pkgconfig:/opt/ffmpeg/lib/pkgconfig:/opt/ffmpeg/lib64/pkgconfig:/opt/intel/mediasdk/lib/pkgconfig"
ARG         PREFIX=/opt/ffmpeg
ARG         LD_LIBRARY_PATH="/opt/ffmpeg/lib:/opt/ffmpeg/lib64:/opt/ffmpeg/lib/x86_64-linux-gnu/:/opt/ffmpeg/mediasdk/lib"


ARG DEBIAN_FRONTEND=noninteractive

RUN      buildDeps="autoconf \
                    automake \
                    cmake \
                    curl \
                    bzip2 \
                    libexpat1-dev \
                    g++ \
                    gcc \
                    git \
                    gperf \
                    libtool \
                    make \
                    meson \
                    nasm \
                    perl \
                    pkg-config \
                    python3 \
                    ninja-build \
                    libssl-dev \
                    yasm \
                    zlib1g-dev" && \
        apt-get -yqq update && \
        apt-get install -yq --no-install-recommends ${buildDeps}

## libvmaf https://github.com/Netflix/vmaf
RUN \
        if which meson || false; then \
        echo "Building VMAF." && \
        DIR=/tmp/vmaf && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://github.com/Netflix/vmaf/archive/v${LIBVMAF_VERSION}.tar.gz && \
        tar -xz --strip-components=1 -f v${LIBVMAF_VERSION}.tar.gz && \
        cd /tmp/vmaf/libvmaf && \
        meson build --buildtype release --prefix=${PREFIX} --libdir=lib && \
        ninja -vC build && \
        ninja -vC build install && \
        mkdir -p ${PREFIX}/share/model/ && \
        cp -r /tmp/vmaf/model/* ${PREFIX}/share/model/ && \
        rm -rf ${DIR}; \
        else \
        echo "VMAF skipped."; \
        fi

## opencore-amr https://sourceforge.net/projects/opencore-amr/
RUN \
        DIR=/tmp/opencore-amr && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sL https://sourceforge.net/projects/opencore-amr/files/opencore-amr/opencore-amr-${OPENCOREAMR_VERSION}.tar.gz/download | \
        tar -zx --strip-components=1 && \
        ./configure --prefix="${PREFIX}" --enable-shared  && \
        make && \
        make install && \
        rm -rf ${DIR}
## x264 http://www.videolan.org/developers/x264.html
RUN \
        DIR=/tmp/x264 && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sL https://download.videolan.org/pub/videolan/x264/snapshots/x264-snapshot-${X264_VERSION}.tar.bz2 | \
        tar -jx --strip-components=1 && \
        ./configure --prefix="${PREFIX}" --enable-shared --enable-pic --disable-cli && \
        make && \
        make install && \
        rm -rf ${DIR}
### x265 http://x265.org/
RUN \
        DIR=/tmp/x265 && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sL https://github.com/videolan/x265/archive/refs/tags/${X265_VERSION}.tar.gz | \
        tar -zx && \
        cd x265-${X265_VERSION}/build/linux && \
        sed -i "/-DEXTRA_LIB/ s/$/ -DCMAKE_INSTALL_PREFIX=\${PREFIX}/" multilib.sh && \
        sed -i "/^cmake/ s/$/ -DENABLE_CLI=OFF/" multilib.sh && \
        ./multilib.sh && \
        make -C 8bit install && \
        rm -rf ${DIR}
### libogg https://www.xiph.org/ogg/
RUN \
        DIR=/tmp/ogg && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO http://downloads.xiph.org/releases/ogg/libogg-${OGG_VERSION}.tar.gz && \
        echo ${OGG_SHA256SUM} | sha256sum --check && \
        tar -zx --strip-components=1 -f libogg-${OGG_VERSION}.tar.gz && \
        ./configure --prefix="${PREFIX}" --enable-shared  && \
        make && \
        make install && \
        rm -rf ${DIR}
### libopus https://www.opus-codec.org/
RUN \
        DIR=/tmp/opus && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://archive.mozilla.org/pub/opus/opus-${OPUS_VERSION}.tar.gz && \
        echo ${OPUS_SHA256SUM} | sha256sum --check && \
        tar -zx --strip-components=1 -f opus-${OPUS_VERSION}.tar.gz && \
        autoreconf -fiv && \
        ./configure --prefix="${PREFIX}" --enable-shared && \
        make && \
        make install && \
        rm -rf ${DIR}
### libvorbis https://xiph.org/vorbis/
RUN \
        DIR=/tmp/vorbis && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO http://downloads.xiph.org/releases/vorbis/libvorbis-${VORBIS_VERSION}.tar.gz && \
        echo ${VORBIS_SHA256SUM} | sha256sum --check && \
        tar -zx --strip-components=1 -f libvorbis-${VORBIS_VERSION}.tar.gz && \
        ./configure --prefix="${PREFIX}" --with-ogg="${PREFIX}" --enable-shared && \
        make && \
        make install && \
        rm -rf ${DIR}
### libtheora http://www.theora.org/
RUN \
        DIR=/tmp/theora && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO http://downloads.xiph.org/releases/theora/libtheora-${THEORA_VERSION}.tar.gz && \
        echo ${THEORA_SHA256SUM} | sha256sum --check && \
        tar -zx --strip-components=1 -f libtheora-${THEORA_VERSION}.tar.gz && \
        ./configure --prefix="${PREFIX}" --with-ogg="${PREFIX}" --enable-shared && \
        make && \
        make install && \
        rm -rf ${DIR}
### libvpx https://www.webmproject.org/code/
RUN \
        DIR=/tmp/vpx && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sL https://codeload.github.com/webmproject/libvpx/tar.gz/v${VPX_VERSION} | \
        tar -zx --strip-components=1 && \
        ./configure --prefix="${PREFIX}" --enable-vp8 --enable-vp9 --enable-vp9-highbitdepth --enable-pic --enable-shared \
        --disable-debug --disable-examples --disable-docs --disable-install-bins  && \
        make && \
        make install && \
        rm -rf ${DIR}
## libpng
RUN \
        DIR=/tmp/png && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        git clone https://git.code.sf.net/p/libpng/code ${DIR} -b v${LIBPNG_VERSION} --depth 1 && \
        ./autogen.sh && \
        ./configure --prefix="${PREFIX}" && \
        make check && \
        make install && \
        rm -rf ${DIR}
### libwebp https://developers.google.com/speed/webp/
RUN \
        DIR=/tmp/vebp && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sL https://storage.googleapis.com/downloads.webmproject.org/releases/webp/libwebp-${WEBP_VERSION}.tar.gz | \
        tar -zx --strip-components=1 && \
        ./configure --prefix="${PREFIX}" --enable-shared  && \
        make && \
        make install && \
        rm -rf ${DIR}
### libmp3lame http://lame.sourceforge.net/
RUN \
        DIR=/tmp/lame && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sL https://sourceforge.net/projects/lame/files/lame/${LAME_VERSION}/lame-${LAME_VERSION}.tar.gz/download | \
        tar -zx --strip-components=1 && \
        ./configure --prefix="${PREFIX}" --bindir="${PREFIX}/bin" --enable-shared --enable-nasm --disable-frontend && \
        make && \
        make install && \
        rm -rf ${DIR}
### xvid https://www.xvid.com/
RUN \
        DIR=/tmp/xvid && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO http://downloads.xvid.org/downloads/xvidcore-${XVID_VERSION}.tar.gz && \
        echo ${XVID_SHA256SUM} | sha256sum --check && \
        tar -zx -f xvidcore-${XVID_VERSION}.tar.gz && \
        cd xvidcore/build/generic && \
        ./configure --prefix="${PREFIX}" --bindir="${PREFIX}/bin" && \
        make && \
        make install && \
        rm -rf ${DIR}
## openjpeg https://github.com/uclouvain/openjpeg
RUN \
        DIR=/tmp/openjpeg && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sL https://github.com/uclouvain/openjpeg/archive/v${OPENJPEG_VERSION}.tar.gz | \
        tar -zx --strip-components=1 && \
        cmake -DBUILD_THIRDPARTY:BOOL=ON -DCMAKE_INSTALL_PREFIX="${PREFIX}" . && \
        make && \
        make install && \
        rm -rf ${DIR}
## libbzip2 https://sourceware.org/bzip2/
RUN \
        DIR=/tmp/bzip2 && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://sourceware.org/pub/bzip2/bzip2-${LIBBZIP2_VERSION}.tar.gz && \
        tar -zx --strip-components=1 -f bzip2-${LIBBZIP2_VERSION}.tar.gz && \
        make -f Makefile-libbz2_so clean && \
        make -f Makefile-libbz2_so && \
        make install PREFIX="${PREFIX}" && \
        find . -type f -name 'libbz2.so.*' -print0 | xargs -0 -n1 install -m 644 -t ${PREFIX}/lib && \
        find . -type l -name 'libbz2.so.*' -print0 | xargs -0 -I {} cp -p -r {} ${PREFIX}/lib && \
        echo -e "prefix=${PREFIX}\nexec_prefix=\${prefix}\nbindir=\${exec_prefix}/bin\nlibdir=\${exec_prefix}/lib\nincludedir=\${prefix}/include\n \
        \nName: bzip2\nDescription: A file compression library\nVersion: ${LIBBZIP2_VERSION}\n \
        \nLibs: -L\${libdir} -lbz2\nCflags: -I\${includedir}" > ${PREFIX}/lib/pkgconfig/bzip2.pc && \
        ldconfig && \
        rm -rf ${DIR}
## freetype https://www.freetype.org/
RUN  \
        DIR=/tmp/freetype && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://downloads.sourceforge.net/project/freetype/freetype2/${FREETYPE_VERSION}/freetype-${FREETYPE_VERSION}.tar.gz && \
        tar -zx --strip-components=1 -f freetype-${FREETYPE_VERSION}.tar.gz && \
        ./configure --prefix="${PREFIX}" --disable-static --enable-shared && \
        make && \
        make install && \
        rm -rf ${DIR}
## libvstab https://github.com/georgmartius/vid.stab
RUN  \
        DIR=/tmp/vid.stab && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://github.com/georgmartius/vid.stab/archive/v${LIBVIDSTAB_VERSION}.tar.gz && \
        echo ${LIBVIDSTAB_SHA256SUM} | sha256sum --check &&  \
        tar -zx --strip-components=1 -f v${LIBVIDSTAB_VERSION}.tar.gz && \
        cmake -DCMAKE_INSTALL_PREFIX="${PREFIX}" . && \
        make && \
        make install && \
        rm -rf ${DIR}
## fridibi https://www.fribidi.org/
RUN  \
        DIR=/tmp/fribidi && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://github.com/fribidi/fribidi/archive/v${FRIBIDI_VERSION}.tar.gz && \
        tar -zx --strip-components=1 -f v${FRIBIDI_VERSION}.tar.gz && \
        meson build --buildtype=release --prefix="${PREFIX}" --libdir=lib -Ddocs=false && \
        ninja -vC build && \
        ninja -vC build install && \
        rm -rf ${DIR}
## fontconfig https://www.freedesktop.org/wiki/Software/fontconfig/
RUN  \
        DIR=/tmp/fontconfig && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://www.freedesktop.org/software/fontconfig/release/fontconfig-${FONTCONFIG_VERSION}.tar.gz && \
        tar -zx --strip-components=1 -f fontconfig-${FONTCONFIG_VERSION}.tar.gz && \
        ./configure --prefix="${PREFIX}" --disable-static --enable-shared && \
        make && \
        make install && \
        rm -rf ${DIR}
## libass https://github.com/libass/libass
RUN  \
        DIR=/tmp/libass && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://github.com/libass/libass/archive/${LIBASS_VERSION}.tar.gz && \
        echo ${LIBASS_SHA256SUM} | sha256sum --check && \
        tar -zx --strip-components=1 -f ${LIBASS_VERSION}.tar.gz && \
        ./autogen.sh && \
        ./configure --prefix="${PREFIX}" --disable-static --enable-shared && \
        make && \
        make install && \
        rm -rf ${DIR}
## kvazaar https://github.com/ultravideo/kvazaar
RUN \
        DIR=/tmp/kvazaar && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://github.com/ultravideo/kvazaar/archive/v${KVAZAAR_VERSION}.tar.gz && \
        tar -zx --strip-components=1 -f v${KVAZAAR_VERSION}.tar.gz && \
        ./autogen.sh && \
        ./configure --prefix="${PREFIX}" --disable-static --enable-shared && \
        make && \
        make install && \
        rm -rf ${DIR}

RUN \
        DIR=/tmp/aom && \
        git clone --branch ${AOM_VERSION} --depth 1 https://aomedia.googlesource.com/aom ${DIR} ; \
        cd ${DIR} ; \
        rm -rf CMakeCache.txt CMakeFiles ; \
        mkdir -p ./aom_build ; \
        cd ./aom_build ; \
        cmake -DCMAKE_INSTALL_PREFIX="${PREFIX}" -DBUILD_SHARED_LIBS=1 ..; \
        make ; \
        make install ; \
        rm -rf ${DIR}

## libxcb (and supporting libraries) for screen capture https://xcb.freedesktop.org/
RUN \
        DIR=/tmp/xorg-macros && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://www.x.org/archive//individual/util/util-macros-${XORG_MACROS_VERSION}.tar.gz && \
        tar -zx --strip-components=1 -f util-macros-${XORG_MACROS_VERSION}.tar.gz && \
        ./configure --srcdir=${DIR} --prefix="${PREFIX}" && \
        make && \
        make install && \
        rm -rf ${DIR}

RUN \
        DIR=/tmp/xproto && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://www.x.org/archive/individual/proto/xproto-${XPROTO_VERSION}.tar.gz && \
        tar -zx --strip-components=1 -f xproto-${XPROTO_VERSION}.tar.gz && \
        ./configure --srcdir=${DIR} --prefix="${PREFIX}" && \
        make && \
        make install && \
        rm -rf ${DIR}

RUN \
        DIR=/tmp/libXau && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://www.x.org/archive/individual/lib/libXau-${XAU_VERSION}.tar.gz && \
        tar -zx --strip-components=1 -f libXau-${XAU_VERSION}.tar.gz && \
        ./configure --srcdir=${DIR} --prefix="${PREFIX}" && \
        make && \
        make install && \
        rm -rf ${DIR}

RUN \
        DIR=/tmp/libpthread-stubs && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://xcb.freedesktop.org/dist/libpthread-stubs-${LIBPTHREAD_STUBS_VERSION}.tar.gz && \
        tar -zx --strip-components=1 -f libpthread-stubs-${LIBPTHREAD_STUBS_VERSION}.tar.gz && \
        ./configure --prefix="${PREFIX}" && \
        make && \
        make install && \
        rm -rf ${DIR}

RUN \
        DIR=/tmp/libxcb-proto && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://xcb.freedesktop.org/dist/xcb-proto-${XCBPROTO_VERSION}.tar.gz && \
        tar -zx --strip-components=1 -f xcb-proto-${XCBPROTO_VERSION}.tar.gz && \
        ACLOCAL_PATH="${PREFIX}/share/aclocal" ./autogen.sh && \
        ./configure --prefix="${PREFIX}" && \
        make && \
        make install && \
        rm -rf ${DIR}

RUN \
        DIR=/tmp/libxcb && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://xcb.freedesktop.org/dist/libxcb-${LIBXCB_VERSION}.tar.gz && \
        tar -zx --strip-components=1 -f libxcb-${LIBXCB_VERSION}.tar.gz && \
        ACLOCAL_PATH="${PREFIX}/share/aclocal" ./autogen.sh && \
        ./configure --prefix="${PREFIX}" --disable-static --enable-shared && \
        make && \
        make install && \
        rm -rf ${DIR}

## libxml2 - for libbluray
RUN \
        DIR=/tmp/libxml2 && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sL https://github.com/GNOME/libxml2/archive/refs/tags/v${LIBXML2_VERSION}.tar.gz | \
        tar -xz --strip-components=1 && \
        ./autogen.sh --prefix="${PREFIX}" --with-ftp=no --with-http=no --with-python=no --enable-static --enable-shared && \
        make && \
        make install && \
        rm -rf ${DIR}

## libbluray - Requires libxml, freetype, and fontconfig
RUN \
        DIR=/tmp/libbluray && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://download.videolan.org/pub/videolan/libbluray/${LIBBLURAY_VERSION}/libbluray-${LIBBLURAY_VERSION}.tar.bz2 && \
        tar -jx --strip-components=1 -f libbluray-${LIBBLURAY_VERSION}.tar.bz2 && \
        ./configure --prefix="${PREFIX}" --disable-examples --disable-bdjava-jar --disable-static --enable-shared && \
        make && \
        make install && \
        rm -rf ${DIR}

## libzmq https://github.com/zeromq/libzmq/
RUN \
        DIR=/tmp/libzmq && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://github.com/zeromq/libzmq/archive/v${LIBZMQ_VERSION}.tar.gz && \
        echo ${LIBZMQ_SHA256SUM} | sha256sum --check && \
        tar -xz --strip-components=1 -f v${LIBZMQ_VERSION}.tar.gz && \
        ./autogen.sh && \
        ./configure --prefix="${PREFIX}" && \
        make && \
        make check && \
        make install && \
        rm -rf ${DIR}

## libsrt https://github.com/Haivision/srt
RUN \
        DIR=/tmp/srt && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://github.com/Haivision/srt/archive/v${LIBSRT_VERSION}.tar.gz && \
        tar -xz --strip-components=1 -f v${LIBSRT_VERSION}.tar.gz && \
        cmake -DCMAKE_INSTALL_PREFIX="${PREFIX}" . && \
        make && \
        make install && \
        rm -rf ${DIR}

## libaribb24
RUN \
        DIR=/tmp/b24 && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://github.com/nkoriyama/aribb24/archive/v${LIBARIBB24_VERSION}.tar.gz && \
        echo ${LIBARIBB24_SHA256SUM} | sha256sum --check && \
        tar -xz --strip-components=1 -f v${LIBARIBB24_VERSION}.tar.gz && \
        autoreconf -fiv && \
        ./configure CFLAGS="-I${PREFIX}/include -fPIC" --prefix="${PREFIX}" && \
        make && \
        make install && \
        rm -rf ${DIR}

## libva
RUN \
        apt-get install -y libdrm-dev && \
        DIR=/tmp/libva && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://github.com/intel/libva/archive/${LIBVA_VERSION}.tar.gz && \
        tar -xz --strip-components=1 -f ${LIBVA_VERSION}.tar.gz && \
        ./autogen.sh --prefix="${PREFIX}" --enable-shared --disable-static --with-pic --disable-docs --enable-drm \
                --disable-x11 --disable-glx --disable-wayland && \
        make && \
        make install && \
        echo /usr/local/lib >> /etc/ld.so.conf.d/local.conf && \
        ldconfig && \
        rm -rf ${DIR}

## libpciaccess
RUN \
        DIR=/tmp/libpciaccess && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://gitlab.freedesktop.org/xorg/lib/libpciaccess/-/archive/libpciaccess-${LIBPCIACCESS_VERSION}/libpciaccess-libpciaccess-${LIBPCIACCESS_VERSION}.tar.gz && \
        tar -xz --strip-components=1 -f libpciaccess-libpciaccess-${LIBPCIACCESS_VERSION}.tar.gz && \
        meson build --buildtype=release --prefix="${PREFIX}" --libdir=lib -Ddefault_library=shared -Dzlib=enabled && \
        ninja -vC build && \
        ninja -vC build install && \
        rm -rf ${DIR}

## libdrm
RUN \
        DIR=/tmp/libdrm && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://gitlab.freedesktop.org/mesa/drm/-/archive/libdrm-${LIBDRM_VERSION}/libdrm-${LIBDRM_VERSION}.tar.gz && \
        tar -xz --strip-components=1 -f libdrm-${LIBDRM_VERSION}.tar.gz && \
        meson build --buildtype=release --prefix="${PREFIX}" --bindir=bin --libdir=lib -Ddefault_library=shared -Dudev=false -Dcairo-tests=disabled \
              -Dvalgrind=disabled -Dexynos=disabled -Dfreedreno=disabled -Domap=disabled -Detnaviv=disabled -Dintel=enabled -Dnouveau=enabled \
              -Dradeon=enabled -Damdgpu=enabled && \
        ninja -vC build && \
        ninja -vC build install && \
        rm -rf ${DIR}
        
## gmmlib
RUN \
        DIR=/tmp/gmmlib && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://github.com/intel/gmmlib/archive/intel-gmmlib-${GMMLIB_VERSION}.tar.gz && \
        tar -xz --strip-components=1 -f intel-gmmlib-${GMMLIB_VERSION}.tar.gz && \
        mkdir build && cd build && \
        cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX="${PREFIX}" .. && \
        make && \
        make install && \
        rm -rf ${DIR}

## MediaDriver
RUN \ 
        DIR=/tmp/mediadriver && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \        
        curl -sLO https://github.com/intel/media-driver/archive/intel-media-${INTEL_MEDIA_DRIVER_VERSION}.tar.gz && \
        tar -xz --strip-components=1 -f intel-media-${INTEL_MEDIA_DRIVER_VERSION}.tar.gz && \
        mkdir build && cd build && \
        cmake -DCMAKE_INSTALL_PREFIX="${PREFIX}" -DENABLE_PRODUCTION_KMD=OFF .. && \
        make && \
        make install && \
        rm -rf ${DIR}

## VaapiDriver
RUN \ 
        DIR=/tmp/intel-vaapi-driver && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \        
        curl -sLO https://github.com/intel/intel-vaapi-driver/archive/${INTEL_VAAPI_DRIVER_VERSION}.tar.gz && \
        tar -xz --strip-components=1 -f ${INTEL_VAAPI_DRIVER_VERSION}.tar.gz && \
        ./autogen.sh && \
        ./configure --prefix="${PREFIX}" && \
        make && \
        make install && \
        rm -rf ${DIR}

## oneVPL runtime
RUN \ 
        DIR=/tmp/oneVPL && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \        
        curl -sLO https://github.com/oneapi-src/oneVPL-intel-gpu/archive/intel-onevpl-${ONEVPL_INTEL_GPU_VERSION}.tar.gz && \
        tar -xz --strip-components=1 -f intel-onevpl-${ONEVPL_INTEL_GPU_VERSION}.tar.gz && \
        mkdir build && cd build && \
        cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX="${PREFIX}" -DBUILD_RUNTIME=1 -DBUILD_TESTS=0 .. && \
        make && \
        make install && \
        rm -rf ${DIR}

## libvpl
RUN \ 
        DIR=/tmp/libvpl && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \        
        curl -sLO https://github.com/intel/libvpl/archive/v${LIBVPL_VERSION}.tar.gz && \
        tar -xz --strip-components=1 -f v${LIBVPL_VERSION}.tar.gz && \
        mkdir build && cd build && \
        cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX="${PREFIX}" -DBUILD_DISPATCHER=1 -DBUILD_DEV=1 -DBUILD_PREVIEW=0 -DBUILD_TOOLS=0 \
          -DBUILD_TOOLS_ONEVPL_EXPERIMENTAL=0 -DINSTALL_EXAMPLE_CODE=0 -DBUILD_SHARED_LIBS=0 -DBUILD_TESTS=0 .. && \
        make && \
        make install && \
        rm -rf ${DIR}


## libva-utils
RUN \ 
        DIR=/tmp/libva-utils && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \        
        curl -sLO https://github.com/intel/libva-utils/archive/${INTEL_LIBVA_UTILS_VERSION}.tar.gz && \
        tar -xz --strip-components=1 -f ${INTEL_LIBVA_UTILS_VERSION}.tar.gz && \
        ./autogen.sh && \
        ./configure --prefix="${PREFIX}" && \
        make && \
        make install && \
        rm -rf ${DIR}
        
## MediaSDK
RUN \ 
        DIR=/tmp/mediasdk && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://github.com/Intel-Media-SDK/MediaSDK/archive/intel-mediasdk-${INTEL_MEDIA_SDK_VERSION}.tar.gz && \
        tar -xz --strip-components=1 -f intel-mediasdk-${INTEL_MEDIA_SDK_VERSION}.tar.gz && \
        mkdir build && cd build && \
        cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX="${PREFIX}" .. && \
        make && \
        make install && \
        echo /opt/intel/mediasdk/lib/ >> /etc/ld.so.conf.d/mediasdk.conf && \
        ldconfig && \
        rm -rf ${DIR}

## intel-opencl-icd
RUN \
        apt-get install -y ocl-icd-libopencl1 && \
        DIR=/tmp/intel-opencl-icd && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://github.com/intel/compute-runtime/archive/${INTEL_OPENCL_ICD_VERSION}.tar.gz && \
        tar -xz --strip-components=1 -f ${INTEL_OPENCL_ICD_VERSION}.tar.gz && \
        mkdir build && cd build && \
        curl -s https://api.github.com/repos/intel/compute-runtime/releases/tags/${INTEL_OPENCL_ICD_VERSION} | grep browser_download_url | egrep '.*\.deb' | cut -d '"' -f 4 | xargs -n 1 curl -sLO && \
        curl -s https://api.github.com/repos/intel/intel-graphics-compiler/releases/tags/igc-${INTEL_GRAPHICS_COMPILER_VERSION} | grep browser_download_url | egrep '.*\.deb' | cut -d '"' -f 4 | xargs -n 1 curl -sLO && \
        for file in *.deb; do \
          dpkg-deb -I "$file" | grep -Po "(?<=Package: ).*" ; \
        done > prebuilds.txt && \
        dpkg -i *.deb && \
        cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX="${PREFIX}" .. && \
        make && \
        make install && \
        cat prebuilds.txt | xargs dpkg -r && \
        ldconfig && \
        rm -rf ${DIR}

# zimg  https://github.com/sekrit-twc/zimg
RUN \
        DIR=/tmp/zimg && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sL https://github.com/sekrit-twc/zimg/archive/refs/tags/release-${ZIMG_VERSION}.tar.gz | \
        tar -zx --strip-components=1 && \
        ./autogen.sh && \
        ./configure --prefix="${PREFIX}" --enable-shared  && \
        make && \
        make install && \
        rm -rf ${DIR}

## vapoursynth
RUN \
        apt-get install -y python3-pip && \
        DIR=/tmp/vapoursynth && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://github.com/vapoursynth/vapoursynth/archive/R${VAPOURSYNTH_VERSION}.tar.gz && \
        tar -zx --strip-components=1 -f R${VAPOURSYNTH_VERSION}.tar.gz && \
        pip install -U cython setuptools wheel && \
        ./autogen.sh && \
        ./configure --prefix="${PREFIX}" && \
        make && \
        make install && \
        ldconfig && \
        rm -rf ${DIR}

#AviSynth+
RUN     set -xe && \
        DIR=/tmp/avisynth && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        git clone --depth 1 -b ${AVISYNTHPLUS_VERSION} https://github.com/AviSynth/AviSynthPlus.git && \
        cd AviSynthPlus && \
        mkdir avisynth-build && \
        cd avisynth-build && \
        #CC=gcc-9 CXX=gcc-9 LD=gcc-9 cmake ../ -G Ninja && \
        cmake ../ -G Ninja && \
        ninja && \
        ninja install && \
        ldconfig && \
        rm -rf ${DIR}

## Download ffmpeg https://ffmpeg.org/
RUN  \
        DIR=/tmp/ffmpeg && mkdir -p ${DIR} && cd ${DIR} && \
        curl -sLO https://ffmpeg.org/releases/ffmpeg-${FFMPEG_VERSION}.tar.bz2 && \
        tar -jx --strip-components=1 -f ffmpeg-${FFMPEG_VERSION}.tar.bz2 && \
        ./configure     --disable-debug  --disable-doc    --disable-ffplay   --enable-shared --enable-gpl  --extra-libs=-ldl && \
        make ;  make install

## Build ffmpeg https://ffmpeg.org/
RUN  \
        DIR=/tmp/ffmpeg && cd ${DIR} && \
        ./configure \
        --disable-debug \
        --disable-doc \
        --disable-ffplay \
        --enable-libvpl \
        --enable-vaapi \
        --enable-avisynth \
        --enable-fontconfig \
        --enable-gpl \
        --enable-libaom \
        --enable-libaribb24 \
        --enable-libass \
        --enable-libbluray \
        --enable-libdrm \
        --enable-libfreetype \
        --enable-libkvazaar \
        --enable-libmp3lame \
        --enable-libopencore-amrnb \
        --enable-libopencore-amrwb \
        --enable-libopenjpeg \
        --enable-libopus \
        --enable-libsrt \
        --enable-libtheora \
        --enable-libvidstab \
        --enable-libvmaf \
        --enable-libvorbis \
        --enable-libvpx \
        --enable-libwebp \
        --enable-libx264 \
        --enable-libx265 \
        --enable-libxcb \
        --enable-libxvid \
        --enable-libzimg \
        --enable-libzmq \
        --enable-nonfree \
        --enable-openssl \
        --enable-postproc \
        --enable-shared \
        --enable-small \
        --enable-version3 \
        --extra-cflags="-I${PREFIX}/include" \
        --extra-ldflags="-L${PREFIX}/lib" \
        --extra-libs=-ldl \
        --extra-libs=-lpthread \
        --prefix="${PREFIX}" && \
        make clean && \
        make && \
        make install && \
        make tools/zmqsend && cp tools/zmqsend ${PREFIX}/bin/ && \
        make distclean && \
        hash -r && \
        cd tools && \
        make qt-faststart && cp qt-faststart ${PREFIX}/bin/

# l-smash
RUN     set -xe && \
        DIR=/tmp/opencore-amr && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        git clone https://github.com/l-smash/l-smash.git && \
        cd l-smash && \
        ./configure \
          --prefix="${PREFIX}" \
          --enable-shared \
          && \
        make && \
        make install && \
        rm -rf ${DIR}

# l-smash-source
RUN     set -xe && \
        DIR=/tmp/lsmashsouce && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        git clone --depth 1 -b ${LSMASHSOURCE_VERSION} https://github.com/HomeOfAviSynthPlusEvolution/L-SMASH-Works.git --recursive && \
        cd L-SMASH-Works/AviSynth && \
        LDFLAGS="-Wl,-Bsymbolic" meson build && \
        cd build && \
        ninja -v && \
        ninja install && \
        cd ../../VapourSynth && \
        LDFLAGS="-Wl,-Bsymbolic" meson build && \
        cd build && \
        ninja -v && \
        ninja install && \
        rm -rf ${DIR}

## QSVEncC
RUN \
        apt-get install -y opencl-headers && \
        DIR=/tmp/qsvencc && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        git clone -b ${QSVENCC_VERSION} https://github.com/rigaya/QSVEnc.git --recursive ${DIR} && \
        ./configure --prefix="${PREFIX}" && \
        make && \
        make install && \
        rm -rf ${DIR}

## cleanup
RUN \
        LD_LIBRARY_PATH="${PREFIX}/lib:${PREFIX}/lib64:${LD_LIBRARY_PATH}" ldd ${PREFIX}/bin/ffmpeg | grep opt/ffmpeg | cut -d ' ' -f 3 | xargs -i cp {} /usr/local/lib/ && \
        ldd ${SRC}/lib/avisynth/liblsmashsource.so | grep opt/ffmpeg | cut -d ' ' -f 3 | xargs -i cp {} /usr/local/lib/ && \
        for lib in /usr/local/lib/*.so.*; do ln -s "${lib##*/}" "${lib%%.so.*}".so; done && \
        cp ${PREFIX}/bin/* /usr/local/bin/ && \
        cp -r ${PREFIX}/share/ffmpeg /usr/local/share/ && \
        cp -r ${PREFIX}/lib/* /usr/local/lib/ && \
        cp -r ${PREFIX}/include/* /usr/local/include/ && \
        LD_LIBRARY_PATH=/usr/local/lib ffmpeg -buildconf && \
        find /usr/local/lib/ -path "*/pkgconfig/*.pc" | while read PCFILE; do \
          echo "Updating ${PREFIX} to /usr/local in $PCFILE" && \
          sed -i "s|${PREFIX}|/usr/local|" $PCFILE; \
        done

FROM        base AS release
LABEL       maintainer="Till0196"

ENV         LD_LIBRARY_PATH=/usr/local/lib \
            LIBVA_DRIVERS_PATH=/usr/local/lib/dri

CMD         ["--help"]
ENTRYPOINT  ["ffmpeg"]

COPY --from=build /usr/local /usr/local/
RUN \
        INTEL_GRAPHICS_COMPILER_VERSION=1.0.15985.7 && \
        apt-get install -y ocl-icd-libopencl1 curl && \
        curl -s https://api.github.com/repos/intel/intel-graphics-compiler/releases/tags/igc-${INTEL_GRAPHICS_COMPILER_VERSION} | grep browser_download_url |egrep '.*\.deb' | egrep -v 'devel|dev' | cut -d '"' -f 4 | xargs -n 1 curl -sLO && \
        dpkg -i *.deb && \
        mkdir -p /etc/OpenCL/vendors && \
        echo /usr/local/lib/intel-opencl/libigdrcl.so > /etc/OpenCL/vendors/intel.icd && \
        apt-get clean && \
        rm -rf /var/lib/apt/lists/* *.deb
