
FROM ghcr.io/archlinux/archlinux:latest

ENV target zeek

RUN pacman -Syu --noconfirm && pacman -S base-devel git cmake curl gcc-libs glibc python python-numpy openmp cuda --noconfirm
RUN useradd -m arch
USER arch
WORKDIR /home/arch
RUN git clone -b main https://github.com/i2z1/pkg_llama.cpp-cuda-git

WORKDIR /home/arch/pkg_llama.cpp-cuda-git

RUN makepkg

RUN sha256sum pkg_llama.cpp-cuda-git-*-x86_64.pkg.tar.zst > pkg_llama.cpp-cuda-git.sha256sum
